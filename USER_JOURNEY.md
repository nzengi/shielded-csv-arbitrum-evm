# Shielded CSV Vault - Kullanıcı Senaryoları

## 📋 Genel Bakış

Shielded CSV Vault sistemi, kullanıcıların **gizli ve güvenli** bir şekilde varlık yatırıp çekebilecekleri bir DeFi protokolüdür. Bu dokümanda, sistemin nasıl kullanılacağına dair detaylı senaryolar bulunmaktadır.

---

## 🎯 Temel Kullanım Senaryoları

### Senaryo 1: Basit Varlık Yatırma ve Çekme

#### **Durum**: Alice, 100 USDC'sini kasaya yatırmak ve daha sonra çekmek istiyor.

#### **Adım 1: Cüzdan Bağlama**

```
1. Alice web uygulamasını açar (http://localhost:3000)
2. "Connect Wallet to Access Vaults" butonuna tıklar
3. MetaMask cüzdanını seçer ve bağlar
4. Arbitrum Sepolia ağına geçer
```

#### **Adım 2: USDC Vault'una Erişim**

```
1. Bağlantı sonrası "Your Private Vaults" sayfası görünür
2. "USDC Vault" kartında şu bilgileri görür:
   - Your Balance: 1000.0000 USDC (cüzdanındaki miktar)
   - Total Deposited: 0.00 USDC (henüz yatırım yok)
   - Vault Balance: 0.00 USDC (kasa boş)
```

#### **Adım 3: USDC Yatırma**

```
1. "Deposit Amount" alanına "100" yazar
2. "Deposit" butonuna tıklar
3. MetaMask'ta işlemi onaylar
4. İşlem tamamlanır ve sayfa güncellenir
```

#### **Adım 4: Yatırım Sonrası Durum**

```
1. Vault kartında güncellenmiş bilgileri görür:
   - Your Balance: 900.0000 USDC (100 USDC azaldı)
   - Total Deposited: 100.00 USDC (yatırılan miktar)
   - Vault Balance: 100.00 USDC (kasadaki miktar)
   - Daily limit remaining: 900.00 USDC (günlük çekim limiti)
```

#### **Adım 5: USDC Çekme**

```
1. "Withdraw Amount" alanına "50" yazar
2. "Withdraw" butonuna tıklar
3. MetaMask'ta işlemi onaylar
4. İşlem tamamlanır ve sayfa güncellenir
```

#### **Adım 6: Çekim Sonrası Durum**

```
1. Vault kartında güncellenmiş bilgileri görür:
   - Your Balance: 950.0000 USDC (50 USDC geri geldi)
   - Total Deposited: 100.00 USDC (değişmedi)
   - Vault Balance: 50.00 USDC (50 USDC kaldı)
   - Daily limit remaining: 850.00 USDC (50 USDC azaldı)
```

---

### Senaryo 2: ETH Vault Kullanımı

#### **Durum**: Bob, 0.5 ETH'sini kasaya yatırmak istiyor.

#### **Adım 1: ETH Vault'una Erişim**

```
1. Bob cüzdanını bağlar
2. "ETH Vault" kartında şu bilgileri görür:
   - Your Balance: 2.5000 ETH
   - Total Deposited: 0.00 ETH
   - Vault Balance: 0.00 ETH
```

#### **Adım 2: ETH Yatırma**

```
1. "Deposit Amount" alanına "0.5" yazar
2. "Deposit" butonuna tıklar
3. MetaMask'ta işlemi onaylar (gas ücreti dahil)
4. İşlem tamamlanır
```

#### **Adım 3: Yatırım Sonrası Durum**

```
1. Vault kartında güncellenmiş bilgileri görür:
   - Your Balance: 2.0000 ETH (0.5 ETH azaldı)
   - Total Deposited: 0.50 ETH
   - Vault Balance: 0.50 ETH
   - Daily limit remaining: 0.50 ETH (günlük limit)
```

---

### Senaryo 3: Günlük Limit Aşımı

#### **Durum**: Charlie, günlük çekim limitini aşmaya çalışıyor.

#### **Başlangıç Durumu**

```
- Charlie'nin kasasında: 1000 USDC
- Günlük çekim limiti: 100 USDC
- Bugün çektiği: 80 USDC
- Kalan limit: 20 USDC
```

#### **Deneme: Limit Aşımı**

```
1. Charlie "Withdraw Amount" alanına "50" yazar
2. "Withdraw" butonuna tıklar
3. Sistem hata verir: "Daily limit exceeded"
4. İşlem iptal edilir
```

#### **Çözüm**

```
1. Charlie "Withdraw Amount" alanına "20" yazar (kalan limit)
2. "Withdraw" butonuna tıklar
3. İşlem başarılı olur
4. Günlük limit sıfırlanır
```

---

### Senaryo 4: Minimum/Maksimum Yatırım Limitleri

#### **Durum**: David, çok küçük veya çok büyük miktar yatırmaya çalışıyor.

#### **Minimum Limit Aşımı**

```
1. David "Deposit Amount" alanına "0.1" yazar (minimum 1 USDC)
2. "Deposit" butonuna tıklar
3. Sistem hata verir: "Amount below minimum"
4. İşlem iptal edilir
```

#### **Maksimum Limit Aşımı**

```
1. David "Deposit Amount" alanına "15000" yazar (maksimum 10000 USDC)
2. "Deposit" butonuna tıklar
3. Sistem hata verir: "Amount above maximum"
4. İşlem iptal edilir
```

---

### Senaryo 5: Cüzdan Bağlantısı Kesilmesi

#### **Durum**: Eve, işlem sırasında cüzdan bağlantısını kesiyor.

#### **Başlangıç**

```
1. Eve cüzdanını bağlar
2. 100 USDC yatırır
3. İşlem tamamlanır
```

#### **Bağlantı Kesilmesi**

```
1. Eve MetaMask'ı kapatır veya ağı değiştirir
2. Sayfa otomatik olarak güncellenir
3. "Connect Wallet to Access Vaults" mesajı görünür
4. Vault kartları gizlenir
```

#### **Yeniden Bağlanma**

```
1. Eve cüzdanını tekrar bağlar
2. Vault kartları tekrar görünür
3. Önceki yatırımları hala mevcut
4. İşlemlere devam edebilir
```

---

### Senaryo 6: Hata Durumları ve Çözümleri

#### **Yetersiz Bakiye**

```
1. Kullanıcı 1000 USDC yatırmaya çalışır
2. Cüzdanında sadece 500 USDC var
3. MetaMask hata verir: "Insufficient balance"
4. Çözüm: Daha az miktar yatırır veya bakiye ekler
```

#### **Gas Ücreti Yetersiz**

```
1. Kullanıcı ETH yatırmaya çalışır
2. Gas ücreti için yeterli ETH yok
3. MetaMask hata verir: "Insufficient funds for gas"
4. Çözüm: Arbitrum Sepolia ETH faucet'ından ETH alır
```

#### **Ağ Hatası**

```
1. Kullanıcı yanlış ağda (Ethereum Mainnet)
2. İşlem başarısız olur
3. Çözüm: Arbitrum Sepolia ağına geçer
```

---

## 🔧 Teknik Detaylar

### **Nullifier Sistemi**

```
- Her yatırım için benzersiz bir nullifier oluşturulur
- Nullifier, kullanıcının adresi + timestamp + random değer ile oluşturulur
- Çekim işleminde nullifier harcanır ve tekrar kullanılamaz
- Bu sistem double-spend saldırılarını engeller
```

### **Proof Sistemi**

```
- Çekim işlemlerinde proof (kanıt) gereklidir
- Proof, kullanıcının gerçekten yatırım yaptığını kanıtlar
- Şu anda basit bir proof sistemi kullanılıyor
- Gelecekte zk-SNARK proof sistemi entegre edilecek
```

### **Güvenlik Özellikleri**

```
- Reentrancy koruması
- Emergency pause sistemi
- Günlük çekim limitleri
- Minimum/maksimum yatırım limitleri
- Vault yetkilendirme sistemi
```

---

## 📊 Örnek İşlem Akışı

### **Başarılı Yatırım İşlemi**

```
1. Kullanıcı 100 USDC yatırmak ister
2. Sistem nullifier oluşturur: 0x1234...
3. Kullanıcı MetaMask'ta onaylar
4. Akıllı sözleşme:
   - USDC'yi kullanıcıdan alır
   - Kasaya yatırır
   - Nullifier'ı kaydeder
   - Event yayınlar
5. İşlem tamamlanır
6. UI güncellenir
```

### **Başarılı Çekim İşlemi**

```
1. Kullanıcı 50 USDC çekmek ister
2. Sistem proof oluşturur: 0x5678...
3. Kullanıcı MetaMask'ta onaylar
4. Akıllı sözleşme:
   - Proof'u doğrular
   - Nullifier'ı kontrol eder
   - Günlük limiti kontrol eder
   - USDC'yi kullanıcıya gönderir
   - Nullifier'ı harcanmış olarak işaretler
5. İşlem tamamlanır
6. UI güncellenir
```

---

## 🎯 Gelecek Özellikler

### **Gelişmiş Gizlilik**

```
- zk-SNARK proof sistemi
- Merkle tree tabanlı nullifier sistemi
- Gelişmiş şifreleme protokolleri
```

### **Ek Fonksiyonlar**

```
- Başka adrese çekim
- Batch işlemler
- Vault paylaşımı
- Not ekleme
- Zaman kilitli çekimler
```

### **UI İyileştirmeleri**

```
- İşlem geçmişi
- Grafik ve istatistikler
- Mobil uygulama
- Dark mode
- Çoklu dil desteği
```

---

## 📝 Özet

Shielded CSV Vault sistemi, kullanıcıların:

1. **Güvenli** bir şekilde varlık yatırmasını
2. **Gizli** bir şekilde varlık çekmesini
3. **Hızlı** ve **ucuz** işlemler yapmasını
4. **EVM uyumlu** cüzdanlarla çalışmasını

sağlar. Sistem, basit ama güçlü bir DeFi altyapısı sunar ve gelecekte daha gelişmiş gizlilik özellikleri eklenebilir.
