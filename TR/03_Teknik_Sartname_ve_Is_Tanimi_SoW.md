# EK-B: TEKNİK ŞARTNAME VE İŞ TANIM BELGESİ (STATEMENT OF WORK - SoW)

**Sözleşme Referans No:** AB-NX-2026-SOW-001  
**Bağlı Olduğu Ana Sözleşme:** AB-NX-2026-MSA-001  
**Yürürlük Tarihi:** 01 Kasım 2026  

İşbu Teknik Şartname ve İş Tanım Belgesi ("**SoW**"), Atlas Bank T.A.Ş. ("**Banka**") ile NexaTech Finansal Yazılım A.Ş. ("**Tedarikçi**") arasında akdedilen Ana Sözleşme'nin ayrılmaz bir eki olup, **FinGuard AI** Platformu'nun teknik altyapı, fonksiyonel kapsam, entegrasyon mimarisi, teslim kilometre taşları ve kabul kriterlerini belirler.

---

## 1. PROJE KAPSAMI VE MİMARİ HEDEFLER

Projenin temel amacı; Banka'nın internet/mobil bankacılık, FAST, EFT, havale ve kredi kartı kanallarından geçen finansal işlemlerin anlık olarak sahtekarlık (fraud) riskine karşı taranması ve yeni kredi başvurularının yapay zekâ tabanlı kredi risk modelleri ile milisaniyeler düzeyinde skorlanarak temel bankacılık (Core Banking) sistemine iletilmesidir.

```
+---------------------------------------------------------------------------------+
|                                ATLAS BANK ALTYAPISI                             |
|  +--------------------+   +-------------------+   +--------------------------+  |
|  | Core Banking & EFT |   | Kredi Kartı Switch|   | Kredi Tahsis Servisleri  |  |
|  +---------+----------+   +---------+---------+   +------------+-------------+  |
|            |                        |                          |                |
|            +------------------------+--------------------------+                |
|                                     |                                           |
|                     +---------------+---------------+                           |
|                     | Banka Güvenli API Gateway     |                           |
|                     | (mTLS, HSM İmza, Token Doğr.) |                           |
+---------------------+---------------+---------------+---------------------------+
                                      |
       Yedekli Dedicated IPsec VPN / Dedicated Leased Line (Point-to-Point)
                                      |
+-------------------------------------v-------------------------------------------+
|               NEXATECH - FINGUARD AI BULUT ALTYAPISI (VPC)                      |
|                     (Türkiye İçi Tier-III Veri Merkezi)                         |
|                                                                                 |
|  +---------------------------------------------------------------------------+  |
|  | Ingress WAF & mTLS Sonlandırma Katmanı                                    |  |
|  +-------------------------------------+-------------------------------------+  |
|                                        |                                        |
|  +-------------------------------------v-------------------------------------+  |
|  | Mikroservis Katmanı (Kubernetes Cluster - Multi-AZ):                      |  |
|  |  [Gerçek Zamanlı Fraud]   [AI Kredi Skorlama]   [Kural Simülasyon Motoru] |  |
|  +-------------------------------------+-------------------------------------+  |
|                                        |                                        |
|  +-------------------------------------v-------------------------------------+  |
|  | Veri ve Önbellek Katmanı:                                                 |  |
|  |  [Redis Cluster (In-Memory)]  [Kafka Event Bus]  [PostgreSQL / TimeScale] |  |
|  +---------------------------------------------------------------------------+  |
+---------------------------------------------------------------------------------+
```

---

## 2. TEKNİK ALTYAPI VE GÜVENLİK MİMARİSİ

1. **Barındırma Ortamı (Dedicated Virtual Private Cloud):**
   * Platform, Banka'ya münhasır tahsis edilmiş (single-tenant dedicated VPC) kaynaklarda çalışacaktır. Banka verisi hiçbir şekilde diğer müşterilerin verileriyle aynı mantıksal veya fiziksel veritabanında paylaştırılmayacaktır (Multi-tenancy isolation).
   * Veri merkezleri İstanbul ve Ankara'da yerleşik, Tier-III sertifikalı, ISO 27001 ve PCI-DSS Level 1 onaylı olacaktır.
2. **Ağ Güvenliği ve İletişim:**
   * Banka Veri Merkezi ile Platform arasında çift yönlü yedekli (Active-Passive failover) en az 1 Gbps bant genişliğinde **IPsec VPN veya Noktadan Noktaya Kiralık Hat (Leased Line)** tesis edilecektir.
   * Tüm API trafiği zorunlu olarak **mTLS (Mutual TLS v1.3)** protokolü üzerinden iletilecek, zayıf şifreleme algoritmaları (cipher suite) engellenecektir.
3. **Veri Güvenliği ve Kriptografi:**
   * *Data-at-Rest:* Tüm diskler ve veritabanı tabloları donanımsal düzeyde **AES-256** ile şifrelenecektir.
   * *Data-in-Transit:* Uçtan uca TLS 1.3 şifrelemesi uygulanacaktır.
   * *Anahtar Yönetimi (KMS):* Kriptografik anahtarlar FIPS 140-2 Level 3 sertifikalı Donanımsal Güvenlik Modülü (HSM) üzerinde üretilecek ve saklanacaktır.

---

## 3. FONKSİYONEL GEREKSİNİMLER VE MODÜLLER

### Modül 1: Gerçek Zamanlı Sahtekarlık Tespit Motoru (Fraud Prevention)
* **Kural Motoru:** Banka analistlerinin GUI üzerinden sürükle-bırak yöntemiyle karmaşık kural mantıkları (örn: "Son 10 dakikada farklı coğrafi konumlardan toplam tutarı 50.000 TL'yi aşan 3 başarısız deneme sonrası para transferi") tanımlayabilmesi.
* **Makine Öğrenmesi (ML) Skorlama:** Gözetimli ve gözetimsiz (Unsupervised Anomaly Detection) modeller ile işlem risk skorunun 0-1000 arasında üretilmesi.
* **Karar Motoru Yanıt Süresi:** Gelen istek başına toplam değerlendirme ve yanıt üretme süresi $\le$ 80 ms (p99) olacaktır.

### Modül 2: Yapay Zekâ Kredi Tahsis ve Skorlama Motoru (Credit Risk)
* KKB (Kredi Kayıt Bürosu), MERNİS, SGK ve Banka içi hesap hareketleri verilerini birleştirerek borç ödeme olasılığını (PD - Probability of Default) hesaplama.
* Açıklanabilir Yapay Zekâ (XAI - SHAP/LIME değerleri) ile verilen kredi ret/onay kararının regülatif gerekçelendirmesini Banka ekranına sunma.

### Modül 3: Vaka Yönetimi ve Analist İnceleme Paneli (Case Management)
* Şüpheli olarak işaretlenen işlemlerin fraud analistlerinin önüne otomatik düşmesi, inceleme ve bloke koyma/kaldırma iş akışları.
* Kullanıcı bazlı detaylı işlem denetim izi (Audit Trail) tutulması; logların değiştirilemez biçimde (WORM depolama) 10 yıl saklanması.

### Modül 4: Gölge Mod (Shadow Mode) ve Geriye Dönük Test (Backtesting)
* Yeni oluşturulan yapay zekâ modellerinin ve kuralların canlı trafiği etkilemeksizin arka planda simüle edilmesi ve başarı metriklerinin kıyaslanması (Champion-Challenger modeli).

---

## 4. ENTEGRASYON VE API SPESİFİKASYONLARI

1. **İletişim Protokolleri:** REST (JSON over HTTPS) ve yüksek hacimli iç servisler için gRPC (Protocol Buffers).
2. **Kimlik Doğrulama:** OAuth 2.0 Mutual-TLS Client Credentials Grant ve HSM imzalı JWT (JSON Web Token).
3. **Dokümantasyon:** Tedarikçi, OpenAPI 3.0 (Swagger) spesifikasyonunu ve Postman entegrasyon koleksiyonlarını teslim edecektir.
4. **Olay Tabanlı Akış (Event Streaming):** Yüksek hacimli log ve analitik veri beslemeleri için Apache Kafka broker kümesi kurulacaktır.

---

## 5. PROJE KİLOMETRE TAŞLARI VE TESLİMAT PLANI

Proje süresi, Sözleşme imza tarihinden itibaren toplam **24 (yirmi dört) hafta** olarak planlanmıştır:

| No | Kilometre Taşı (Milestone) | Kapsam ve Çıktılar | Hedef Hafta | Kabul Şartı |
| :--- | :--- | :--- | :--- | :--- |
| **M1** | Analiz ve Mimari Onay | Sistem Mimarisi Tasarım Dokümanı (HLD/LLD), Güvenlik & BDDK Uyum Onayı | Hafta 1 - 4 | Banka Mimari Komitesi İmzalı Onayı |
| **M2** | Altyapı ve Ağ Entegrasyonu | Dedicated VPC Kurulumu, Yedekli IPsec VPN, mTLS, Test Ortamı Kurulumu | Hafta 5 - 8 | Ağ Bağlantı ve İletişim Test Raporu |
| **M3** | API ve Servis Entegrasyonu | Core Banking, KKB ve Kart Switch entegrasyonları, Mock veri testleri | Hafta 9 - 14 | Uçtan Uca Entegrasyon Test Raporu |
| **M4** | Gölge Mod & Model Eğitimi | Banka geçmiş anonim verisiyle model eğitimi, Canlı trafikte Shadow Test | Hafta 15 - 18 | Model Doğrulama Raporu (AUC > 0.92) |
| **M5** | UAT ve Güvenlik Testleri | Kullanıcı Kabul Testleri, Yük/Stres Testi, Bağımsız Sızma (Pentest) Testi | Hafta 19 - 22 | Sıfır Kritik/Yüksek Bulgu, UAT Tutanağı |
| **M6** | Canlıya Geçiş (Go-Live) | Aşamalı canlıya geçiş (%10 -> %50 -> %100 trafik yönlendirme), 7/24 Hiper-Bakım | Hafta 23 - 24 | Canlıya Geçiş Başarı Tutanağı |

---

## 6. KABUL TESTLERİ VE KRİTERLERİ (UAT PROTOKOLÜ)

1. **Fonksiyonel Kabul:** Ek-B'de belirtilen tüm fraud ve kredi kurallarının test senaryolarında %100 başarıyla sonuçlanması.
2. **Performans ve Stres Testi:** Sistemin kesintisiz **10.000 TPS** anlık yük altında p99 gecikmesinin 150 ms altında kaldığının ve hata oranının %0.01'i aşmadığının 4 saatlik stres testi ile kanıtlanması.
3. **Güvenlik Şartı:** Bağımsız akredite siber güvenlik firması tarafından gerçekleştirilecek sızma testinde (Pentest) hiçbir Kritik (Critical) veya Yüksek (High) seviyeli güvenlik açığının bulunmaması; tespit edilen orta seviye bulguların canlıya geçiş öncesinde kapatılması.
4. **Kabul Tutanağı:** Yukarıdaki koşullar sağlandığında Taraflar müştereken "Kullanıcı Kabul Testi (UAT) Onay Belgesi"ni tanzim eder.

---

## 7. MALİ ŞARTLAR VE ÖDEME PLANI

| Kalem No | Hizmet / Lisans Açıklaması | Tutar (TL / USD) | Ödeme Koşulu |
| :--- | :--- | :--- | :--- |
| **1** | Platform Kurulum, Entegrasyon ve Mimari Uyarlama | 4.500.000 TL | Kilometre taşlarına bağlı hakediş (M1 %20, M3 %30, M5 %30, M6 %20) |
| **2** | Yıllık Sabit FinGuard AI SaaS Lisans Bedeli | 7.200.000 TL / Yıl | Aylık eşit taksitlerle (600.000 TL/Ay), ay sonu tahakkuk |
| **3** | Hacim Bazlı Ek Kullanım (Aylık 15 Milyon işlem üzeri) | 0,012 TL / İşlem | Aylık fatura döneminde gerçekleşen sayaç verisi üzerinden |

---

| **ATLAS BANK T.A.Ş.** | **NEXATECH FİNANSAL YAZILIM A.Ş.** |
| :--- | :--- |
| **İmza:** ___________________________ | **İmza:** ___________________________ |
| **İsim:** Mehmet Yılmaz / CIO | **İsim:** Caner Özkan / CEO |
| **Tarih:** 01.11.2026 | **Tarih:** 01.11.2026 |
