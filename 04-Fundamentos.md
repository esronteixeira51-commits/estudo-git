---
title: "Fundamentos"
subtitle: "Nível Iniciante"
section: "Parte 1"
series: "Git & GitHub — Do zero ao nível profissional"
author: Esron
brand: Esron Tech Books
chapters:
  - "Capítulo 1 — Entendendo Git e GitHub"
  - "Capítulo 2 — Seu Primeiro Repositório"
  - "Capítulo 3 — Conectando ao GitHub"
  - "Capítulo 4 — Commits Profissionais e .gitignore"
---

# Parte 1 — Fundamentos

> *Nível Iniciante*

Bem-vindo à base de tudo.

Nesta parte você vai aprender a andar com Git antes de correr. Não vamos decorar 50 comandos de uma vez. Vamos entender o que realmente está acontecendo por trás dos comandos mais importantes.

Pense no Git como um caderno de anotações superpoderoso para o seu código:

- Ele guarda todas as versões do seu projeto.
- Ele permite voltar no tempo quando você estraga algo.
- Ele ajuda você a trabalhar sozinho ou com outras pessoas sem bagunça.

Vamos construir isso passo a passo, de forma sólida.

---

## Capítulo 1 — Entendendo Git e GitHub

Imagine que você está escrevendo um livro. Você escreve um capítulo, gosta, mas depois muda algumas partes. Depois muda de novo. Depois percebe que a primeira versão estava melhor. O que você faz?

Sem controle de versão, você fica salvando arquivos como:

```
livro-final.docx
livro-final-v2.docx
livro-final-v2-corrigido.docx
livro-final-mesmo-agora-v3.docx
```

Isso vira uma bagunça rapidamente.

> **Git resolve exatamente esse problema.** Ele é um sistema que registra automaticamente todas as mudanças do seu código, guarda cada versão e permite voltar para qualquer ponto anterior com um simples comando.

### 01 — Git vs. GitHub: a diferença simples

**Git** é o programa que roda no seu computador e controla versões localmente.

**GitHub** é como uma nuvem onde você guarda esse caderno. Ele permite:

- Mostrar seu código para outras pessoas (portfólio)
- Trabalhar em equipe sem pisar no pé de ninguém
- Fazer backup automático do seu projeto

Você pode usar Git sem GitHub, mas quase ninguém faz isso hoje. Juntos, eles formam a ferramenta mais usada no mundo profissional de desenvolvimento.

### 02 — Por que isso é importante?

> **💼 Mercado de trabalho:** praticamente todas as vagas de programação exigem conhecimento de Git e GitHub. Saber usar bem é o que separa quem "sabe programar" de quem "sabe trabalhar em equipe".

---

## Capítulo 2 — Seu Primeiro Repositório

Vamos colocar a mão na massa. Abra o VS Code, crie uma pasta chamada `treino-git` e abra o terminal integrado (**Ctrl + `**).

### 01 — Criando o repositório

```bash
# 1. Crie a pasta e entre nela
mkdir treino-git
cd treino-git

# 2. Inicialize o Git neste projeto
git init
```

> **O que aconteceu?** O Git criou uma pasta oculta chamada `.git` dentro do seu projeto. É lá que ele guarda todo o histórico de versões. Você nunca precisa mexer nessa pasta — o Git cuida dela automaticamente.

### 02 — Criando arquivos e verificando o status

```bash
echo "# Meu Primeiro Projeto com Git" > README.md
echo "<h1>Olá, mundo!</h1>" > index.html
git status
```

Você vai ver os arquivos marcados como **untracked** — o Git os enxerga, mas ainda não os controla.

### 03 — Staging e primeiro commit

**Adicionando arquivos ao staging:**

```bash
git add .
git status
```

Agora os arquivos estão na área de preparação (staging area). É como se você tivesse colocado os ingredientes na mesa antes de cozinhar.

**Fazendo o primeiro commit:**

```bash
git commit -m "feat: estrutura inicial do projeto"
```

> **O que é um commit?** Um commit é uma fotografia do seu projeto naquele momento. Cada commit fica salvo no histórico para sempre — você pode voltar para qualquer um deles quando quiser.

**Veja o histórico:**

```bash
git log --oneline
```

### 04 — O ciclo de vida do Git

Entenda este diagrama e o resto do Git fica muito mais fácil:

```
Working Directory  →  git add  →  Staging Area  →  git commit  →  Repositório Local
  (onde você edita)                (preparando)                    (salvo no histórico)
```

> **💡 Dica:** sempre que fizer mudanças, o ciclo é o mesmo: editar no Working Directory → `git add` → `git commit`. Simples assim.

---

## Capítulo 3 — Conectando ao GitHub

Ter o projeto só no seu computador é bom, mas não é suficiente. Vamos colocar ele na nuvem.

### 01 — Criando o repositório no GitHub

Faça no navegador:

1. Acesse github.com e faça login.
2. Clique em **New repository**.
3. Dê o nome **treino-git**.
4. **Não** marque "Add a README file".
5. Clique em **Create repository**.

Copie a URL do repositório gerada pelo GitHub (formato: `https://github.com/SEU-USUARIO/treino-git.git`).

### 02 — Conectando e enviando o código

```bash
# Conectar seu projeto local ao GitHub
git remote add origin https://github.com/SEU-USUARIO/treino-git.git

# Garantir que o branch principal se chama "main"
git branch -M main

# Enviar o código para o GitHub
git push -u origin main
```

> **✅ Seu projeto está no GitHub!** A flag `-u` no `git push -u origin main` configura o rastreamento automático. Nos próximos pushes, basta digitar `git push` — sem precisar especificar o remote e o branch toda vez.

### 03 — Clonando em outro computador

Para baixar o projeto em outro computador ou pasta:

```bash
git clone https://github.com/SEU-USUARIO/treino-git.git
```

---

## Capítulo 4 — Commits Profissionais e .gitignore

### 01 — Mensagens de commit: boas vs. ruins

A mensagem do commit é o que vai aparecer no histórico do projeto. Uma mensagem boa vale ouro — tanto para você no futuro quanto para a sua equipe.

| ❌ Mensagem ruim | ✅ Mensagem boa (Conventional Commits) |
|---|---|
| `commit` | `feat: adiciona página inicial` |
| `atualizei` | `fix: corrige bug de login` |
| `corrigi` | `docs: atualiza README` |
| `final agora vai` | `chore: atualiza dependências` |

> **📐 Conventional Commits:** o padrão usa prefixos como `feat:` (nova funcionalidade), `fix:` (correção), `docs:` (documentação) e `chore:` (tarefas de manutenção). É o padrão adotado nas melhores equipes do mercado.

### 02 — Criando o .gitignore

Crie um arquivo chamado `.gitignore` na raiz do projeto. Ele diz ao Git quais arquivos deve ignorar — senhas, dependências e arquivos temporários **nunca** devem ir para o repositório.

```gitignore
# Dependências
node_modules/
venv/
__pycache__/

# Builds
dist/
build/

# Variáveis de ambiente (nunca commitar!)
.env
.env.local

# Logs e temporários
*.log
.DS_Store
```

Depois salve e faça o commit:

```bash
git add .gitignore
git commit -m "chore: adiciona .gitignore"
```

---

## ✅ Fim da Parte 1

Você agora já sabe:

- O que é Git e GitHub — e a diferença entre eles
- Criar um repositório local com `git init`
- Fazer commits e navegar pelo histórico
- Enviar o projeto para o GitHub com `git push`
- Escrever mensagens de commit profissionais
- Ignorar arquivos desnecessários com `.gitignore`

---

## Próximo passo

Vá para a **Parte 2 — Colaboração**, onde você vai aprender a trabalhar com branches — o recurso que faz o Git brilhar de verdade.
