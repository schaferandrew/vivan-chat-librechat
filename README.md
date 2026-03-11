# vivian-chat

LibreChat deployment for the Vivian household AI assistant. Provides a chat PWA backed by OpenRouter (cloud models) and optionally Ollama (local models).

## Prerequisites

- Docker + Docker Compose
- An OpenRouter API key — https://openrouter.ai/keys
- A `.env` file (see setup below)

## Setup

**1. Copy the example env file and fill in secrets**

```bash
cp .env.example .env
```

Open `.env` and set:

- `OPENROUTER_API_KEY` — your OpenRouter key
- `MEILI_MASTER_KEY` — random hex string: `openssl rand -hex 32`
- `JWT_SECRET`, `JWT_REFRESH_SECRET`, `CREDS_KEY` — 64 hex chars each:
  `node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"`
- `CREDS_IV` — 32 hex chars:
  `node -e "console.log(require('crypto').randomBytes(16).toString('hex'))"`

**2. Start the stack**

```bash
docker compose up -d
```

**3. Open the app**

http://localhost:3080

**4. Create the first user**

Registration is disabled by default. Create the first account from the container:

```bash
docker compose exec librechat npm run create-user
```

## Services

| Service       | Image                                    | Purpose              |
|---------------|------------------------------------------|----------------------|
| `librechat`   | `ghcr.io/danny-avila/librechat:latest`   | Chat UI + API        |
| `mongo`       | `mongo:7`                                | Message/user storage |
| `meilisearch` | `getmeili/meilisearch:latest`            | Message search index |

## Stopping

```bash
docker compose down          # stop containers, keep volumes
docker compose down -v       # stop and delete all data
```

## MCP Servers

MCP servers are configured through the LibreChat UI under Settings → MCP Servers. No server-side config required.

## Model IDs

Models are listed in `librechat.yaml`. Some OpenRouter IDs may drift — verify against https://openrouter.ai/models if a model fails to load.
