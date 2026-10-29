<div align="center">

[ 🇬🇧 English ](#english-version) | [ 🇮🇩 Indonesia ](#versi-indonesia)

</div>

---

<div id="english-version" align="center">

# Citizen Trust Hub -  Trust Citizen Colaboration Platform

[![Python](https://img.shields.io/badge/Python-3.12+-blue.svg?logo=python&logoColor=white)](https://www.python.org/)
[![Flask](https://img.shields.io/badge/Flask-Async-black.svg?logo=flask&logoColor=white)](https://flask.palletsprojects.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-336791.svg?logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Redis](https://img.shields.io/badge/Redis-7-DC382D.svg?logo=redis&logoColor=white)](https://redis.io/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.4-38B2AC.svg?logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)
[![License](https://img.shields.io/badge/License-Proprietary-red.svg)]()

**Building Trust in Every Digital Handshake.**

Citizen Trust Hub is a secure Citizen-to-Citizen (C2C) collaboration ecosystem designed with **Zero-Trust Architecture** and **Transparency by Default** principles. This platform facilitates rentals, donations, community projects, and social campaigns whose audit trails are permanently secured using a Cryptographic WORM (*Write-Once-Read-Many*) Ledger.

[Citizen Website](https://citizen.tatanota.com) • [Trust Center](https://citizen.tatanota.com/trust_center) • [API & Developer Docs](https://citizen.tatanota.com/developer_manual)

</div>

## Our Vision

A connected world where communities can collaborate, build trust, and turn shared ideas into meaningful social and economic impact through transparent and auditable digital records.

## What We Are Building

### 1. Zero-Trust Security & Hardware Identity (Core Engine)
*   **WebAuthn (Passkeys):** Replaces legacy passwords and brittle browser-bound keys with FIDO2 hardware-bound biometric authentication (TouchID/FaceID). Ensures robust *Non-Repudiation* where users authenticate securely via their OS password manager.
*   **WORM Ledger (Append-Only):** Every digital agreement, status report, and dispute facilitation is chained using a *SHA-256 Hash-Chain*. The slightest alteration to past data will mathematically break the entire chain (*Tamper-Evident*).
*   **Optimistic Concurrency Control (OCC):** Strict conflict resolution to prevent *race conditions* or stale data manipulation during simultaneous state mutations.

### 2. Citizen Hub & Operations Management 
*   **Multi-Initiative Type:** Supports various collaborative activities such as Rentals, Donations, Sales, Community Discussions, and Green Campaigns.
*   **Zero-Escrow Financial Tracking:** The platform explicitly acts *only* as a recording facilitator. We do not hold funds or provide automated payment gateways. Users self-report financial milestones and fund transfers independently, ensuring legal compliance and reducing centralized financial risk.
*   **Kanban & Budgeting:** Organizers (Tenants) can manage schedules (*Milestones*) and self-reported budgets with full transparency to the public via a micro-ERP interface.

### 3. Cognitive AI Copilot & Multi-Signal Validation
*   **Universal Omnibox (OSINT + AI):** A unified search bar allowing citizens to scan initiative links or names against live Open Source Intelligence (OSINT), legal compliance rules, and AI Fraud Detection models, producing a holistic Risk Score before participation.
*   **Visual Inspection (Vision AI):** AI (Gemini 3.5 Flash) analyzes uploaded images (Multimodal) to identify potential anomalies or forensic manipulation during digital handshakes.
*   **Semantic Similarity Search (RAG):** Utilizes *Local Embeddings (BAAI/bge-m3)* coupled with an internal Neo4j Knowledge Graph to recommend relevant initiatives and contextualize anomalies.

### 4. Governance & Dispute Facilitation
*   **Citizen Flagging:** Citizens can report initiatives indicated as *Scams* or duplicates.
*   **Automated Risk Escalation:** The *Policy Engine* autonomously labels risky initiatives as `HIGH` if they breach multi-signal AI thresholds or human reporting limits.
*   **Dispute Facilitation (HITL):** Operators (*Human-in-the-Loop*) can intervene in flagged transactions or user disputes, reviewing the WORM audit trail to execute instant freezes (Takedown) via the central control dashboard.

## Architecture & Technology

*   **Backend & Gateway:** Python 3.12+, Flask (Async), SQLAlchemy (AsyncPG), Pydantic V2 (Strict DTO Validation), PyOTP.
*   **Frontend (Edge PWA):** Vanilla JS, Tailwind CSS, DOMPurify, Marked.js, WebAuthn API.
*   **Event Bus & Workers:** Redis Streams, *Transactional Outbox Pattern* (PostgreSQL to Redis) with isolated background daemon to prevent lock collisions.
*   **Web Server (Reverse Proxy):** NGINX configured for *Server-Sent Events* (SSE) chunking and HTTP Connection Pooling.

## Roadmap

- [x] Release Core Engine with WORM Ledger & Zero-Trust Architecture.
- [x] Migrate to Biometric-First WebAuthn (Passkeys) Identity.
- [x] Release Citizen Hub (PWA) for C2C collaboration.
- [x] Implement Multi-Signal Cognitive AI (Omnibox) for OSINT & Fraud Detection.
- [x] Isolate microservices with Gunicorn Gthread for concurrent scalability.
- [x] Publish Open API Contract for public exploration.
- [ ] Release Developer SDK for third-party integrations.
- [ ] Implement Web of Trust (Vouching) for rural entities lacking global OSINT footprints.

## Getting Started (Internal Team Deployment)

### System Requirements
*   Linux VM (Ubuntu/Debian)
*   Python 3.12+ (Virtual Environment)
*   PostgreSQL 15+ & Redis 7+
*   NGINX
*   Minimum 4GB RAM (8GB recommended for Local Embedder Memory Mapping)
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
    *Critical: You must provide a valid `SECRET_KEY`, async `PostgreSQL` credentials, `Redis` URL, and `GOOGLE_API_KEY` to prevent AI fallback crashes.*

3.  **Dependencies & Services Preparation (Systemd)**
    Use `pip` within the *virtual environment* (`.venv`) to install `requirements.txt`.
    The system utilizes multiple independent *Systemd Services*:
    *   `tatanota-web.service` (IdP, WebAuthn & Core API on Port 5000)
    *   `citizentrusthub.service` (C2C Microservice on Port 5001)
    *   `tatanota-outbox.service` (Isolated Background Event Worker)

4.  **NGINX Configuration**
    Ensure NGINX routes are configured to handle streaming (SSE) without *buffering*, inject `X-Forwarded-For` for IP Spoofing protection, and route traffic to Ports 5000 and 5001.

5.  **Access the Application**
    *   Citizen Hub: `https://citizen.tatanota.com`
    *   Trust Center (WORM & AI Scanner): `https://citizen.tatanota.com/trust_center`

## Documentation & Open API Exploration

Citizens, researchers, and the *Open Source* developer community can transparently explore public services and data within the Citizen Trust Hub ecosystem through the provided BFF (*Backend-For-Frontend*) API Contract.

*   [**OpenAPI Contract (Swagger JSON)**](https://api.tatanota.com/v1/openapi) - Complete Swagger v3.0.3 specification. You can import this JSON file into Postman or Swagger UI.
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

# Citizen Trust Hub -  Trust Citizen Colaboration Platform

[![Python](https://img.shields.io/badge/Python-3.12+-blue.svg?logo=python&logoColor=white)](https://www.python.org/)
[![Flask](https://img.shields.io/badge/Flask-Async-black.svg?logo=flask&logoColor=white)](https://flask.palletsprojects.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-336791.svg?logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Redis](https://img.shields.io/badge/Redis-7-DC382D.svg?logo=redis&logoColor=white)](https://redis.io/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.4-38B2AC.svg?logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)
[![License](https://img.shields.io/badge/License-Proprietary-red.svg)]()

**Membangun Kepercayaan Di Setiap Jabat Tangan Digital.**

Citizen Trust Hub adalah ekosistem kolaborasi *Citizen-to-Citizen* (C2C) aman yang dirancang dengan prinsip **Zero-Trust Architecture** dan **Transparency by Default**. Platform ini memfasilitasi persewaan, donasi, proyek komunitas, dan kampanye sosial yang jejak auditnya diikat secara permanen menggunakan Kriptografi WORM (*Write-Once-Read-Many*) Ledger.

[Website Warga](https://citizen.tatanota.com) • [Trust Center](https://citizen.tatanota.com/trust_center) • [API & Dokumen Developer](https://citizen.tatanota.com/developer_manual)

</div>

## Visi Kami

Dunia yang terhubung di mana komunitas dapat berkolaborasi, membangun kepercayaan, dan mewujudkan gagasan bersama menjadi dampak sosial dan ekonomi yang nyata melalui jejak rekam digital yang transparan dan dapat diaudit.

## Apa yang Kami Bangun

### 1. Keamanan Zero-Trust & Identitas Berbasis Perangkat (Core Engine)
*   **WebAuthn (Passkeys):** Menggantikan kata sandi usang dan kunci *browser* yang rentan dengan otentikasi biometrik bawaan perangkat keras (FIDO2/TouchID/FaceID). Menjamin *Non-Repudiation* yang sangat tangguh sekaligus kebal dari insiden terhapusnya *cache*.
*   **WORM Ledger (Append-Only):** Setiap kesepakatan digital, pelaporan status, dan fasilitasi sengketa diikat menggunakan *SHA-256 Hash-Chain*. Sedikit saja perubahan pada data masa lalu akan secara matematis merusak seluruh rantai (*Tamper-Evident*).
*   **Optimistic Concurrency Control (OCC):** Resolusi konflik yang sangat ketat untuk mencegah *race conditions* atau manipulasi data usang saat mutasi status (*state*) terjadi bersamaan.

### 2. Citizen Hub & Manajemen Operasional 
*   **Multi-Tipe Inisiatif:** Mendukung berbagai kegiatan seperti Persewaan Jasa, Donasi, Jual-Beli, Rembuk Komunitas, dan Kampanye Hijau (*Green Initiative*).
*   **Pelacakan Finansial Tanpa Escrow Internal (Zero-Escrow):** Platform bertindak *sebatas* sebagai fasilitator pencatatan. Kami **tidak menahan dana** atau menyediakan gerbang pembayaran otomatis. Pengguna melaporkan (*self-report*) tonggak capaian dan transfer dana secara mandiri di luar sistem, memastikan kepatuhan hukum dan meminimalisir risiko finansial terpusat.
*   **Kanban & Budgeting:** Penyelenggara (Tenant) dapat mengelola jadwal (*Milestones*) dan pelaporan anggaran secara transparan kepada publik melalui antarmuka mikro-ERP.

### 3. Copilot AI Kognitif & Validasi Multi-Sinyal
*   **Universal Omnibox (OSINT + AI):** Kotak pencarian terpadu yang memungkinkan warga memindai tautan atau nama inisiatif. Mesin AI memadukan Open Source Intelligence (OSINT) langsung, aturan kepatuhan hukum, dan detektor penipuan (Fraud) untuk menghasilkan Skor Risiko menyeluruh sebelum warga berpartisipasi.
*   **Inspeksi Visual (Vision AI):** AI (Gemini 3.5 Flash) menganalisis foto yang diunggah (Multimodal) untuk mendeteksi potensi anomali fisik atau manipulasi forensik selama proses jabat tangan digital.
*   **Semantic Similarity Search (RAG):** Menggunakan *Local Embeddings (BAAI/bge-m3)* yang disatukan dengan internal Neo4j Knowledge Graph untuk merekomendasikan inisiatif yang relevan dan memberikan konteks tambahan atas sebuah anomali.

### 4. Tata Kelola & Fasilitasi Sengketa
*   **Pelaporan Warga (Flagging):** Warga dapat melaporkan inisiatif yang terindikasi *Scam* atau duplikasi.
*   **Eskalasi Risiko Otomatis:** *Policy Engine* akan secara mandiri melabeli inisiatif berisiko menjadi `HIGH` jika menembus ambang batas peringatan AI atau batas pelaporan warga.
*   **Fasilitasi Sengketa (HITL):** Operator (*Human-in-the-Loop*) dapat mengintervensi transaksi yang bermasalah, meninjau jejak audit WORM, dan melakukan pembekuan instan (Takedown) melalui dasbor kendali.

## Arsitektur & Teknologi Terkini

*   **Backend & Gateway:** Python 3.12+, Flask (Async), SQLAlchemy (AsyncPG), Pydantic V2 (Validasi DTO Mutlak), PyOTP.
*   **Frontend (Edge PWA):** Vanilla JS, Tailwind CSS, DOMPurify, Marked.js, WebAuthn API.
*   **Event Bus & Workers:** Redis Streams, *Transactional Outbox Pattern* (PostgreSQL ke Redis) dengan daemon latar belakang yang diisolasi (Mencegah *Lock Collisions*).
*   **Web Server (Reverse Proxy):** NGINX dengan konfigurasi *Chunking Server-Sent Events* (SSE) dan *HTTP Connection Pooling*.

## Peta Jalan (Roadmap)

- [x] Rilis Core Engine dengan WORM Ledger & Zero-Trust Architecture.
- [x] Migrasi ke Identitas Biometrik (Biometric-First WebAuthn / Passkeys).
- [x] Rilis Citizen Hub (PWA) untuk kolaborasi C2C.
- [x] Implementasi AI Kognitif Multi-Sinyal (Omnibox) untuk OSINT & Deteksi Fraud.
- [x] Isolasi layanan (Microservices) dengan Gunicorn Gthread untuk skalabilitas konkuren.
- [x] Publikasi Open API Contract untuk eksplorasi publik.
- [ ] Rilis Developer SDK untuk integrasi sistem pihak ketiga.
- [ ] Implementasi Web of Trust (Vouching) untuk inisiatif komunitas lokal yang tidak memiliki rekam jejak digital global (OSINT).

## Memulai (Panduan Instalasi Tim Internal)

### Persyaratan Sistem
*   Linux VM (Ubuntu/Debian)
*   Python 3.12+ (Virtual Environment)
*   PostgreSQL 15+ & Redis 7+
*   NGINX
*   Minimal 4GB RAM (Direkomendasikan 8GB untuk alokasi memori Local Embedder)
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
    *Sangat Penting: Anda wajib mengisi `SECRET_KEY`, kredensial `PostgreSQL` asinkron, URL `Redis`, dan `GOOGLE_API_KEY` guna mencegah sistem AI mengalami Crash seketika (Fallback Error).*

3.  **Persiapan Dependensi & Layanan (Systemd)**
    Gunakan `pip` dalam *virtual environment* (`.venv`) untuk menginstal `requirements.txt`.
    Sistem mengeksekusi beberapa *Service Systemd* independen:
    *   `tatanota-web.service` (IdP, WebAuthn API & Core Gateway di Port 5000)
    *   `citizentrusthub.service` (Layanan Microservice C2C di Port 5001)
    *   `tatanota-outbox.service` (Daemon Pekerja Event terisolasi)

4.  **Konfigurasi NGINX**
    Pastikan rute NGINX telah dikonfigurasi untuk menyalurkan aliran *streaming* (SSE) tanpa *buffering*, menyuntikkan `X-Forwarded-For` untuk pelindung IP Spoofing, serta merutekan lalu lintas ke Port 5000 dan 5001.

5.  **Akses Aplikasi**
    *   Citizen Hub (Warga): `https://citizen.tatanota.com`
    *   Pusat Transparansi (WORM & Omnibox): `https://citizen.tatanota.com/trust_center`

## Dokumentasi & Eksplorasi Terbuka (Open API)

Warga, peneliti, dan komunitas pengembang *Open Source* dapat menjelajahi layanan dan data publik secara transparan di dalam ekosistem Citizen Trust Hub melalui Kontrak API BFF (*Backend-For-Frontend*) yang disediakan.

*   [**OpenAPI Contract (Swagger JSON)**](https://api.tatanota.com/v1/openapi) - Spesifikasi lengkap Swagger v3.0.3.
*   [**Panduan Warga & Penyelenggara (User Manual)**](https://citizen.tatanota.com/user_manual) - Petunjuk penggunaan sistem terpadu bagi masyarakat dan penyelenggara inisiatif.
*   [**Whitepaper & Arsitektur Teknis (Developer Manual)**](https://citizen.tatanota.com/developer_manual) - Dokumentasi komprehensif mengenai topologi infrastruktur, *Zero-Trust*, keamanan, dan telemetri jaringan.

## Dukungan & Kontribusi

Kami menyambut baik keterlibatan pengembang, desainer, peneliti, dan penggerak komunitas yang tertarik membangun ekosistem kolaborasi digital yang tepercaya.

Dukungan Anda membantu menjaga keberlangsungan pengembangan sumber terbuka, dokumentasi, pengujian infrastruktur, dan pemeliharaan *Open API* modul kolaborasi ini.

Jika Anda menganggap platform ini berharga dan bermanfaat, pertimbangkan untuk mensponsori pengembang melalui GitHub Sponsors.

<div align="center">
  <a href="https://github.com/sponsors/bambangirawans" target="_blank"><img src="https://img.shields.io/badge/Sponsor_Project-EA4AAA?style=for-the-badge&logo=githubsponsors&logoColor=white" alt="Sponsor via GitHub" style="height: 35px !important;" ></a>
</div>
