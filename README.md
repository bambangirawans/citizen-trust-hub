<div align="center">

[ 🇬🇧 English ](#english-version) | [ 🇮🇩 Indonesia ](#versi-indonesia)

</div>

---

<div id="english-version" align="center">

# TataNota TrustDeal: Citizen Hub & C2C Platform

[![Python](https://img.shields.io/badge/Python-3.12+-blue.svg?logo=python&logoColor=white)](https://www.python.org/)
[![Flask](https://img.shields.io/badge/Flask-Async-black.svg?logo=flask&logoColor=white)](https://flask.palletsprojects.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-336791.svg?logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Redis](https://img.shields.io/badge/Redis-7-DC382D.svg?logo=redis&logoColor=white)](https://redis.io/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.4-38B2AC.svg?logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)
[![License](https://img.shields.io/badge/License-Proprietary-red.svg)]()

**Building Trust in Every Digital Handshake.**

Citizen Trust Hub is a secure Citizen-to-Citizen (C2C) collaboration ecosystem designed with **Zero-Trust Architecture** and **Transparency by Default** principles. This platform facilitates rentals, donations, community projects, and social campaigns that are permanently bound using an encrypted WORM (*Write-Once-Read-Many*) Ledger.

[Citizen Website](https://citizen.tatanota.com) • [Trust Center](https://citizen.tatanota.com/trust_center) • [API & Developer Docs](https://citizen.tatanota.com/developer_manual)

</div>

## Our Vision

A connected world where communities can collaborate, build trust, and turn shared ideas into meaningful social and economic impact.

## What We Are Building

### 1. Zero-Trust Security & Cryptography (Core Engine)
*   **WebCrypto ECDSA P-256:** Digital contract signing (*Smart Agreement*) is performed entirely within the user's browser (Edge PWA), ensuring *Non-Repudiation* without any third party knowing the Private Key.
*   **WORM Ledger (Append-Only):** Every agreement, handover proof, and transaction status is chained using a *SHA-256 Hash-Chain*. The slightest alteration to past data will mathematically break the entire chain (*Tamper-Evident*).
*   **Optimistic Concurrency Control (OCC):** Strict conflict resolution to prevent *race conditions* or stale data manipulation during simultaneous state mutations.

### 2. Citizen Hub & Micro-ERP 
*   **Multi-Initiative Type:** Supports various activities such as Services, Donations, Sales, Community Discussions, and Green Campaigns.
*   **Integrated Escrow:** Citizen funds are securely held and only forwarded to the organizer (Vendor) after consensus is reached or a mediation decision (Dispute) is executed.
*   **Kanban & Budgeting:** Organizers (Tenants) can manage schedules (*Milestones*) and budgets with full transparency to the public.

### 3. Cognitive AI & Multi-Modal Vision
*   **Visual Inspection:** AI (Gemini 3.5 Flash) analyzes handover proof photos (Multimodal) to match physical item conditions with Terms and Conditions (T&C) specifications.
*   **Semantic Similarity Search (RAG):** Utilizes *Local Embeddings (BAAI/bge-m3)* to recommend relevant initiatives to citizens without relying on exact keyword matches.
*   **Content Generator:** *AI Wizard* helps organizers instantly craft titles, persuasive descriptions, and campaign rules.

### 4. Governance & Anti-Scam
*   **Citizen Flagging:** Citizens can report initiatives indicated as *Scams* or duplicates.
*   **Automated Risk Escalation:** The *Policy Engine* autonomously labels risky initiatives as `HIGH` if they reach a reporting threshold.
*   **Operator Takedown:** Moderators (*Human-in-the-Loop*) can perform instant freezes (Takedown) via the control dashboard to protect public funds.

## Architecture & Technology

*   **Backend & Gateway:** Python 3.12+, Flask (Async), SQLAlchemy (AsyncPG), Pydantic (Strict DTO Validation).
*   **Frontend (Edge PWA):** Vanilla JS, Tailwind CSS, DOMPurify, Marked.js, Chart.js.
*   **Edge Storage:** Dexie.js (IndexedDB) for *Offline-First* synchronization and *Session* key storage.
*   **Event Bus & Workers:** Redis Streams (Isolated Background Worker), *Transactional Outbox Pattern* with Redis Delayed Queue.
*   **Web Server (Reverse Proxy):** NGINX with specific *Proxy Buffer* configurations to support real-time *Server-Sent Events* (SSE).

## Roadmap

- [x] Release Core Engine with WORM Ledger & Zero-Trust Architecture.
- [x] Release Citizen Hub (PWA) for C2C collaboration.
- [x] Integrate Micro-ERP and Kanban Operational Analytics.
- [x] Implement Multimodal AI for visual inspection and content generation.
- [x] Isolate microservices with Gunicorn Gthread for concurrent scalability.
- [x] Publish Open API Contract for public exploration.
- [ ] Release SDK for third parties.
- [ ] Integrate with *Public Blockchain* ecosystems for full decentralization (WORM Ledger).

## Getting Started (Internal Team Deployment)

### System Requirements
*   Linux VM (Ubuntu/Debian)
*   Python 3.12+ (Virtual Environment)
*   PostgreSQL 15+ & Redis 7+
*   NGINX
*   Minimum 4GB RAM (8GB recommended for LlamaIndex/Local Embedder)
*   Google GenAI (Gemini) API Key

### Installation & Running (Production/VM)

1.  **Clone the Repository**
    ```bash
    git clone [https://github.com/bambangirawans/citizen-trust-hub.git](https://github.com/bambangirawans/citizen-trust-hub.git)
    cd citizen-trust-hub
    ```

2.  **Environment Configuration**
    Copy the `.env.example` file to `.env` and fill in the required configurations.
    ```bash
    cp .env.example .env
    ```
    *Ensure you provide `SECRET_KEY`, async `PostgreSQL` credentials, `Redis` URL, and `GOOGLE_API_KEY`.*

3.  **Dependencies & Services Preparation (Systemd)**
    Use `pip` within the *virtual environment* (`.venv`) to install `requirements.txt`.
    The system utilizes two main *Systemd Services* and several independent *Background Workers*:
    *   `tatanota-web.service` (IdP & Core API on Port 5000)
    *   `citizentrusthub.service` (C2C Microservice on Port 5001)

4.  **NGINX Configuration**
    Ensure NGINX routes are configured to handle streaming (SSE) without *buffering*, and route traffic to Ports 5000 and 5001 according to the blueprint.

5.  **Access the Application**
    *   Citizen Hub: `[https://citizen.tatanota.com]`
    *   Organizer Admin Dashboard: `[https://citizen.tatanota.com/admin]`
    *   OpenAPI Specification: `[https://api.tatanota.com/v1/openapi]`

## Documentation & Open API Exploration

Citizens, researchers, and the *Open Source* developer community can transparently explore public services and data within the Citizen Trust Hub ecosystem through the provided BFF (*Backend-For-Frontend*) API Contract.

*   [**OpenAPI Contract (Swagger JSON)**](https://api.tatanota.com/v1/openapi) - Complete Swagger v3.0.3 specification. You can import this JSON file into Postman or Swagger UI to simulate initiative searches (`GET /items`) or monitor transaction traffic.
*   [**Citizen & Organizer Guide (User Manual)**](https://citizen.tatanota.com/user_manual) - Integrated system usage guidelines for the public and initiative organizers.
*   [**Whitepaper & Technical Architecture (Developer Manual)**](https://citizen.tatanota.com/developer_manual) - Comprehensive documentation on infrastructure topology, *Zero-Trust*, security, and network telemetry.

## Support & Contribution

We welcome the involvement of developers, designers, researchers, and community builders interested in building a trusted digital collaboration ecosystem.

Your support helps maintain the continuity of open-source development, documentation, infrastructure testing, and maintenance of this collaboration module's *Open API*.

If you find this platform valuable, consider sponsoring the developer through GitHub Sponsors.

<div align="center">
  <a href="https://github.com/sponsors/bambangirawans" target="_blank"><img src="https://img.shields.io/badge/Sponsor_Project-EA4AAA?style=for-the-badge&logo=githubsponsors&logoColor=white" alt="Sponsor via GitHub" style="height: 35px !important;" ></a>
</div>

---
<br>

<div id="versi-indonesia" align="center">

# TataNota TrustDeal: Citizen Hub & C2C Platform

[![Python](https://img.shields.io/badge/Python-3.12+-blue.svg?logo=python&logoColor=white)](https://www.python.org/)
[![Flask](https://img.shields.io/badge/Flask-Async-black.svg?logo=flask&logoColor=white)](https://flask.palletsprojects.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-336791.svg?logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Redis](https://img.shields.io/badge/Redis-7-DC382D.svg?logo=redis&logoColor=white)](https://redis.io/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.4-38B2AC.svg?logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)
[![License](https://img.shields.io/badge/License-Proprietary-red.svg)]()

**Membangun Kepercayaan Di Setiap Jabat Tangan Digital.**

Citizen Trust Hub adalah ekosistem kolaborasi *Citizen-to-Citizen* (C2C) aman yang dirancang dengan prinsip **Zero-Trust Architecture** dan **Transparency by Default**. Platform ini memfasilitasi persewaan, donasi, proyek komunitas, dan kampanye sosial yang diikat secara permanen menggunakan WORM (*Write-Once-Read-Many*) Ledger terenkripsi.

[Website Warga](https://citizen.tatanota.com) • [Trust Center](https://citizen.tatanota.com/trust_center) • [API & Dokumen Developer](https://citizen.tatanota.com/developer_manual)

</div>

## Visi Kami

Dunia yang terhubung di mana komunitas dapat berkolaborasi, membangun kepercayaan, dan mewujudkan gagasan bersama menjadi dampak sosial dan ekonomi yang nyata.

## Apa yang Kami Bangun

### 1. Keamanan Zero-Trust & Kriptografi (Core Engine)
*   **WebCrypto ECDSA P-256:** Penandatanganan kontrak digital (*Smart Agreement*) dilakukan sepenuhnya di dalam *browser* pengguna (Edge PWA), menjamin *Non-Repudiation* tanpa ada pihak ketiga yang mengetahui kunci privat (Private Key).
*   **WORM Ledger (Append-Only):** Setiap kesepakatan, bukti serah terima (handover), dan status transaksi diikat menggunakan *SHA-256 Hash-Chain*. Sedikit saja perubahan pada data masa lalu akan secara matematis merusak seluruh rantai (*Tamper-Evident*).
*   **Optimistic Concurrency Control (OCC):** Resolusi konflik yang sangat ketat untuk mencegah *race conditions* atau manipulasi data usang saat mutasi *state* (transaksi) terjadi bersamaan.

### 2. Citizen Hub & Micro-ERP 
*   **Multi-Tipe Inisiatif:** Mendukung berbagai kegiatan seperti Jasa, Donasi, Jual-Beli, Rembuk Komunitas, dan Kampanye Hijau (*Green Initiative*).
*   **Escrow Terintegrasi:** Dana warga ditahan sementara secara aman dan hanya diteruskan ke penyelenggara (Vendor) setelah tercapai konsensus atau putusan mediasi (Sengketa).
*   **Kanban & Budgeting:** Penyelenggara (Tenant) dapat mengelola jadwal (*Milestones*) dan RAB (Rencana Anggaran Biaya) secara transparan dan terbuka kepada publik.

### 3. AI Kognitif & Vision Multimodal
*   **Inspeksi Visual:** AI (Gemini 3.5 Flash) menganalisis foto bukti serah terima (Multimodal) untuk mencocokkan kondisi fisik barang dengan spesifikasi pada Syarat dan Ketentuan (S&K).
*   **Semantic Similarity Search (RAG):** Menggunakan *Local Embeddings (BAAI/bge-m3)* untuk merekomendasikan inisiatif yang relevan kepada warga tanpa bergantung pada kecocokan kata kunci eksak.
*   **Generator Konten:** *AI Wizard* membantu penyelenggara merancang judul, deskripsi persuasif, serta aturan kampanye secara instan.

### 4. Tata Kelola & Anti-Scam
*   **Pelaporan Warga (Flagging):** Warga dapat melaporkan inisiatif yang terindikasi *Scam* atau duplikasi.
*   **Eskalasi Risiko Otomatis:** *Policy Engine* akan secara mandiri melabeli inisiatif berisiko menjadi `HIGH` jika mencapai ambang batas pelaporan.
*   **Operator Takedown:** Moderator (*Human-in-the-Loop*) dapat melakukan pembekuan instan (Takedown) melalui dasbor kendali untuk melindungi dana publik.

## Arsitektur & Teknologi Terkini

*   **Backend & Gateway:** Python 3.12+, Flask (Async), SQLAlchemy (AsyncPG), Pydantic (Validasi DTO Ekstra Ketat).
*   **Frontend (Edge PWA):** Vanilla JS, Tailwind CSS, DOMPurify, Marked.js, Chart.js.
*   **Edge Storage:** Dexie.js (IndexedDB) untuk sinkronisasi *Offline-First* dan penyimpanan kunci *Session*.
*   **Event Bus & Workers:** Redis Streams (Background Worker Terisolasi), *Transactional Outbox Pattern* dengan Redis Delayed Queue.
*   **Web Server (Reverse Proxy):** NGINX dengan konfigurasi *Proxy Buffer* khusus untuk mendukung *Server-Sent Events* (SSE) secara *real-time*.

## Peta Jalan (Roadmap)

- [x] Rilis Core Engine dengan WORM Ledger & Zero-Trust Architecture.
- [x] Rilis Citizen Hub (PWA) untuk kolaborasi C2C.
- [x] Integrasi Micro-ERP dan Analitik Operasional Kanban.
- [x] Implementasi AI Multimodal untuk inspeksi visual dan generator konten.
- [x] Isolasi layanan (Microservices) dengan Gunicorn Gthread untuk skalabilitas konkuren.
- [x] Publikasi Open API Contract untuk eksplorasi publik.
- [ ] Rilis SDK untuk pihak ketiga.
- [ ] Integrasi ke ekosistem *Public Blockchain* untuk desentralisasi penuh (WORM Ledger).

## Memulai (Panduan Instalasi Tim Internal)

### Persyaratan Sistem
*   Linux VM (Ubuntu/Debian)
*   Python 3.12+ (Virtual Environment)
*   PostgreSQL 15+ & Redis 7+
*   NGINX
*   Minimal 4GB RAM (Direkomendasikan 8GB untuk LlamaIndex/Local Embedder)
*   Google GenAI (Gemini) API Key

### Instalasi & Menjalankan (Produksi/VM)

1.  **Kloning Repositori**
    ```bash
    git clone [https://github.com/bambangirawans/citizen-trust-hub.git](https://github.com/bambangirawans/citizen-trust-hub.git)
    cd citizen-trust-hub
    ```

2.  **Konfigurasi Lingkungan**
    Salin file `.env.example` ke `.env` dan lengkapi konfigurasi yang diwajibkan.
    ```bash
    cp .env.example .env
    ```
    *Pastikan Anda mengisi `SECRET_KEY`, kredensial `PostgreSQL` asinkron, URL `Redis`, dan `GOOGLE_API_KEY`.*

3.  **Persiapan Dependensi & Layanan (Systemd)**
    Gunakan `pip` dalam *virtual environment* (`.venv`) untuk menginstal `requirements.txt`.
    Sistem menggunakan dua *Service Systemd* utama dan beberapa *Background Worker* independen:
    *   `tatanota-web.service` (IdP & Core API di Port 5000)
    *   `citizentrusthub.service` (Layanan Microservice C2C di Port 5001)

4.  **Konfigurasi NGINX**
    Pastikan rute NGINX telah dikonfigurasi untuk menangani aliran *streaming* (SSE) tanpa *buffering*, serta merutekan lalu lintas ke Port 5000 dan 5001 sesuai *blueprint*.

5.  **Akses Aplikasi**
    *   Citizen Hub (Warga): `[https://citizen.tatanota.com]`
    *   Dasbor Admin Penyelenggara: `[https://citizen.tatanota.com/admin]`
    *   Spesifikasi OpenAPI: `[https://api.tatanota.com/v1/openapi]`

## Dokumentasi & Eksplorasi Terbuka (Open API)

Warga, peneliti, dan komunitas pengembang *Open Source* dapat menjelajahi layanan dan data publik secara transparan di dalam ekosistem Citizen Trust Hub melalui Kontrak API BFF (*Backend-For-Frontend*) yang disediakan.

*   [**OpenAPI Contract (Swagger JSON)**](https://api.tatanota.com/v1/openapi) - Spesifikasi lengkap Swagger v3.0.3. Anda dapat mengimpor berkas JSON ini ke Postman atau Swagger UI untuk menyimulasikan pencarian inisiatif (`GET /items`) atau memantau lalu lintas transaksi.
*   [**Panduan Warga & Penyelenggara (User Manual)**](https://citizen.tatanota.com/user_manual) - Petunjuk penggunaan sistem terpadu bagi masyarakat dan penyelenggara inisiatif.
*   [**Whitepaper & Arsitektur Teknis (Developer Manual)**](https://citizen.tatanota.com/developer_manual) - Dokumentasi komprehensif mengenai topologi infrastruktur, *Zero-Trust*, keamanan, dan telemetri jaringan.

## Dukungan & Kontribusi

Kami menyambut baik keterlibatan pengembang, desainer, peneliti, dan penggerak komunitas yang tertarik membangun ekosistem kolaborasi digital yang tepercaya.

Dukungan Anda membantu menjaga keberlangsungan pengembangan sumber terbuka, dokumentasi, pengujian infrastruktur, dan pemeliharaan *Open API* modul kolaborasi ini.

Jika Anda menganggap platform ini berharga dan bermanfaat, pertimbangkan untuk mensponsori pengembang melalui GitHub Sponsors.

<div align="center">
  <a href="https://github.com/sponsors/bambangirawans" target="_blank"><img src="https://img.shields.io/badge/Sponsor_Project-EA4AAA?style=for-the-badge&logo=githubsponsors&logoColor=white" alt="Sponsor via GitHub" style="height: 35px !important;" ></a>
</div>
