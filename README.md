# AI-Powered Web Threat Detection & Digital Trust Intelligence

A 48-hour hackathon project delivering real-time AI-powered threat analysis and decentralized digital trust intelligence. The platform combines intelligent web scanning (phishing, malware, and social engineering detection via Large Language Models) with verifiable on-chain trust score attestations, providing organizations and end-users with actionable security telemetry and verifiable cryptographic proof of website integrity.

---

## Folder Structure

```
kernal/
├── backend/                  # FastAPI service + ML pipelines + Hardhat smart contracts
│   └── README.md
├── frontend/                 # Next.js interactive threat intelligence dashboard
│   └── README.md
├── docs/                     # Shared system contracts and workflows
│   ├── API_CONTRACT.md       # Backend <-> Frontend API schemas and mock specifications
│   └── BRANCHING.md          # Multi-agent/machine collaboration rules and sync protocol
├── .env.example              # Environment variables template
├── .gitignore                # Global ignore rules for Next.js, Python, Hardhat, secrets
├── docker-compose.yml        # Multi-container orchestration placeholder
└── README.md                 # Project root documentation
```

---

## Branch Table

| Branch | Primary User / Agent | Allowed Scope | Purpose |
|---|---|---|---|
| `main` | Integration | `docs/`, root files, and PR/branch merges only | Stable integration branch; no direct feature work. |
| `backend-dev` | Laptop (Codex) | `backend/` only | FastAPI backend, ML engines, Hardhat contracts. |
| `frontend-dev` | Desktop (Antigravity) | `frontend/` only | Next.js frontend UI, visualizations, client mocks. |

For detailed development rules and synchronization routines, see [BRANCHING.md](docs/BRANCHING.md).

---

## How to run

> [!NOTE]
> **TODO**: Setup and execution instructions will be added as backend and frontend services are implemented.
