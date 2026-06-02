---
title: "A História do Git e do GitHub"
subtitle: "De onde vieram as ferramentas que mudaram o desenvolvimento de software"
series: "Git & GitHub — Do zero ao nível profissional"
author: Esron
brand: Esron Tech Books
location: "Gurupi, Tocantins"
year: 2026
type: "Capítulo Especial • Contexto Histórico"
---

# A História do Git e do GitHub

> *De onde vieram as ferramentas que mudaram o desenvolvimento de software.*

Antes de mergulhar nos comandos e nas práticas, vale entender de onde vieram essas ferramentas. A história do Git e do GitHub não é apenas técnica — é uma história de conflito, colaboração, visão e impacto mundial.

---

## Parte I — A Origem do Git

Para entender o Git, precisamos voltar a 2005 — e a uma das mentes mais influentes da história da computação.

### 1.1 Linus Torvalds e o Linux

Em 1991, um estudante finlandês de 21 anos chamado **Linus Torvalds** publicou numa lista de e-mails uma mensagem que mudaria o mundo da tecnologia:

> *"Estou fazendo um sistema operacional (livre), apenas um hobby, não será grande e profissional como o GNU."*
>
> — Linus Torvalds, agosto de 1991

Esse sistema operacional era o **Linux**. Em poucos anos, milhares de desenvolvedores ao redor do mundo começaram a contribuir com o projeto. O problema: como coordenar o trabalho de tantas pessoas modificando o mesmo código ao mesmo tempo?

### 1.2 O problema de versionar o Linux

Por anos, o Linux usou um sistema proprietário chamado **BitKeeper** — cedido gratuitamente pela empresa ao projeto. Funcionava bem, mas havia um problema fundamental: software fechado, incompatível com a filosofia open source do Linux.

Em 2005, a relação azedou. A BitMover revogou o acesso gratuito após descobrir que desenvolvedores do Linux tentavam fazer engenharia reversa do protocolo. O projeto do kernel ficou sem um sistema de controle de versão.

O mercado de ferramentas da época era dominado por soluções lentas, centralizadas e proprietárias como **CVS** e **Subversion (SVN)**. Nenhuma delas atendia às necessidades de um projeto do porte do Linux — distribuído, com milhares de colaboradores simultâneos.

### 1.3 Linus cria o Git em 10 dias

A resposta de Linus foi típica dele: ao invés de adotar outra solução existente, ele decidiu criar a própria. Em abril de 2005, Torvalds interrompeu temporariamente o desenvolvimento do kernel e se dedicou exclusivamente a construir um novo sistema de controle de versão.

**Os objetivos eram claros desde o início:**

- **Velocidade** — rápido o suficiente para o kernel do Linux
- **Design simples** — fácil de entender por baixo dos panos
- **Suporte a desenvolvimento não-linear** — milhares de branches paralelas
- **Completamente distribuído** — sem servidor central obrigatório
- **Eficiência em projetos grandes** — capaz de lidar com repositórios massivos

> **Resultado:** Em menos de duas semanas, Linus tinha uma versão funcional do Git. Em **29 de abril de 2005**, o próprio kernel do Linux migrou para o Git. Era o começo de uma revolução silenciosa.

> *"Eu sou um ser egoísta e nomeio todos os meus projetos com meu próprio nome. Primeiro Linux, agora Git."*
>
> — Linus Torvalds

O nome **"Git"** é uma gíria britânica que significa algo como "pessoa desagradável ou idiota". Linus disse que nomeou assim porque é teimoso e sempre acha que está certo — e também como piada com o próprio ego. Outros dizem que é um acrônimo para *"Global Information Tracker"* — quando está de bom humor.

---

## Parte II — A Ascensão e Adoção do Git

O Git foi criado para resolver um problema específico do kernel do Linux. Ninguém imaginava que em menos de 20 anos se tornaria a ferramenta de controle de versão dominante no mundo inteiro.

### 2.1 Timeline: do kernel do Linux ao mundo

| Ano  | Marco |
|------|-------|
| **2005** | Linus Torvalds cria o Git em abril. O kernel Linux migra em 29 de abril. Junio Hamano assume a manutenção — e mantém até hoje. |
| **2007** | Projetos como Ruby on Rails migram para o Git. Desenvolvedores percebem as vantagens do modelo distribuído. |
| **2008** | Tom Preston-Werner, Chris Wanstrath e PJ Hyett lançam o **GitHub**. A plataforma resolve o maior problema do Git: a colaboração social entre desenvolvedores. |
| **2009** | O GitHub atinge 100 mil repositórios. O Pull Request torna o Git acessível para todos os níveis. |
| **2011** | O Git supera o Subversion em número de projetos ativos. O modelo distribuído venceu o centralizado. |
| **2013** | GitHub chega a 10 milhões de repositórios. Google, Facebook e Twitter adotam o Git internamente. |
| **2018** | **Microsoft adquire o GitHub por US$ 7,5 bilhões.** Polêmica na comunidade; desenvolvedores migram para o GitLab. Com o tempo, o GitHub mantém sua independência. |
| **2020** | GitHub passa de 50 milhões de usuários. Lançamento do Copilot, GitHub Actions e Codespaces. |
| **2025** | Git instalado em mais de 90% dos ambientes de desenvolvimento. GitHub hospeda mais de 420 milhões de repositórios. |

### 2.2 Por que o Git venceu?

Outros sistemas existiam antes — CVS, SVN, Mercurial. O que fez o Git se tornar o padrão universal?

**Distribuído por natureza**
Cada desenvolvedor tem uma cópia completa do repositório. Não há ponto central de falha. Você pode trabalhar offline e sincronizar quando quiser.

**Branches baratas**
No SVN, criar uma branch era uma operação custosa e lenta. No Git, criar uma branch é quase instantâneo — o que mudou completamente a forma de trabalhar.

**Integridade garantida**
Cada commit tem um hash SHA-1 único que garante que o histórico não foi alterado. É impossível mudar um commit sem que o Git perceba.

**Open source e gratuito**
O Git é software livre. Qualquer empresa pode usá-lo, modificá-lo e distribuí-lo sem pagar licença — o que acelerou sua adoção massiva.

---

## Parte III — A História do GitHub

O Git resolveu o problema técnico do controle de versão. Mas faltava uma camada social — um lugar onde desenvolvedores pudessem descobrir, compartilhar e colaborar em código de forma simples.

### 3.1 O nascimento do GitHub

Em 2007, **Tom Preston-Werner** e **Chris Wanstrath** se conheceram num encontro de desenvolvedores em San Francisco. Os dois eram frustrados com a dificuldade de colaborar em projetos open source — forks manuais, patches enviados por e-mail, listas de discussão caóticas.

A ideia era simples: criar uma plataforma que tornasse o Git **social**. Um lugar onde você pudesse ver o código dos outros, copiar projetos (fork), sugerir mudanças (pull request) e acompanhar o que acontecia nos projetos que você usava.

> O GitHub foi construído por Tom Preston-Werner **nos fins de semana**, enquanto ainda trabalhava em outro emprego. O site foi lançado em **abril de 2008** — apenas 3 anos após o nascimento do Git.

### 3.2 O conceito que mudou tudo: o Pull Request

A maior inovação do GitHub não foi técnica — foi social. O conceito de **Pull Request** transformou a forma como o mundo colabora em software.

**Antes do GitHub**, contribuir com um projeto open source era assim:

1. Baixar o código-fonte
2. Fazer suas modificações localmente
3. Gerar um arquivo de patch (diff)
4. Enviar o patch por e-mail para a lista de discussão do projeto
5. Esperar dias ou semanas por uma resposta

**Com o GitHub**, o processo virou:

1. Fazer fork do repositório com um clique
2. Fazer suas modificações na sua cópia
3. Abrir um Pull Request com uma descrição
4. Discussão, revisão e merge acontecem na própria plataforma

> **Impacto real:** Rails, Bootstrap, React, Python, Kubernetes — praticamente todo grande projeto de software do mundo hoje é desenvolvido e mantido via GitHub, usando exatamente esse fluxo.

### 3.3 A aquisição pela Microsoft

Em junho de 2018, a Microsoft anunciou a compra do GitHub por **US$ 7,5 bilhões** — a maior aquisição da história da empresa até então. A notícia gerou reação imediata na comunidade tech.

Desenvolvedores temiam que a Microsoft, historicamente hostil ao open source, fechasse o GitHub ou o transformasse numa plataforma paga. Em 24 horas, o GitLab registrou mais de **100 mil novos repositórios migrados**.

> A história mostrou que os temores eram infundados. A Microsoft, sob a liderança de **Satya Nadella**, havia mudado radicalmente sua postura em relação ao open source — contribuindo com o Linux, lançando o VS Code como software livre e adquirindo o GitHub sem interferir em sua cultura. O GitHub continuou independente e crescendo.

---

## Parte IV — Git vs GitHub: Diferenças e Impacto Atual

Uma confusão extremamente comum entre iniciantes é tratar Git e GitHub como sinônimos. São ferramentas completamente diferentes — **uma não depende da outra para existir**.

### 4.1 Comparação completa

| Critério | Git | GitHub |
|---|---|---|
| **O que é** | Software instalado no seu computador | Plataforma web na nuvem |
| **Criador** | Linus Torvalds (2005) | Preston-Werner, Wanstrath, Hyett (2008) |
| **Função** | Controle de versão local | Hospedagem e colaboração remota |
| **Funciona sem o outro?** | ✅ Sim — 100% offline | ❌ Não — depende do Git |
| **Custo** | Gratuito e open source | Gratuito (planos pagos para times) |
| **Analogia** | O caderno de anotações | A estante onde você guarda e compartilha o caderno |

> **Alternativas ao GitHub** que também usam o Git por baixo: **GitLab** (muito usado em empresas com servidores próprios), **Bitbucket** (popular com equipes que usam Jira) e **Gitea** (solução leve e self-hosted). Mas o GitHub continua sendo o padrão da indústria.

### 4.2 O impacto do Git no mundo

É difícil exagerar o quanto o Git mudou o desenvolvimento de software. Alguns números para contextualizar:

- **+420 milhões** de repositórios no GitHub (2025)
- **+100 milhões** de desenvolvedores ativos no GitHub
- **+90%** das empresas de tecnologia usam Git como padrão
- O kernel do Linux tem mais de **1 milhão de commits** no Git
- React, Python, Kubernetes, VS Code e Android são desenvolvidos no GitHub

> *"O GitHub democratizou o open source. Qualquer pessoa, em qualquer lugar do mundo, pode contribuir com qualquer projeto com apenas alguns cliques."*
>
> — Nat Friedman, ex-CEO do GitHub

---

De uma lista de e-mails finlandesa em 1991 até uma plataforma com 100 milhões de desenvolvedores em 2025 — essa é a história das ferramentas que você está aprendendo a usar.

Quando você faz um commit ou abre um Pull Request, você participa de uma das maiores colaborações da história humana.

---
