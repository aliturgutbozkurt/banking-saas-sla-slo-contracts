# Banka & FinTech SaaS Sözleşme Paketi / Banking & FinTech SaaS Contract Suite

Bu proje deposu, bir **Mevduat/Katılım/Yatırım Bankası** ile bir **Yazılım Şirketi (SaaS Sağlayıcısı)** arasında akdedilebilecek kurumsal düzeyde (Enterprise-Grade), yasal ve teknik regülasyonlara (BDDK, TCMB, KVKK, GDPR, EBA, DORA) tam uyumlu örnek sözleşme paketini Türkçe ve İngilizce olarak içermektedir.

---

## 🏢 Örnek Proje Senaryosu (Case Study: FinGuard AI)

* **Müşteri (Banka):** Atlas Bank T.A.Ş. (Genel Müdürlük: İstanbul, Türkiye)
* **Tedarikçi (SaaS Sağlayıcı):** NexaTech Finansal Yazılım ve Yapay Zekâ Çözümleri A.Ş. / NexaTech Solutions Inc.
* **Proje Adı:** **FinGuard AI — Yeni Nesil Gerçek Zamanlı Sahtekarlık Tespit ve Kredi Risk Skorlama SaaS Platformu**
* **Sistem Mimarisi:** Banka içi Core Banking sistemleri ile güvenli API (mTLS, HSM imzalı token) üzerinden konuşan, yüksek erişilebilirlikli (High Availability), BDDK yerindelik/veri egemenliği kurallarına uygun hibrit/özel bulut (Dedicated Virtual Private Cloud) üzerinde barındırılan kurumsal SaaS mimarisi.

---

## 📂 Dizin Yapısı / Directory Structure

```text
SLA-SLO-Sözleşme/
├── README.md                                             # Proje genel rehberi ve fihrist
│
├── TR/                                                   # TÜRKÇE SÖZLEŞMELER VE EKLERİ
│   ├── 01_Ana_Hizmet_Sozlesmesi_MSA.md                   # Master Services Agreement (MSA)
│   ├── 02_Hizmet_Seviyesi_Taahhudu_SLA_SLO.md            # SLA, SLO, SLI ve Servis Kredisi Şartnamesi
│   ├── 03_Teknik_Sartname_ve_Is_Tanimi_SoW.md            # Statement of Work (SoW) & Fonksiyonel Şartname
│   ├── 04_Veri_Isleme_ve_Gizlilik_Sozlesmesi_DPA_KVKK.md # DPA, Bankacılık Sırrı ve KVKK Uyum Sözleşmesi
│   ├── 05_Bilgi_Guvenligi_ve_Siber_Dayaniklilik.md       # Bilgi Güvenliği, Pentest ve Denetim Hakları
│   └── 06_Is_Surekliligi_Escrow_ve_Cikis_Stratejisi.md   # BCP/DR, Escrow (Kaynak Kod Yediemini) & Exit Plan
│
└── EN/                                                   # ENGLISH CONTRACTS & SCHEDULES
    ├── 01_Master_Services_Agreement_MSA.md               # Master Cloud Services Agreement
    ├── 02_Service_Level_Agreement_SLA_SLO.md             # SLA, SLO, SLI & Service Credit Matrix
    ├── 03_Statement_of_Work_SoW_Technical_Specs.md       # Statement of Work & Technical Specifications
    ├── 04_Data_Processing_Agreement_DPA_GDPR.md          # Data Processing Agreement & Banking Secrecy
    ├── 05_Information_Security_and_Cyber_Resilience.md   # InfoSec, Pentests, DORA/Audits
    └── 06_Business_Continuity_Escrow_and_Exit_Strategy.md# BCP/DR, Source Code Escrow & Exit Strategy
```

---

## ⚖️ Sözleşmelerin Kapsamı ve Regülasyon Matrisi

| Sözleşme Adı | Hukuki / Teknik Odak | Referans Standart ve Mevzuat |
| :--- | :--- | :--- |
| **01. Ana Hizmet Sözleşmesi (MSA)** | Lisans, Fikri Mülkiyet, Süreç, Fesih, Sorumluluk Sınırları | Türk Borçlar Kanunu, TTK, US/UK Commercial Law |
| **02. SLA & SLO Şartnamesi** | Uptime (%99.95), MTTA/MTTR, Latency, Error Budget, Cezai Şart / Kredi | ITIL v4, SRE Best Practices, ISO 20000 |
| **03. Teknik Şartname & SoW** | API Gateway, mTLS, Veri Modelleri, Kabul Testleri (UAT), Sprint Planı | IEEE 830, REST/gRPC API Standards, Open Banking |
| **04. Veri İşleme Sözleşmesi (DPA)** | Veri İşleyen / Veri Sorumlusu, Bankacılık Sırrı (m.73), Sınır Ötesi Yasak | 6698 Sayılı KVKK, 5411 Sayılı Bankacılık Kanunu, GDPR |
| **05. Bilgi Güvenliği Şartnamesi** | Şifreleme, SOC2, Pentest, SIEM Entegrasyonu, BDDK Denetim Yetkisi | BDDK Bilgi Sistemleri Yönetmeliği, ISO 27001, DORA |
| **06. BCP, DR & Escrow** | RPO <= 15 dk, RTO <= 60 dk, Kaynak Kod Yediemini, Çıkış Planı | ISO 22301, NCC Group Escrow Standartları, EBA Outsourcing |

---

Bu paket hem şirket hukukçuları, hem regülasyon uyum direktörleri (Compliance Officers), hem de Kurumsal Mimarlar / CISO / CTO ekipleri için doğrudan üretim ve müzakereye uygun derinlikte hazırlanmıştır.
