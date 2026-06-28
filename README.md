# Vitrus Enterprise

**The glass-box structured-data brain for regulated, on-prem & air-gapped organizations.**

Vitrus Enterprise extends the open-core [Vitrus](https://github.com/ahmetvural79/Vitrus) engine to **relational databases** (MySQL/Postgres) and **sovereign on-prem deployments** — so AI agents and people can ask questions across your existing systems and get answers that are grounded, auditable, and paired with an explicit, deterministic list of **what the system does *not* know**.

> This repository is **informational only** — it documents the Enterprise edition. The engine ([@vitrus/core](https://github.com/ahmetvural79/Vitrus)) is open. The Enterprise capabilities below are **commercial / source-available on request** and live in a private repository.

---

## The thesis (preserved on structured data)

> **The LLM proposes, a deterministic guard decides — and it shows the gap instead of bluffing.**

Most "chat with your database" tools generate SQL and run it blindly. Vitrus Enterprise puts a **deterministic, LLM-free guard** between the model and your data: if the model hallucinates a table, writes anything but a read-only `SELECT`, touches a protected column, or the schema can't answer the question — **the query never runs**, and you get an honest "I couldn't answer this safely," not a confident wrong number.

---

## What it adds

### 🛡️ Text-to-SQL with a deterministic anti-hallucination guard
Natural-language question → relevant tables → candidate `SELECT` (local or cloud LLM) → **deterministic guard** (single-statement · read-only/SELECT-only · no unknown tables/columns · policy/PII rules · mandatory row limit) → read-only execution → answer **+ provenance** (which tables, which exact SQL). The trust layer is LLM-free and auditable.

### 🧠 Verified-query memory (accuracy that compounds)
Confirmed `question → SQL` pairs become **deterministic, auditable memory** and are retrieved as few-shot examples for similar future questions — so the system learns your schema, joins, and business definitions over time. The Vanna-style "RAG as memory" loop, with a Vitrus twist: **only guard-passed, verified queries become memory.**

### 🤖 Governed MCP — let agents query your data without bypassing the guard
A Model Context Protocol server exposes the SQL brain to **Claude Desktop, Cursor, Codex, OpenClaw / Hermes** and your own agents — `sql_ask`, `sql_run`, `list_tables`, `verify_claim`, `data_quality_gaps`, `teach_query`. The guard, row-level security, column masking, and audit trail are enforced **inside every tool**, so an agent cannot hallucinate a table, write data, or read a protected column. `stdio` + Streamable HTTP. Most text-to-SQL tools ship no governed MCP at all — here it's a first-class, governed surface.

### 🔍 Structured glass-box
Deterministic, LLM-free data-quality gaps (**orphan foreign keys, stale rows, empty tables, missing primary keys** — each with its probe SQL), claim verification (**grounded / unsupported / cannot-verify** with evidence), full provenance, and a **KVKK/GDPR audit trail** with PII masking.

### 🖥️ Modern white-label operator console
A single-tenant, brandable **dark dashboard**: ask in plain language → see the SQL → edit & run → results **+ auto chart** (deterministic, rendered client-side — **zero code execution**) · suggested starter & follow-up questions · "is this SQL correct?" write-back · gap / verify / provenance panels · training-data management with one-click **schema seeding** · setup wizard. Runs as one process — no external dependencies, air-gapped friendly.

### 🔒 Fully local & air-gapped
Local LLM (**Ollama / Gemma**) + local embedder (**BGE-M3 / Qwen3**, strong Turkish & multilingual) — **data never leaves the building.** No cloud keys required.

### 📦 One-command on-prem
`docker compose up` (Postgres + pgvector, Ollama, console) — or an **air-gapped USB bundle**: carry it in, load it, it runs. Backup/restore included.

### 🔌 Connects to the systems you already run — including ERP
MySQL & Postgres today; **SQL Server, Oracle, and SAP HANA** drivers for **SAP** (S/4HANA via HANA SQL / CDS views; ECC via a read-only replica) and **Canias** — the ERP systems factories actually run. Plus token-REST connectors for SaaS & developer tools (**GitHub, GitLab, Jira, Notion, Zendesk, Airtable, Stripe, HubSpot, Salesforce…**) that flow into the same brain. Recommended path for ERP: a **read-only replica**, so production is never touched and the same guard / masking / audit applies.

### ✅ Read-only by construction
Connects to your **existing** databases without ever writing to them — four layers: a SELECT-only DB user, a read-only transaction, a statement timeout, and the AST guard.

---

## Who it's for

Governments & **municipalities**, **factories**, and regulated / sovereignty-sensitive organizations — where data can't leave the premises and a wrong answer has real consequences. Connect it to the relational databases and document tables you already run; keep the source of truth yours.

## Open-core

Vitrus is **open-core**. The engine — hybrid retrieval, deterministic gap analysis, the self-linking typed graph, MCP, SKILL.md — is open at **[github.com/ahmetvural79/Vitrus](https://github.com/ahmetvural79/Vitrus)** and stays open. Enterprise builds **on top of it** without modifying it: the structured-data, Text-to-SQL, memory, console, and air-gapped deployment capabilities are the commercial layer.

## Get in touch

Interested in a pilot or evaluation? Open an issue or discussion on the **[core repository](https://github.com/ahmetvural79/Vitrus)**.

---

### Özet (Türkçe)

**Vitrus Enterprise**, açık-çekirdek Vitrus'u **ilişkisel veritabanlarına** (MySQL/Postgres) ve **air-gapped on-prem** kurulumlara taşır. Doğal dilde sorun → aday SQL → **deterministik guard** (yalnız tek-ifade `SELECT`, şemada olmayan tablo/kolon yok, PII/politika, zorunlu LIMIT) → salt-okunur çalıştırma → cevap + kaynak. Guard güvenle çeviremezse **uydurmaz, "bilmiyorum" der.** Doğrulanmış sorgular kalıcı, denetlenebilir hafıza olur (doğruluk birikir). Yapılandırılmış glass-box (orphan FK / bayat satır / boş tablo boşlukları + KVKK denetim izi, PII maskeli). **Yönetişimli MCP**: AI agent'ları (Claude/Cursor/Codex/OpenClaw) guard + RLS + maskeleme tool içinde zorunlu olarak veriyi sorgular. Modern white-label konsol (otomatik grafik — kod çalıştırmaz, başlangıç/devam soruları). **SAP & Canias dahil ERP bağlantıları** (SQL Server / Oracle / SAP HANA sürücüleri; önerilen yol salt-okunur replika). Tamamen yerel: Ollama/Gemma + BGE-M3/Qwen3 — **veri sunucudan çıkmaz.** Tek-komut on-prem + USB ile air-gapped paket. Belediye, fabrika ve regüle/egemen-veri kurumları için.
