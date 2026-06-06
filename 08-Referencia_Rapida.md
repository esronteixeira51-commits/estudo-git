---
title: "Referência Rápida"
subtitle: "Consulta em segundos"
section: "Parte 5"
series: "Git & GitHub — Do zero ao nível profissional"
author: Esron
brand: Esron Tech Books
chapters:
  - "Capítulo 13 — Cheat Sheet Completo"
  - "Capítulo 14 — Dicionário de Comandos e Problemas Comuns"
  - "Capítulo 15 — Exercícios Práticos com Resoluções"
  - "Apêndices A–D"
---

# Parte 5 — Referência Rápida

> *Consulta em segundos*

Você chegou à parte mais usada do livro.

Enquanto as partes anteriores são para **estudar**, esta parte foi feita para **consultar rapidamente**. Quando você estiver no meio de um projeto e pensar "como era mesmo aquele comando?" — é aqui que você vai vir.

> **Organização desta parte:** cheat sheet por categoria, dicionário de problemas com soluções diretas, lista de exercícios com resolução e apêndices de referência. Tudo estruturado para você encontrar o que precisa em menos de 10 segundos.

---

## Capítulo 13 — Cheat Sheet Completo

*Todos os comandos essenciais organizados por categoria*

---

### 🚀 Iniciando um Repositório

| Comando | O que faz |
|---|---|
| `git init` | Inicializa um novo repositório local |
| `git clone <url>` | Clona um repositório remoto para o seu computador |

---

### 🔄 Status e Ciclo Básico

| Comando | O que faz |
|---|---|
| `git status` | Ver o estado atual dos arquivos |
| `git add .` | Adicionar todos os arquivos ao staging |
| `git add <arquivo>` | Adicionar um arquivo específico |
| `git commit -m "msg"` | Commitar com mensagem |
| `git commit -am "msg"` | Add + Commit (apenas arquivos já rastreados) |

---

### 📜 Histórico

| Comando | O que faz |
|---|---|
| `git log --oneline` | Histórico resumido — um commit por linha |
| `git log --oneline --graph` | Histórico com grafo visual de branches |
| `git log -p` | Histórico com as diferenças de cada commit |

---

### 🌿 Branches

| Comando | O que faz |
|---|---|
| `git branch` | Listar branches locais (branch atual marcada com `*`) |
| `git branch -a` | Listar todas as branches (locais e remotas) |
| `git switch -c <nome>` | Criar e mudar para nova branch |
| `git switch main` | Voltar para a branch main |
| `git branch -d <nome>` | Deletar branch (somente se já foi mergeada) |
| `git branch -D <nome>` | Forçar deleção — sem verificação de merge ⚠️ |

---

### ☁️ Sincronização com GitHub

| Comando | O que faz |
|---|---|
| `git remote -v` | Ver os remotos configurados |
| `git push origin main` | Enviar commits para o GitHub |
| `git pull origin main` | Trazer mudanças do GitHub |
| `git push -u origin main` | Primeiro push — configura rastreamento automático |

---

### ↩️ Desfazendo Coisas

| Comando | O que faz |
|---|---|
| `git restore <arquivo>` | Desfazer mudanças não commitadas em um arquivo |
| `git restore .` | Desfazer todas as mudanças não commitadas |
| `git reset HEAD~1` | Desfazer último commit (mantém os arquivos) |
| `git reset --soft HEAD~1` | Desfazer commit e manter mudanças no staging |
| `git reset --hard HEAD~1` | ⚠️ Desfazer commit E apagar as mudanças |
| `git revert <commit>` | Desfazer commit de forma segura (cria novo commit) |
| `git stash` | Guardar mudanças temporariamente |
| `git stash pop` | Recuperar o último stash |

---

### ✏️ Reorganizando o Histórico

| Comando | O que faz |
|---|---|
| `git rebase -i HEAD~5` | Rebase interativo nos últimos 5 commits |
| `git commit --amend` | Corrigir a mensagem ou conteúdo do último commit |
| `git cherry-pick <commit>` | Copiar um commit específico para a branch atual |
| `git reflog` | Ver histórico completo de operações (salva-vidas) |

---

### 🍴 Remotos e Fork

| Comando | O que faz |
|---|---|
| `git remote add upstream <url>` | Adicionar o repositório original como upstream |
| `git pull upstream main` | Atualizar fork com as mudanças do original |
| `git remote set-url origin <url>` | Corrigir a URL do remote origin |
| `git remote -v` | Ver todos os remotos configurados |

---

### ⚙️ Workflow básico de GitHub Actions

Salve como `.github/workflows/ci.yml`:

```yaml
name: CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4
      - run: npm ci
      - run: npm test
```

---

## Capítulo 14 — Dicionário de Comandos e Problemas Comuns

*Como faço isso? — Respostas diretas*

### 01 — Soluções rápidas por situação

| Situação / Problema | Solução |
|---|---|
| Quero desfazer mudanças que ainda não commitei | `git restore .` ou `git restore <arquivo>` |
| Quero desfazer o último commit, mantendo as alterações | `git reset --soft HEAD~1` |
| Apaguei tudo por acidente com `--hard` | `git reflog` → `git reset --hard <hash>` |
| Fiz commit com mensagem errada | `git commit --amend` |
| Quero juntar vários commits em um só | `git rebase -i HEAD~n` → `squash` ou `fixup` |
| Conflito no merge | Editar arquivo → remover marcadores → `git add` → `git commit` |
| `main` e `master` com históricos divergentes | `git merge main --allow-unrelated-histories` |
| Remote apontando para o lugar errado | `git remote set-url origin <nova-url>` |
| Quero remover arquivo do Git mas manter no computador | `git rm --cached <arquivo>` |
| Preciso voltar para versão antiga de um arquivo | `git restore --source HEAD~3 <arquivo>` |

---

### 02 — Erros comuns e soluções

| Mensagem de erro | O que fazer |
|---|---|
| `fatal: refusing to merge unrelated histories` | `git merge --allow-unrelated-histories` |
| `Everything up-to-date` mas há mudanças | Verifique a branch atual: `git branch` |
| `Permission denied` ao fazer push | Verifique o remote: `git remote -v` |

---

## Capítulo 15 — Exercícios Práticos com Resoluções

*11 situações reais — do básico ao avançado*

Esta seção contém os 11 exercícios práticos do livro, com situação real, objetivo, passo a passo e lição aprendida.

| # | Exercício | Foco |
|---|---|---|
| **01** | Primeiro repositório completo | Configurar, inicializar, commitar e publicar no GitHub do zero |
| **02** | Trabalhando com branches | Criar, comutar, commitar e deletar branches de forma correta |
| **03** | Desfazendo erros | Praticar `restore`, `reset --soft`, `revert` e `stash` em situações reais |
| **04** | Simulando main vs master | Criar e resolver conflito de históricos não relacionados |
| **05** | Publicando no GitHub do zero | Criar repositório no GitHub e conectar com projeto local existente |
| **06** | Corrigindo remote errado | Identificar e corrigir URL de remote incorreta |
| **07** | PC formatado — recuperando projeto | Clonar repositório e reconfigurar identidade em máquina nova |
| **08** | Dois computadores sincronizados | Simular fluxo de trabalho com push e pull entre dois ambientes |
| **09** | Conflitos com arquivos diferentes | Gerar e resolver conflito de merge em arquivos distintos |
| **10** | Conflitos no mesmo arquivo | Gerar e resolver conflito de merge na mesma linha — resolução avançada |
| **11** | Fork + Pull Request | Simular contribuição open source completa com Fork e PR |

**Estrutura de cada exercício:**

- **Situação real** → o contexto do problema
- **Objetivo** → o que você deve conseguir fazer
- **Passo a passo** → comandos com explicação
- **Resultado esperado** → como validar que funcionou
- **Lição aprendida** → o conceito fixado pelo exercício

---

## Apêndices

*Material de referência complementar*

| Apêndice | Conteúdo |
|---|---|
| **Apêndice A** | Configurações recomendadas do VS Code para Git |
| **Apêndice B** | Aliases úteis para o dia a dia |
| **Apêndice C** | Recursos recomendados para continuar aprendendo |
| **Apêndice D** | Soluções detalhadas dos 11 exercícios práticos |

---

## Fim do Livro

**Você agora tem em mãos um material completo.**

Desde o zero absoluto até o nível profissional, com explicações claras, prática intensa e uma referência rápida poderosa.

*O segredo para dominar Git não é decorar tudo —*

**é entender o que está acontecendo e saber onde encontrar a solução rapidamente.**

- Pratique todos os dias.
- Contribua em projetos.
- Quebre repositórios de teste — é para isso que eles existem.

**Você agora está pronto para o mercado de trabalho.**

*Boa jornada!*

---

*— Esron*
*Gurupi, Tocantins · 2026*
