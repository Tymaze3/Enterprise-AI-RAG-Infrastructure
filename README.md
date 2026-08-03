# 🤖 Enterprise AI RAG Infrastructure
### Secure Self-Hosted LLM Pipeline for CMMC and HIPAA Environments

> Built and deployed in production at a DoD contractor operating  
> within a CMMC Level 2 / GCC High compliance boundary.

---

## 🎯 Why This Exists

Commercial AI tools like ChatGPT, Microsoft Copilot, and Claude cannot be used in environments handling CUI (Controlled Unclassified Information) or PHI (Protected Health Information) without significant compliance risk. Organizations in defense and healthcare need AI capabilities without the data sovereignty risk of cloud-based LLMs.

This project solves that problem with a fully self-hosted, auditable, permission-aware RAG architecture that keeps sensitive data on-premises.

---

## 🏗️ Architecture

```
User Request
     │
     ▼
Open WebUI (Frontend)
     │
     ▼
Ollama (LLM Engine) ◄──── Local Model (Llama 3 / Mistral)
     │
     ▼
RAG Pipeline
     ├── OneDrive Connector (enterprise documents)
     └── Odoo ERP Connector (operational data)
     │
     ▼
Permission-Aware Retrieval
(only returns documents the requesting user is authorized to access)
     │
     ▼
Response → User
```

**Reverse Proxy (HTTPS/TLS)**  
All traffic encrypted in transit. No public endpoints exposed.  
Internal network only — no data leaves the compliance boundary.

---

## 🔐 Security Design Decisions

| Decision | Rationale |
|----------|-----------|
| Fully self-hosted | CUI/PHI never leaves the compliance boundary |
| Containerized via Docker | Isolated, reproducible, auditable deployments |
| HTTPS/TLS enforced | Encrypted transport for all internal traffic |
| Permission-aware retrieval | Users only see documents they are authorized to access |
| No telemetry | All external phone-home features disabled |
| Air-gap capable | Can operate fully offline with local models |

---

## 🛠️ Tech Stack

| Component | Technology |
|-----------|------------|
| LLM Engine | Ollama |
| Frontend | Open WebUI |
| Container Orchestration | Docker / Docker Compose |
| Reverse Proxy | Nginx (HTTPS/TLS termination) |
| Enterprise Data — Documents | Microsoft OneDrive |
| Enterprise Data — Operations | Odoo ERP |
| Operating System | Ubuntu Linux |
| Transport Security | TLS 1.2 / 1.3 |

---

## 📋 Compliance Relevance

### CMMC Level 2 / NIST 800-171

| Control | Description | How This Architecture Addresses It |
|---------|-------------|-----------------------------------|
| AC.1.001 | Limit CUI access to authorized users | Permission-aware retrieval enforces user-level access |
| AU.2.041 | Audit logs of CUI access | All document retrievals logged at the container level |
| SC.3.177 | Encryption of CUI in transit | HTTPS/TLS enforced on all internal traffic |
| SI.1.210 | Protection from malicious code | Self-hosted eliminates cloud-side model risk entirely |

### HIPAA

| Requirement | How This Architecture Addresses It |
|-------------|-----------------------------------|
| PHI never transmitted to external providers | Fully self-hosted — no external API calls |
| Access controls aligned with minimum necessary | Permission-aware retrieval returns only authorized content |
| Audit trail for all document access | Container-level logging for all retrieval events |

---

## 🚀 Deployment Overview

```bash
# Clone the repository
git clone https://github.com/Tymaze3/Enterprise-AI-RAG-Infrastructure

# Configure environment variables
cp .env.example .env
# Edit .env with your Odoo and OneDrive credentials

# Start the full stack
docker-compose up -d

# Access Open WebUI at your internal domain
https://your-internal-domain.com
```

---

## 📁 Repository Structure

```
Enterprise-AI-RAG-Infrastructure/
├── docker-compose.yml          # Full stack orchestration
├── nginx/
│   └── nginx.conf              # Reverse proxy with TLS config
├── docs/
│   ├── architecture.md         # Detailed architecture writeup
│   ├── compliance-mapping.md   # Full CMMC and HIPAA control mapping
│   └── deployment-guide.md     # Step-by-step deployment instructions
├── .env.example                # Environment variable template
└── README.md
```

---

## 🎯 Use Cases

| Environment | Problem Solved |
|-------------|---------------|
| Defense contractors | AI assistance without CUI exposure |
| Healthcare organizations | AI workflows without PHI risk |
| Compliance-sensitive enterprises | Auditable AI with full data sovereignty |
| Air-gapped environments | Offline LLM capability with local models |

---

## 🗺️ Roadmap

- [x] Core Ollama + Open WebUI deployment
- [x] Nginx reverse proxy with HTTPS/TLS
- [x] OneDrive document connector
- [x] Odoo ERP data connector
- [x] Permission-aware retrieval layer
- [ ] Role-based document access control (RBAC integration)
- [ ] Audit log dashboard
- [ ] Automated compliance report generation

---

## 👤 Author

**Tyree Maeser** — Cybersecurity Engineer  
Active Secret Clearance | CMMC L2 | HIPAA | USAF Veteran

- 💼 [LinkedIn](https://www.linkedin.com/in/tyree-maeser)
- 🐙 [GitHub](https://github.com/Tymaze3)

---

> *Built to solve a real problem in a real production environment.*
