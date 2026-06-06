# Persona AI News Aggregator

## What this repo does

This repo runs n8n and Ollama with Docker so a user can register in the chatbot, choose interests, and receive a newsletter. The workflow uses the Chat Trigger for commands and a scheduled branch for sending emails.

## What to copy

Use the files already in this repo:

- `docker-compose.yml`
- `.env`
- workflow JSON

The Docker setup keeps n8n data in a volume and exposes n8n on port 5678.

## Start the stack

Run this in the repo root:

```bash
docker compose up -d
```

Then open n8n at:

```text
http://localhost:5678
```

## Commands

Type these in the chatbot:

- `<help>` to see all commands.
- `<register your@email.com password123>` to create an account.
- `<login your@email.com password123>` to log in.
- `<set interests ai, gamedev>` to choose topics.
- `<set schedule 08:00>` to choose the newsletter time.
- `<status>` to check saved settings.
- `<newsletter now>` to send a newsletter right away.
- `<unsubscribe>` to delete your account and stop emails.

The Chat Trigger node is the user-facing entry point, and each message runs the workflow once.

## Ollama

The repo includes Ollama in Docker, so the LLM can run inside the same network. n8n can reach Ollama through the shared Docker network name when both services are in the same compose file.

## Email

The workflow sends the newsletter through the email node using SMTP settings from the repo environment.

## Notes

Set `N8N_ENCRYPTION_KEY` in `.env` before starting the stack and keep it the same after the first run. n8n uses that key to protect saved credentials.

If the workflow is already imported, the main thing the user needs is: start Docker, open n8n, register, set interests, and type `<newsletter now>`.
