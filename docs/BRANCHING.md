# Branching Strategy & Development Rules

This document outlines the strict collaboration and branching workflow for the 48-hour hackathon project: **AI-Powered Web Threat Detection & Digital Trust Intelligence**.

---

## 1. Branch Ownership & Scopes

| Branch | Machine / Agent | Allowed Scope | Responsibility |
|---|---|---|---|
| `main` | Integration | `docs/`, root config files, and merges only | Stable integration branch. No direct feature work allowed. |
| `backend-dev` | Laptop (Codex) | Files inside `backend/` only | FastAPI service, ML models, analysis pipelines, Hardhat contracts. |
| `frontend-dev` | Desktop (Antigravity) | Files inside `frontend/` only | Next.js interactive dashboard, UI components, client state. |

---

## 2. Strict Rules

1. **Isolation of Dev Branches:**
   - `backend-dev` may **only** modify files inside `backend/`.
   - `frontend-dev` may **only** modify files inside `frontend/`.
   - Neither dev branch should edit files in `docs/` or root files (`.gitignore`, `.env.example`, `docker-compose.yml`, etc.).

2. **API Contract & Root Updates:**
   - Any API contract or root file modifications must originate on `main`.
   - Once merged into `main`, both `backend-dev` and `frontend-dev` pull/merge `main` to receive the updated contract.

3. **Commit Message Format:**
   - Standard format: `<prompt-id>: <short summary>`
   - Examples:
     - `C1: phishing and ssrf modules`
     - `A2: result page`
     - `DOCS: update threat analysis schema`

4. **Security & Secrets:**
   - **Never commit** `.env`, `.env.*`, private keys, API keys, seed phrases, or wallet JSON files.
   - All secret names must follow `.env.example`.

---

## 3. Synchronization Routine

When syncing work between the laptop (Codex) and desktop (Antigravity):

1. **Commit & Push Dev Branch:**
   ```bash
   git add <allowed-files>
   git commit -m "<prompt-id>: <short summary>"
   git push origin <dev-branch>
   ```

2. **Merge into Main (Integration):**
   ```bash
   git checkout main
   git pull origin main
   git merge <dev-branch>
   git push origin main
   ```

3. **Sync Other Dev Branch with Main:**
   On the other machine / dev branch:
   ```bash
   git checkout <other-dev-branch>
   git pull origin <other-dev-branch>
   git merge main
   git push origin <other-dev-branch>
   ```
