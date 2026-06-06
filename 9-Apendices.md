---
title: "Apêndices"
subtitle: "Material de referência complementar"
section: "Apêndices A–D"
series: "Git & GitHub — Do zero ao nível profissional"
author: Esron
brand: Esron Tech Books
appendices:
  - "Apêndice A — Configurações Recomendadas do VS Code para Git"
  - "Apêndice B — Aliases Úteis para o Dia a Dia"
  - "Apêndice C — Recursos Recomendados para Continuar Aprendendo"
  - "Apêndice D — Soluções Detalhadas dos Exercícios Práticos"
---

# Apêndices

> *Material de referência complementar*

---

## Apêndice A — Configurações Recomendadas do VS Code para Git

Estas configurações vão tornar sua experiência com Git no VS Code muito mais agradável e produtiva. Faça uma vez e esqueça — elas ficam ativas em todos os projetos.

### 01 — Configurações essenciais: settings.json

Pressione **Ctrl + Shift + P**, digite **"Settings (JSON)"** e adicione ou altere:

```json
{
  "git.enableSmartCommit": true,
  "git.autofetch": true,
  "git.confirmSync": false,
  "git.allowForcePush": true,
  "git.branchProtection": ["main", "master"],
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": "explicit"
  },
  "terminal.integrated.defaultProfile.windows": "Git Bash",
  "terminal.integrated.defaultProfile.linux": "bash",
  "terminal.integrated.defaultProfile.osx": "zsh",
  "gitlens.plusFeatures.enabled": false,
  "gitlens.showWelcomeOnInstall": false
}
```

### 02 — Extensões essenciais

Instale todas pelo painel de extensões (**Ctrl + Shift + X**):

| Extensão | Para que serve |
|---|---|
| **GitLens** | Histórico, blame, autores por linha — a mais importante |
| **GitHub Pull Requests and Issues** | Gerenciar PRs e issues sem sair do VS Code |
| **Error Lens** | Exibe erros e avisos inline, ao lado do código |
| **Prettier** | Formatação automática de código ao salvar |
| **ESLint** | Verificação de qualidade e estilo do JavaScript |
| **Markdown All in One** | Preview, shortcuts e edição aprimorada de Markdown |
| **GitHub Copilot** *(opcional)* | Assistente de código com IA |

### 03 — Atalhos úteis no VS Code

| Atalho | O que faz |
|---|---|
| **Ctrl + Shift + G** | Abre o painel Source Control (Git) |
| **Ctrl + Enter** | Stage + Commit rápido (com GitLens ativo) |
| **Alt + Click** (numa linha) | Ver histórico completo daquela linha (GitLens) |
| **Ctrl + Shift + P** | Command Palette — acesso a todos os comandos |
| **Ctrl + `** | Abre o terminal integrado |

---

## Apêndice B — Aliases Úteis para o Dia a Dia

Aliases são atalhos para comandos Git longos. Configure uma vez e ganhe velocidade todos os dias.

### 01 — Configurando os aliases

Abra o arquivo de configuração global do Git:

```bash
git config --global --edit
```

Cole o bloco abaixo dentro da seção `[alias]` (ou crie a seção se não existir):

```ini
[alias]
    st      = status
    co      = checkout
    br      = branch
    sw      = switch
    ci      = commit
    cm      = commit -m
    ca      = commit --amend
    caa     = commit --amend --no-edit
    lg      = log --oneline --graph --all
    lgg     = log --oneline --graph --decorate --all
    diff    = diff --color-words
    undo    = reset HEAD^ --mixed
    unstage = reset HEAD --
    last    = log -1 HEAD --stat
    save    = stash push -m
    pop     = stash pop
    wipe    = reset --hard
    pub     = push -u origin HEAD
    pullr   = pull --rebase
    remotes = remote -v
    who     = shortlog -s -n --all
```

### 02 — Tabela de referência dos aliases

| Alias | Equivale a | Quando usar |
|---|---|---|
| `git st` | `git status` | Verificar estado do repositório |
| `git sw` | `git switch` | Trocar de branch |
| `git cm` | `git commit -m` | Commit com mensagem |
| `git ca` | `git commit --amend` | Corrigir último commit |
| `git caa` | `git commit --amend --no-edit` | Adicionar arquivo ao último commit |
| `git lg` | `git log --oneline --graph --all` | Ver histórico visual de branches |
| `git undo` | `git reset HEAD^ --mixed` | Desfazer último commit |
| `git unstage` | `git reset HEAD --` | Tirar arquivo do staging |
| `git save` | `git stash push -m` | Guardar trabalho com nome |
| `git pop` | `git stash pop` | Recuperar último stash |
| `git pub` | `git push -u origin HEAD` | Primeiro push da branch atual |
| `git pullr` | `git pull --rebase` | Pull sem criar merge commit |
| `git who` | `git shortlog -s -n --all` | Ver quem mais commitou |

---

## Apêndice C — Recursos Recomendados para Continuar Aprendendo

O Git é uma ferramenta com décadas de profundidade. O que está neste livro é o suficiente para trabalhar com excelência — mas se quiser ir além, aqui estão os melhores recursos.

### Documentação oficial

| Recurso | URL |
|---|---|
| **Git Documentation** | https://git-scm.com/doc |
| **Pro Git** *(gratuito, em português)* | https://git-scm.com/book/pt-br |
| **GitHub Docs** | https://docs.github.com |

### Cursos e conteúdo em português

| Recurso | Descrição |
|---|---|
| **Apostilas Fases 1 a 4** | Material base que originou este livro |
| **Canal Gustavo Guanabara** | Git e GitHub no YouTube — linguagem acessível |
| **Rocketseat** | Trilha de Git integrada ao ecossistema Node/React |

### Prática real

| Recurso | Descrição |
|---|---|
| **Issues "good first issue"** | Contribua em projetos open source desde o início |
| **Seus próprios projetos** | Version desde o primeiro commit — sem exceção |
| **Desafios no GitHub** | Explore repositórios de exercícios e katas |

### Ferramentas avançadas para explorar

| Ferramenta | Para que serve |
|---|---|
| **GitHub CLI (`gh`)** | Gerenciar o GitHub inteiramente pelo terminal |
| **GitKraken ou Sourcetree** | Interface gráfica para visualizar branches e histórico |
| **Conventional Commits + Commitizen** | Automatizar e padronizar mensagens de commit |
| **Husky + lint-staged** | Executar verificações automáticas antes de cada commit |

### Livros recomendados

| Livro | Descrição |
|---|---|
| **Pro Git — Scott Chacon** | A referência definitiva. Gratuito online. |
| **Git Pocket Guide — R. Silverman** | Referência compacta para consulta rápida |

---

## Apêndice D — Soluções Detalhadas dos Exercícios Práticos

Resoluções completas dos 11 exercícios do Capítulo 15. Cada exercício traz a situação, os passos com comandos e a lição principal.

---

### Exercício 01 — Seu primeiro repositório completo

**Situação:** você está começando um novo projeto do zero e quer versioná-lo corretamente desde o início.

```bash
mkdir meu-projeto && cd meu-projeto
git init

# Crie os arquivos iniciais (README.md, index.html, etc.)

git add .
git commit -m "feat: estrutura inicial do projeto"

# Crie o repositório no GitHub (sem README). Copie a URL.

git remote add origin <url>
git push -u origin main
```

> *Todo projeto merece um repositório desde o primeiro arquivo. Nunca "vou fazer depois".*

---

### Exercício 02 — Trabalhando com branches

**Situação:** você precisa adicionar uma nova funcionalidade sem afetar o código estável da `main`.

```bash
git switch -c feature/nova-funcionalidade

# Faça as modificações necessárias nos arquivos.

git add . && git commit -m "feat: adiciona nova funcionalidade"
git switch main && git merge feature/nova-funcionalidade
git branch -d feature/nova-funcionalidade
```

> *Branches são baratas e rápidas no Git. Use uma para cada funcionalidade, sem exceção.*

---

### Exercício 03 — Desfazendo um erro

**Situação:** você commitou arquivos errados ou com uma mensagem ruim e precisa corrigir.

```bash
git log --oneline           # identifique o commit problemático
git reset --soft HEAD~1     # desfaz o commit, mantém os arquivos

# Corrija o que for necessário nos arquivos.

git add . && git commit -m "feat: mensagem correta"
```

> *`git reset --soft` é seguro. Só use `--hard` quando tiver certeza absoluta.*

---

### Exercício 04 — Simulando main vs master

**Situação:** o GitHub criou a branch `main` mas seu repositório local usa `master` — os históricos não se conectam.

```bash
git switch master
git merge main --allow-unrelated-histories

# Resolva eventuais conflitos.

git push origin master
git push origin --delete main   # opcional: remove branch main remota
```

> *A flag `--allow-unrelated-histories` força o Git a unir dois históricos independentes.*

---

### Exercício 05 — Publicando no GitHub do zero

**Situação:** você tem um projeto local pronto e quer publicá-lo no GitHub pela primeira vez.

```bash
# Crie o repositório no GitHub — sem marcar "Add a README file".
# Copie a URL HTTPS ou SSH gerada.

git remote add origin <url>
git branch -M main
git push -u origin main
```

> *O `-u` no primeiro push configura o rastreamento. Nos próximos, basta `git push`.*

---

### Exercício 06 — Corrigindo remote errado

**Situação:** você percebeu que o repositório local está apontando para a URL errada no GitHub.

```bash
git remote -v    # confirme qual URL está configurada
git remote set-url origin https://github.com/SEU-USUARIO/repo-correto.git
git remote -v    # confirme a correção
git push origin main
```

> *Sempre verifique `git remote -v` antes de fazer push em repositórios novos.*

---

### Exercício 07 — PC formatado: recuperando o projeto

**Situação:** seu computador foi formatado e você precisa retomar o trabalho de onde parou.

```bash
# Instale Git e VS Code (conforme Parte 0 do livro).

git config --global user.name "Seu Nome"
git config --global user.email "email@exemplo.com"
git clone https://github.com/SEU-USUARIO/projeto.git

# Abra a pasta no VS Code e continue normalmente.
```

> *O GitHub é seu backup. Enquanto você fizer push regularmente, nunca perde nada.*

---

### Exercício 08 — Dois PCs, um projeto

**Situação:** você trabalha no projeto em casa e no trabalho. Precisa manter os dois sincronizados.

```bash
git pull origin main              # sempre antes de começar a trabalhar

# Faça suas alterações normalmente.

git add . && git commit -m "feat: trabalho do dia"
git push origin main              # sempre ao terminar

# No outro computador: git pull antes de continuar.
```

> *Pull antes, push depois. Esse hábito evita 90% dos conflitos em projetos pessoais.*

---

### Exercício 09 — Equipe com arquivos diferentes

**Situação:** duas pessoas do time editaram arquivos diferentes ao mesmo tempo. O merge cria um histórico duplo.

```bash
# Pessoa A: commita alterações em index.html e faz push.

# Pessoa B: commita alterações em style.css (sem ter feito pull antes).
git pull origin main    # Git cria um merge commit automático
git push origin main

# Nenhum conflito — arquivos diferentes, merge automático.
```

> *Quando dois colaboradores editam arquivos diferentes, o Git resolve o merge sozinho.*

---

### Exercício 10 — Conflito no mesmo arquivo: resolução avançada

**Situação:** dois colaboradores editaram a mesma função no mesmo arquivo. O Git não sabe qual versão usar.

```bash
# Pessoa A: altera a função com desconto de 15% e faz push.

# Pessoa B:
git pull origin main    # conflito aparece

# Abra o arquivo — localize os marcadores <<<<<<, ======= e >>>>>>>.
# Decida qual versão fica (ou combine as duas).
# Remova os marcadores.

git add <arquivo> && git commit
```

> *Conflito não é erro do Git. É falta de comunicação na equipe — resolva e siga em frente.*

---

### Exercício 11 — Fork + Pull Request: fluxo open source

**Situação:** você quer contribuir com um projeto open source do qual não é colaborador direto.

```bash
# Acesse o repositório no GitHub e clique em Fork.

git clone https://github.com/SEU-USUARIO/repo-forkado.git
git remote add upstream https://github.com/DONO/repo-original.git
git pull upstream main                         # atualizar antes de trabalhar
git switch -c feature/minha-contribuicao

# Faça as alterações. Commite com mensagem clara.

git push origin feature/minha-contribuicao

# No GitHub: abra um Pull Request do seu fork para o repositório original.
```

> *O fluxo Fork + PR é como milhões de projetos open source recebem contribuições todos os dias.*

---

*Fim dos Apêndices*

*Git & GitHub: Do zero ao nível profissional · Esron · 2026*
