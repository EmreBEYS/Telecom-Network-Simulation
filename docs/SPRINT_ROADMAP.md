# Telecom Network Simulation — Sprint Yol Haritası

## 1. Proje hedefi

Bu proje, bir telekom/kurumsal ağ altyapısının gereksinim analizinden başlayarak tasarlanmasını,
Cisco Packet Tracer üzerinde uygulanmasını, arıza ve güvenlik senaryolarıyla test edilmesini ve
teknik olarak raporlanmasını amaçlar.

Yol haritası; önce küçük ve doğrulanabilir LAN senaryoları kurar, ardından bunları yönlendirme,
servis, güvenlik, ses, yedeklilik ve izleme katmanlarıyla tek bir bütünleşik operatör senaryosuna
dönüştürür.

## 2. Teknik kapsam

- Cisco Packet Tracer topolojileri
- IPv4 subnetting ve adres planı
- VLAN, trunk, STP ve EtherChannel
- Inter-VLAN, statik ve dinamik routing
- OSPF
- DHCP, DNS, NAT/PAT ve NTP
- ACL ve ağ segmentasyonu
- WAN ve şube bağlantıları
- HSRP tabanlı gateway yedekliliği
- IP telefon ve VoIP temelleri
- QoS ve ses trafiği önceliklendirme
- IPv6 ve dual-stack
- SNMP, Syslog ve ağ görünürlüğü
- Arıza, güvenlik ve performans testleri
- Teknik rapor, demo ve yeniden üretilebilir yapılandırmalar

## 3. Önerilen depo yapısı

```text
Telecom-Network-Simulation/
├── README.md
├── docs/
│   ├── SPRINT_ROADMAP.md
│   ├── architecture/
│   ├── addressing/
│   ├── diagrams/
│   └── sprints/
├── topologies/
│   ├── sprint-00-01/
│   └── final/
├── configs/
│   ├── routers/
│   ├── switches/
│   ├── services/
│   └── security/
├── tests/
│   ├── connectivity/
│   ├── failure/
│   ├── security/
│   └── performance/
└── reports/
    ├── validation/
    └── final/
```

Packet Tracer dosyaları, dışarı aktarılan cihaz yapılandırmaları ve test kanıtları aynı sprint
klasörü altında birbirine bağlanmalıdır.

## 4. Sprint planı

### Sprint 00-00 — Gereksinimler ve Mimari Sözleşme

**Amaç:** Projenin kapsamını, kullanıcılarını ve teknik sınırlarını belirlemek.

**Görevler:**

- Merkez, şube, veri merkezi ve internet bağlantısı gereksinimlerini tanımlamak
- Tahmini kullanıcı, cihaz, telefon ve sunucu sayılarını belirlemek
- Başarı ölçütlerini ve kapsam dışı konuları yazmak
- Cihaz adlandırma, arayüz ve dokümantasyon standartlarını belirlemek
- Packet Tracer sürümünü sabitlemek
- Mantıksal ve fiziksel mimari taslağını hazırlamak

**Teslim:**

- Gereksinim belgesi
- Üst seviye mimari diyagram
- Cihaz envanteri
- Test ve tamamlanma ölçütleri

### Sprint 00-01 — Temel LAN ve IPv4 Adresleme

**Amaç:** İlk çalışan yerel ağı ve doğrulanmış adres planını oluşturmak.

**Görevler:**

- Bir router, iki switch ve istemci cihazlarını kurmak
- IPv4 ağlarını VLSM ile planlamak
- Cihaz yönetim adreslerini tanımlamak
- Temel switch/router güvenliğini yapılandırmak
- Ping ve ARP davranışını doğrulamak

**Teslim:**

- İlk `.pkt` topolojisi
- IPv4 adresleme tablosu
- Başlangıç cihaz yapılandırmaları
- Bağlantı test raporu

### Sprint 00-02 — VLAN ve Trunk Altyapısı

**Amaç:** Kullanıcı gruplarını mantıksal ağlara ayırmak.

**Görevler:**

- Yönetim, çalışan, misafir, sunucu ve ses VLAN’larını tanımlamak
- Access portlarını atamak
- 802.1Q trunk bağlantılarını kurmak
- Native VLAN ve kullanılmayan port politikasını belirlemek
- VLAN izolasyonunu test etmek

**Teslim:**

- VLAN planı
- Switch yapılandırmaları
- Trunk doğrulama çıktıları
- İzolasyon testleri

### Sprint 00-03 — Inter-VLAN Routing, STP ve EtherChannel

**Amaç:** VLAN’lar arası kontrollü iletişim ve Layer 2 dayanıklılığı sağlamak.

**Görevler:**

- Router-on-a-stick veya Layer 3 switch yaklaşımını uygulamak
- Rapid PVST yapılandırmak
- Root bridge rollerini belirlemek
- EtherChannel bağlantısı kurmak
- Link kesintisi ve STP yakınsamasını test etmek

**Teslim:**

- Inter-VLAN routing
- STP/EtherChannel yapılandırması
- Döngü ve link arızası test raporu

### Sprint 00-04 — WAN ve Statik Routing

**Amaç:** Merkez ve şube ağlarını WAN üzerinden bağlamak.

**Görevler:**

- Merkez–şube topolojisini oluşturmak
- Noktadan noktaya WAN adreslerini planlamak
- Statik ve varsayılan rotaları tanımlamak
- Ulaşılmaz rota ve hatalı gateway senaryolarını test etmek

**Teslim:**

- Çok lokasyonlu Packet Tracer topolojisi
- Routing tablosu kanıtları
- Merkez–şube bağlantı raporu

### Sprint 00-05 — OSPF Dinamik Routing

**Amaç:** Ölçeklenebilir ve otomatik yakınsayan yönlendirme altyapısı kurmak.

**Görevler:**

- Tek alanlı OSPF ile başlamak
- Router ID ve passive-interface politikasını belirlemek
- Varsayılan rota dağıtımı yapmak
- Metrik ve yol seçimini doğrulamak
- Bağlantı kesintisinde yakınsamayı ölçmek

**Teslim:**

- OSPF yapılandırmaları
- Komşuluk ve LSDB doğrulaması
- Failover/yakınsama test raporu

### Sprint 00-06 — DHCP, DNS, NAT/PAT ve NTP

**Amaç:** Temel ağ servislerini merkezi ve tekrar üretilebilir hâle getirmek.

**Görevler:**

- VLAN bazlı DHCP havuzları oluşturmak
- DHCP relay uygulamak
- İç DNS kayıtlarını tanımlamak
- İnternet çıkışı için NAT/PAT yapılandırmak
- Cihaz saatlerini NTP ile eşitlemek
- Hatalı servis ve adres çakışması senaryolarını test etmek

**Teslim:**

- Servis topolojisi
- DHCP/DNS/NAT/NTP yapılandırmaları
- İstemci servis testleri

### Sprint 00-07 — ACL ve Ağ Segmentasyonu

**Amaç:** Ağlar arası erişimi en az ayrıcalık ilkesiyle sınırlandırmak.

**Görevler:**

- Standart ve extended ACL uygulamak
- Misafir ağının iç kaynaklara erişimini engellemek
- Yönetim VLAN’ına yalnız yetkili erişim sağlamak
- Sunucu servislerini port bazında sınırlandırmak
- İzin verilen ve reddedilen trafik matrisini test etmek

**Teslim:**

- Erişim kontrol matrisi
- ACL yapılandırmaları
- Pozitif ve negatif güvenlik testleri

### Sprint 00-08 — Gateway ve Bağlantı Yedekliliği

**Amaç:** Tek hata noktalarını azaltmak.

**Görevler:**

- Çift dağıtım cihazı tasarlamak
- HSRP ile sanal varsayılan gateway kurmak
- Yedek bağlantıları STP/EtherChannel ile bütünleştirmek
- Aktif cihaz ve uplink kesintilerini test etmek
- Kesinti ve toparlanma sürelerini kaydetmek

**Teslim:**

- Yedekli kampüs topolojisi
- HSRP yapılandırması
- Failover raporu

### Sprint 00-09 — IP Telefon ve VoIP Temelleri

**Amaç:** Veri ağına temel ses iletişimi eklemek.

**Görevler:**

- Voice VLAN oluşturmak
- IP telefon ve uç cihaz bağlantılarını kurmak
- Dahili numara planı hazırlamak
- Packet Tracer’ın desteklediği Call Manager Express/telephony-service yapısını uygulamak
- Telefon kayıt ve dahili arama testleri yapmak

**Teslim:**

- VoIP topolojisi
- Numara planı
- Telefon kayıt ve çağrı testleri

### Sprint 00-10 — QoS ve Ses Trafiği Önceliklendirme

**Amaç:** Ses trafiğinin gecikme ve kayıp karşısındaki davranışını iyileştirmek.

**Görevler:**

- Ses ve veri trafiğini sınıflandırmak
- DSCP/CoS işaretleme politikasını belgelemek
- Güven sınırlarını belirlemek
- Yoğun trafik altında ses önceliğini doğrulamak
- Packet Tracer sınırlamalarını açıkça raporlamak

**Teslim:**

- QoS politikası
- Önceliklendirme yapılandırmaları
- Normal/yüksek yük karşılaştırması

### Sprint 00-11 — IPv6 ve Dual-Stack

**Amaç:** Mevcut yapıyı IPv6’ya hazırlamak.

**Görevler:**

- IPv6 adres planı oluşturmak
- Dual-stack istemci ve router yapılandırmak
- SLAAC ve DHCPv6 davranışlarını incelemek
- OSPFv3 veya desteklenen IPv6 routing yöntemini uygulamak
- IPv4 ve IPv6 erişimini ayrı ayrı test etmek

**Teslim:**

- IPv6 adresleme planı
- Dual-stack topoloji
- IPv6 bağlantı testleri

### Sprint 00-12 — Güvenli Yönetim ve Cihaz Sertleştirme

**Amaç:** Ağ cihazlarının yönetim yüzeyini korumak.

**Görevler:**

- SSH yönetimi ve yerel kullanıcı hesapları oluşturmak
- Telnet’i devre dışı bırakmak
- Port security uygulamak
- Kullanılmayan portları kapatmak
- Banner, parola ve oturum zaman aşımı politikalarını eklemek
- Yetkisiz yönetim erişimini test etmek

**Teslim:**

- Güvenli cihaz şablonları
- Sertleştirme kontrol listesi
- Yönetim erişim testleri

### Sprint 00-13 — İzleme, Syslog ve SNMP

**Amaç:** Ağın durumunu merkezi olarak gözlemlemek.

**Görevler:**

- Syslog sunucusu kurmak
- SNMP tabanlı temel izleme yapılandırmak
- NTP ile log zamanlarını eşitlemek
- Arayüz, routing ve güvenlik olaylarını toplamak
- Kritik olaylar için izleme senaryoları yazmak

**Teslim:**

- İzleme topolojisi
- Syslog/SNMP yapılandırmaları
- Olay ve alarm doğrulama raporu

### Sprint 00-14 — Şube Güvenliği ve VPN Senaryosu

**Amaç:** Şubeler arası trafiği güvenli bir taşıma senaryosuyla modellemek.

**Görevler:**

- Packet Tracer desteğine göre site-to-site VPN veya güvenli tünel senaryosu kurmak
- İlgi alanı trafiğini tanımlamak
- Tünel öncesi ve sonrası erişimi karşılaştırmak
- Anahtar/kimlik bilgilerini örnek değerlerle belgelemek
- Tünel kesintisi ve yanlış politika senaryolarını test etmek

**Teslim:**

- Güvenli şube bağlantısı
- VPN/tünel yapılandırmaları
- Güvenlik doğrulama raporu

### Sprint 00-15 — Arıza ve Troubleshooting Laboratuvarı

**Amaç:** Bilinçli hatalar üzerinden sistematik sorun giderme pratiği oluşturmak.

**Görevler:**

- Yanlış VLAN, trunk, subnet mask, gateway, ACL ve OSPF hataları üretmek
- Katman bazlı troubleshooting akışı uygulamak
- `show` komutlarıyla kanıt toplamak
- Kök neden ve çözüm sürelerini kaydetmek
- Her hata için tekrar kullanılabilir test kartı oluşturmak

**Teslim:**

- En az 10 arıza senaryosu
- Troubleshooting karar ağacı
- Kök neden ve çözüm raporu

### Sprint 00-16 — Performans ve Kapasite Değerlendirmesi

**Amaç:** Tasarımın kapasite sınırlarını ve darboğazlarını değerlendirmek.

**Görevler:**

- Gecikme, paket kaybı ve yakınsama ölçütlerini belirlemek
- Normal yük ve arıza durumlarını karşılaştırmak
- Broadcast domain ve IP kapasitesini değerlendirmek
- Kritik bağlantı ve cihazları belirlemek
- Packet Tracer sonuçlarının gerçek ağla farklarını belgelemek

**Teslim:**

- Performans test matrisi
- Kapasite ve darboğaz raporu
- İyileştirme önerileri

### Sprint 00-17 — Final Entegrasyon, Demo ve Rapor

**Amaç:** Tüm modülleri tek bir tutarlı telekom ağı senaryosunda birleştirmek.

**Görevler:**

- Merkez, şube, sunucu, misafir, yönetim ve ses ağlarını birleştirmek
- Adres, VLAN, routing ve güvenlik çakışmalarını gidermek
- Baştan sona kabul testlerini çalıştırmak
- Cihaz yapılandırmalarını dışarı aktarmak
- Mimari, test ve sınırlama raporlarını tamamlamak
- Demo akışını ve sunumu hazırlamak

**Teslim:**

- Final `.pkt` topolojisi
- Tam cihaz yapılandırma arşivi
- Kabul test raporu
- Teknik proje raporu
- Demo senaryosu ve sunum

## 5. Sprint bağımlılık sırası

```text
Gereksinimler
    ↓
LAN ve adresleme
    ↓
VLAN / trunk
    ↓
Inter-VLAN / STP / EtherChannel
    ↓
WAN ve OSPF
    ↓
Ağ servisleri
    ↓
Güvenlik ve yedeklilik
    ↓
VoIP / QoS / IPv6
    ↓
İzleme ve güvenli şube
    ↓
Arıza / performans testleri
    ↓
Final entegrasyon
```

## 6. Her sprint için tamamlanma ölçütleri

Bir sprint ancak aşağıdaki koşullar karşılandığında tamamlanmış sayılır:

1. Topoloji dosyası açılıyor ve bozuk değil.
2. Adres ve cihaz isimleri belgelenmiş durumda.
3. Cihaz yapılandırmaları dışarı aktarılmış.
4. En az bir olumlu test başarılı.
5. En az bir hata/olumsuz test uygulanmış.
6. Beklenen ve gerçekleşen sonuçlar karşılaştırılmış.
7. Ekran görüntüsü yerine mümkün olduğunda komut çıktısı ve yapılandırma kanıtı saklanmış.
8. Packet Tracer sınırlamaları belirtilmiş.
9. README veya sprint belgesi güncellenmiş.
10. Değişiklikler ayrı Git dalı ve inceleme akışıyla hazırlanmış.

## 7. Proje genel başarı ölçütleri

- Tüm kullanıcı VLAN’ları doğru adres alabilmeli.
- Yetkili ağlar birbirine ulaşırken yasaklı trafik engellenmeli.
- Merkez–şube routing’i bir bağlantı arızasından sonra toparlanmalı.
- DNS, DHCP, NAT ve NTP servisleri doğrulanmalı.
- IP telefonlar kayıt olmalı ve dahili arama yapabilmeli.
- Yönetim erişimi yalnız güvenli ve yetkili ağdan sağlanmalı.
- Log ve izleme kanıtları merkezi olarak görülebilmeli.
- Final topoloji temiz başlangıçtan yeniden üretilebilmeli.
- Tüm test sonuçları teknik raporda izlenebilir olmalı.

## 8. Kapsam dışı

İlk sürüm için aşağıdaki konular kapsam dışında tutulabilir:

- Gerçek operatör çekirdek ağı
- MPLS ve BGP’nin ileri seviye üretim tasarımları
- 4G/5G RAN ve EPC/5GC emülasyonu
- Gerçek donanım performans garantileri
- Üretim ortamında kullanılacak gerçek parolalar ve anahtarlar
- Packet Tracer’ın desteklemediği ayrıntılı QoS/VPN/telemetri özellikleri

Bu alanlar proje tamamlandıktan sonra V2 yol haritası olarak ele alınabilir.
