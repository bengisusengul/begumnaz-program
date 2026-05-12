# PWA Adaptation TODO — Bengisu → Begümnaz

> Phase 2 başladı. Bu doküman tamamlanması gereken adaptasyon işlerini listeler.

## ✅ Tamamlanan (Faz 2 — Bu Commit)

- ✅ `manifest.json` — "Bengisu Program" → "Begümnaz Program", description Begümnaz'ın tıbbi tablosuna güncellendi
- ✅ `sw.js` — Cache name: `bengisu-v9-...` → `begumnaz-v1-2026-05-12`
- ✅ `cloudflare-worker.js` — Yorum + auth header: `x-bengisu-token` → `x-begumnaz-token`
- ✅ `HEALTH_SHORTCUT.md` — Bengisu Program → Begümnaz Program
- ✅ `DEPLOY-API-PROXY.md` — Tüm Bengisu/bengisu/bengisusengul referansları → Begümnaz/begumnaz/begumnazsengul
- ✅ `bg.jpeg` — Background image (Bengisu repodan kopyalandı; gelecekte Begümnaz tercihiyle değişebilir)
- ✅ `index.html` — Global find-replace: "Bengisu/bengisu" → "Begümnaz/begumnaz" (768 KB dosya, başlık/meta/title hepsi güncellendi)

## 🚧 Hala Yapılması Gereken (Önemli + Büyük)

### 1. Bengisu-spesifik Tıbbi Verilerin Temizliği

`index.html` içinde hala Bengisu'nun tıbbi geçmişi referansları var:

| Terim | Adet | Aksiyon |
|---|---|---|
| **Levotiron** | 74 | Sil veya Begümnaz'ın 16 ürün protokolüne değiştir |
| **Calciday** | 37 | Sil |
| **tiroidektomi** | 24 | Sil/Endo'ya değiştir |
| **FH** (Familial Hypercholesterolemia) | 16 | Sil |
| **Hakan Bey** (Bengisu'nun doktoru) | 15 | Sil veya "fonksiyonel tıp doktoru" |
| **Hashimoto** | 15 | Sil |
| **hipopara** (hipoparatiroidi) | 13 | Sil |
| **Calcitriol** | 12 | Sil |
| **papiller** (papiller karsinom) | 4 | Sil |
| **NHS** | 1 | Sil/Türkiye e-nabız ile değiştir |

**Toplam ~211 referans manuel adaptasyon gerekir**.

### 2. Sekme Eklenmesi: Supplements

Bengisu'da 6 sekme: Dashboard, Cycle, Diet, Exercise, Skin, Measurements.

Begümnaz için **+1 sekme**: **Supplements** (16 ürün saat çizelgesi + reminder).

İhtiyaç:
- HTML tab UI (yeni `<button data-tab="supplements">`)
- JS tab logic (`switchTab('supplements')`)
- Tab content (16 ürün listesi + saat hatırlatıcı)
- localStorage key (`supplement_log`)
- AI integration (opsiyonel — Anthropic'a "bugünkü supplement durumu" sorma)

### 3. Begümnaz Verisi Entegrasyonu

#### A. Cycle Sekmesi — Endo Flare Awareness
- Bengisu'nun cycle engine korunur
- Endo flare logger eklenir (kullanıcı "endo flare" check ettiğinde 24-48 saat downshift uyarısı)
- Period takip standart

#### B. Diet Sekmesi — Mizaç Temelli + Yasak Listesi
- Bengisu'nun "Modifiye Akdeniz-Karnivor" diyeti → Begümnaz'ın "Mizaç temelli + 17 madde yasak + izinli liste"ye değişir
- Yasak ürün ekleme uyarısı (örn. süt, dana, tavuk, patlıcan, çiğ sebze)
- İzinli protein 3x/hafta (kuzu/koyun/hindi)

#### C. Exercise Sekmesi — 3 Ağırlık + 2 Pelvik Taban + 2 Pilates + Yürüyüş
- Bengisu'nun "5-day strength split" → Begümnaz'ın yeni şeması
- Pelvik taban video havuzu eklenir (Move with Nicole, Pahla B, vs.)
- Full Body Pilates dersi sabit zaman (Çar+Cum 18:00)
- Cycle-aware yoğunluk ayarı

#### D. Skin Sekmesi — Begümnaz Cilt Aktif Takibi
- Bengisu'nun cilt yaklaşımı → Begümnaz'ın "Bariyer-önce + 8 haftalık aşamalı plan"
- Tret günleri sabit (Sal + Paz)
- AHA günü (Per)
- Esnek tret kuralı (gym/yoğun terleme şift)
- Cilt foto karşılaştırma + AI analiz

#### E. Measurements Sekmesi — Begümnaz Antropometri + Kan Değerleri
- Bengisu'nun 76→62 kg hedefi → kaldırılır (Begümnaz'ın hedefi tanımlanmadı, manuel girilir)
- Kan değerleri trend (21.04.2026 paneli + gelecek paneller)
- Vücut ölçüleri standart

### 4. AI Sistem Prompt'ları Güncellemesi

Bengisu'nun AI çağrılarında system prompt'lar Bengisu'nun tıbbi profilini içeriyor. Bu prompt'lar Begümnaz'a göre yeniden yazılmalı:
- Recipe AI → "Mizaç temelli + 17 madde yasak + izinli liste, sıcak su mecbur"
- Food Analysis AI → "Yasak gıdalardan kaçınma + makro hedef"
- Skin Photo AI → "Post-iso bariyer + PIE/PIH değerlendirme + Acnelyse tret uyumu"
- Apple Health AI → Aynı (Bengisu = Begümnaz aynı şekilde okur)

### 5. localStorage Keys Temizliği

Bengisu PWA localStorage'da Bengisu-spesifik veriler:
- `medication_log` (Levotiron/Calciday/Calcitriol)
- `weight_log` (76kg start)
- `cycle_log`
- vs.

Begümnaz için **yeni başlangıç state** — Bengisu'nun verisi taşınmaz. Localde clean install önerilir.

### 6. CSS / Branding (Opsiyonel)

Bengisu "Akşam Bahçesi" paleti — koyu yeşil/krema/mercan. Begümnaz için:
- **Aynı bırakılabilir** (kullanıcı sevdi)
- **Değiştirilebilir** (Begümnaz tercihiyle — örn. lila/pembe/mavi tonları)

Şu an aynı palet. Begümnaz/abla istediğinde değiştiririz.

### 7. Apple Health Entegrasyonu

Bengisu'nun Apple Health screenshot + JSON entegrasyonu kalıyor. Begümnaz için:
- iOS kullanıyor mu?
- Apple Health verisi takip ediyor mu?
- Eğer evet → aynı sistem çalışır
- Eğer hayır → manuel ölçü girer; sekme yine var

## 📋 Önerilen Sıra (Sonraki Iterasyonlar)

1. **Iterasyon 1**: Bengisu medikal terim temizliği (211 referans → 0)
2. **Iterasyon 2**: Diet sekmesi Begümnaz'a uyarlama (mizaç + yasak liste)
3. **Iterasyon 3**: Exercise sekmesi yeniden yapılandırma
4. **Iterasyon 4**: Skin sekmesi adaptasyonu
5. **Iterasyon 5**: Measurements sekmesi
6. **Iterasyon 6**: Supplements sekmesi (yeni — 16 ürün)
7. **Iterasyon 7**: AI prompt'lar
8. **Iterasyon 8**: Test + iOS Safari PWA install + bug fix

Her iterasyon **1-2 saat** + test. Toplam **~15-20 saat** PWA adaptasyon emek.

## 🚨 Şu Anki Durum

PWA **çalışmaya hazır** ama içerik **Bengisu'nun tıbbi verisiyle**. Begümnaz/abla şimdi açıp denerse:
- Title: "Begümnaz ☀️" ✓
- App ikon: "Begümnaz" ✓
- AMA içeride: Bengisu'nun ilaç listesi, tiroid bilgisi, NHS UK verileri görür

**Bu yüzden iterasyon 1-5 acil**, ondan sonra Begümnaz kullanmaya başlayabilir.

## 🔗 İlgili

- [`README.md`](README.md) — Repo overview
- [`PROGRESS.md`](PROGRESS.md) — Genel ilerleme
- [`CLAUDE.md`](CLAUDE.md) — AI agent context
- Source-of-truth: `/Users/agent9/.claude/plans/haftalik-program-olarak-kardesim-golden-clarke.md`
