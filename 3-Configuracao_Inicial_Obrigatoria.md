---
title: "Configuração Inicial Obrigatória"
subtitle: "Git + VS Code + Git Bash"
section: "Parte 0 • Configuração"
series: "Git & GitHub — Do zero ao nível profissional"
author: Esron
brand: Esron Tech Books
---

# Configuração Inicial Obrigatória

> *Git + VS Code + Git Bash*

Antes de escrever uma única linha de código com Git, precisamos montar o ambiente corretamente.

Pense nisso como preparar a cozinha antes de cozinhar: se a faca não corta ou o fogão não acende, tudo vira sofrimento.

> **⚠️ Atenção:** esta configuração é obrigatória. Faça com calma uma única vez e você vai usar por anos.

---

## 01 — Instalando o Git

O Git é o programa que vai controlar as versões do seu código.

### Windows

1. Baixe em: <https://git-scm.com/download/win>
2. Durante a instalação, escolha as opções recomendadas (padrão).
3. Importante: marque **"Git from the command line and also from 3rd-party software"** — necessário para usar no VS Code.

### macOS

```bash
brew install git
```

Ou baixe o instalador oficial em <https://git-scm.com>.

### Linux (Ubuntu/Debian)

```bash
sudo apt update && sudo apt install git
```

### Verificando a instalação

Depois de instalar, rode:

```bash
git --version
```

Deve aparecer algo como `git version 2.XX.X`.

---

## 02 — Configurando sua identidade no Git

O Git precisa saber quem você é. Isso aparece em **todos** os commits.

Abra o terminal (Git Bash no Windows ou Terminal no Mac/Linux) e rode:

```bash
git config --global user.name "Seu Nome Completo"
git config --global user.email "seuemail@exemplo.com"
```

> **💡 Dica importante:** use o **mesmo e-mail** cadastrado na sua conta do GitHub. Assim seus commits aparecem automaticamente vinculados ao seu perfil.

Verifique se ficou certo:

```bash
git config --global user.name
git config --global user.email
```

---

## 03 — Instalando o Visual Studio Code

VS Code é o editor mais usado no mundo atualmente e tem integração excelente com Git.

1. Baixe em: <https://code.visualstudio.com>
2. Instale normalmente.
3. Durante a instalação, marque **todas as opções de integração** (Add to PATH, etc.).

---

## 04 — Configurando o terminal integrado do VS Code

No Windows, o Git Bash é o melhor terminal para usar com Git. Configure assim:

1. Abra o VS Code.
2. Pressione **Ctrl + Shift + P** (Command Palette).
3. Digite: `Terminal: Select Default Profile`.
4. Escolha **Git Bash**.
5. Abra o terminal integrado com **Ctrl + `** (acento grave, tecla ao lado do 1).

> **✅ Resultado:** agora seu terminal dentro do VS Code já usa Git Bash por padrão — isso facilita muito a vida.

---

## 05 — Configurações globais recomendadas do Git

Rode esses comandos uma única vez:

```bash
# Branch padrão será "main" (padrão moderno)
git config --global init.defaultBranch main

# Editor padrão para commits e rebase (abre no VS Code)
git config --global core.editor "code --wait"

# Ativa cores no terminal
git config --global color.ui auto
```

---

## 06 — Extensões essenciais do VS Code para Git

Abra o VS Code, pressione **Ctrl + Shift + X** e instale:

| Extensão | Para que serve |
|---|---|
| **GitLens** | A mais importante — mostra quem mudou cada linha, histórico, blame e muito mais |
| **GitHub Pull Requests and Issues** | Integração nativa com PRs e issues do GitHub |
| **GitHub Copilot** *(opcional)* | Assistente de código com IA |
| **Error Lens** | Exibe erros em tempo real, diretamente na linha do código |

---

## 07 — Teste final da configuração

Crie uma pasta de teste e verifique tudo:

```bash
mkdir teste-config-git
cd teste-config-git
code .
```

Dentro do VS Code, abra o terminal (**Ctrl + `**) e rode:

```bash
git init
git status
```

> **✅ Configuração perfeita:** se tudo apareceu sem erro, seu ambiente está 100% configurado e pronto para aprender Git de verdade.

---

## Resumo Rápido

*Cole na parede ou salve como referência rápida.*

| Etapa | Comando / Ação | Por quê? |
|---|---|---|
| **Instalar Git** | Baixar em git-scm.com | Programa principal |
| **Configurar identidade** | `git config --global user.name` / `user.email` | Aparece em todos os commits |
| **Instalar VS Code** | code.visualstudio.com | Melhor editor + integração com Git |
| **Terminal padrão** | Git Bash no VS Code | Facilita usar comandos Git |
| **Branch padrão** | `init.defaultBranch main` | Padrão atual do GitHub |
| **Editor padrão** | `core.editor "code --wait"` | Commits e rebase abrem no VS Code |

---

## Próximo passo

Crie a pasta `treino-git` no seu computador e mantenha ela aberta no VS Code. Vamos usar ela em todos os exercícios do livro.
