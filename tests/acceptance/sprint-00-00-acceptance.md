# Sprint 00-00 Kabul ve Doğrulama Kaydı

## Sonuç

Sprint 00-00 dokümantasyon ve mimari sözleşme kapsamı tamamlandı. Bu sprint çalışan ağ topolojisi
iddiasında bulunmaz; Packet Tracer uygulaması Sprint 00-01’de başlayacaktır.

| Kimlik | Kontrol | Sonuç | Kanıt |
|---|---|---|---|
| AC-00-01 | Merkez ve iki şube kapsamı tanımlı | PASS | Sprint README bölüm 2 |
| AC-00-02 | Kullanıcı telefon sunucu ve misafir kapasiteleri tanımlı | PASS | Sprint README bölüm 2 |
| AC-00-03 | VLAN kimlikleri ve görevleri benzersiz | PASS | Sprint README bölüm 5 |
| AC-00-04 | Site IPv4 blokları birbiriyle çakışmıyor | PASS | initial-addressing-plan.csv |
| AC-00-05 | WAN /30 ağları birbiriyle çakışmıyor | PASS | initial-addressing-plan.csv |
| AC-00-06 | Gateway standardı tanımlı | PASS | Sprint README bölüm 6 |
| AC-00-07 | Mantıksal mimari ve trafik akışları tanımlı | PASS | logical-architecture.md |
| AC-00-08 | Cihaz rolleri ve planlanan sprintleri kayıtlı | PASS | device-inventory.csv |
| AC-00-09 | Güvenlik bölgeleri ve temel politika tanımlı | PASS | Sprint README bölüm 8 |
| AC-00-10 | Packet Tracer sürüm politikası tanımlı | PASS | Sprint README bölüm 10 |
| AC-00-11 | Riskler ve kapsam dışı konular açık | PASS | Sprint README bölüm 11 ve 13 |
| AC-00-12 | Sonraki sprint giriş koşulları açık | PASS | logical-architecture.md açık kararlar |

## Adres çakışması incelemesi

- 10.10.0.0/16 yalnız HQ için ayrılmıştır.
- 10.20.0.0/16 yalnız Şube A için ayrılmıştır.
- 10.30.0.0/16 yalnız Şube B için ayrılmıştır.
- 10.255.0.0/24 yalnız WAN transit için ayrılmıştır.
- 10.254.0.0/24 yalnız loopback/router kimliği için ayrılmıştır.
- Her kullanıcı VLAN’ı ayrı /24 sınırındadır.
- WAN bağlantıları sırasıyla 10.255.0.0/30, 10.255.0.4/30 ve 10.255.0.8/30 kullanır.

Sonuç: Planlanan IPv4 ağlarında örtüşme bulunmamaktadır.

## Sprint 00-01 giriş kontrolü

Sprint 00-01 başlamadan önce:

- Packet Tracer tam sürümü kaydedilmeli.
- HQ-RTR-01, HQ-ASW-01 ve ISP-RTR-01 modelleri arayüz ihtiyacına göre doğrulanmalı.
- İlk PKT dosyası temiz açılış testinden geçmeli.
- HQ STAFF ağı için ilk iki temsilî istemci seçilmeli.
- Kullanılan portlar cihaz envanterine işlenmeli.
