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

> As soluções completas e detalhadas dos 11 exercícios práticos estão no arquivo **`10-Apendice_D_Solucoes_Detalhadas.md`**.
>
> Lá você encontra, para cada exercício: situação, objetivo, passo a passo comentado, resultado esperado e lição aprendida.

---

*Fim dos Apêndices*

*Git & GitHub: Do zero ao nível profissional · Esron · 2026*
