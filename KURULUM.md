# Rosso Diamond — Kurulum ve Yönetim Rehberi

Bu klasör, rossodiamond gibi gerçek bir alan adında yayınlanacak sitenin tamamıdır.
Barındırma GitHub Pages üzerinde **ücretsizdir**; tek kalıcı maliyet alan adıdır (yılda yaklaşık 10–15 USD).

---

## BÖLÜM 1 — Siteyi yayına alma (bir kez yapılır, ~30 dakika)

### 1. GitHub deposu oluştur
1. github.com'da oturum aç.
2. Sağ üstten **+ → New repository**.
3. Repository name: `rosso-diamond` (veya istediğin ad).
4. **Public** seç (GitHub Pages'in ücretsiz sürümü için gerekli — kod ve fotoğraflar herkese açık olur; vitrin sitesi için sorun değil).
5. **Create repository**.

### 2. Dosyaları yükle
1. Açılan sayfada **uploading an existing file** bağlantısına tıkla.
2. Bu klasördeki HER ŞEYİ sürükleyip bırak:
   - `index.html`
   - `content.json`
   - `gallery.json`
   - `images` klasörü
   - `.github` klasörü (gizli klasördür; görünmüyorsa dosya yöneticisinde "gizli dosyaları göster" aç. Yüklenemezse sorun değil — Bölüm 3'teki not geçerli olur.)
3. Alttaki **Commit changes** düğmesine bas.

### 3. GitHub Pages'i aç
1. Depoda **Settings → Pages** (sol menüde).
2. "Source" altında **Deploy from a branch** seç.
3. Branch: **main**, klasör: **/ (root)** → **Save**.
4. 1–2 dakika içinde sitenin şu adreste yayında:
   `https://KULLANICIADIN.github.io/rosso-diamond/`

### 4. Alan adı satın al ve bağla
1. Alan adını herhangi bir kayıt firmasından al (Cloudflare Registrar maliyetine satar;
   Türkiye'den isimtescil, natro vb. de olur). Örnek: `rossodiamond.com`
2. Aldığın firmanın DNS ayarlarına gir ve şu kayıtları ekle:
   - **A kaydı** (4 adet), ad: `@`, değerler:
     - 185.199.108.153
     - 185.199.109.153
     - 185.199.110.153
     - 185.199.111.153
   - **CNAME kaydı**, ad: `www`, değer: `KULLANICIADIN.github.io`
3. GitHub'da **Settings → Pages → Custom domain** alanına `rossodiamond.com` yaz → Save.
4. "Enforce HTTPS" kutusunu işaretle (aktifleşmesi birkaç saat sürebilir).
5. DNS'in dünyaya yayılması 24 saate kadar sürebilir; genelde 1 saat içinde çalışır.

---

## BÖLÜM 2 — Günlük yönetim (senin "admin panelin" = GitHub arayüzü)

### Fotoğraf eklemek
1. Depoda `images/gallery` klasörünü aç.
2. **Add file → Upload files** → fotoğrafları sürükle → **Commit changes**.
3. Otomasyon (galeri-bot) 1 dakika içinde listeyi günceller, site kendini yeniler.

Dosya adı kuralları:
- Türkçe karakter ve boşluk KULLANMA: `tektas-yuzuk-050ct.jpg` gibi yaz.
- Sıralama alfabetiktir; sıra vermek için başa numara koy: `01-tektas.jpg`, `02-bileklik.jpg`
  (numara sitede görünmez, otomatik temizlenir).
- Fotoğrafın altında dosya adı, tireler boşluğa çevrilerek gösterilir:
  `tektas-yuzuk.jpg` → "tektas yuzuk". Türkçe karakterli düzgün açıklama istiyorsan
  aşağıdaki captions yöntemini kullan.

### Fotoğraf silmek
1. `images/gallery` içinde dosyaya tıkla → sağ üstteki çöp kutusu simgesi → **Commit changes**.

### Banner değiştirmek
1. `images` klasörüne, adı TAM OLARAK `banner.jpg` olan bir dosya yükle
   (aynı adla yüklemek eskisinin üzerine yazar).
2. Geniş/yatay bir fotoğraf seç (en az 1600 px genişlik önerilir).

### Metinleri değiştirmek (başlık, alt başlık, tanıtım — İngilizce ve Türkçe)
1. Depoda `content.json` dosyasına tıkla → sağ üstteki kalem simgesi (Edit).
2. Tırnak içindeki metinleri değiştir. DİKKAT: tırnakları ve virgülleri silme;
   metnin içinde çift tırnak kullanma (gerekiyorsa \" yaz).
3. **Commit changes** → site 1 dakika içinde güncellenir.

### Fotoğraflara özel açıklama yazmak (isteğe bağlı)
`content.json` içindeki `captions` bölümüne dosya adı → açıklama ekle:

    "captions": {
      "01-tektas.jpg": "Tektaş Yüzük · 0.50 ct",
      "02-bileklik.jpg": "Su Yolu Bileklik"
    }

Açıklamayı tamamen gizlemek için boş bırak: `"03-kolye.jpg": ""`

---

## Sık karşılaşılan sorunlar
- **Fotoğraf yükledim, sitede çıkmıyor:** 1–2 dakika bekle; hâlâ yoksa deponun
  **Actions** sekmesine bak — "Galeri listesini guncelle" çalışmış mı? Hiç çalışmamışsa
  `.github/workflows/galeri.yml` dosyası yüklenmemiş demektir; depoda **Add file →
  Create new file** ile `.github/workflows/galeri.yml` yolunu yazıp içeriğini yapıştır.
- **content.json'u bozdum, site metinsiz kaldı:** Dosyanın **History** bölümünden
  önceki sürüme bak, düzgün halini kopyalayıp geri yapıştır. Git'in en güzel yanı:
  hiçbir şey gerçekten kaybolmaz.
- **Alan adı çalışmıyor:** DNS yayılması 24 saate kadar sürebilir. dnschecker.org
  üzerinden A kayıtlarının göründüğünü doğrula.
