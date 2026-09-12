# Repositório Template

Template de repositório da organização FATEC SJC — APIs. Contém os arquivos base que devem ser copiados para todo novo repositório de projeto.

---

## Conteudo

```
repo-template/
├── workflows/
│   ├── backend.yml
│   ├── branch-name.yml
│   ├── frontend.yml
└── pull_request_template.md
```

---

## Como usar

Copie os arquivos deste repositório para o novo repo do projeto, mantendo a estrutura de pastas:

- `workflows/` deve ser colocado em `.github/workflows/`
- `pull_request_template.md` deve ser colocado em `.github/`

---

## Workflows

### `branch-name.yml` — Validacao de nome de branch

Roda em todo pull request aberto contra `main`, `stg` ou `develop`.

Valida que o nome da branch segue o padrao obrigatorio:

```
<tipo>/<JIRA-TICKET>_titulo-do-ticket
```

**Tipos validos:** `feat`, `fix`, `hotfix`, `refactor`, `chore`, `docs`, `test`, `style`, `perf`, `ci`, `build`

**Exemplo:** `feat/FC404-42_criar-tela-de-login`

Se o nome nao estiver no padrao, o job falha e bloqueia o merge.

---

### `backend.yml` — CI do Backend

Roda em push para `main`, `stg` ou `develop` e em pull requests que alterem arquivos dentro de `backend/`.

Etapas:

1. Configura Python 3.12
2. Instala o [Ruff](https://docs.astral.sh/ruff/)
3. Executa `ruff check .` (lint)
4. Executa `ruff format --check .` (verificacao de formatacao)

> O passo de deploy esta comentado no arquivo. Descomente e configure quando o ambiente de deploy estiver definido.

---

### `frontend.yml` — CI do Frontend

Roda em push para `main`, `stg` ou `develop` e em pull requests que alterem arquivos dentro de `frontend/`.

Etapas:

Etapas:

1. Configura Node.js 22 com cache de `npm`
2. Instala dependencias com `npm ci`
3. Executa `npm run lint` (ESLint + Prettier)
4. Executa `npm run build`

Requer o secret `PUBLIC_API_BASE` configurado no repositorio para o build funcionar.

---

## Pull Request Template

O arquivo `pull_request_template.md` e carregado automaticamente pelo GitHub ao abrir uma PR. Ele padroniza as informacoes exigidas:

- **Titulo:** mesmo formato dos commits (`<tipo>(JIRA-TICKET): descricao`)
- **Tarefa:** link para o ticket no Jira
- **O que essa PR muda:** descricao das alteracoes
- **Como testar:** passo a passo para o revisor
- **Checklist:** criterios minimos antes do merge (testes locais, sem debug logs, criterios de aceite do ticket, padrao de branch e commits)
- **Dependencias:** PRs das quais essa depende
