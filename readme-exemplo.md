<h1 align="center">API DSM Xº SEMESTRE XXXX</h1>

<h2 align="center">[Nome do Projeto]</h2>

<p align="center">
  <a href="#cliente">Cliente</a> |
  <a href="#dor">Dor do Cliente</a> |
  <a href="#desafio">Desafio</a> |
  <a href="#solucao">Solução</a> |
  <a href="#backlog">Backlog do Produto</a> |
  <a href="#dor-ready">DoR</a> |
  <a href="#dod">DoD</a> |
  <a href="#requisitos">Requisitos</a> |
  <a href="#arquitetura">Arquitetura</a> |
  <a href="#cicd">CI/CD</a> |
  <a href="#branch">Estratégia de Branch</a> |
  <a href="#jira">Integração Jira + GitHub</a> |
  <a href="#instalacao">Manual de Instalação</a> |
  <a href="#sprint">Cronograma de Sprints</a> |
  <a href="#tecnologias">Tecnologias</a> |
  <a href="#equipe">Equipe</a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/status-[status]-yellow" alt="Status do Projeto">
  <img src="https://img.shields.io/badge/semestre-Xº%20XXXX-blue" alt="Semestre">
  <img src="https://img.shields.io/badge/FATEC-SJC-red" alt="FATEC SJC">
</p>

> **Status do Projeto:** [Status]
>
> **Documentação:** [Acessar documentação geral](docs/README.md)
>
> **Jira:** [Adicionar link]
>
> **Vídeo do Projeto:** [Adicionar link]

---

## 🏢 Cliente <a id="cliente"></a>

[Preencher.]

---

## 😢 Dor do Cliente <a id="dor"></a>

[Preencher.]

---

## 🏅 Desafio <a id="desafio"></a>

[Preencher.]

---

## 💡 Solução <a id="solucao"></a>

[Preencher.]

---

# 📋 Backlog do Produto <a id="backlog"></a>

O backlog está sendo registrado dentro da pasta de produto.
[Acessar Backlog](docs/produto/backlog.md)

---

# ✅ Definition of Ready e Definition of Done

## 🏃 DoR — Definition of Ready <a id="dor-ready"></a>

Para que qualquer **User Story**, tarefa ou card do Backlog seja considerado pronto (**Ready**) para ser puxado para a Sprint, os seguintes critérios devem ser atendidos:

- [ ] **Contexto e Objetivo:** O problema a ser resolvido e o objetivo da tarefa estão claramente definidos e compreendidos por todo o time.
- [ ] **Formato do Card:** A história do usuário e seus critérios de aceite estão explicitamente descritos de forma clara.
- [ ] **Insumos e Fontes de Dados:** Mapeamento e especificação completa das fontes de dados, APIs ou insumos necessários para a execução da tarefa.
- [ ] **Escopo de Integração e Automação:** Escopo técnico mapeado (ex: scraping, rotinas, frequência de atualização ou regras de negócio envolvidas).
- [ ] **Arquitetura e Ambiente:** Ferramentas, estrutura de código/notebooks e modelos de dados (ex: esquemas de tabelas do banco) alinhados entre os responsáveis.
- [ ] **Design e Interface:** Protótipos de tela, fluxos visuais ou formatos de exportação (ex: gráficos, relatórios) definidos e aprovados.
- [ ] **Mapeamento de Dependências:** Dependências técnicas (ex: rotinas de backend antes do banco) ou de negócios identificadas e tratadas.
- [ ] **Estimativa e Sem Bloqueios:** A tarefa foi discutida, estimada pelo time e não possui impedimentos conhecidos para o início imediato.

---

## 🏆 DoD — Definition of Done <a id="dod"></a>

Para que qualquer User Story e Pull Request seja definido como concluído e seja integrado à branch principal (`main`), os seguintes critérios devem ser atendidos:

- [ ] O código está integrado em `develop` (ou superior) via PR aprovado.
- [ ] O PR teve ao menos 2 aprovações e todos os comentários foram resolvidos.
- [ ] O CI passou com sucesso — Frontend CI e/ou Backend CI conforme os arquivos alterados.
- [ ] A branch de origem foi criada a partir de `develop` com o nome no padrão correto.
- [ ] Os commits seguem o Conventional Commits com o ticket Jira no escopo.
- [ ] Os critérios de aceite definidos no card do Backlog da Sprint foram atendidos.
- [ ] Testes unitários foram criados ou atualizados para novas regras de negócio e passaram com 100% de sucesso.
- [ ] `README.md` e documentos necessários foram devidamente atualizados conforme a demanda da task.

Os critérios de conclusão de cada tarefa estão documentados em **[docs/workflows/processo-pr.md](docs/workflows/processo-pr.md#5-definition-of-done-dod)**.

Os critérios específicos de cada User Story estão no card correspondente no [Jira](#).

---

# 📝 Requisitos <a id="requisitos"></a>

## 🎯 Requisitos Funcionais — RF

Os requisitos funcionais estão registrados como User Stories no Backlog do Produto:

**[docs/produto/backlog.md](docs/produto/backlog.md)**

---

## ⚙️ Requisitos Não Funcionais — RNF

Os requisitos não funcionais estão definidos no documento de definição do projeto:

**[docs/arquitetura/definicao-do-projeto.md](docs/arquitetura/definicao-do-projeto.md)**

---

# 🏗️ Arquitetura do Sistema <a id="arquitetura"></a>

A definição de arquitetura, componentes, banco de dados e integrações está documentada em:

**[docs/arquitetura/definicao-do-projeto.md](docs/arquitetura/definicao-do-projeto.md)**

## Diagrama de Arquitetura

[Adicionar diagrama.]

---

# 🔄 Integração e Entrega Contínua — CI/CD <a id="cicd"></a>

A estratégia de CI é dividida em duas camadas: **hooks locais** (executados na máquina do desenvolvedor antes do commit/push) e **workflows remotos** (executados no GitHub a cada push ou PR).

## Pipeline

### Hooks Locais — Lefthook

O [Lefthook](https://github.com/evilmartians/lefthook) gerencia os hooks do Git localmente. Ele é configurado pelo arquivo `lefthook.yml` na raiz do repositório e instalado automaticamente ao rodar `npm install`.

| Hook         | Quando executa      | O que faz                                                                                                                                                                              |
| :----------- | :------------------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `pre-commit` | A cada `git commit` | Roda ESLint + Prettier nos arquivos `.ts`/`.tsx` do frontend e Ruff nos arquivos `.py` do backend que estão em stage. Arquivos corrigidos automaticamente são re-adicionados ao stage. |
| `pre-push`   | A cada `git push`   | Valida se o nome da branch segue o padrão obrigatório. Bloqueia o push caso contrário.                                                                                                 |
| `commit-msg` | A cada `git commit` | Valida se a mensagem de commit segue o padrão Conventional Commits com ticket Jira.                                                                                                    |

### Workflows Remotos — GitHub Actions

Três workflows são executados no GitHub em resposta a pushes e pull requests:

| Workflow              | Arquivo                             | Gatilho                                        | O que faz                                 |
| :-------------------- | :---------------------------------- | :--------------------------------------------- | :---------------------------------------- |
| **Frontend CI**       | `.github/workflows/frontend.yml`    | Push ou PR com mudanças em `frontend/**`       | Instala dependências, roda lint e build   |
| **Backend CI**        | `.github/workflows/backend.yml`     | Push ou PR com mudanças em `backend/**`        | Roda `ruff check` e `ruff format --check` |
| **Branch Name Check** | `.github/workflows/branch-name.yml` | Abertura de PR para `main`, `stg` ou `develop` | Valida o nome da branch de origem         |

> Os workflows de frontend e backend são disparados **apenas quando arquivos da respectiva pasta mudam**, evitando execuções desnecessárias.

## Ferramentas

| Ferramenta                                                       | Finalidade                          |
| :--------------------------------------------------------------- | :---------------------------------- |
| [Lefthook](https://github.com/evilmartians/lefthook)             | Gerenciador de hooks Git (local)    |
| [commitlint](https://commitlint.js.org/)                         | Validação de mensagens de commit    |
| [ESLint](https://eslint.org/) + [Prettier](https://prettier.io/) | Lint e formatação do frontend       |
| [Ruff](https://docs.astral.sh/ruff/)                             | Lint e formatação do backend Python |
| [GitHub Actions](https://docs.github.com/en/actions)             | CI remoto                           |

---

# 🌿 Estratégia de Branch <a id="branch"></a>

As convenções de branches, commits e rastreabilidade com Jira estão documentadas em detalhes em:

**[docs/workflows/fluxo-git.md](docs/workflows/fluxo-git.md)**

## Resumo rápido

| O que         | Padrão                                                                                       |
| :------------ | :------------------------------------------------------------------------------------------- |
| Branch        | `<tipo>/PROJ-XX_titulo-do-ticket`                                                            |
| Commit        | `<tipo>(PROJ-XX): descricao curta`                                                           |
| Tipos válidos | `feat`, `fix`, `hotfix`, `refactor`, `chore`, `docs`, `test`, `style`, `perf`, `ci`, `build` |

Branches `main`, `stg` e `develop` são protegidas — não aceitam push direto nem deleção.

## Pull Requests

O fluxo de PR, regras de proteção do GitHub, critérios de Code Review e Definition of Done estão em:

**[docs/workflows/processo-pr.md](docs/workflows/processo-pr.md)**

---

# 🧪 Estratégia de Testes

[Definir após o Kick-off.]

## Testes de Integração

[Preencher.]

## Testes de API

[Preencher.]

## Testes de Interface

[Preencher, caso aplicável.]

---

# 📖 Manual de Instalação <a id="instalacao"></a>

## ⚙️ Pré-requisitos

- [Node.js 20+](https://nodejs.org/) — necessário para todos os membros (instala os hooks Git automaticamente)
- [Ruff](https://docs.astral.sh/ruff/installation/) — necessário apenas para quem trabalha no backend Python

---

## 🚀 Passo a Passo de Instalação

### 1. Clonar o repositório

```bash
git clone [URL_DO_REPOSITORIO]
cd [NOME_DO_REPOSITORIO]
```

### 2. Instalar dependências e ativar os hooks Git

```bash
npm install
```

> O `npm install` já instala os hooks Git automaticamente via Lefthook (script `prepare`). Após isso, as validações de commit, branch e lint passam a funcionar localmente.

### 3. Configurar ambiente

```text
[Preencher após o Kick-off — variáveis de ambiente, .env, etc.]
```

### 4. Executar aplicação

```bash
[COMANDO]
```

### 5. Acessar o sistema

```text
[URL / PORTA]
```

---

# 🗓️ Cronograma de Sprints <a id="sprint"></a>

| Evento                           | Período | Status |
| :------------------------------- | :------ | :----: |
| Kick-off geral                   |         |        |
| Construção do Backlog / Planning |         |        |
| **Sprint 1**                     |         |        |
| Sprint Review / Planning         |         |        |
| **Sprint 2**                     |         |        |
| Sprint Review / Planning         |         |        |
| **Sprint 3**                     |         |        |
| Sprint Review                    |         |        |
| Feira de Soluções                |         |        |

---

# 🛠️ Tecnologias Utilizadas <a id="tecnologias"></a>

_Frontend_

[Preencher.]

_Backend_

[Preencher.]

_Banco de Dados_

[Preencher.]

_Análise de Dados_

[Preencher, caso aplicável.]

_DevOps & Qualidade_

![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat&logo=githubactions&logoColor=white)
![Lefthook](https://img.shields.io/badge/Lefthook-FF1E1E?style=flat)
![Ruff](https://img.shields.io/badge/Ruff-D7FF64?style=flat&logoColor=black)
![commitlint](https://img.shields.io/badge/commitlint-000000?style=flat)
![Jira](https://img.shields.io/badge/Jira-0052CC?style=flat&logo=jira&logoColor=white)

## Testes

[Preencher.]

## Gestão e Qualidade de Código

- GitHub — versionamento e CI/CD
- Jira — gerenciamento de tarefas e sprints
- Lefthook — hooks Git locais (lint, validação de branch e commit)
- commitlint — padronização de mensagens de commit
- GitHub Actions — integração contínua remota

---

## 👥 Equipe <a id="equipe"></a>

| Integrante | Papel              |                                                             GitHub                                                              |                                                              LinkedIn                                                               |
| :--------- | :----------------- | :-----------------------------------------------------------------------------------------------------------------------------: | :---------------------------------------------------------------------------------------------------------------------------------: |
| **[Nome]** | PO / Developer     | <a href="[URL]"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/github/github-original.svg" width="30"></a> | <a href="[URL]"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/linkedin/linkedin-original.svg" width="30"></a> |
| **[Nome]** | Master / Developer | <a href="[URL]"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/github/github-original.svg" width="30"></a> | <a href="[URL]"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/linkedin/linkedin-original.svg" width="30"></a> |
| **[Nome]** | Developer          | <a href="[URL]"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/github/github-original.svg" width="30"></a> | <a href="[URL]"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/linkedin/linkedin-original.svg" width="30"></a> |

# 📚 Documentação

## Documentação Geral

- [Acordos do Time](docs/workflows/acordos.md)
- [Fluxo Git — Convenções de Branch, Commit e Hooks](docs/workflows/fluxo-git.md)
- [Processo de Pull Request, Code Review e Definition of Done](docs/workflows/processo-pr.md)
- [Jira — Fluxo de Trabalho e Gestão de Cards](docs/workflows/jira.md)

## Atas de Reunião

[Adicionar links.]

## Documentação das Sprints

[Adicionar links.]

## Diagramas

[Adicionar links.]

---

# 📹 Vídeos das Entregas

|  Sprint  | Vídeo       |
| :------: | ----------- |
| Sprint 1 | [Adicionar] |
| Sprint 2 | [Adicionar] |
| Sprint 3 | [Adicionar] |
