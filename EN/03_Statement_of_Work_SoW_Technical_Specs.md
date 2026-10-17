# SCHEDULE B: STATEMENT OF WORK & TECHNICAL SPECIFICATIONS (SoW)

**Schedule Reference:** AB-NX-2026-SOW-001  
**Associated Agreement:** AB-NX-2026-MSA-001  
**Effective Date:** November 01, 2026  

This Statement of Work and Technical Specifications ("**SoW**") is entered into by and between Atlas Bank T.A.Ş. ("**Bank**") and NexaTech Solutions Inc. ("**Vendor**") pursuant to the Master Services Agreement to define the technical architecture, functional requirements, integration protocols, deployment milestones, and acceptance testing criteria for the **FinGuard AI** Platform.

---

## 1. PROJECT OBJECTIVE AND ARCHITECTURAL SCOPE

The primary objective of this deployment is to integrate the FinGuard AI Platform with the Bank's Core Banking, credit card processing switch, and instant payment rails (FAST/EFT) to deliver millisecond-level automated fraud evaluation and AI-driven credit risk underwriting.

```
+---------------------------------------------------------------------------------+
|                                ATLAS BANK ENTERPRISE LAN                        |
|  +--------------------+   +-------------------+   +--------------------------+  |
|  | Core Banking & EFT |   | Card Payment Switch|  | Loan Origination Engine  |  |
|  +---------+----------+   +---------+---------+   +------------+-------------+  |
|            |                        |                          |                |
|            +------------------------+--------------------------+                |
|                                     |                                           |
|                     +---------------+---------------+                           |
|                     | Bank Secure API Gateway       |                           |
|                     | (mTLS, HSM Signature, JWT)    |                           |
+---------------------+---------------+---------------+---------------------------+
                                      |
         Redundant Dedicated IPsec VPN / Point-to-Point 1 Gbps Fiber
                                      |
+-------------------------------------v-------------------------------------------+
|              NEXATECH - FINGUARD AI DEDICATED SOVEREIGN VPC                     |
|                 (Tier-III In-Country Sovereign Data Center)                     |
|                                                                                 |
|  +---------------------------------------------------------------------------+  |
|  | Ingress WAF & Dual-Terminating mTLS Layer                                 |  |
|  +-------------------------------------+-------------------------------------+  |
|                                        |                                        |
|  +-------------------------------------v-------------------------------------+  |
|  | Microservices Tier (Multi-AZ Kubernetes Cluster):                         |  |
|  |  [Real-Time Fraud Engine]  [AI Credit Risk Engine]  [Simulation & Backtest]|  |
|  +-------------------------------------+-------------------------------------+  |
|                                        |                                        |
|  +-------------------------------------v-------------------------------------+  |
|  | High-Performance Persistence Layer:                                       |  |
|  |  [Redis Cluster (In-Memory)]  [Kafka Event Bus]  [PostgreSQL / TimeScale] |  |
|  +---------------------------------------------------------------------------+  |
+---------------------------------------------------------------------------------+
```

---

## 2. INFRASTRUCTURE AND SECURITY ARCHITECTURE

1. **Dedicated Hosting Environment (Single-Tenant VPC):**
   * The Platform shall run on dedicated bare-metal or single-tenant virtualized resources within a private Virtual Private Cloud (VPC). Multi-tenant database sharing or co-mingling of the Bank's data with other clients is strictly prohibited.
   * Hosting facilities must be certified Tier-III, ISO 27001, and PCI-DSS Level 1, located in Istanbul (Primary) and Ankara (Disaster Recovery).
2. **Network Connectivity & Encryption:**
   * A redundant, active-passive **1 Gbps IPsec VPN tunnel or dedicated leased line** shall connect the Bank's on-premise gateway to the Platform VPC.
   * All API communication must mandate **Mutual TLS (mTLS v1.3)** with PFS (Perfect Forward Secrecy) cipher suites.
3. **Cryptographic Standards:**
   * *Data at Rest:* AES-256 hardware-accelerated volume and database-level encryption.
   * *Data in Transit:* End-to-end TLS 1.3 encryption across all internal and ingress networks.
   * *Key Management:* Cryptographic keys generated, rotated, and secured within FIPS 140-2 Level 3 certified Hardware Security Modules (HSM).

---

## 3. FUNCTIONAL MODULES AND SPECIFICATIONS

### Module 1: Real-Time Fraud Detection Engine
* **Dynamic Rule Engine:** Enables Bank analysts to configure and publish real-time deterministic fraud rules via a web GUI (e.g., velocity checks, geographic impossibility, card-not-present cross-channel anomalies).
* **Machine Learning Scoring:** Pre-trained and fine-tuned supervised/unsupervised anomaly detection models producing risk scores (0–1000) within $\le$ 80 ms (p99).

### Module 2: AI Credit Decisioning and Risk Underwriting
* Integrates with Credit Bureau (KKB), National Identity Registry (MERNIS), and internal transactional history to compute Probability of Default (PD) and Loss Given Default (LGD).
* **Explainable AI (XAI):** Generates SHAP/LIME contribution vectors for every credit decision to satisfy regulatory compliance requirements for algorithmic transparency.

### Module 3: Case Management and Operations Console
* Automated queuing of flagged transactions for analyst inspection, featuring freeze/unfreeze action buttons and customer notification triggers.
* Tamper-evident Audit Trail recording all user interactions, immutable and retained for 10 years.

### Module 4: Shadow Simulation and Backtesting
* Provides side-by-side (Champion-Challenger) execution where new candidate models run against live production traffic without influencing actual transaction decisions.

---

## 4. INTEGRATION INTERFACES AND DATA CONTRACTS

1. **API Protocols:** Synchronous RESTful APIs (OpenAPI 3.0 / JSON) and high-throughput gRPC (Protobuf).
2. **Authentication:** OAuth 2.0 Client Credentials Grant with Mutual-TLS and HSM-backed token verification.
3. **Event Streaming:** Managed Apache Kafka cluster for asynchronous streaming of transaction logs and telemetry.

---

## 5. PROJECT TIMELINE AND MILESTONES

The end-to-end delivery timeline spans **twenty-four (24) weeks** from the Effective Date:

| Milestone | Deliverables and Scope | Target Week | Sign-Off Criteria |
| :--- | :--- | :--- | :--- |
| **M1: Architecture & Compliance** | High-Level Design (HLD), Low-Level Design (LLD), Security & BRSA Compliance Dossier | Weeks 1 — 4 | Bank Architecture Review Board Sign-Off |
| **M2: VPC & Network Connectivity**| Dedicated VPC provisioning, redundant IPsec VPN, mTLS certificates, staging environment | Weeks 5 — 8 | Network connectivity & latency test pass |
| **M3: API & Service Integration** | Core Banking, Card Switch, and KKB connector development; mock testing | Weeks 9 — 14 | End-to-end integration test report approval |
| **M4: Model Training & Shadow Run**| Historical data training, synthetic testing, live Shadow Mode deployment | Weeks 15 — 18 | Model validation report (AUC $\ge$ 0.92) |
| **M5: UAT & Security Audit** | Business user acceptance, 10k TPS load testing, independent grey-box pentest | Weeks 19 — 22 | Zero Critical/High vulnerabilities; UAT Certificate |
| **M6: Production Cutover (Go-Live)**| Phased production traffic routing (10% $\to$ 50% $\to$ 100%), 24/7 hyper-care | Weeks 23 — 24 | Final Production Acceptance Certificate |

---

## 6. ACCEPTANCE TESTING PROTOCOL (UAT)

1. **Functional Criteria:** 100% of defined fraud rules and credit scoring logic pass automated regression test suites.
2. **Performance Stress Test:** System sustains a continuous load of **10,000 TPS** for four (4) hours while maintaining p99 latency under 150 ms and error rate below 0.01%.
3. **Cybersecurity Sign-Off:** An independent CREST/TSE certified penetration testing firm verifies **zero Critical or High severity findings**, and all Medium findings have an approved remediation roadmap.
4. **Execution of Acceptance Certificate:** Upon satisfying all criteria, both Parties shall execute the formal User Acceptance Testing (UAT) Sign-Off Document.

---

## 7. FINANCIAL SCHEDULE AND PAYMENT TERMS

| Item | Scope Description | Fee (USD / Equivalent TRY) | Payment Milestone |
| :--- | :--- | :--- | :--- |
| **1** | Architecture, Setup, and Custom Core Banking Integration | $150,000 USD | Milestone-based (M1: 20%, M3: 30%, M5: 30%, M6: 20%) |
| **2** | Annual FinGuard AI SaaS Subscription Base Fee | $240,000 USD / Year | Payable in monthly installments ($20,000/month) |
| **3** | Volume Overage Fee (Exceeding 15M transactions/month) | $0.0004 USD / Call | Invoiced monthly in arrears based on verified telemetry |

---

| **ATLAS BANK T.A.Ş.** | **NEXATECH SOLUTIONS INC.** |
| :--- | :--- |
| **Signature:** ___________________________ | **Signature:** ___________________________ |
| **Name:** Mehmet Yılmaz / CIO | **Name:** Caner Özkan / CEO |
| **Date:** November 01, 2026 | **Date:** November 01, 2026 |
