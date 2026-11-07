# API Contract: AI-Powered Web Threat Detection & Digital Trust Intelligence

This contract defines the interface between the FastAPI backend and Next.js frontend for the 48-hour hackathon project.

**Base URL:**
- Local: `http://localhost:8000`
- Production: Configurable via `NEXT_PUBLIC_API_BASE_URL`

**Global Headers:**
- `Content-Type: application/json`
- `Accept: application/json`

---

## 1. Endpoints Overview

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/v1/health` | Health check endpoint |
| `POST` | `/api/v1/scan/url` | Submit a URL for real-time threat scanning |
| `GET` | `/api/v1/scan/{scan_id}` | Fetch scan status, results, and classification |
| `POST` | `/api/v1/threat/analyze` | AI-driven deep threat analysis & explanation |
| `GET` | `/api/v1/trust/score` | Retrieve reputation metrics & trust score for a domain |
| `POST` | `/api/v1/trust/verify-onchain` | Verify on-chain cryptographic attestation |

---

## 2. Endpoint Details

### 2.1 Health Check
- **`GET /api/v1/health`**
- **Response `200 OK`**:
```json
{
  "status": "healthy",
  "version": "1.0.0",
  "timestamp": "2026-11-07T21:00:00Z"
}
```

---

### 2.2 Submit URL Scan
- **`POST /api/v1/scan/url`**
- **Request Body**:
```json
{
  "url": "https://example-suspicious-domain.com/login",
  "deep_scan": true
}
```
- **Response `202 Accepted`** (or `200 OK` if cached/synchronous):
```json
{
  "scan_id": "scan_8f3a9e12-3b8c-4a1d-91b6-e25f82ac845a",
  "url": "https://example-suspicious-domain.com/login",
  "status": "processing",
  "submitted_at": "2026-11-07T21:00:00Z"
}
```

---

### 2.3 Get Scan Result
- **`GET /api/v1/scan/{scan_id}`**
- **Response `200 OK`**:
```json
{
  "scan_id": "scan_8f3a9e12-3b8c-4a1d-91b6-e25f82ac845a",
  "url": "https://example-suspicious-domain.com/login",
  "status": "completed",
  "threat_level": "CRITICAL",
  "verdict": "PHISHING",
  "confidence_score": 0.94,
  "indicators": [
    "Homograph domain masquerading",
    "Credential harvesting form detected",
    "Domain registered < 48 hours ago"
  ],
  "categories": ["phishing", "impersonation"],
  "domain_metadata": {
    "ip": "198.51.100.24",
    "registrar": "Suspicious Registrar Inc.",
    "country": "US",
    "ssl_valid": true,
    "ssl_issuer": "Let's Encrypt"
  },
  "completed_at": "2026-11-07T21:00:05Z"
}
```

---

### 2.4 Deep AI Threat Analysis
- **`POST /api/v1/threat/analyze`**
- **Request Body**:
```json
{
  "scan_id": "scan_8f3a9e12-3b8c-4a1d-91b6-e25f82ac845a",
  "include_remediation": true
}
```
- **Response `200 OK`**:
```json
{
  "scan_id": "scan_8f3a9e12-3b8c-4a1d-91b6-e25f82ac845a",
  "model": "gemini-1.5-pro",
  "summary": "High-confidence spear phishing targeting enterprise single sign-on credentials.",
  "technical_breakdown": "The page mimics the OAuth consent screen with form inputs sending data to an unverified third-party relay endpoint.",
  "risk_score": 92,
  "recommended_actions": [
    "Block domain at DNS firewall level",
    "Revoke active SSO sessions for affected users",
    "Submit domain takedown request"
  ]
}
```

---

### 2.5 Trust Score & Intelligence
- **`GET /api/v1/trust/score?domain=example-suspicious-domain.com`**
- **Response `200 OK`**:
```json
{
  "domain": "example-suspicious-domain.com",
  "overall_trust_score": 12,
  "max_score": 100,
  "factors": {
    "domain_age_days": 2,
    "reputation_score": 5,
    "dnssec_enabled": false,
    "safe_browsing_flagged": true
  },
  "historical_incidents": 0,
  "attestation_status": "UNVERIFIED"
}
```

---

### 2.6 On-Chain Attestation Verification
- **`POST /api/v1/trust/verify-onchain`**
- **Request Body**:
```json
{
  "domain": "example-suspicious-domain.com",
  "scan_id": "scan_8f3a9e12-3b8c-4a1d-91b6-e25f82ac845a"
}
```
- **Response `200 OK`**:
```json
{
  "chain_id": 11155111,
  "network": "Sepolia",
  "contract_address": "0x0000000000000000000000000000000000000000",
  "transaction_hash": "0xabc...def",
  "attested_at": "2026-11-07T21:00:10Z",
  "is_valid": true,
  "attestation_data_hash": "0x123...456"
}
```

---

## 3. Mock Data Mode
For frontend development when `NEXT_PUBLIC_USE_MOCKS=true`:
- The frontend client must consume local mock fixtures adhering strictly to the above JSON response schemas.
