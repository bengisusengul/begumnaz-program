# PROGRESS — Begümnaz Program · Oturum Devamlılık Dosyası

> **Bu dosya yeni oturumun ilk okunan dosyasıdır.** Burada nerede kaldığımız, yarın ne yapacağımız, hangi kararların değişmediği yazılır. Önceki oturumda olan her kritik şey buraya yansır.

**Son güncelleme**: 13 Mayıs 2026 — Faz 2 İterasyon 18 (README cheetah hero + görsel iyileştirme)

---

## 🚨 SONRAKİ OTURUMDA İLK YAPILACAK (Next session first action)

### 1. Manuel `git push` — 7+ commit unpushed (push'lanmadıysa)

Şu commit'ler GitHub'a gönderilmedi çünkü Claude'un push to main izni kapalı (default branch protection):
- `aa2c4bf` — PROGRESS.md kapsamlı yeniden yazıldı
- `b2f5a98` — Iter 15 Hacettepe Lab kaldırıldı
- `c771a81` — Iter 16 DEPLOY-API-PROXY.md path/origin fix
- `64f85bd` — PROGRESS.md commit geçmişi listesi (Iter 16 follow-up)
- `a954ba4` — Iter 17 Glossary Bengisu kalıntıları temizliği + SW v8
- `a196a5f` — PROGRESS.md commit geçmişi listesi (Iter 17 follow-up)
- (Iter 18) — README cheetah hero + görsel iyileştirme

```bash
cd /Users/agent9/Desktop/bnsp-repo
git status                    # "ahead of origin/main by 7+ commits" görmeli
git push origin main          # manuel push (kullanıcı çalıştırır)
```

Push sonrası GitHub Pages otomatik deploy → https://bengisusengul.github.io/begumnaz-program/

**Doğrulama**: Push'tan ~1 dk sonra deploy URL açıp Egzersiz sekmesine git, Hacettepe Lab kartının yok olduğunu gör. Toolkit (🔧) modalı aç, "🧪 Bilim Lab" butonu yok olmalı.

### 2. Cloudflare Worker AI proxy deploy (Faz 3)

DEPLOY-API-PROXY.md rehberi 13 Mayıs 2026 Iter 16'da temizlendi (path + origin tutarsızlıkları). 15 dk'lık kurulum:

1. Cloudflare hesap + Wrangler CLI (`brew install cloudflare-wrangler`)
2. `cd ~/Desktop/bnsp-repo` → `mkdir api-proxy && cd api-proxy` → `wrangler.toml` + `worker.js`
3. Worker secrets:
   - `ANTHROPIC_API_KEY` (Anthropic console'dan `sk-ant-...`)
   - `ALLOWED_ORIGINS=https://bengisusengul.github.io,http://localhost:8000`
   - `AUTH_TOKEN` (opsiyonel ekstra koruma)
4. `wrangler deploy` → URL al (`https://begumnaz-api-proxy.YOUR-USERNAME.workers.dev`)
5. PWA Döngü sekmesi → 🛡️ API Proxy → URL set + (varsa) Auth Token → Kaydet
6. Diet sekmesinde Custom Food AI testi (Network tab'da `workers.dev` görmeli, `api.anthropic.com` değil)

### 3. (Opsiyonel) iOS Safari install + cache test

PWA install → "Ana ekrana ekle". Service Worker v7-no-hacettepe yeni cache → eski cache'i yeneceği için ilk açılışta hard reload gerekebilir.

### 4. (Opsiyonel) Tret günü teyidi

Cilt protokolü Sal+Paz tret olarak konumlandı. Eğer Begümnaz farklı gün istiyorsa belirtmeli.

---

## 📍 Şu Anki Sistem Durumu

### Repo

| | |
|---|---|
| **Local** | `/Users/agent9/Desktop/bnsp-repo/` |
| **Remote** | `https://github.com/bengisusengul/begumnaz-program.git` |
| **Deploy** | https://bengisusengul.github.io/begumnaz-program/ (GitHub Pages) |
| **Branch** | `main` (origin/main 1 commit gerisi) |
| **PWA file** | `index.html` (9912 satır, ~688 KB) |
| **SW cache** | `begumnaz-v7-no-hacettepe-2026-05-12` |
| **Manifest** | `manifest.json` — Begümnaz branding |
| **Bg image** | `bg.jpeg` |

> **DİKKAT**: macOS case-insensitive FS yüzünden `Begumnaz-program` (raw materyal Desktop'ta) ile `begumnaz-program` (repo adı) çakışıyordu. Çözüm: local repo klasör adı `bnsp-repo`, GitHub repo adı `begumnaz-program`.

### Faz Durumu

- ✅ **Faz 1**: Markdown dokümantasyon iskeleti (tamamlandı)
- 🟢 **Faz 2**: PWA içerik adaptasyonu (Iter 15/?, ~%85 tamam — büyük temizlikler bitti)
- ⏳ **Faz 3**: Deploy (kısmen — GitHub Pages aktif, Cloudflare Worker AI proxy henüz deploy değil)

---

## 📜 Bu Oturumda Yapılanlar (13 Mayıs 2026)

### Iter 18 — README cheetah hero + görsel iyileştirme

Faz 2 son temizlik kalemi: repo README görsel olarak çıplaktı, başlık metinden ibaretti.

**Eklenen**:
- `hero-image.jpeg` (208 KB, 736×1223, cheetah, JPEG) — `Begumnaz-program/gorseller/`'dan repo'ya kopyalandı (Iter 9'da CSS pembe/bordo teması için referans alınmıştı, şimdi README hero olarak da kullanılıyor).
- README başına `<p align="center"><img src="hero-image.jpeg" width="400"></p>` (HTML center, 400px width).
- Tema notu (blockquote): "Cheetah hero — gücün ve hassasiyetin birlikteliği. PWA pembe/bordo teması (Playfair Display, Billie Eilish ref) bu görselden esinlenildi."

**Yapılmayan** (gelecek Iter'a):
- PWA ekran görüntüleri (Dashboard/Cycle/Diet/Skin/Workout) — kullanıcının PWA'yı kendi cihazında açıp screenshot alması gerekecek.
- GitHub Pages deploy URL badge.

---

### Iter 17 — Glossary Bengisu kalıntıları temizliği + SW v8

PWA glossary'sinde (`LEGEND_DEFS`, satır 7280-7400 civarı) kapsamlı Bengisu kalıntıları bulundu — bazıları **yanlış tıbbi bilgi** içeriyordu. Iter 7'de "KAPSAMLI Bengisu temizliği" yapılmış olmasına rağmen glossary bölümü atlanmıştı.

**Silinen 4 glossary maddesi** (Begümnaz protokolünde yok):
- `calciday` — Kalsiyum karbonat efervesan (Bengisu E89.2 paratiroid yetersizliği için)
- `qalyviz` — Aktif D vit (Bengisu)
- `levotiroksin` — Sentetik T4 (Bengisu tiroidektomi için)
- `endo komplikasyonu` — Paratiroid yetersizliği (Bengisu E89.2)

**Yanlış tanım tamamen yeniden yazıldı**:
- `endometriozis` def: "Tiroid bezinin cerrahi alınması" ← TAMAMEN YANLIŞ TIBBİ BİLGİ. Doğru tanım: "Endometrium dokusunun uterus dışında bulunması" + Begümnaz context (Visanne tamamlandı, içerde kalan endo, bütüncül protokol, endo flare, süt+dana+tavuk yasak).

**Yanlış tıbbi cümleler temizlendi**:
- `t4` glossary'sinde `Lugol iyot (levotiroksin) sentetik T4` ← Lugol ≠ levotiroksin (Lugol potasyum iyot çözeltisi). Yerine: Begümnaz selenyum/iyot düşük → Lugol reçete bağlamı.
- `t4` l3'te `Total endometriozis sonrası life-long T4 replacement` cümlesi (Bengisu için).
- `tsh` def'te `Tiroidektomi sonrası replacement dozu` cümlesi. Yerine: Anti-TPO negatif → Hashimoto yok.
- `bmr` l3'te `Tiroidektomi T4 replacement uygunsa...` cümlesi. Yerine: Begümnaz T3 hafif yüksek → BMR hafif artmış.
- Satır 2614 yorum: `// Tiroidektomi: ≥35 minimum (post-thyroidectomy adjustment)` → `// EA ≥35 minimum (endo flare/post-isotretinoin adjustment)`.

**Yeni eklenen madde**:
- `post-isotretinoin` — Begümnaz için tam bağlamlı (8 ay × 40 mg Zoretanin etki etmedi, bariyer onarımı 12-24 ay, PIE/PIH/güneş lekeleri, tret 2x/hf sandwich, mezoterapi öncesi/sonrası 5 gün retinoid kes).

**Yapısal**:
- Bölüm başlığı `// ── Tıp/Tiroid (6) ──` → `// ── Tıp/Begümnaz (5) ──` (Bengisu silindi → madde sayısı eşleşti).

**SW cache bump**:
- `sw.js:4` → `begumnaz-v7-no-hacettepe-2026-05-12` → `begumnaz-v8-glossary-fix-2026-05-13` (eski cache invalide olacak, kullanıcı ilk açılışta yeni glossary'yi görür).

**Tıbbi önem**: Kullanıcı glossary kartlarını açtığında daha önce Bengisu'nun tiroidektomi geçmişine ait yanlış bilgilerle karşılaşıyordu. Özellikle "endometriozis = tiroidektomi" tanımı klinik açıdan kritik yanlış. Iter 17 ile glossary Begümnaz tıbbi profiline (post-isotretinoin + endometriozis + Anti-TPO negatif) tam uyumlu hale getirildi.

---

### Iter 16 — DEPLOY-API-PROXY.md path/origin fix

Faz 3 (Cloudflare Worker AI proxy deploy) öncesi tarama → `DEPLOY-API-PROXY.md`'de **3 tutarsızlık** bulundu ve düzeltildi:

| Satır | Eski | Yeni | Neden |
|---|---|---|---|
| 15 | `begumnazsengul.github.io` | `bengisusengul.github.io` | Origin açıklama metni |
| 39 | `cd ~/Desktop/begumnaz-program` | `cd ~/Desktop/bnsp-repo` | macOS case-insensitive FS path collision (PROGRESS.md "Kritik Hatırlanması Gerekenler"da belgeli) |
| 62 | `begumnazsengul.github.io,http://localhost:8000` | `bengisusengul.github.io,http://localhost:8000` | `ALLOWED_ORIGINS` secret değeri |

**Önem**: Rehberi takip eden kullanıcı Worker'ı yanlış konfigüre ederse origin kontrolü tüm AI çağrılarını 403 ile reddederdi. Faz 3 deploy'una geçmeden temizlendi.

`cloudflare-worker.js` satır 8'deki comment'te `bengisusengul.github.io` doğru yazılmış — sadece rehber tutarsızdı.

---

## 📜 Önceki Oturum (12 Mayıs 2026)

Bugünkü iterasyonlar **9-15 arası**. Önceki oturumlardan devralınan + bu oturumda eklenen:

### Iter 9 — Pembe/Bordo Tema (Billie Eilish + Cheetah ref)
- `hero-image.jpeg` (cheetah) + `fonts.jpg` referansından Begümnaz görsel kimliği
- CSS değişkenleri: cream/sage palette → pink/burgundy + mustard accent
- Font: Inter → **Playfair Display** (h1, h2, .hl-title vb.)

### Iter 10 — Diet sayfası temizlik + SUPPLEMENT_ALARMS
- Bengisu'dan kalan 4 alarm (Levotiron, Calciday vb.) → Begümnaz'ın 16 ürün protokolü
- Diet kartlarında cream-bg + cream-text kontrast sorunu ilk geçiş

### Iter 11 — Glossary + AI prompt Bengisu kalıntıları + JS apostrof fix
- `Begümnaz'da iyot düşük` → `Begümnaz iyot ölçümü` (apostrof JS string kırıyor)
- `KMY'yi etkileyebilir` → `kemik yoğunluğunu`
- AI prompt'larda kalan Hashimoto/post-tiroidektomi referansları temizlendi

### Iter 12 — fixPeriodData20260504 disabled
- Bengisu'nun period seed fonksiyonu her first-run'da `2026-04-28→2026-05-03` ekliyordu
- "1 regl kaydı yüklendi" screenshot → fonksiyon body `return;` yapıldı

### Iter 13 — Diyet kart kontrast agresif override
- `body[data-page="diyet"] .card *` → `color:#2A0E14 !important`
- Inline cream-text style'ları override etmek için son çare

### Iter 14 — "acıkmadan" → "acıkınca" semantik düzeltme
- Kullanıcı screenshot: "1. öğün — kahvaltı (acıkmadan)" = TR olarak yanlış (aç olmadan ye demek)
- 6 satır düzeltildi: topbar, diet section, JS comment, AI slotName, AI prompt, hero
- SW cache: v5-contrast → v6-acikinca

### Iter 15 — Hacettepe Lab tamamen kaldırıldı (bu oturumun son işi)
- Bengisu'nun "🧪 Bilim Modu L3" 4-tab modülü (Veri/Hipotez/PMID/Pedagoji)
- 342 satır silindi (CSS .hl-*/.hlab-* + HTML container + Toolkit butonu + openHacettepeLab + renderHacettepeLab tüm modülü + Bilim Modu L3 desc mention'ları)
- **İlk deneme başarısız** (Python script tek `skip` flag'i CSS+JS bloklarını paylaşıyordu, 3474 satır siliyordu) → `git checkout` ile geri alındı
- **İkinci deneme** (`/tmp/remove_hacettepe_v2.py`) — line-range tabanlı, 342 satır temiz silindi
- JS syntax breakage: `glossary'de` Türkçe apostrofu single-quoted JS string'i kırıyordu → `glossary kartında` ile değiştirildi
- SW cache: v6-acikinca → **v7-no-hacettepe**
- Commit `b2f5a98` (unpushed)

---

## 📋 Bekleyen Görevler

### Doktor cevabı bekleyen (Begümnaz son görüşmede sordu — abla iletecek)

1. **NADH dozu** — Şimdilik **1 tablet sabah AC** uygulanır (varsayım: 5-20 mg sublingual/tablet)
2. **NAC nasıl** — Şimdilik **2×500 mg (sabah AC + ikindi AC)** uygulanır. Doktor "tek sefer 1000 mg" derse o uygulamaya geçilir
3. **Probiyotik markası** — Duobalance BV Cran dışında alternatif var mı?

**KURAL**: Bu 3 cevap dışında **doktor protokolü dışına çıkılmaz**. Doktor 21.04.2026 kan panelini görerek 16 ürünlük protokolü yazdı. Bizim işimiz protokolün **uygulamasını optimize etmek** (saatler, etkileşim, beslenme + yaşam uyumu), ek supplement önermek değil.

### Yapılması düşünülen ama henüz açılmayanlar

- [ ] **Cloudflare Worker AI proxy deploy** — `cloudflare-worker.js` repo'da var ama deploy edilmedi. Begümnaz/abla kendi Anthropic API key girene kadar AI özellikleri (yemek analizi, cilt foto karşılaştırma, tarif üretimi) çalışmaz.
- [ ] **3 yeni cilt ürünü alışverişi** — Yumuşak temizleyici (CeraVe/Bioderma/LRP, 250-450 TL), Niacinamide serum 5-10% (TO/COSRX, 200-350 TL), Azelaic acid 10% (TO/Naturium, 250-450 TL). Bütçe ~700-1200 TL.
- [ ] **Itır yağı + Epsom tuzu** — Eczane/Aksu Vital'den. Ayak banyosu için.
- [ ] **iOS Safari "Ana ekrana ekle"** test — install + offline çalışma + manifest icon kontrolü
- [ ] **Doktor kontrol** — 6-8 hafta sonra Lugol başlangıcı sonrası TSH/T3/T4 tekrar
- [ ] **Pelvik-takip.md** — Her hafta yapılan pelvik taban video'sunun adı/link'i not edilmeli (tekrar engellemek için). `/Users/agent9/Desktop/Begumnaz-program/pelvik-takip.md` dosyası henüz yok, kullanıcı manuel ekleyebilir.

### Açık konular (kullanıcı yönlendirmeli)

- [ ] Begümnaz gym günü sabit olursa → tret günü konumlandırması yeniden yapılır (şu an Sal+Paz, gym günü sabitlenirse o güne yakın olmayan günlere kayar)
- [ ] Mezoterapi tekrar başlarsa → tret+azelaic protokolü 7-10 gün durur, sonra kademeli başlar
- [ ] Visanne tekrar başlarsa → Lugol iyot doktor onayı (etkileşim olabilir)

---

## ⚠️ Kritik Hatırlanması Gerekenler

### Kullanıcı kararları (değişmez)

1. **Repo public, her şey açık** (medical-documents/ dahil). Begümnaz onayı verildi. Sorumluluk ablada.
2. **AI özellikleri korunacak** (Bengisu gibi) — Anthropic API + Cloudflare Worker proxy
3. **Faz 1 markdown dokümantasyon source-of-truth** — `/Users/agent9/.claude/plans/haftalik-program-olarak-kardesim-golden-clarke.md` plan dosyası ana kaynak. Repo SYNTHESIS dosyaları buradan üretilir.
4. **`Desktop/Begumnaz-program/` raw materyal arşivi** — repo'ya kopyalanan ham veriler burada, dokunulmaz
5. **PWA single-file** — `index.html` tek dosya yaklaşımı Bengisu'dan miras, korunuyor

### Begümnaz tıbbi profili (özet)

- **Tanılar**: Endometriozis (Visanne tamamlandı, içerde kalan endo arada şişlik yapıyor) · Post-isotretinoin (8 ay 40 mg Zoretanin etki etmedi) hassas cilt · Hormonal jawline akne · İdrar iyot düşük (27 µg/L) · Selenyum düşük (58 µg/L) · Serum demir yüksek (204) · T3 hafif yüksek · Anti-TPO **negatif** (Hashimoto **YOK**)
- **Cilt geçmişi**: 8 ay isotretinoin + 3× akne+scar mezoterapi (en yenisi 2 ay önce)
- **Doktor protokolü** (Mayıs 2026): 16 ürün — Akavital + Alkemist + Gül sirkesi + NAC + NADH + Anti turmeric + More than + Anti MM-12 + NBT Life Guard + Lifextra On Hepa + Time Mg + Lugol %5 + Colewinde + Benfolife + Duobalance BV Cran + Bach çiçekleri
- **Beslenme**: Mizaç temelli — yasaklar (pirinç, beyaz un, dana/tavuk, süt ürünü, salça, soğuk su, çay/kahve, patlıcan, yer fıstığı vb.) · izinli (kuzu/koyun/hindi 3x/hafta, pişmiş sebze, ancient grain ekmek, sıcak su 5 bardak)
- **Yaşam**: Ayak banyosu (4-5 damla ıtır + 2 yk Epsom) her gece 20:00-20:30 · Karın+bel+popo+ayak sıcak tutma · Itır yağı koklama gün içinde

### Programatik kural notları

- **Acnelyse 0.025% = tretinoin**, retinol DEĞİL (presciption retinoid) — daha güçlü, hassas ciltte 2x/hafta + sandwich tekniği
- **Anti-TPO negatif** → Hashimoto yok, Lugol güvenle başlatılabilir
- **CRP, KCFT, HbA1c normal** → sistemik durum sakin, protokol önleyici
- **Demir takviyesi YASAK** (serum demir 204, paradoks: ferritin 31.7 orta) → 3 ay sonra tekrar test, devam yüksekse HFE C282Y/H63D gen taraması doktor karar verir
- **İyot tedavisi başlangıcında selenyum eksikliği RİSK** — doktora soruldu (Bölüm 5.1 plan)

### Teknik notlar (kodlamada hatırlanması gereken)

- **Türkçe apostrof JS string'i kırıyor**: `Begümnaz'da`, `glossary'de`, `KMY'yi` gibi ifadeler `'...'` single-quoted JS string'inde olduğunda parse hatası → ya escape (`\'`) ya da apostrof'suz yeniden yazım
- **Card text contrast**: Diyet sayfasında inline cream-color style'lar problem yapıyor → `body[data-page="diyet"] .card *` aggressive override kullanıldı (Iter 13)
- **Service Worker cache busting**: Her büyük değişiklikte `CACHE_NAME` versiyonu bump'lanmalı (v7-no-hacettepe son), aksi halde kullanıcı eski versiyonu görmeye devam eder
- **Python script çoklu skip flag**: Tek `skip` değişkeniyle çoklu blok silme HATA (Iter 15 ilk deneme) → her blok için ayrı flag VEYA line-range tabanlı silme (sanity check'li)
- **Repo path collision**: Local repo `bnsp-repo`, GitHub repo adı `begumnaz-program`, raw arşiv `/Users/agent9/Desktop/Begumnaz-program/`. Karıştırma.

---

## 📂 Kritik Dosya Konumları

```
/Users/agent9/
├── .claude/plans/haftalik-program-olarak-kardesim-golden-clarke.md  ← SOURCE OF TRUTH (plan)
├── .claude/projects/-Users-agent9-Desktop-Begumnaz-program/
│   └── memory/MEMORY.md  ← Auto-memory profile linkleri
└── Desktop/
    ├── Begumnaz-program/                  ← Raw materyal arşivi (dokunulmaz)
    │   ├── medical records/               (12 PDF kan testleri)
    │   ├── skin status/                   (cilt fotoğrafları + inuse-product)
    │   ├── body image/, period records/, supplements/, gorseller/
    │   ├── alisveris-listesi.{html,pdf,png}
    │   └── beslenme-ornegi-yasak-listesi.jpg
    └── bnsp-repo/                          ← GİT REPO (deploy edilen)
        ├── index.html                      (PWA — 9912 satır)
        ├── manifest.json, sw.js, cloudflare-worker.js, bg.jpeg
        ├── README.md, CLAUDE.md, PROGRESS.md (bu dosya), DEPLOY-API-PROXY.md, HEALTH_SHORTCUT.md, PWA-ADAPTATION-TODO.md
        ├── skin-ultimate/                  (SYNTHESIS + 3 agent)
        ├── supplements-ultimate/           (SYNTHESIS + 2 agent + photos/)
        ├── workout-ultimate/               (SYNTHESIS + 4 agent)
        ├── diet-ultimate/                  (SYNTHESIS + 3 agent)
        ├── lifestyle-ultimate/             (SAC-BAKIM dahil)
        └── medical-documents/              (KAN-DEGERLERI-TREND + kan-testleri/ + cilt-fotograflari/ + ...)
```

### Git çalışma dizini

`/Users/agent9/Desktop/bnsp-repo` — burada `git status`, `git push` çalıştırılır.

---

## 📊 Commit Geçmişi (20 commit · son 19 bu oturum + önceki iterasyonları)

```
3b469ad  Phase 1: Markdown dokümantasyon iskeleti tamamlandı
4fed444  Faz 2 Iter 1:  PWA dosyaları Bengisu'dan kopyalandı + ilk adaptasyon
d34ca2d  Faz 2 Iter 2:  Dashboard timeline tamamen Begümnaz protokolü
2790138  Faz 2 Iter 3:  Welcome modal + SUPPLEMENTS_INVENTORY + AI prompt temizliği
3b65723  Faz 2 Iter 4:  Diet rules + slot description mizaç temelli
530c739  Faz 2 Iter 5:  Doktor soruları + PDF özet + Bilim modalı temizlik
7532937  Faz 2 Iter 6:  Dashboard mode (sabah/öğlen/akşam/gece) nextActions Begümnaz
780d36b  Faz 2 Iter 7:  KAPSAMLI Bengisu temizliği — tüm referanslar kaldırıldı
76283af  Faz 2 Iter 8:  i18n TR/EN + Akıllı Ölçüm + Bengisu seed data temizliği
0621007  Faz 2 Iter 9:  Pembe & Bordo teması + Playfair Display (Billie Eilish ref)
0f84011  Faz 2 Iter 10: Diet sayfası Bengisu temizliği + SUPPLEMENT_ALARMS + kart kontrastı
ae9c213  Faz 2 Iter 11: Glossary + AI prompt Bengisu kalıntıları + JS apostrof fix
f95d2d7  Faz 2 Iter 12: fixPeriodData20260504 disabled (Bengisu period seed)
f224140  Faz 2 Iter 13: Diyet sayfası kart kontrastı — agresif text override
59bc99a  Faz 2 Iter 14: "acıkmadan" → "acıkınca" (Türkçe semantik düzeltme)
b2f5a98  Faz 2 Iter 15: Hacettepe Lab tamamen kaldırıldı — Bengisu kalıntısı  ⬅ UNPUSHED
aa2c4bf  PROGRESS.md kapsamlı yeniden yazıldı — oturum devamlılık dosyası  ⬅ UNPUSHED
c771a81  Faz 2 Iter 16: DEPLOY-API-PROXY.md path/origin tutarsızlık fix  ⬅ UNPUSHED
64f85bd  PROGRESS.md commit geçmişi listesi: Iter 16 + aa2c4bf eklendi  ⬅ UNPUSHED
a954ba4  Faz 2 Iter 17: Glossary Bengisu kalıntıları temizliği + SW v8  ⬅ UNPUSHED
```

---

## 🎯 Stratejik Sıra (yarın ve sonraki oturumlar için)

### Bugünden devralınan (öncelik sırası)

1. **`git push` Iter 15** (manuel — Claude izni kapalı)
2. **Deploy URL'de Hacettepe Lab gerçekten yok mu** kontrol (1 dk iş)
3. **Begümnaz iOS Safari install** (eğer henüz yapmadıysa) → ilk gerçek kullanım feedback'i
4. **Cilt 3 yeni ürün alışveriş** (~700-1200 TL bütçe) — Begümnaz başlayabilsin diye
5. **Itır + Epsom alımı** — bu gece ayak banyosuna başlamak için

### Faz 2 son temizlikler (kalmış küçük şeyler)

- [ ] **AI prompt'lar son tarama** — bilim modu fizyoloji prompt'unda Bengisu kalıntısı kalmış olabilir
- [ ] **Tooltip + glossary contrast pass** — Iter 13 sadece Diyet sayfasını çözdü, diğer sayfalarda kalan kart text-color sorunu olabilir (kullanıcı önceki screenshot'ta "hala okunmayan kısımlar var" demişti — tam çözülmedi)
- [ ] **Repo README görsel iyileştirme** — Hero image + screenshot ekleme

### Faz 3 (Deploy + Stabilizasyon)

- [ ] Cloudflare Worker AI proxy deploy (`DEPLOY-API-PROXY.md` rehberinden)
- [ ] Anthropic API key (Begümnaz/abla kendi) Worker'a koyma
- [ ] Apple Health iOS Shortcut (`HEALTH_SHORTCUT.md` — opsiyonel, manuel input fallback var)
- [ ] Push notification (opsiyonel — sw.js base var)
- [ ] Begümnaz kullanım periyodu 1-2 hafta → ilk gerçek feedback iterasyonu

---

## 🔄 Bu Dosya Nasıl Güncellenir

Her oturumun sonunda **şunları güncelle**:
1. **Son güncelleme** tarihi
2. **Yarın ilk yapılacak** bölümü (yeni session başı için)
3. **Bu Oturumda Yapılanlar** altına yeni iter eklenir
4. **Commit Geçmişi** son commit hash'ı eklenir
5. **Bekleyen Görevler** içinde tamamlananları `~~strikethrough~~` ya da sil
6. **Kritik Hatırlanması Gerekenler** bölümü değişen kararlarda güncellenir

Yarın açılan oturum:
1. **Bu dosyayı oku** (kullanıcı yönlendirir veya auto-context surface eder)
2. "Yarın ilk yapılacak" bölümünden başla
3. Yeni iterasyon başlarken commit'i tamamla, SW cache bump'la, bu dosyaya not düş
