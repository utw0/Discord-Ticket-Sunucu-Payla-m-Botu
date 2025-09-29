# Discord Ticket & Sunucu Paylaşım Botu

Destek taleplerini yönetmek ve sunucu paylaşımını otomatikleştirmek için tasarlanmış, satışa hazır bir Discord botu. Modern Discord bileşenleri (buton, modal, select menu) ile hızlı, şık ve yetki odaklı deneyim sunar.

## Öne Çıkanlar
- Ticket sistemi: modal ile açılış, sahiplenme, kapatma onayı, transcript, üye ekle/çıkar, öncelik yönetimi.
- Sunucu paylaşım sistemi: onay/red akışı, otomatik tier tespiti, kategoriye göre paylaşım, detay kartları.
- Tam yetki kontrolü: yönetici/staff rolü, kanal izinleri ve özel görünürlük.
- MongoDB ile kalıcı veri: GuildConfig, Ticket, SharePost modelleri.
- discord.js v14 ile modern etkileşimler.

### Görüntüler
<details>
  <summary>Komutlar</summary>

| Komut                  | Resim                                                                                                  |
| ---------------------- | ------------------------------------------------------------------------------------------------------ |
| GÖRSEL | <img width="338" height="232" alt="image" src="https://github.com/user-attachments/assets/14d27450-eb04-411e-8a29-919db6ccd401" />
| GÖRSEL | <img width="616" height="237" alt="image" src="https://github.com/user-attachments/assets/cfda0664-42da-4310-8baf-77db68bde90c" />
| GÖRSEL | <img width="395" height="427" alt="image" src="https://github.com/user-attachments/assets/5129e415-d69d-49a0-9c8c-baa60fdffc33" />
| GÖRSEL | <img width="520" height="229" alt="image" src="https://github.com/user-attachments/assets/0ad38ada-f23b-4104-ab51-62d1d5834f7f" />
| GÖRSEL | <img width="590" height="373" alt="image" src="https://github.com/user-attachments/assets/8e781540-ee68-4f48-8d86-95ef47164fe1" />
| GÖRSEL | <img width="1578" height="356" alt="image" src="https://github.com/user-attachments/assets/c2b7deb5-725c-4192-834e-cd9ff039a49e" />
| GÖRSEL | <img width="492" height="351" alt="image" src="https://github.com/user-attachments/assets/645b8254-5019-4b5a-8f0e-e5381c35033d" />
| GÖRSEL | <img width="533" height="301" alt="image" src="https://github.com/user-attachments/assets/30442388-d85b-4031-b6a3-ec5a1834f386" />
| GÖRSEL | <img width="595" height="556" alt="image" src="https://github.com/user-attachments/assets/ae9c9563-a6fb-404b-aaeb-0a1101629d15" />

|
</details>
## Komutlar ve Paneller

### Slash Komutlar
- /ticket-setup
  - Ticket sistemi için kategori ve yetkili rolü kurulumunu yapar.
- /share-setup
  - Paylaşım sistemi için log kanalı, tier kanalları ve yetkili rolü kurulumunu yapar.


### Kullanıcı Panelleri ve Modallar
- Sunucu Paylaş paneli
  - Buton: Sunucu Paylaş (share:create)
  - Modal alanları: Sunucu Adı, Sınırsız Davet Linki, Açıklama
  - Akış: Başvuru → Log kanalına düşer → Yetkili onayı ile ilgili kanala gönderilir.
- Geri Bildirim / Şikayet / Reklam Bildir
  - Butonlar: Öneri/İstek (share:feedback), Şikayet (share:complaint), Reklam Bildir (share:adreport)
  - Her biri birer ticket kanalı oluşturur ve yetkili rolünü pingler.
- Paylaşım Bilgi
  - Buton: share:info → Kurallar ve bilgilendirme embed’i.

### Yetkili İşlemleri (Paylaşım)
- Onayla / Reddet: share:approve:<id> / share:reject:<id>
  - Onaylanınca otomatik tier tespitine göre uygun kanala gönderir.
- Kategori: share:category:<id> → select menu (design, team, gif, nsfw, clan, roleplay, music, dev)
  - Seçime göre çevresel değişkenle tanımlı kategori kanalına paylaşır.
- Detay: share:detail:<id>
  - Sunucu adı, davet, açıklama ve sahibi bilgilerini gösterir.

### Ticket Kanalı Butonları
- Sahiplen: ticket:claim
- Kapat: ticket:close (onay/cancel akışı)
- Üye Ekle / Çıkar: ticket:add / ticket:remove (select menülerle)
- Transkript: ticket:transcript
- Öncelik Seçici: ticket:priority (low, normal, high, blocker)

## Tier Sistemi (Otomatik Kanal Seçimi)
Onaylanan paylaşımlar için üye sayısına göre tier belirlenir ve ilgili kanala gönderilir:
- Desteklenen anahtarlar: t0_1k, t1_2k, t2_3k, t3_5k, t5_7k, t7_10k, t10_20k, t20_50k, t50_250k
- Sunucunun üye sayısı davet linkinden tespit edilmeye çalışılır; tespit edilemezse uygun varsayılan/yetkili seçimi devreye girer.
