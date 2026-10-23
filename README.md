<div align="center">

# TataNota TrustDeal: Citizen Hub & C2C Platform

[![Python](https://img.shields.io/badge/Python-3.12+-blue.svg?logo=python&logoColor=white)](https://www.python.org/)
[![Flask](https://img.shields.io/badge/Flask-Async-black.svg?logo=flask&logoColor=white)](https://flask.palletsprojects.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-336791.svg?logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Redis](https://img.shields.io/badge/Redis-7-DC382D.svg?logo=redis&logoColor=white)](https://redis.io/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.4-38B2AC.svg?logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)
[![License](https://img.shields.io/badge/License-Proprietary-red.svg)]()

**Building Trust in Every Digital Handshake.**

TataNota TrustDeal is an *Enterprise-grade* Citizen-to-Citizen (C2C) collaboration ecosystem designed with **Zero-Trust Architecture** and **Transparency by Default** principles. This platform facilitates rentals, donations, community projects, and social campaigns that are permanently bound using a WORM (*Write-Once-Read-Many*) Ledger.

[Website](https://tatanota.com/trustdeal/welcome) • [Trust Center](https://tatanota.com/trustdeal/trust_center) • [Developer Docs](https://tatanota.com/trustdeal/developer_manual)

</div>

---

## Our Vision

A connected world where communities can collaborate, build trust, and turn shared ideas into meaningful social and economic impact.

##  What We Are Building

### 1. Zero-Trust Security & Cryptography (Core Engine)
*   **WebCrypto ECDSA P-256:** Digital contract signing (*Smart Agreement*) is performed purely in the user's browser (Edge), ensuring *Non-Repudiation* without any third party knowing the private key.
*   **WORM Ledger (Append-Only):** Every agreement, item handover, and transaction status is chained using a *SHA-256 Hash-Chain*. The slightest alteration in the past will mathematically break the entire chain (*Tamper-Evident*).
*   **Optimistic Concurrency Control (OCC):** Strict conflict resolution to prevent *race conditions* or stale data during simultaneous state mutations.

### 2. Citizen Hub & Micro-ERP (Open API)
*   **Multi-Initiative Type:** Supports Services, Donations, Sales, Community Discussions, and Green Campaigns (*Green Initiative*).
*   **Integrated Escrow:** Citizen funds are securely held and only *settled* to the organizer after consensus completion or a mediation decision (Dispute).
*   **Kanban & Budgeting:** Organizers (Tenants) can manage schedules (*Milestones*) and budgets with full transparency to the public.

### 3. Cognitive AI & Multi-Modal Vision
*   **Vision Inspection:** AI (Gemini 3.5 Flash) analyzes handover proof photos (Multimodal) to match physical item conditions with terms and conditions descriptions.
*   **Semantic Similarity Search:** Utilizes *Local Embeddings (BAAI/bge-m3)* to recommend similar initiatives without relying on exact keyword matches.
*   **Content Generation:** *AI Wizard* helps organizers design titles, persuasive descriptions, and T&C campaigns instantly.

### 4. Governance & Anti-Scam
*   **Citizen Flagging:** Citizens can report initiatives indicated as *Scams* or duplicates.
*   **Automated Risk Escalation:** The *Policy Engine* autonomously labels risky initiatives as `HIGH` if they reach a reporting threshold.
*   **Operator Takedown:** Moderators (*HitL*) can perform instant *Takedowns* (Suspensions) via the command dashboard to protect public funds.

---

## Architecture & Technology

*   **Backend:** Python 3.12+, Flask (Async), SQLAlchemy (AsyncPG), Pydantic (Strict DTO Validation).
*   **Frontend (PWA):** Vanilla JS, Tailwind CSS, DOMPurify, Marked.js, Chart.js.
*   **Edge Store:** Dexie.js (IndexedDB) for Offline-First Synchronization.
*   **Event Bus & Worker:** Redis Streams, *Transactional Outbox Pattern* with Redis Delayed Queue.
*   **Telemetry:** Prometheus Client (Custom metrics: *Queue Depth*, *AI Latency*, *SSE Connections*).

---

## Roadmap

- [x] Release Core Engine with WORM Ledger & Zero-Trust Architecture.
- [x] Release Citizen Hub (PWA) for C2C collaboration.
- [x] Integrate Micro-ERP and Kanban Analytics.
- [x] Implement Multi-Modal AI for visual inspection and content generation.
- [x] Publish Open API for Citizen exploration.
- [ ] Release SDK for third parties.
- [ ] Integrate with public blockchain ecosystems for WORM Ledger decentralization.

---

## Getting Started (Internal Team Deployment)

### System Requirements
*   Docker & Docker Compose
*   Minimum 4GB RAM (8GB recommended for LlamaIndex/Local Embedder)
*   Google GenAI (Gemini) API Key

### Installation & Running (Development)

1.  **Clone the Repository**
    ```bash
    git clone https://github.com/bambangirawans/citizen-trust-hub.git
    cd citizen-trust-hub
    ```

2.  **Environment Configuration**
    Copy the `.env.example` file to `.env` and fill in the required configurations.
    ```bash
    cp .env.example .env
    ```
    *Ensure you provide `SECRET_KEY`, `PostgreSQL` credentials, `Redis`, and `GOOGLE_API_KEY`.*

3.  **Run Docker Compose**
    ```bash
    docker-compose up -d --build
    ```

4.  **Access the Application**
    *   Citizen Hub: `[https://tatanota.com/trustdeal]`
    *   Swagger/OpenAPI: `[https://api.tatanota.com/v1/trustdeal/openapi]`
    *   API Healthcheck: `[https://api.tatanota.com/health]`

---

## Documentation & Citizen Exploration (Open API)

Citizens and the *Open Source* developer community can transparently explore the services and public data within TrustDeal through the provided BFF (Backend-For-Frontend) API Contract.

*   [**OpenAPI Contract (Swagger JSON)**](https://api.tatanota.com/v1/trustdeal/openapi) - Complete Swagger v3.0.3 specification. You can import this JSON file into Postman or Swagger UI to simulate initiative searches (`GET /items`) or monitor transactions.
*   [**Citizen & Tenant Guide (User Manual)**](https://tatanota.com/trustdeal/user_manual) - System usage guide for the public and initiative organizers.
*   [**Whitepaper & Technical Architecture (Developer Manual)**](https://tatanota.com/trustdeal/developer_manual) - Comprehensive documentation on topology, *Zero-Trust*, DevOps, and *Telemetry*.

---

## Contributing

We welcome developers, designers, researchers, and community builders interested in trusted digital collaboration.

Please check our contribution guidelines before submitting changes.

## Support Development

Your support helps sustain open-source development, documentation, testing, and maintenance of the *Open API* and public collaboration modules.

If you find our work valuable, consider sponsoring the developer through GitHub Sponsors when sponsorship is available.

---

---
<div align="center">
  <a href="https://github.com/sponsors/bambangirawans" target="_blank"><img src="https://img.shields.io/badge/Sponsor_Project-EA4AAA?style=for-the-badge&logo=githubsponsors&logoColor=white" alt="Sponsor via GitHub" style="height: 35px !important;" ></a>
</div>
