---
title: "Automação e Profissionalismo Avançado"
subtitle: "O salto final — do desenvolvedor que usa Git para o que domina o fluxo completo"
section: "Parte 4"
series: "Git & GitHub — Do zero ao nível profissional"
author: Esron
brand: Esron Tech Books
chapters:
  - "Capítulo 11 — GitHub Actions: CI/CD na Prática"
  - "Capítulo 12 — Segurança, Boas Práticas e Ferramentas Avançadas"
---

# Parte 4 — Automação e Profissionalismo Avançado

> *O salto final — do desenvolvedor que usa Git para o que domina o fluxo completo*

Você já sabe trabalhar sozinho, colaborar em equipe e até consertar bagunças no Git.

Agora vamos dar o salto final: transformar seu trabalho em algo **profissional de verdade**.

O objetivo não é mais só versionar código — é fazer com que o código seja testado, verificado e entregue de forma confiável, sem você precisar lembrar de fazer tudo manualmente.

> **O que você vai aprender nesta parte:**
>
> - Automatizar testes e builds com GitHub Actions
> - Proteger seu repositório com regras, secrets e permissões
> - Usar ferramentas avançadas que as melhores empresas do mundo adotam no dia a dia

---

## Capítulo 11 — GitHub Actions: CI/CD na Prática

### 01 — O que é CI/CD?

Imagine que toda vez que você termina uma funcionalidade e faz push, uma máquina automaticamente:

- testa seu código
- verifica se está tudo funcionando
- e se passar nos testes, faz o deploy automaticamente

> **Definição:** CI/CD significa *Continuous Integration* (integração contínua) e *Continuous Deployment* (entrega contínua). Em vez de testar e fazer deploy manualmente, o processo acontece de forma automática e confiável a cada push.

**GitHub Actions** é a ferramenta nativa do GitHub que faz essa automação — gratuita para repositórios públicos e com cota generosa nos privados.

---

### 02 — Como funciona?

Você cria arquivos YAML dentro da pasta `.github/workflows/`. Cada arquivo é um *workflow* — um conjunto de tarefas que o GitHub executa automaticamente quando algo acontece (push, PR, agendamento, etc.).

```bash
# Criar a estrutura de pastas necessária
mkdir -p .github/workflows
```

---

### 03 — Exemplo prático: Primeiro Workflow

Crie o arquivo `.github/workflows/ci.yml`:

```yaml
name: CI Pipeline

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

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: 20

      - name: Install dependencies
        run: npm ci

      - name: Run tests
        run: npm test
```

**O que significa cada parte:**

| Chave | O que faz |
|---|---|
| `on:` | Quando o workflow deve rodar — neste caso, em todo push na `main` e em todo Pull Request |
| `jobs:` | Um "trabalho" completo que será executado numa máquina virtual |
| `runs-on:` | O sistema operacional da máquina virtual (`ubuntu`, `windows`, `macos`) |
| `steps:` | Cada passo sequencial que o workflow executa |

> **✅ Resultado prático:** toda vez que você fizer push ou abrir um PR, o GitHub vai automaticamente pegar seu código, instalar as dependências e rodar os testes. Se os testes falharem, você descobre antes de entregar para o cliente — e o PR fica bloqueado até corrigir.

---

### 04 — Outros usos comuns de GitHub Actions

- Rodar lint — verificação automática de qualidade e estilo de código
- Buildar o projeto e gerar os artefatos de produção
- Fazer deploy automático para **Vercel, Netlify ou GitHub Pages** a cada merge na `main`
- Enviar notificações via Slack ou e-mail quando algo falha
- Gerar changelogs e criar releases automáticos

---

## Capítulo 12 — Segurança, Boas Práticas e Ferramentas Avançadas

Chegamos ao nível que as empresas esperam de um desenvolvedor pleno ou sênior. Esta seção reúne as práticas e ferramentas que separam repositórios amadores de repositórios profissionais.

### 01 — Proteção da branch main

No GitHub, você pode configurar **Branch Protection Rules** para blindar a branch principal contra alterações acidentais:

- Exigir Pull Request aprovado por pelo menos um revisor
- Exigir que os testes (status checks) passem antes do merge
- Impedir push direto na `main` — mesmo do dono do repositório
- Exigir histórico linear (sem merge commits diretos)

> **Como configurar:** vá em **Settings → Branches → Branch protection rules → Add rule**. Digite `main` no nome da branch e marque as opções desejadas. A partir daí, nenhum código entra na `main` sem passar pelo processo definido.

---

### 02 — Secrets: armazenando informações sensíveis

> **⚠️ Nunca faça isso:** nunca coloque senhas, tokens de API, chaves privadas ou qualquer informação sensível diretamente no código ou no arquivo de workflow. Mesmo em repositórios privados, isso é uma falha de segurança grave.

Use os **Secrets do GitHub** para armazenar informações sensíveis com segurança:

1. Vá em **Settings → Secrets and variables → Actions**.
2. Clique em **New repository secret**.
3. Adicione seus secrets (exemplo: `VERCEL_TOKEN`, `DATABASE_URL`).
4. Use no workflow com a sintaxe `${{ secrets.NOME_DO_SECRET }}`.

Exemplo de uso num workflow:

```yaml
- name: Deploy para Vercel
  run: vercel --token ${{ secrets.VERCEL_TOKEN }}
```

---

### 03 — Ferramentas importantes do GitHub

| Ferramenta | O que faz |
|---|---|
| **Dependabot** | Atualiza dependências automaticamente e alerta sobre vulnerabilidades de segurança |
| **Code Scanning** | Analisa o código em busca de falhas de segurança usando análise estática |
| **GitHub CLI (`gh`)** | Executa quase tudo direto do terminal: criar PRs, issues, releases, etc. |
| **CODEOWNERS** | Define quem deve obrigatoriamente revisar alterações em cada pasta do projeto |

Exemplo de arquivo `.github/CODEOWNERS`:

```
# Todo o repositório — revisado pelo dono
*                   @esron

# Frontend — revisado pelo time de front
/src/frontend/      @time-frontend

# Backend — revisado pelo time de back
/backend/           @time-backend
```

---

### 04 — Boas práticas profissionais

| Prática | Por quê importa |
|---|---|
| **Nunca force push em branches compartilhadas** | Sobrescreve trabalho alheio sem aviso |
| **Commits pequenos e atômicos** | Facilita revisão, rollback e entendimento do histórico |
| **Conventional Commits consistentemente** | Permite geração automática de changelogs e versionamento semântico |
| **Atualizar a branch antes do PR** | Evita conflitos na hora do merge e acelera a revisão |
| **Deletar branches após o merge** | Mantém o repositório organizado e sem branches mortas |
| **Proteger a branch main** | Garante que código não revisado nunca entre em produção |

---

### 05 — Ferramentas avançadas

| Ferramenta | Quando usar |
|---|---|
| **Git LFS** | Arquivos grandes que não devem ficar no repositório principal: imagens, datasets, vídeos, binários |
| **Git Submodules** | Quando um projeto depende de outro repositório Git como dependência versionada |
| **Monorepos** | Gerenciar múltiplos projetos ou serviços dentro de um único repositório centralizado |

> **💡 Quando aprender essas ferramentas?** Git LFS, Submodules e Monorepos são para necessidades específicas — não para todo projeto. Aprenda-as quando encontrar o problema que elas resolvem. Por ora, saber que existem já é suficiente.

---

## ✅ Fim da Parte 4

**Parabéns.**

Ao terminar esta parte, você chegou ao nível profissional em Git e GitHub.

Você agora sabe:

- Automatizar testes, builds e deploys com GitHub Actions
- Escrever workflows em YAML e entender cada parte da sintaxe
- Proteger a branch `main` com Branch Protection Rules
- Armazenar credenciais com segurança usando GitHub Secrets
- Usar Dependabot, Code Scanning, GitHub CLI e CODEOWNERS
- Aplicar as boas práticas que as melhores equipes do mercado usam
- Conhecer ferramentas avançadas como Git LFS, Submodules e Monorepos

---

*Você não é mais alguém que "sabe usar Git".*

**Você é alguém que domina o fluxo completo de desenvolvimento moderno.**

---

## Próximo passo

Vá para a **Parte 5 — Referência Rápida**, onde você encontra o Cheat Sheet completo, o Dicionário de Comandos e os Exercícios Práticos com Resoluções.
