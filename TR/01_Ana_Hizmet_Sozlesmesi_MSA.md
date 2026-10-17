# BULUT BİLİŞİM HİZMET VE LİSANS ANA SÖZLEŞMESİ (MSA)

**Sözleşme Referans No:** AB-NX-2026-MSA-001  
**Yürürlük Tarihi:** 01 Kasım 2026  

İşbu Bulut Bilişim Hizmet ve Lisans Ana Sözleşmesi ("**Sözleşme**" veya "**MSA**"), aşağıda belirtilen taraflar arasında yukarıda yazılı Yürürlük Tarihi itibarıyla akdedilmiştir.

---

## 1. TARAFLAR

1. **ATLAS BANK T.A.Ş.**  
   *Adres:* Büyükdere Cad. No: 180, Levent, Beşiktaş / İstanbul  
   *Mersis No:* 0123456789000014  
   *Vergi Dairesi & No:* Boğaziçi Kurumlar V.D. - 1234567890  
   *(Bundan böyle "**Banka**" veya "**Müşteri**" olarak anılacaktır).*

2. **NEXATECH FİNANSAL YAZILIM VE YAPAY ZEKÂ ÇÖZÜMLERİ A.Ş.**  
   *Adres:* ITU ARI Teknokent 3, No: 4/2, Maslak, Sarıyer / İstanbul  
   *Mersis No:* 0987654321000018  
   *Vergi Dairesi & No:* Maslak V.D. - 9876543210  
   *(Bundan böyle "**Tedarikçi**" veya "**SaaS Sağlayıcı**" olarak anılacaktır).*

Banka ve Tedarikçi münferiden "**Taraf**", müştereken "**Taraflar**" olarak anılacaktır.

---

## 2. TANIMLAR VE YORUMLAMA

* **"FinGuard AI" / "Platform" / "Yazılım":** Tedarikçi tarafından geliştirilen, gerçek zamanlı finansal sahtekarlık (fraud) tespiti, anomali izleme ve yapay zekâ destekli kredi risk skorlama kabiliyetlerine sahip Hizmet Olarak Yazılım (SaaS) platformunu ifade eder.
* **"Banka Verisi":** Banka'nın ve müşterilerinin Platform'a yüklediği, işlediği, aktardığı veya Platform kullanımı sırasında üretilen her türlü finansal veri, işlem kaydı, log, kişisel veri ve ticari sırları ifade eder.
* **"Bankacılık Sırrı":** 5411 sayılı Bankacılık Kanunu'nun 73. maddesi ve ilgili ikincil mevzuat uyarınca sır kapsamında kabul edilen her türlü müşteri sırrı ve banka sırrını ifade eder.
* **"BDDK":** Bankacılık Düzenleme ve Denetleme Kurumu'nu ifade eder.
* **"Mevzuat":** 5411 sayılı Bankacılık Kanunu, BDDK'nın Bankaların Bilgi Sistemleri ve Destek Hizmetleri Hakkında Yönetmeliği, 6698 sayılı Kişisel Verilerin Korunması Kanunu (KVKK), TCMB düzenlemeleri ve yürürlükteki tüm amir hükümleri ifade eder.
* **"Ekler":** İşbu Sözleşme'nin ayrılmaz parçası olan Hizmet Seviyesi Taahhüdü (SLA/SLO), İş Tanımı Belgesi (SoW), Veri İşleme Sözleşmesi (DPA), Bilgi Güvenliği Şartnamesi ve İş Sürekliliği/Escrow protokollerini ifade eder.

---

## 3. SÖZLEŞMENİN KONUSU VE AMACI

İşbu Sözleşme'nin konusu; Banka'nın risk analizi, dolandırıcılık önleme ve kredi değerlendirme süreçlerinde kullanılmak üzere, mülkiyeti Tedarikçi'ye ait olan FinGuard AI Platformu'nun, Banka'ya münhasır tahsis edilmiş Sanal Özel Bulut (Dedicated VPC) altyapısı üzerinden SaaS modeliyle sunulması, Banka'nın temel bankacılık (Core Banking) sistemleri ile entegrasyonu, bakım, destek ve danışmanlık hizmetlerinin ifasına ilişkin usul, esas, mali ve hukuki koşulların belirlenmesidir.

---

## 4. LİSANS MODELİ VE ERİŞİM HAKLARI

4.1. **Lisansın Niteliği:** Tedarikçi, Sözleşme süresince geçerli olmak üzere, Banka'ya ve Banka'nın doğrudan/dolaylı iştiraklerine, Platform'u ticari amaçları doğrultusunda kullanmaları için dünya çapında, inhisari olmayan (non-exclusive), devredilemez (işbu maddedeki istisnalar saklı kalmak kaydıyla) ve geri alınamaz bir SaaS erişim ve kullanım hakkı vermiştir.  
4.2. **Kullanıcı ve Hacim Kapsamı:** Banka, Ek-B (Teknik Şartname ve SoW) kapsamında belirlenen API çağrı kotaları, işlem hacimleri ve yetkili kullanıcı sayısı dahilinde Platform'a 7/24 erişim hakkına sahiptir.  
4.3. **Kaynak Kod ve Kısıtlamalar:** Banka, Sözleşme'de ve Escrow Protokolü'nde açıkça izin verilen haller haricinde, Platform'un kaynak kodlarını tersine mühendislik (reverse engineering) işlemine tabi tutamaz, Platform'u üçüncü taraflara kiraya veremez.

---

## 5. TARAFLARIN HAK VE YÜKÜMLÜLÜKLERİ

### 5.1. Tedarikçinin Yükümlülükleri:
a) Platform'u Ek-A'da (SLA/SLO) öngörülen yıllık en az %99.95 erişilebilirlik oranıyla kesintisiz, güvenli ve yüksek performansla çalıştırmak.  
b) Banka verilerini yalnızca Türkiye Cumhuriyeti sınırları içerisinde bulunan, BDDK standartlarına uygun Tier-III veya üstü sertifikalı veri merkezlerinde barındırmak; hiçbir koşulda veriyi yurt dışına çıkarmamak (Data Residency).  
c) Banka sistemleri ile entegrasyonu Ek-B'de (SoW) yer alan teknik spesifikasyonlara ve kilometre taşlarına uygun olarak tamamlamak.  
d) Bilgi güvenliği, sızma testleri, kod denetimleri ve siber güvenlik zafiyet kapatmalarını Ek-D hükümleri uyarınca gecikmeksizin gerçekleştirmek.

### 5.2. Bankanın Yükümlülükleri:
a) Hizmet bedellerini Sözleşme'nin 6. maddesinde kararlaştırılan takvim ve koşullarda ödemek.  
b) Entegrasyon süreçleri için gerekli test ortamlarını, API anahtarlarını ve teknik dokümantasyonu zamanında temin etmek.  
c) Platform erişim kimlik bilgilerini yetkisiz erişimlere karşı korumak ve güvenli iletişim protokollerini (mTLS, IP Whitelisting) uygulamak.

---

## 6. MALİ HÜKÜMLER, FATURALAMA VE ÖDEME

6.1. **Hizmet Bedeli:** Hizmet ve abonelik bedelleri, Ek-B'de (Fiyatlandırma ve Ödeme Planı) belirlenen aylık/yıllık sabit SaaS kullanım bedeli ve hacim bazlı API tarife tablosuna göre tahakkuk ettirilir.  
6.2. **Faturalama ve Vade:** Tedarikçi, her takvim ayının son iş gününde aylık hizmet faturasını tanzim eder. Faturaya ilgili ayın SLA raporu ve Hizmet Kredisi (Service Credit) kesintileri yansıtılır. Banka, usulüne uygun düzenlenen faturayı tebliğ aldığı tarihten itibaren **30 (otuz) takvim günü** içinde Tedarikçi'nin banka hesabına havale/EFT yoluyla öder.  
6.3. **Vergiler:** Aksi kararlaştırılmadıkça belirtilen tüm tutarlar KDV hariçtir. Yasal mevzuat gereği Banka tarafından yapılması gereken stopaj veya vergi kesintileri faturadan mahsup edilir.

---

## 7. FİKRİ VE SINAİ MÜLKİYET HAKLARI (IPR)

7.1. **Mevcut Fikri Mülkiyet (Background IP):** Tedarikçi'nin Platform'a, temel yapay zekâ algoritmalarına, yazılım mimarisine ve dokümantasyona ait tüm telif, patent, ticari sır ve fikri mülkiyet hakları münhasıran Tedarikçi'ye aittir.  
7.2. **Banka Verisi ve Çıktılar:** Banka Verisi'nin, Banka'ya ait iş kurallarının, Platform'un Banka verileriyle eğitilmesi sonucu oluşan bankaya özel makine öğrenmesi modellerinin ve üretilen analiz raporlarının tüm mülkiyeti kayıtsız şartsız Banka'ya aittir.  
7.3. **Fikri Mülkiyet İhlal Tazminatı (IP Indemnity):** Tedarikçi, Platform'un üçüncü kişilerin fikri mülkiyet haklarını ihlal etmediğini garanti eder. Üçüncü bir tarafça Banka aleyhine açılabilecek fikri mülkiyet ihlali davalarında, Banka'nın uğrayacağı tüm doğrudan ve dolaylı zararları, mahkeme masraflarını ve avukatlık ücretlerini Tedarikçi nakden ve defaten tazmin etmekle yükümlüdür.

---

## 8. REGÜLATİF UYUM VE DENETİM HAKLARI (AUDIT RIGHTS)

8.1. **BDDK ve Yetkili Kurum Denetimi:** 5411 sayılı Kanun ve ilgili mevzuat uyarınca; Tedarikçi, Banka'nın iç denetçilerine, bağımsız denetim kuruluşlarına ve başta BDDK ve TCMB olmak üzere yetkili düzenleyici ve denetleyici kurumlara; Platform'un barındırıldığı veri merkezlerinde, sistem altyapısında, kaynak kodlarında ve süreçlerinde **yerinde inceleme, denetim ve kopyalama yapma yetkisini** kayıtsız şartsız tanır.  
8.2. **Denetim İşbirliği:** Tedarikçi, talep edilen her türlü log, sistem mimarisi dokümanı, SOC 2 raporu ve güvenlik kanıtlarını en geç 3 (üç) iş günü içinde denetim ekiplerine sunmak zorundadır.

---

## 9. SORUMLULUK VE TAZMİNAT SINIRLARI

9.1. **Genel Sorumluluk Sınırı:** İşbu Sözleşme'den doğan genel tazminat taleplerinde her bir Taraf'ın sorumluluğu, olayın vuku bulduğu tarihten önceki son 12 (on iki) ayda Banka tarafından Tedarikçi'ye ödenen toplam sözleşme bedeli ile sınırlıdır.  
9.2. **Sorumluluk Sınırının İstisnaları (Limitsiz Sorumluluk):** Aşağıdaki hallerde sorumluluk sınırlaması uygulanmaz; kusurlu Taraf tüm doğrudan ve fer'i zararlardan sınırsız olarak sorumludur:  
a) 5411 sayılı Kanun m. 73 (Bankacılık Sırrı) ve Gizlilik hükümlerinin ihlali,  
b) 6698 sayılı KVKK ve veri güvenliği ihlalleri neticesinde oluşan zararlar ve idari para cezaları,  
c) Fikri mülkiyet ihlalleri ve 7.3 kapsamındaki tazminat yükümlülükleri,  
d) Ağır kusur, kasıt veya hileli davranışlar.

---

## 10. SÖZLEŞMENİN SÜRESİ VE FESİH

10.1. **Süre:** Sözleşme, Yürürlük Tarihi'nden itibaren **3 (üç) yıl** süreyle yürürlüktedir. Taraflardan biri süre bitiminden en az 60 (altmış) gün önce yazılı fesih ihbarında bulunmadığı takdirde birer yıllık dönemler halinde kendiliğinden uzar.  
10.2. **Haklı Nedenle Fesih:** Taraflardan birinin Sözleşme yükümlülüklerini esaslı şekilde ihlal etmesi ve yazılı ihtara rağmen 15 (on beş) takvim günü içinde ihlali gidermemesi halinde diğer Taraf Sözleşme'yi derhal ve tazminatsız feshedebilir.  
10.3. **Regülatif Zorunluluk Nedeniyle Fesih:** BDDK, TCMB veya mahkemelerin hizmetin durdurulmasını talep etmesi halinde Banka, hiçbir cezai şart ödemeksizin sözleşmeyi derhal feshetme hakkına sahiptir.  
10.4. **Sona Erme Sonrası Geçiş (Exit Assistance):** Sözleşme hangi nedenle sona ererse ersin, Tedarikçi Ek-F'de (Geçiş ve Çıkış Stratejisi) belirtilen şartlarla en az 6 (altı) ay boyunca Banka verilerini eksiksiz teslim etmeyi ve yeni sağlayıcıya geçiş desteği sağlamayı taahhüt eder.

---

## 11. UYUŞMAZLIKLARIN ÇÖZÜMÜ VE UYGULANACAK HUKUK

İşbu Sözleşme Türkiye Cumhuriyeti kanunlarına tabidir. Sözleşme'nin yorumundan ve uygulanmasından doğabilecek her türlü uyuşmazlığın çözümünde **İstanbul (Çağlayan) Mahkemeleri ve İcra Daireleri** münhasıran yetkilidir.

---

## 12. EKLER LİSTESİ

İşbu Sözleşme aşağıdaki ayrılmaz ekleri ile bir bütündür:
* **Ek-A:** Hizmet Seviyesi Taahhüdü ve Hedefleri (SLA & SLO Şartnamesi)
* **Ek-B:** Teknik Şartname, Fonksiyonel Kapsam ve İş Tanımı (SoW)
* **Ek-C:** Veri İşleme Sözleşmesi (DPA) ve Bankacılık Sırrı Taahhütnamesi
* **Ek-D:** Bilgi Güvenliği, Siber Dayanıklılık ve Denetim Şartnamesi
* **Ek-E:** İş Sürekliliği, Felaketten Kurtarma ve Kaynak Kod Yediemini (Escrow) Protokolü

---

İşbu Sözleşme, 2 (iki) asıl nüsha olarak tanzim edilmiş, yetkili temsilcilerce okunarak tam bir mutabakatla imza altına alınmıştır.

| **ATLAS BANK T.A.Ş.** (Müşteri) | **NEXATECH FİNANSAL YAZILIM A.Ş.** (Tedarikçi) |
| :--- | :--- |
| **İmza:** ___________________________ | **İmza:** ___________________________ |
| **İsim:** Mehmet Yılmaz | **İsim:** Caner Özkan |
| **Unvan:** Genel Müdür Yardımcısı (CIO) | **Unvan:** İcra Kurulu Başkanı (CEO) |
| **Tarih:** 01.11.2026 | **Tarih:** 01.11.2026 |
| **İmza:** ___________________________ | **İmza:** ___________________________ |
| **İsim:** Av. Zeynep Kaya | **İsim:** Av. Murat Erdem |
| **Unvan:** Hukuk Müşaviri / CCO | **Unvan:** Genel Hukuk Direktörü |
| **Tarih:** 01.11.2026 | **Tarih:** 01.11.2026 |
