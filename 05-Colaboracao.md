---
title: "Colaboração"
subtitle: "Nível Intermediário"
section: "Parte 2"
series: "Git & GitHub — Do zero ao nível profissional"
author: Esron
brand: Esron Tech Books
chapters:
  - "Capítulo 5 — Branches: O Coração do Git"
  - "Capítulo 6 — Merge, Conflitos e Pull Requests"
  - "Capítulo 7 — Trabalhando em Equipe e Open Source"
---

# Parte 2 — Colaboração

> *Nível Intermediário*

Agora que você já sabe andar sozinho com Git, vamos aprender a **andar com outras pessoas** — ou com você mesmo em momentos diferentes.

Trabalhar sozinho é fácil. Trabalhar em equipe é onde a maioria das pessoas se enrola.

> **A ideia central desta parte:** branches são o segredo. Elas permitem que várias pessoas — ou você em funcionalidades diferentes — trabalhem ao mesmo tempo sem pisar no pé umas das outras.
>
> Imagine uma estrada principal (a branch `main`). Cada nova funcionalidade é uma rua paralela que você constrói sem atrapalhar o tráfego. Quando a rua está pronta e testada, você a conecta de volta à estrada principal de forma segura.

---

## Capítulo 5 — Branches: O Coração do Git

### 01 — O que é uma branch?

Uma branch (ramo) é uma linha independente de desenvolvimento.

Por padrão, todo repositório tem uma branch principal chamada **main** (antigamente era **master**). Ela representa a versão estável do projeto — aquela que está em produção ou pronta para o cliente.

Quando você quer adicionar uma nova funcionalidade, corrigir um bug ou testar algo, você **não trabalha direto na main**. Você cria uma branch separada.

> **🛣️ Analogia simples:** a `main` é a estrada principal da cidade. Cada branch é uma rua paralela onde você pode construir, testar, errar e consertar — sem fechar a estrada principal.

### 02 — Comandos básicos de branches

```bash
# Ver em qual branch você está
git branch

# Criar uma nova branch e já mudar para ela (comando mais usado)
git switch -c feature/login

# Listar todas as branches (locais e remotas)
git branch -a

# Voltar para a branch main
git switch main

# Deletar uma branch após o trabalho ser integrado
git branch -d feature/login

# -D (maiúsculo): força a deleção sem verificar merge
# Use com cuidado — apaga mesmo sem merge
git branch -D feature/login
```

### 03 — Boas práticas de nomes de branches

| Prefixo | Quando usar | Exemplo |
|---|---|---|
| `feature/` | Nova funcionalidade | `feature/cadastro-usuarios` |
| `bugfix/` | Correção de erro | `bugfix/login-erro-500` |
| `hotfix/` | Correção crítica em produção | `hotfix/pagamento-quebrado` |
| `experiment/` | Testes descartáveis | `experiment/nova-ui` |

Exemplo real de criação com nome correto:

```bash
git switch -c feature/cadastro-usuarios
```

> **💡 Dica de fluxo:** faça commits normalmente na sua branch. Quando terminar, volte para a `main` e integre o trabalho. Nunca deixe código inacabado acumulando na `main`.

---

## Capítulo 6 — Merge, Conflitos e Pull Requests

### 01 — Fazendo merge: juntando branches

```bash
# 1. Vá para a branch principal
git switch main

# 2. Atualize com as últimas mudanças do remoto
git pull origin main

# 3. Traga o trabalho da sua branch
git merge feature/login
```

Existem dois resultados comuns após um merge:

- **Fast-forward** — o Git simplesmente avança o ponteiro. O histórico fica linear e limpo.
- **Merge commit** — cria um commit especial que une as duas linhas de desenvolvimento. Acontece quando as duas branches divergiram.

### 02 — Conflitos de merge: o que acontece na vida real

Quando duas pessoas editam a mesma linha do mesmo arquivo ao mesmo tempo, o Git não sabe qual versão escolher. Ele para e marca o conflito diretamente no arquivo:

```
<<<<<<< HEAD
function calcularDesconto(valor) {
    return valor * 0.15;
}
=======
function calcularDesconto(valor) {
    return valor * 0.20;
}
>>>>>>> feature/desconto
```

**Como resolver — passo a passo:**

1. Abra o arquivo e decida qual versão fica (ou combine as duas).
2. Remova os marcadores `<<<<<<<`, `=======` e `>>>>>>>`.
3. Salve o arquivo.
4. Rode `git add nome-do-arquivo`.
5. Rode `git commit` — o Git já sugere uma mensagem padrão para conflitos.

> **Conflito não é erro — é normal.** Todo desenvolvedor experiente já resolveu centenas de conflitos. O Git apenas está pedindo que você tome uma decisão. Com prática, isso vira rotina.

### 03 — Pull Requests: a forma profissional de colaborar

Em vez de fazer merge direto no terminal, o fluxo moderno em equipe usa **Pull Requests (PRs)**. Eles garantem que alguém revise o código antes de entrar na `main`.

**Fluxo completo de um Pull Request:**

1. Trabalhe na sua branch e faça os commits.
2. Envie para o GitHub: `git push origin feature/nome`
3. No GitHub, clique em **"Compare & pull request"**.
4. Escreva uma boa descrição do que foi feito e por quê.
5. Peça revisão a um colega (code review).
6. Após aprovação, faça o merge pelo GitHub.

> **✅ Vantagem do PR:** a branch principal fica sempre estável. Nenhum código entra na `main` sem ter sido revisado — isso é o que as melhores equipes do mercado fazem.

---

## Capítulo 7 — Trabalhando em Equipe e Open Source

### 01 — GitHub Flow: o fluxo recomendado para equipes

| # | Etapa |
|---|---|
| **1** | `main` sempre estável — nunca commite direto nela |
| **2** | Crie uma branch com nome claro: `feature/`, `bugfix/`, etc. |
| **3** | Faça commits pequenos e frequentes com mensagens claras |
| **4** | Abra um Pull Request com descrição do que foi feito |
| **5** | Aguarde o code review de um colega |
| **6** | Merge na `main` somente após aprovação |
| **7** | Delete a branch após o merge |

> **Por que este fluxo funciona?** É simples o suficiente para times pequenos, mas robusto o suficiente para times grandes. Empresas como GitHub, Basecamp e Shopify usam variações desse modelo.

### 02 — Fork + Pull Request: contribuindo em projetos de terceiros

Quando você não tem permissão para escrever diretamente em um repositório — como em projetos open source — o fluxo é via **Fork**.

**Passo a passo:**

1. Clique em **Fork** no GitHub (cria uma cópia do projeto na sua conta).

2. Clone o seu fork:

```bash
git clone https://github.com/SEU-USUARIO/projeto.git
```

3. Adicione o repositório original como **upstream**:

```bash
git remote add upstream https://github.com/DONO-ORIGINAL/projeto.git
```

4. Sempre atualize antes de trabalhar:

```bash
git pull upstream main
```

5. Crie sua branch, faça o trabalho e envie para o seu fork.

6. Abra um Pull Request do seu fork para o repositório original.

### 03 — Comandos úteis para trabalho com forks

```bash
# Ver os remotos configurados
git remote -v

# Atualizar com o projeto original
git pull upstream main

# Enviar sua contribuição
git push origin feature/minha-contribuicao
```

> **`origin` vs `upstream`**
>
> - `origin` = o seu fork (você tem permissão de escrita)
> - `upstream` = o repositório original (somente leitura para você)
>
> Nunca tente dar push direto no `upstream`.

---

## ✅ Fim da Parte 2

Você agora entende:

- Como usar branches para trabalhar em paralelo sem conflitos
- Como juntar trabalho com `git merge`
- Como identificar e resolver conflitos de merge
- Como colaborar de forma profissional usando Pull Requests
- Como contribuir em projetos open source usando Fork
- O GitHub Flow — fluxo padrão de equipes profissionais

---

## Próximo passo

Vá para a **Parte 3 — Nível Profissional**, onde você vai aprender os comandos que os desenvolvedores experientes usam para desfazer erros, limpar histórico e trabalhar com confiança em projetos grandes.
