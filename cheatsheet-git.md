---
title: "Git — Cheat Sheet Completo"
subtitle: "Referência Rápida"
series: "Git & GitHub — Do zero ao nível profissional"
volume: "Apostila 4 de 4"
author: Esron
brand: Esron Tech Books
version: "git 2.x"
year: 2025
---

# Git — Cheat Sheet Completo

> Referência rápida. Consulte as Apostilas 1, 2 e 3 para explicações detalhadas.

---

## Índice

| | Seção | Tópicos |
|---|---|---|
| 🖥️ | [Terminal — Arquivos & Pastas](#️-terminal--arquivos--pastas) | Navegação · Pastas · Arquivos · Mover/Copiar · Produtividade |
| 📁 | [Arquivos & Repositório Git](#-arquivos--repositório-git) | Iniciar · Mover/Deletar · .gitignore · Restaurar |
| 💾 | [Commits & Histórico](#-commits--histórico) | Staging · Commits · Diff · Log · Desfazer · Referências |
| 🌿 | [Branches & Merge](#-branches--merge) | Gerenciar · Merge · Rebase · Squash · Histórico |
| ☁️ | [Remoto & GitHub](#️-remoto--github) | Remotos · Push · Pull · Fork · Tags · Config · Aliases |

---

## 🖥️ Terminal — Arquivos & Pastas

### 📍 Navegação

| Descrição | Comando |
|---|---|
| Mostrar pasta atual | `pwd` |
| Listar arquivos e pastas | `ls` |
| Listar com detalhes | `ls -l` |
| Listar incluindo ocultos | `ls -la` |
| Entrar em uma pasta | `cd nome-da-pasta` |
| Voltar uma pasta acima | `cd ..` |
| Voltar duas pastas acima | `cd ../..` |
| Ir para a pasta raiz do usuário | `cd ~` ou só `cd` |
| Voltar para a pasta anterior | `cd -` |

> **💡 Dica:** pressione **Tab** para autocompletar nomes de arquivos e pastas.

---

### 📂 Pastas — Criar e Excluir

| Descrição | Comando |
|---|---|
| Criar pasta | `mkdir minha-pasta` |
| Criar várias pastas de uma vez | `mkdir pasta-a pasta-b pasta-c` |
| Criar pasta e subpastas de uma vez | `mkdir -p projetos/2025/janeiro` |
| Criar pasta e já entrar nela | `mkdir minha-pasta && cd minha-pasta` |
| Deletar pasta vazia | `rmdir minha-pasta` |
| Deletar pasta e todo o conteúdo ⚠️ | `rm -rf minha-pasta` |

> **⚠️ Nomes compostos:** prefira **hífen** (`meu-projeto`, não `Meu Projeto`). Espaços no nome exigem aspas ou escape em todo comando: `cd "Meu Projeto"` ou `cd Meu\ Projeto`.

> **⚠️ `rm -rf` é irreversível:** não vai para a lixeira. Use `ls` antes para confirmar o que será apagado.

---

### 📄 Arquivos — Criar, Ler e Excluir

| Descrição | Comando |
|---|---|
| Criar arquivo vazio | `touch index.html` |
| Criar vários arquivos de uma vez | `touch index.html style.css app.js` |
| Criar arquivo já com conteúdo | `echo "# Título" > README.md` |
| Adicionar conteúdo sem apagar o existente | `echo "nova linha" >> README.md` |
| Ver conteúdo do arquivo | `cat arquivo.txt` |
| Ver as primeiras N linhas | `head -n 10 arquivo.txt` |
| Ver as últimas N linhas | `tail -n 10 arquivo.txt` |
| Deletar arquivo | `rm arquivo.txt` |
| Deletar todos os arquivos com extensão | `rm *.log` |

> **⚠️ `>` substitui tudo. `>>` adiciona ao final.** Confundir os dois apaga conteúdo sem aviso.

---

### ✏️ Renomear, Mover e Copiar

| Descrição | Comando |
|---|---|
| Renomear arquivo ou pasta | `mv nome-antigo nome-novo` |
| Mover arquivo para outra pasta | `mv arquivo.txt pasta/` |
| Mover e renomear ao mesmo tempo | `mv rascunho.md docs/versao-final.md` |
| Mover vários arquivos para uma pasta | `mv *.html src/` |
| Copiar arquivo | `cp origem.txt destino.txt` |
| Copiar para outra pasta | `cp arquivo.txt backup/` |
| Copiar pasta inteira | `cp -r pasta-original pasta-copia` |

---

### ⚡ Produtividade no Terminal

| Descrição | Comando / Tecla |
|---|---|
| Autocompletar nome | **Tab** |
| Repetir último comando | **↑** (seta para cima) |
| Limpar a tela | `clear` ou **Ctrl + L** |
| Cancelar comando em execução | **Ctrl + C** |
| Ver histórico de comandos | `history` |
| Abrir VS Code na pasta atual | `code .` |

[↑ voltar ao índice](#índice)

---

## 📁 Arquivos & Repositório Git

### 🚀 Iniciando

| Descrição | Comando |
|---|---|
| Criar repositório novo | `git init` |
| Clonar repositório existente | `git clone <url>` |
| Clonar com nome diferente | `git clone <url> outro-nome` |

---

### 📁 Arquivos — Mover e Deletar

| Descrição | Comando |
|---|---|
| Mover ou renomear arquivo | `git mv <antigo> <novo>` |
| Deletar arquivo e stagear remoção | `git rm <arquivo>` |
| Remover do Git mas manter no disco | `git rm --cached <arquivo>` |
| Remover arquivos não rastreados | `git clean -fd` |

> **⚠️ Atenção:** use `--cached` quando tiver commitado um `.env` acidentalmente — remove do Git sem deletar do disco.

---

### 🚫 .gitignore

```gitignore
# Pastas de dependências
node_modules/
venv/
__pycache__/

# Builds e compilados
dist/
build/
*.pyc

# Variáveis de ambiente
.env
.env.local
*.log

# Sistema operacional
.DS_Store
Thumbs.db
```

> **💡 Dica:** use **gitignore.io** para gerar automaticamente para sua stack.

---

### ⏪ Restaurar Arquivo Antigo

| Descrição | Comando |
|---|---|
| Versão de 3 commits atrás | `git restore <arquivo> --source HEAD~3` |
| Versão de uma tag | `git restore <arquivo> --source v1.0.0` |
| Forma alternativa | `git checkout <commit> -- <arquivo>` |

[↑ voltar ao índice](#índice)

---

## 💾 Commits & Histórico

### 📦 Preparando Commits (Staging)

| Descrição | Comando |
|---|---|
| Adicionar arquivo específico | `git add <arquivo>` |
| Adicionar tudo | `git add .` |
| Modo interativo — escolhe partes | `git add -p` |
| Ver estado atual | `git status` |
| Tirar arquivo do staging | `git reset <arquivo>` |
| Tirar tudo do staging | `git reset` |

---

### 💾 Fazendo Commits

| Descrição | Comando |
|---|---|
| Commit com editor de texto | `git commit` |
| Commit com mensagem inline | `git commit -m 'mensagem'` |
| Stagear rastreados + commitar | `git commit -am 'mensagem'` |
| Corrigir último commit | `git commit --amend` |

> **⚠️ Nunca** use `--amend` em commits já publicados no remoto.

---

### 🔍 Visualizando Diferenças

#### Staged vs Unstaged

| Descrição | Comando |
|---|---|
| Mudanças não staged | `git diff` |
| Mudanças staged | `git diff --staged` |
| Staged + unstaged vs último commit | `git diff HEAD` |

#### Entre Commits

| Descrição | Comando |
|---|---|
| Diff de um commit vs pai | `git show <commit>` |
| Diff entre dois commits | `git diff <c1> <c2>` |
| Diff de um arquivo desde commit | `git diff <commit> <arquivo>` |
| Resumo de quantas linhas mudaram | `git diff <commit> --stat` |

---

### 📜 Histórico — git log

#### Formatos visuais

| Descrição | Comando |
|---|---|
| Histórico da branch | `git log main` |
| Uma linha por commit | `git log --oneline` |
| Árvore visual de branches | `git log --oneline --graph --all` |
| Últimos N commits | `git log --oneline -10` |
| Commits que tocaram um arquivo | `git log <arquivo>` |
| Incluindo antes de renomear | `git log --follow <arquivo>` |
| Quem escreveu cada linha | `git blame <arquivo>` |

#### Filtros

| Descrição | Comando |
|---|---|
| Por autor | `git log --author="Esron"` |
| Por data — a partir de | `git log --since="2 weeks ago"` |
| Por data — até | `git log --until="2025-01-01"` |
| Por texto na mensagem do commit | `git log --grep="fix"` |
| Commits que adicionaram/removeram texto no código | `git log -G "texto"` |

---

### ↩️ Desfazendo Alterações

| Descrição | Comando |
|---|---|
| Descartar mudanças de um arquivo | `git restore <arquivo>` |
| Descartar staged + unstaged de um arquivo | `git restore --staged --worktree <arquivo>` |
| Desfazer último commit | `git reset --soft HEAD~1` |
| Reverter commit já publicado (seguro) | `git revert <commit>` |

#### Modos do git reset

| Modo | Desfaz commit? | Mantém no staging? | Mantém nos arquivos? |
|---|---|---|---|
| `--soft` | ✅ Sim | ✅ Sim | ✅ Sim |
| `--mixed` *(padrão)* | ✅ Sim | ❌ Não | ✅ Sim |
| `--hard` | ✅ Sim | ❌ Não | ❌ Não ⚠️ |

```bash
git reset --soft HEAD~1   # desfaz o commit, mantém tudo no staging
git reset HEAD~1          # desfaz o commit, tira do staging
git reset --hard HEAD~1   # desfaz o commit e apaga as mudanças ⚠️
```

> **⚠️ `--hard` é irreversível.** Em caso de acidente, consulte `git reflog` antes de entrar em pânico.
| Guardar trabalho temporariamente | `git stash` |
| Guardar com nome descritivo | `git stash push -m "wip: login"` |
| Listar todos os stashes salvos | `git stash list` |
| Recuperar e remover o último stash | `git stash pop` |
| Aplicar stash específico sem remover | `git stash apply stash@{2}` |
| Descartar stash específico | `git stash drop stash@{0}` |
| Apagar todos os stashes | `git stash clear` |
| Histórico de todos os HEADs | `git reflog` |

---

### 🏷️ Referências de Commit

| Referência | Significado |
|---|---|
| `main` | último commit da branch |
| `v1.0.0` | commit marcado com tag |
| `3e887ab` | hash curto do commit |
| `origin/main` | branch remota |
| `HEAD` | commit atual |
| `HEAD~3` | 3 commits atrás |
| `HEAD^^^` | mesmo que HEAD~3 |

[↑ voltar ao índice](#índice)

---

## 🌿 Branches & Merge

### 🌿 Gerenciando Branches

| Descrição | Comando |
|---|---|
| Listar branches locais | `git branch` |
| Listar locais + remotos | `git branch -a` |
| Listar por commit mais recente | `git branch --sort=-committerdate` |
| Trocar de branch | `git switch <nome>` *(ou `git checkout <nome>`)* |
| Criar branch e trocar | `git switch -c <nome>` *(ou `git checkout -b <nome>`)* |
| Voltar para branch anterior | `git switch -` |
| Renomear branch atual | `git branch -M novo-nome` |
| Deletar branch (seguro) | `git branch -d <nome>` |
| Forçar deleção | `git branch -D <nome>` |
| Deletar branch no GitHub | `git push origin --delete <nome>` |

---

### 🔀 Combinando Branches

#### Merge — preserva histórico

```bash
git switch main
git merge feature
```

```
# antes → depois
A─B─C   D─E  (feature)
A─B─C─◆─E   (merge commit)
```

#### Rebase — histórico linear

```bash
git switch feature
git rebase main
```

```
# antes → depois
A─B─C  (main)   D─E  (feature)
A─B─C─D'─E'     (feature rebaseada)
```

> **⚠️ Cuidado:** nunca rebase branches que outros colaboradores usam.

#### Squash — compacta em 1 commit

```bash
git switch main
git merge --squash feature
git commit -m 'Implementa X'
```

#### Fast-forward — avança o ponteiro

```bash
# Quando main não divergiu
git switch main
git merge feature
```

#### Cherry-pick — copia um commit

```bash
git cherry-pick <commit-id>
```

#### Históricos não relacionados

```bash
# Quando Git rejeita o merge (main vs master)
git merge main --allow-unrelated-histories
```

---

### ✏️ Editando Histórico

| Descrição | Comando |
|---|---|
| Squash dos últimos 5 commits | `git rebase -i HEAD~6` |
| Desfazer rebase que deu errado | `git reflog BRANCH` → `git reset --hard <commit>` |

> No editor interativo do rebase: troque **`pick`** por **`fixup`** nos commits a fundir.

[↑ voltar ao índice](#índice)

---

## ☁️ Remoto & GitHub

### 🔗 Gerenciando Remotos

| Descrição | Comando |
|---|---|
| Listar remotos e URLs | `git remote -v` |
| Adicionar remote | `git remote add <nome> <url>` |
| Corrigir URL sem remover | `git remote set-url origin <url>` |
| Remover remote completamente | `git remote remove origin` |
| Renomear remote | `git remote rename origin upstream` |

---

### 🚀 Publicar Repositório Novo

Fluxo completo: `git init` → `git add .` → `git commit` → `git push`

```bash
echo "# projeto" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin <url>
git push -u origin main
```

---

### ⬆️ Enviando — git push

| Descrição | Comando |
|---|---|
| Enviar branch main | `git push origin main` |
| Enviar branch atual (após `-u`) | `git push` |
| Primeiro push — configura tracking | `git push -u origin <branch>` |
| Force push seguro | `git push --force-with-lease` |
| Enviar todas as tags | `git push --tags` |
| Deletar branch no remoto | `git push origin --delete <branch>` |

---

### ⬇️ Recebendo — git pull / fetch

| Descrição | Comando |
|---|---|
| Baixar SEM aplicar (seguro) | `git fetch origin main` |
| Baixar todas as branches remotas | `git fetch --all` |
| Baixar e remover referências de branches deletadas no remoto | `git fetch --prune` |
| Fetch + merge (padrão) | `git pull` |
| Especificar remote e branch | `git pull origin main` |
| Fetch + rebase (histórico limpo) | `git pull --rebase` |
| Buscar do upstream (Fork) | `git pull upstream main` |

---

### 🍴 Fork e Upstream

```bash
# 1. Clonar o seu Fork
git clone <url-do-seu-fork>

# 2. Adicionar repositório original
git remote add upstream <url-original>

# 3. Atualizar Fork com o original
git pull upstream main
git push origin main
```

| Remote | Papel |
|---|---|
| `origin` | seu Fork — você escreve aqui |
| `upstream` | repo original — só leitura |

---

### 🏷️ Tags — Marcando Versões

| Descrição | Comando |
|---|---|
| Criar tag no commit atual | `git tag v1.0.0` |
| Tag anotada com mensagem | `git tag -a v1.0.0 -m "Release 1.0"` |
| Enviar tags para o remoto | `git push --tags` |

---

### ⚙️ Configuração Global

| Descrição | Comando |
|---|---|
| Nome | `git config --global user.name 'Nome'` |
| E-mail | `git config --global user.email 'e@mail.com'` |
| Editor padrão (VS Code) | `git config --global core.editor "code --wait"` |
| Branch inicial padrão | `git config --global init.defaultBranch main` |
| Criar alias | `git config --global alias.st status` |
| Ver todas as configurações | `git config --global --list` |

#### Arquivos importantes

| Arquivo | Descrição |
|---|---|
| `.git/config` | configuração local do repositório |
| `~/.gitconfig` | configuração global do usuário |
| `.gitignore` | arquivos ignorados pelo Git |

---

### ⚡ Aliases Recomendados

| Alias | Equivale a |
|---|---|
| `git st` | `git status` |
| `git co` | `git checkout` |
| `git br` | `git branch` |
| `git lg` | `git log --oneline --graph --all` |
| `git undo` | `git reset HEAD^` |
| `git pub` | `git push -u origin HEAD` |

Para configurar todos de uma vez:

```bash
git config --global alias.st   status
git config --global alias.co   checkout
git config --global alias.br   branch
git config --global alias.lg   "log --oneline --graph --all"
git config --global alias.undo "reset HEAD^"
git config --global alias.pub  "push -u origin HEAD"
```

[↑ voltar ao índice](#índice)

---

*Apostila 4 — Cheat Sheet Git · Esron Tech Books · 2025*
*Baseada em `git --help` · Consulte as Apostilas 1, 2 e 3 para explicações detalhadas*
