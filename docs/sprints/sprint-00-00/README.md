# Sprint 00-00 — Gereksinimler ve Mimari Sözleşme

## Sprint bilgileri

- Tarih: 23 Kasım 2026
- Durum: Tamamlandı
- Aşama: Temel
- Sonraki sprint: 00-01 — Temel LAN ve IPv4 Adresleme
- Simülasyon aracı: Cisco Packet Tracer 9.0.x
- Yazarak kaydetme politikası: İlk PKT dosyası oluşturulurken kullanılan tam patch sürümü bu belgeye eklenecek

## 1. Amaç

Bu sprint, Telecom Network Simulation projesinin davranış değiştirmeyen planlama temelidir.
Merkez ve iki şubeli örnek telekom/kurumsal ağın kapsamını, kapasite varsayımlarını, güvenlik
bölgelerini, cihaz rollerini, adres alanlarını, adlandırma kurallarını ve kabul ölçütlerini sabitler.

Bu sayılar gerçek bir müşteriyi temsil etmez. Simülasyon başlangıç kapasitesidir ve ölçümle
değiştirilebilir. Packet Tracer dosyasında her kullanıcıyı tek tek oluşturmak yerine temsilî uç
cihazlar kullanılacak; subnet kapasitesi ise aşağıdaki toplamları karşılayacaktır.

## 2. Senaryo

### Merkez — HQ

- 120 çalışan
- 24 IP telefon
- 30 eşzamanlı misafir cihazı
- 8 sunucu veya ağ servisi
- 10 yönetim/uplink adresi
- İnternet çıkışı ve iki şubeye WAN bağlantısı
- Nihai yapıda çift dağıtım cihazı ve gateway yedekliliği

### Şube A — BRA

- 40 çalışan
- 10 IP telefon
- 10 misafir cihazı
- 5 yönetim/uplink adresi
- Merkez üzerinden ortak servislere ve kontrollü internet erişimine bağlantı

### Şube B — BRB

- 25 çalışan
- 8 IP telefon
- 8 misafir cihazı
- 5 yönetim/uplink adresi
- Merkez üzerinden ortak servislere ve kontrollü internet erişimine bağlantı

### Simülasyon yoğunluğu

Her kullanıcı grubunda başlangıçta 2–3 temsilî istemci bulunur. Adres planı gerçek planlanan
kapasiteye göre boyutlandırılır. Böylece topoloji okunabilir kalırken subnet, routing, güvenlik ve
servis davranışları doğrulanabilir.

## 3. İş gereksinimleri

| Kimlik | Gereksinim | Öncelik |
|---|---|---|
| BR-01 | Merkez ve şubeler birbirine yönlendirilmiş bağlantı kurabilmeli | Zorunlu |
| BR-02 | Çalışan, ses, misafir, sunucu ve yönetim trafiği ayrılmalı | Zorunlu |
| BR-03 | Misafir ağı kurum içi kaynaklara erişememeli | Zorunlu |
| BR-04 | Çalışanlar yalnız izin verilen ortak servislere erişebilmeli | Zorunlu |
| BR-05 | IP telefonlar kayıt olabilmeli ve dahili arama yapabilmeli | Zorunlu |
| BR-06 | Kritik bağlantı veya gateway arızasında ağ toparlanabilmeli | Yüksek |
| BR-07 | Ağ olayları merkezi olarak izlenebilmeli | Yüksek |
| BR-08 | Topoloji ve cihaz ayarları yeniden üretilebilir olmalı | Zorunlu |
| BR-09 | Hatalı yapılandırmalar için troubleshooting senaryoları bulunmalı | Yüksek |
| BR-10 | Tüm iddialar test kanıtına bağlanmalı | Zorunlu |

## 4. Teknik gereksinimler

| Kimlik | Gereksinim |
|---|---|
| TR-01 | IPv4 adresleme VLSM veya belgelenmiş sabit subnetlerle çakışmasız olmalı |
| TR-02 | VLAN kimlikleri tüm lokasyonlarda aynı işlevi ifade etmeli |
| TR-03 | Switch uplinkleri 802.1Q trunk kullanmalı |
| TR-04 | Dinamik routing aşamasında OSPF kullanılmalı |
| TR-05 | İstemci adresleri DHCP, altyapı adresleri statik olmalı |
| TR-06 | Merkez internet çıkışında NAT/PAT uygulanmalı |
| TR-07 | Yönetim trafiği ayrı VLAN ve ACL ile sınırlandırılmalı |
| TR-08 | Telnet yerine SSH hedeflenmeli |
| TR-09 | Voice VLAN ve veri VLAN’ı ayrılmalı |
| TR-10 | IPv6 aşamasında dokümantasyon prefixi 2001:db8::/32 kullanılmalı |
| TR-11 | Syslog, SNMP ve NTP merkezi servislerle bütünleşmeli |
| TR-12 | Cihaz konfigürasyonları metin olarak dışarı aktarılmalı |

## 5. VLAN sözleşmesi

| VLAN | Ad | İşlev |
|---:|---|---|
| 10 | MGMT | Router, switch ve yönetim arayüzleri |
| 20 | STAFF | Çalışan istemcileri |
| 30 | VOICE | IP telefonlar |
| 40 | SERVER | Merkez sunucu ve servisleri |
| 50 | GUEST | İzole misafir istemcileri |
| 60 | NET-SVC | DHCP, DNS, NTP, Syslog ve SNMP servisleri |
| 999 | NATIVE-BLACKHOLE | Kullanıcı taşımayan native/kapalı VLAN |

VLAN 40 ve 60 merkezde bulunur. Şubeler bu servislere routing ve ACL politikaları üzerinden
erişir. VLAN 999 üzerinde kullanıcı portu veya yönetim SVI’sı oluşturulmaz.

## 6. Adresleme özeti

- HQ site bloğu: 10.10.0.0/16
- Şube A site bloğu: 10.20.0.0/16
- Şube B site bloğu: 10.30.0.0/16
- WAN transit bloğu: 10.255.0.0/24
- Loopback ve router kimliği bloğu: 10.254.0.0/24
- IPv6 dokümantasyon bloğu: 2001:db8::/32

Ayrıntılı ve çakışmasız ilk plan docs/addressing/initial-addressing-plan.csv dosyasındadır.
Gateway için her subnetin ilk kullanılabilir adresi ayrılır. DHCP havuzları altyapı, gateway ve
sunucu adreslerini hariç tutar.

## 7. Adlandırma standardı

Biçim: SITE-ROLE-NN

Örnekler:

- HQ-RTR-01
- HQ-DSW-01
- HQ-ASW-01
- BRA-RTR-01
- BRB-ASW-01
- HQ-SRV-DNS-01
- HQ-PC-STAFF-01
- BRA-PHONE-01

Site kodları: HQ, BRA, BRB ve ISP.
Rol kodları: RTR, DSW, ASW, SRV, PC, PHONE ve AP.

Arayüz açıklaması karşı uç ve amaç içermelidir. Örnek: TO-HQ-DSW-01_TRUNK.

## 8. Güvenlik bölgeleri ve temel politika

- MGMT: yalnız yönetici istemcileri ve gerekli izleme servisleri
- STAFF: iç servisler ve internet; yönetim arayüzlerine doğrudan erişim yok
- VOICE: çağrı kontrolü, DHCP/TFTP ve gerekli ses trafiği
- SERVER/NET-SVC: yalnız belgelenmiş portlar
- GUEST: yalnız internet; RFC1918 iç ağlarına erişim yok
- WAN: yalnız routing, VPN ve açıkça izin verilen transit trafik

Gerçek parola, özel anahtar, müşteri IP’si veya kurum yapılandırması GitHub’a yazılmaz. Örnek
değerler açıkça SAMPLE veya CHANGE_ME biçiminde işaretlenir.

## 9. Fonksiyonel olmayan gereksinimler

- Topoloji yeni bir kullanıcı tarafından belgelerle yeniden kurulabilmeli.
- Her sprintte en az bir olumlu ve bir olumsuz test bulunmalı.
- Yapılandırma isimleri ve adresleri belgelerle tutarlı olmalı.
- Kritik link arızalarında beklenen toparlanma süresi raporlanmalı.
- Packet Tracer’ın desteklemediği davranışlar gerçek ağ sonucu gibi sunulmamalı.
- Her PKT dosyası kullanılan Packet Tracer sürümüyle birlikte belgelenmeli.
- Sonuçlar eğitim/simülasyon amaçlı olmalı; üretim garantisi vermemeli.

## 10. Packet Tracer sürüm kararı

Proje Cisco Packet Tracer 9.0 ailesini hedefler. Sprint 00-01’de ilk PKT dosyası oluşturulmadan
önce ekipte kullanılan tam sürüm (örneğin 9.0.0 veya 9.0.1), işletim sistemi ve dosyanın yeniden
açılma sonucu kaydedilir. Farklı patch sürümleri kullanılıyorsa en eski ortak sürüm yazma sürümü
olarak seçilir.

Cisco, Packet Tracer’ı Windows, Linux ve macOS için Networking Academy Resource Hub üzerinden
dağıtır. Eski bir sürüm yalnız uyumluluk sorunu kanıtlanırsa ve istisna belgelenirse kullanılır.

## 11. Riskler

| Risk | Etki | Önlem |
|---|---|---|
| Packet Tracer özellik sınırlaması | Orta | Desteklenmeyen davranışı belgelemek ve sadeleştirmek |
| Sürüm uyumsuzluğu | Yüksek | Yazma sürümünü sabitlemek ve temiz açılış testi yapmak |
| Topolojinin gereksiz büyümesi | Orta | Temsilî istemciler ve modüler sprint dosyaları kullanmak |
| Adres/VLAN çakışması | Yüksek | CSV planını tek kaynak kabul etmek ve inceleme yapmak |
| Güvenlik kuralının routing’i bozması | Yüksek | ACL öncesi/sonrası pozitif ve negatif testler |
| Tek hata noktaları | Orta | Sprint 00-08’de yedeklilik ve failover testi |
| Gerçekçi olmayan performans iddiası | Yüksek | Sonuçları simülasyon sınırlarıyla raporlamak |

## 12. Sprint teslimleri

- [x] Gereksinim ve kapsam belgesi
- [x] Mantıksal mimari belgesi
- [x] Başlangıç cihaz envanteri
- [x] VLAN ve IPv4 adresleme taslağı
- [x] Adlandırma standardı
- [x] Güvenlik bölgeleri
- [x] Kabul ölçütleri ve doğrulama kaydı
- [x] Risk ve kapsam dışı listesi
- [x] Sprint yol haritası bağlantısı

## 13. Kapsam dışı

İlk sürüm; gerçek operatör çekirdek ağı, MPLS/BGP üretim tasarımı, 4G/5G RAN, EPC/5GC,
gerçek donanım performans garantisi, gerçek kimlik bilgileri, replikasyonlu servis kümeleri ve
Packet Tracer dışı üretim otomasyonunu kapsamaz.

## 14. Sonuç

Sprint 00-00, davranış veya performans iddiası üretmeden proje sınırlarını ve teknik sözleşmeyi
tamamladı. Sprint 00-01 bu sözleşmeyi kullanarak ilk temel LAN ve IPv4 Packet Tracer topolojisini
oluşturacaktır.
