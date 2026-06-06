---
title: "Nível Profissional"
subtitle: "Comandos que separam quem usa Git de quem domina Git"
section: "Parte 3"
series: "Git & GitHub — Do zero ao nível profissional"
author: Esron
brand: Esron Tech Books
chapters:
  - "Capítulo 8 — Desfazendo Erros com Segurança"
  - "Capítulo 9 — Limpando e Reorganizando o Histórico"
  - "Capítulo 10 — Casos Reais e Soluções Comuns"
---

# Parte 3 — Nível Profissional

> *Comandos que separam quem usa Git de quem domina Git*

Você já sabe criar repositórios, fazer commits, trabalhar com branches e colaborar via Pull Requests.

Agora vamos entrar no território dos desenvolvedores experientes — aqueles que trabalham em empresas grandes, mantêm projetos com centenas de commits e precisam consertar problemas sem causar pânico no time.

> **⚠️ Atenção antes de começar:** os comandos desta parte são poderosos — e alguns são perigosos se usados sem entender. Vamos aprender cada um com calma, mostrando quando usar, quando evitar e quais são as alternativas seguras.

---

## Capítulo 8 — Desfazendo Erros com Segurança

Todo mundo comete erros. O Git foi feito para te ajudar a consertá-los sem desespero — desde que você use as ferramentas certas.

### 01 — git restore: desfaz mudanças nos arquivos

Use quando você editou arquivos mas ainda **não fez commit** e quer voltar ao estado do último commit:

```bash
# Desfazer alterações não commitadas em um arquivo específico
git restore index.html

# Desfazer tudo que ainda não foi commitado
git restore .
```

> **Quando usar:** você editou um arquivo, percebeu que foi pelo caminho errado e quer começar do zero. O `git restore` descarta as mudanças sem afetar o histórico.

---

### 02 — git reset: desfaz commits

O `git reset` é mais poderoso — e mais delicado. Ele desfaz commits com três comportamentos diferentes:

| Modo | Desfaz commit? | Mantém no staging? | Mantém nos arquivos? |
|---|---|---|---|
| `--soft` | ✅ Sim | ✅ Sim | ✅ Sim |
| `--mixed` | ✅ Sim | ❌ Não | ✅ Sim |
| `--hard` | ✅ Sim | ❌ Não | ❌ Não ⚠️ |

```bash
# --soft: desfaz o commit, mantém tudo no staging
git reset --soft HEAD~1

# --mixed (padrão): desfaz o commit, tira do staging
git reset HEAD~1

# --hard: desfaz o commit E apaga as mudanças dos arquivos
git reset --hard HEAD~1
```

> **⚠️ Regra de ouro:** nunca use `--hard` se não tiver certeza absoluta do que está fazendo. As mudanças apagadas com `--hard` não vão para a lixeira — elas somem. Prefira sempre `--soft` ou `--mixed`. Se errar com `--hard`, o `git reflog` pode salvar você (veja a seção 05 deste capítulo).

---

### 03 — git revert: a forma segura para commits já publicados

Quando um commit já foi enviado ao GitHub (`git push`), use `git revert` — ele cria um novo commit que desfaz o anterior, **sem apagar o histórico**:

```bash
# Desfaz o último commit criando um novo commit de reversão
git revert HEAD

# Desfaz um commit específico pelo hash
git revert abc1234
```

> **`git reset` vs `git revert`**
>
> - Use `git reset` para commits que ainda **não foram compartilhados**.
> - Use `git revert` para commits que já **estão no repositório remoto**.
>
> Essa distinção evita dor de cabeça no time.

---

### 04 — git stash: guardar trabalho temporariamente

Útil quando você precisa trocar de branch mas ainda não quer commitar o que está fazendo:

```bash
git stash          # guarda as mudanças em um "bolso" temporário
git stash list     # lista todos os stashes salvos
git stash pop      # aplica o último stash e remove da lista
git stash apply    # aplica sem remover da lista
```

> **📋 Cenário real:** você está no meio de uma feature quando alguém pede para corrigir um bug urgente em outra branch. Faça `git stash`, troque de branch, resolva o bug, volte e rode `git stash pop`. Seu trabalho estará intacto.

---

### 05 — git reflog: o maior salva-vidas do Git

Se você "perdeu" um commit, fez reset errado ou algo deu muito errado, o reflog é sua última linha de defesa:

```bash
git reflog
git reflog --oneline
```

O reflog mostra **tudo que você fez recentemente** — mesmo commits que não aparecem mais no `git log`. Para recuperar um estado anterior:

```bash
# Use o hash mostrado no reflog para recuperar o estado
git reset --hard abc1234
```

> **✅ Você quase nunca perde trabalho no Git:** o reflog guarda o histórico de todas as suas operações por **90 dias** por padrão. Antes de entrar em pânico por um reset ou rebase errado, sempre consulte o reflog primeiro.

---

## Capítulo 9 — Limpando e Reorganizando o Histórico

Aqui entram os comandos mais poderosos — e os mais perigosos — do Git. Use-os com consciência.

### 01 — Interactive Rebase: o rei da limpeza

O `rebase -i` (interactive rebase) permite reorganizar, combinar, renomear e remover commits antes de compartilhar seu trabalho:

```bash
# Reorganizar os últimos 5 commits interativamente
git rebase -i HEAD~5
```

Um editor de texto abre com a lista dos commits. Para cada um, você escolhe o que fazer:

| Comando | O que faz |
|---|---|
| `pick` | Mantém o commit como está |
| `reword` | Mantém o commit, mas abre o editor para mudar a mensagem |
| `squash` | Junta este commit com o anterior, combinando as mensagens |
| `fixup` | Junta com o anterior, mas descarta a mensagem deste commit |
| `drop` | Remove o commit completamente do histórico |
| `edit` | Para a execução neste commit para que você possa editá-lo |

> **⚠️ Regra fundamental do rebase:** nunca faça rebase em branches que já foram compartilhadas com o time (como a `main` ou branches que outros já clonaram). O rebase reescreve o histórico — isso causa conflitos sérios para quem estiver usando a mesma branch.

> **💡 Quando usar o rebase:** use **antes de abrir um Pull Request** para deixar o histórico limpo e legível. Use apenas em branches que **ainda não foram compartilhadas** com o time.

---

### 02 — git commit --amend: corrigir o último commit

Errou a mensagem do último commit ou esqueceu de incluir um arquivo? O `--amend` resolve:

```bash
# Abre o editor para mudar a mensagem (ou adicionar arquivos staged)
git commit --amend

# Adiciona arquivos sem mudar a mensagem
git commit --amend --no-edit
```

> **⚠️ Atenção:** assim como o rebase, o `--amend` reescreve o commit. Use apenas se o commit **ainda não foi enviado ao GitHub**.

---

### 03 — cherry-pick: copiar um commit específico

Às vezes você quer trazer apenas um commit de outra branch — sem fazer merge de tudo:

```bash
# Copia o commit com aquele hash para a branch atual
git cherry-pick abc1234
```

> **📋 Cenário real:** sua branch de feature tem um bugfix que a `main` precisa urgente, mas a feature ainda não está pronta. Use `cherry-pick` para copiar só o commit do bugfix para a `main`, sem trazer o restante da feature.

---

## Capítulo 10 — Casos Reais e Soluções Comuns

Aqui resolvemos os problemas que aparecem de verdade no dia a dia — aqueles que ninguém ensina na teoria mas todo mundo encontra na prática.

### 01 — Mapa de problemas e soluções

| Problema | Solução rápida |
|---|---|
| Remote errado configurado | `git remote set-url origin <nova-url>` |
| PC formatado / novo computador | `git clone <url>` → configurar nome e e-mail |
| `main` vs `master` divergindo | `git merge main --allow-unrelated-histories` |
| Commit já enviado ao GitHub | `git revert <hash>` → `git push` (seguro) |
| Precisa desfazer push (urgente) | `git reset --hard` → `git push --force-with-lease` |

---

### 02 — main vs master: unificando históricos divergentes

Situação comum: o GitHub criou a branch `main` e você tem `master` localmente (ou vice-versa), e os históricos não se conectam:

```bash
git switch master
git merge main --allow-unrelated-histories
git push origin master

# Se quiser remover a branch main do remoto após a unificação
git push origin --delete main
```

---

### 03 — Removendo um commit já enviado ao GitHub

**Opção segura — recomendada para branches compartilhadas:**

```bash
git revert abc1234
git push origin main
```

**Opção de força — apenas em emergências, avise o time antes:**

```bash
git reset --hard HEAD~1
git push origin main --force-with-lease
```

> **⚠️ Sobre o force push:** o `--force-with-lease` é a versão mais segura do `--force` — ele falha se alguém tiver feito push depois de você, evitando sobrescrever trabalho alheio. Mesmo assim, force push em branches compartilhadas deve ser **comunicado ao time antes** de executar.

---

### 04 — Corrigindo o remote errado

```bash
# Ver qual remote está configurado
git remote -v

# Trocar a URL do origin
git remote set-url origin https://github.com/SEU-USUARIO/novo-repo.git
```

---

### 05 — PC formatado ou dois computadores

1. No computador novo, clone o repositório: `git clone <url>`
2. Configure novamente seu nome e e-mail (`git config --global`).
3. Continue trabalhando normalmente — todo o histórico estará lá.

> **💡 Dica profissional:** sempre prefira `git revert` em branches compartilhadas. Use force push só quando realmente necessário e avise o time com antecedência. Repositórios são colaborativos — comunicação é tão importante quanto os comandos.

---

## ✅ Fim da Parte 3

**Você já não é mais um iniciante.** Você está no nível intermediário-avançado.

Você agora domina:

- Desfazer erros com segurança usando `git restore`, `git reset` e `git revert`
- Guardar trabalho temporário com `git stash`
- Recuperar commits "perdidos" com `git reflog`
- Limpar e reorganizar o histórico com interactive rebase
- Corrigir o último commit com `git commit --amend`
- Copiar commits específicos entre branches com `cherry-pick`
- Resolver problemas reais: `main` vs `master`, remote errado, force push e mais

---

## Próximo passo

Vá para a **Parte 4 — Automação e Profissionalismo Avançado**, onde vamos aprender GitHub Actions — a ferramenta que faz testes, builds e deploys automáticos toda vez que você faz push.
