---
title: "Apêndice D — Soluções Detalhadas dos Exercícios Práticos"
section: "Apêndices"
series: "Git & GitHub — Do zero ao nível profissional"
author: Esron
brand: Esron Tech Books
exercises:
  - "Ex. 01 — Seu Primeiro Repositório Completo"
  - "Ex. 02 — Trabalhando com Branches"
  - "Ex. 03 — Desfazendo um Erro"
  - "Ex. 04 — Simulando Main vs Master"
  - "Ex. 05 — Publicando no GitHub do Zero"
  - "Ex. 06 — Corrigindo Remote Errado"
  - "Ex. 07 — PC Formatado: Recuperando o Projeto"
  - "Ex. 08 — Dois PCs, Um Projeto"
  - "Ex. 09 — Equipe com Arquivos Diferentes"
  - "Ex. 10 — Conflito no Mesmo Arquivo: Resolução Avançada"
  - "Ex. 11 — Fork + Pull Request: Fluxo Open Source"
---

# Apêndice D — Soluções Detalhadas dos Exercícios Práticos

Esta seção traz as soluções completas dos 11 exercícios práticos do Capítulo 15.

> **💡 Recomendação:** tente resolver cada exercício sozinho antes de consultar a solução. O aprendizado acontece no esforço — a solução aqui é para confirmar, corrigir ou desbloquear, não para substituir a tentativa.

---

## Exercício 01 — Seu Primeiro Repositório Completo

**Situação:** você criou um projeto novo e quer versioná-lo corretamente desde o início.

**Objetivo:** dominar o fluxo básico: inicializar, adicionar, commitar e visualizar o histórico.

### Solução passo a passo

```bash
# 1. Criar a pasta do projeto e entrar nela
mkdir meu-primeiro-projeto
cd meu-primeiro-projeto

# 2. Inicializar o Git
git init

# 3. Criar os arquivos iniciais
echo "# Meu Primeiro Projeto com Git" > README.md
echo "<h1>Olá, Mundo!</h1>" > index.html
touch style.css

# 4. Ver o que o Git enxerga
git status

# 5. Adicionar todos os arquivos ao staging
git add .

# 6. Fazer o primeiro commit
git commit -m "feat: estrutura inicial do projeto (README, index e CSS)"

# 7. Ver o histórico
git log --oneline --graph
```

**✅ Resultado esperado:**
- `git status` mostra os arquivos como "untracked" antes do `git add`
- `git log --oneline` exibe um único commit com a mensagem definida

> *Todo repositório começa com `git init`, seguido de `git add` e `git commit`. Commits devem ser atômicos e ter mensagens claras.*

---

## Exercício 02 — Trabalhando com Branches

**Situação:** você precisa desenvolver uma nova página sem afetar o código principal.

**Objetivo:** praticar criação, desenvolvimento e integração de branches.

### Solução passo a passo

```bash
# 1. Criar e mudar para a branch da feature
git switch -c feature/pagina-sobre

# 2. Desenvolver na branch
echo "## Sobre Nós" >> README.md
echo "<section><h2>Sobre o Projeto</h2></section>" > sobre.html
git add .
git commit -m "feat: adiciona página sobre"

# 3. Voltar para main e integrar
git switch main
git merge feature/pagina-sobre

# 4. Deletar a branch após o merge
git branch -d feature/pagina-sobre

# 5. Verificar o resultado
git log --oneline --graph
ls
```

**✅ Resultado esperado:**
- O arquivo `sobre.html` só aparece na `main` após o merge
- O grafo do `git log` mostra as branches se unindo no commit de merge
- `git branch` não lista mais a `feature/pagina-sobre`

> *Branches permitem trabalhar em paralelo com segurança. Nunca desenvolva diretamente na `main` — crie uma branch para cada funcionalidade.*

---

## Exercício 03 — Desfazendo um Erro

**Situação:** você fez um commit com conteúdo errado e precisa corrigi-lo sem perder o trabalho.

**Objetivo:** entender a diferença entre `git reset --soft`, `--mixed` e `--hard`.

### Solução passo a passo

```bash
# 1. Simular um commit problemático
echo "Código com erro grave" >> index.html
git add index.html
git commit -m "feat: adiciona nova funcionalidade"

# 2. Desfazer o commit, mantendo as alterações no staging
git reset --soft HEAD~1

# 3. Corrigir o arquivo
echo "Código corrigido corretamente" > index.html

# 4. Commitar a versão certa
git add index.html
git commit -m "feat: adiciona nova funcionalidade (corrigida)"

# Alternativa radical — apaga tudo sem recuperação:
# git reset --hard HEAD~1
```

**✅ Resultado esperado:**
- `git log --oneline` mostra apenas o commit corrigido — o errado sumiu do histórico
- O arquivo `index.html` contém o conteúdo correto

> *`--soft` é a opção segura: desfaz o commit mas mantém o trabalho. Use `--hard` apenas quando tiver certeza absoluta de que quer apagar as mudanças.*

---

## Exercício 04 — Simulando Main vs Master

**Situação:** dois históricos completamente separados — problema comum ao conectar repositório local ao GitHub.

**Objetivo:** aprender a mesclar históricos não relacionados com `--allow-unrelated-histories`.

### Solução passo a passo

```bash
mkdir teste-unrelated && cd teste-unrelated
git init

# Commit no master (histórico local)
echo "Projeto local" > local.txt
git add . && git commit -m "commit inicial local (master)"

# Criar main como branch órfã (sem histórico compartilhado)
git checkout --orphan main
git rm -rf .
echo "Projeto do GitHub" > github.txt
git add . && git commit -m "commit inicial do GitHub (main)"

# Tentar merge normal — vai falhar
git switch master
git merge main

# Solução: forçar o merge com a flag correta
git merge main --allow-unrelated-histories
git log --oneline --graph
```

**✅ Resultado esperado:**
- O primeiro `git merge` retorna `refusing to merge unrelated histories`
- Com `--allow-unrelated-histories`, o merge é concluído e ambos os arquivos existem
- `git log --graph` mostra as duas linhas se unindo

> *Quando o GitHub criar o repositório com README e você já tiver commits locais, use `--allow-unrelated-histories`. Evite isso criando o repositório sem "Initialize with README".*

---

## Exercício 05 — Publicando no GitHub do Zero

**Situação:** você tem um projeto local pronto e quer publicá-lo no GitHub pela primeira vez.

**Objetivo:** executar o fluxo completo de conexão local → remoto.

### Solução passo a passo

```bash
mkdir projeto-github && cd projeto-github
echo "# Projeto Publicado no GitHub" > README.md
git init
git add README.md
git commit -m "first commit"

# Garantir que a branch se chama main
git branch -M main

# Conectar ao repositório criado no GitHub
git remote add origin https://github.com/SEU-USUARIO/projeto-github.git

# Primeiro push — configura rastreamento automático
git push -u origin main
```

**✅ Resultado esperado:**
- O repositório aparece no GitHub com o `README.md`
- Nos próximos commits, basta `git push` — sem precisar especificar `origin main`

> *Sempre renomeie para `main` antes do primeiro push. O `-u` no `git push -u` configura o rastreamento automático e economiza digitação nos próximos pushes.*

---

## Exercício 06 — Corrigindo Remote Errado

**Situação:** você percebeu que o repositório local está apontando para a URL errada no GitHub.

**Objetivo:** identificar e corrigir a URL de um remote configurado incorretamente.

### Solução passo a passo

```bash
# 1. Verificar o que está configurado
git remote -v

# 2. Corrigir a URL do origin
git remote set-url origin https://github.com/SEU-USUARIO/novo-repositorio.git

# 3. Confirmar a correção
git remote -v

# 4. Testar com um push
git push -u origin main
```

**✅ Resultado esperado:**
- `git remote -v` exibe a URL atualizada após o `set-url`
- `git push` funciona sem erro de autenticação ou repositório não encontrado

> *Sempre verifique `git remote -v` antes de fazer push em repositórios novos. Erros de remote são fáceis de corrigir com `set-url`.*

---

## Exercício 07 — PC Formatado: Recuperando o Projeto

**Situação:** seu computador foi formatado e você precisa retomar o trabalho de onde parou.

**Objetivo:** clonar um repositório existente e reconfigurar o ambiente.

### Solução no novo computador

```bash
# 1. Instalar Git e VS Code (conforme Parte 0 do livro)

# 2. Reconfigurar identidade
git config --global user.name "Seu Nome"
git config --global user.email "seu@email.com"

# 3. Clonar o repositório do GitHub
git clone https://github.com/SEU-USUARIO/seu-projeto.git

# 4. Entrar na pasta e verificar o estado
cd seu-projeto
git status
git log --oneline
```

**✅ Resultado esperado:**
- Todo o histórico de commits está disponível após o clone
- `git status` mostra "nothing to commit, working tree clean"
- Você pode continuar trabalhando exatamente de onde parou

> *O repositório remoto é sua fonte da verdade. Enquanto você fizer push regularmente, nunca perde trabalho — independente do que aconteça com o computador.*

---

## Exercício 08 — Dois PCs, Um Projeto

**Situação:** você trabalha no mesmo projeto em casa e no trabalho e precisa mantê-los sincronizados.

**Objetivo:** praticar o fluxo de pull → trabalhar → push entre dois ambientes.

### Fluxo recomendado em ambos os computadores

```bash
# Sempre comece o dia com pull
git pull origin main

# Trabalhe na sua branch
git switch -c feature/tarefa-do-dia

# Commite ao longo do trabalho
git add .
git commit -m "feat: progresso do dia"

# Ao terminar, envie para o GitHub
git push origin feature/tarefa-do-dia

# No outro computador: atualize antes de continuar
git pull origin main
git switch feature/tarefa-do-dia
git pull origin feature/tarefa-do-dia
```

**✅ Resultado esperado:**
- Nenhum trabalho é perdido entre os dois computadores
- `git pull` traz exatamente o estado que você deixou no outro ambiente

> *Pull antes, push depois. Esse hábito evita 90% dos conflitos em projetos pessoais e garante que você nunca perca trabalho ao trocar de máquina.*

---

## Exercício 09 — Equipe com Arquivos Diferentes

**Situação:** duas pessoas do time editaram arquivos diferentes ao mesmo tempo.

**Objetivo:** entender como o Git resolve merges automáticos sem conflito.

### Simulação

```bash
# Pessoa A — trabalha em frontend/
git switch -c feature/pessoa-a
echo "<nav>Menu</nav>" > frontend/navbar.html
git add . && git commit -m "feat: adiciona navbar"
git switch main && git merge feature/pessoa-a
git push origin main

# Pessoa B — trabalha em backend/ (sem pull antes)
git switch -c feature/pessoa-b
echo "def health(): return 'ok'" > backend/health.py
git add . && git commit -m "feat: adiciona health check"
git switch main
git pull origin main
git merge feature/pessoa-b
git push origin main
```

**✅ Resultado esperado:**
- O `git pull` da Pessoa B cria um merge commit automático — sem conflito
- Ambos os arquivos (`navbar.html` e `health.py`) existem na `main`
- Nenhuma intervenção manual foi necessária

> *Quando colaboradores editam arquivos ou pastas diferentes, o Git resolve o merge sozinho. Boa divisão de responsabilidades é a melhor forma de evitar conflitos.*

---

## Exercício 10 — Conflito no Mesmo Arquivo: Resolução Avançada

**Situação:** dois colaboradores editaram a mesma função no mesmo arquivo. O Git não sabe qual versão usar.

**Objetivo:** gerar, identificar e resolver um conflito de merge manualmente.

### Criando a situação de conflito

```bash
mkdir conflito-equipe && cd conflito-equipe
git init
echo "function calcular(valor) { return valor * 0.10; }" > calculos.js
git add . && git commit -m "feat: estrutura inicial"

# Aluno A cria branch e altera para 15%
git switch -c feature/aluno-a
echo "function calcular(valor) { return valor * 0.15; }" > calculos.js
git commit -am "feat: Aluno A — desconto 15%"

# Aluno B cria branch a partir da main e altera para 20%
git switch main
git switch -c feature/aluno-b
echo "function calcular(valor) { return valor * 0.20; }" > calculos.js
git commit -am "feat: Aluno B — desconto 20%"

# Merge da branch A — ok
git switch main
git merge feature/aluno-a

# Merge da branch B — conflito!
git merge feature/aluno-b
```

### O arquivo `calculos.js` ficará assim após o conflito

```
<<<<<<< HEAD
function calcular(valor) { return valor * 0.15; }
=======
function calcular(valor) { return valor * 0.20; }
>>>>>>> feature/aluno-b
```

### Resolvendo o conflito

```bash
# Editar o arquivo manualmente — escolher ou combinar
# Exemplo: decisão da equipe foi usar média (17,5%)
echo "function calcular(valor) { return valor * 0.175; }" > calculos.js

# Sinalizar que o conflito foi resolvido
git add calculos.js

# Commitar a resolução
git commit -m "fix: resolve conflito — desconto definido em 17,5%"
git log --oneline --graph
```

**✅ Resultado esperado:**
- Os marcadores `<<<<<<`, `=======` e `>>>>>>>` somem após a edição
- `git log --graph` mostra as três branches se convergindo
- `calculos.js` contém a versão decidida pela equipe

> *Conflito não é falha do Git — é falta de comunicação na equipe. A ferramenta parou para que você tome a decisão. Quanto melhor a divisão de responsabilidades, menos conflitos você verá.*

---

## Exercício 11 — Fork + Pull Request: Fluxo Open Source

**Situação:** você quer contribuir com um projeto open source do qual não é colaborador direto.

**Objetivo:** executar o fluxo completo de Fork → branch → commit → PR.

### Solução passo a passo

```bash
# 1. No GitHub: clique em Fork no repositório do projeto

# 2. Clone o SEU fork (não o original)
git clone https://github.com/SEU-USUARIO/projeto-turma.git
cd projeto-turma

# 3. Adicionar o repositório original como upstream
git remote add upstream https://github.com/PROFESSOR/projeto-turma.git

# 4. Sempre atualizar antes de trabalhar
git pull upstream main

# 5. Criar sua branch com nome descritivo
git switch -c feature/seu-nome/cadastro-usuarios

# 6. Fazer as alterações e commitar
git add .
git commit -m "feat: adiciona módulo de cadastro de usuários"

# 7. Enviar para o SEU fork (não para o upstream)
git push origin feature/seu-nome/cadastro-usuarios

# 8. No GitHub: abrir Pull Request
#    Do seu fork → repositório original
#    Escrever boa descrição do que foi feito e por quê
```

**✅ Resultado esperado:**
- `git remote -v` mostra dois remotos: `origin` (seu fork) e `upstream` (original)
- O Pull Request aparece no repositório original para o dono revisar
- Após aprovação e merge, a contribuição entra no projeto

> **`origin` vs `upstream`**
>
> - `origin` → seu fork (você tem permissão de escrita)
> - `upstream` → repositório original (somente leitura para você)
>
> Nunca tente dar push direto no `upstream`.

> *O fluxo Fork + PR é como milhões de projetos open source recebem contribuições todos os dias. É assim que o próprio Linux, React, Python e praticamente todo projeto relevante é desenvolvido colaborativamente.*

---

*Fim do Apêndice D*

*Git & GitHub: Do zero ao nível profissional · Esron · 2026*
