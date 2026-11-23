# Başlangıç Mantıksal Ağ Mimarisi

## Amaç

Bu belge Sprint 00-00 kapsamında hedeflenen merkez ve iki şubeli ağın mantıksal sınırlarını
tanımlar. Henüz çalışan Packet Tracer topolojisi değildir; Sprint 00-01 ve sonraki sprintler için
tasarım sözleşmesidir.

## Üst seviye görünüm

    Internet / ISP
          |
      HQ-RTR-01
       /      \
  HQ-DSW-01  HQ-DSW-02        (yedeklilik Sprint 00-08)
       \      /
       HQ access katmanı
       |      |       |
     STAFF  VOICE  SERVER/NET-SVC
       |
       +---- WAN ---- BRA-RTR-01 ---- BRA-ASW-01 ---- STAFF/VOICE/GUEST
       |
       +---- WAN ---- BRB-RTR-01 ---- BRB-ASW-01 ---- STAFF/VOICE/GUEST

## Bölgeler

### HQ kampüs

HQ internet çıkışını, ortak sunucuları, DHCP/DNS/NTP/Syslog/SNMP servislerini ve merkezi çağrı
kontrolünü barındırır. Başlangıç sprintinde tek router/switch ile sade bir LAN kurulabilir; nihai
mimari çift dağıtım cihazını ve yedek gateway’i hedefler.

### Şubeler

Her şubede bir WAN router ve en az bir access switch bulunur. STAFF, VOICE, GUEST ve MGMT
segmentleri merkezle aynı VLAN kimliklerini kullanır fakat siteye özel IP bloklarından adreslenir.

### ISP bölgesi

ISP cihazı gerçek interneti temsil etmez. Varsayılan rota, NAT/PAT ve erişim testleri için kontrollü
bir simülasyon sınırıdır.

## Trafik akışları

1. STAFF istemcileri DHCP’den adres alır, DNS kullanır ve izin verilen sunucu/internet hedefine gider.
2. GUEST yalnız ISP yönüne erişir; 10.0.0.0/8 iç adreslerine erişemez.
3. VOICE istemcileri çağrı kontrolü ve gerekli ses servislerine erişir.
4. MGMT yalnız yetkili yönetim bilgisayarından SSH ve izleme trafiği kabul eder.
5. Şube trafiği OSPF sprintinden sonra dinamik yönlendirilir; öncesinde statik routing kullanılır.
6. Sunucu erişimi ACL matrisine göre servis/port bazında sınırlandırılır.

## Katman sorumlulukları

| Katman | Sorumluluk |
|---|---|
| Edge/WAN | ISP çıkışı, NAT/PAT, şube transit bağlantıları, routing |
| Distribution | Inter-VLAN routing, gateway, ACL, STP root, yedeklilik |
| Access | Uç portları, voice/data VLAN, port security, trunk uplink |
| Services | DHCP, DNS, NTP, Syslog, SNMP ve çağrı kontrolü |
| Management | SSH, cihaz yönetimi, izleme ve yapılandırma erişimi |

## Tasarım kararları

- Site başına ayrı /16 blok, okunabilirlik ve özetleme için seçildi.
- Aynı işlev tüm sitelerde aynı VLAN kimliğini kullanır.
- Gateway adresi subnetin ilk kullanılabilir adresidir.
- Yönetim, misafir, ses ve sunucu trafiği birbirinden ayrıdır.
- Packet Tracer topolojisi temsilî uç cihaz kullanır; adres planı hedef kapasiteyi taşır.
- Yedeklilik ve güvenlik kuralları ilgili sprintlerden önce başarı iddiası olarak sunulmaz.

## Açık kararlar

Sprint 00-01 başlamadan önce şu bilgiler kaydedilecektir:

- ekipte kurulu Packet Tracer tam patch sürümü;
- kullanılacak router ve switch modellerinin Packet Tracer arayüz desteği;
- Layer 3 switch mi router-on-a-stick mi kullanılacağı;
- ilk topolojinin Windows, Linux veya macOS üzerinde üretileceği.
