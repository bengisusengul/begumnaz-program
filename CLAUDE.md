# CLAUDE.md — Project Context Summary

Bu doküman Claude Code'un bu repo'da çalışırken bilmesi gereken kritik bilgileri içerir.

## Ana Çerçeve

Begümnaz için kişiselleştirilmiş sağlık programı. Multi-agent sentez (mevcut plan dosyası → konu klasörlerine dağıtılmış SYNTHESIS dosyaları + uzman ajan perspektifleri) + tek dosyalık PWA (`index.html`).

**Begümnaz profili**:
- 27 yaş kadın, Türkiye
- Endometriozis (ameliyat sonrası Visanne tamamlandı)
- Post-isotretinoin hassas cilt (8 ay × 40 mg Zoretanin, etki etmedi)
- 3× akne+scar mezoterapi (en yenisi Mart 2026)
- Hormonal jawline akne (endo flare ile koreleli)
- Doktor protokolü: 16 ürün bütüncül tıp + mizaç temelli diyet + yaşam protokolü

## Kritik Kurallar

### 1. Doktor protokolü dışına ÇIKMA
Doktor 21.04.2026 kan paneli görerek 16 ürünlük protokolü yazdı. **Ek supplement / takviye / tarama önerme**. Selenyum/Brazil cevizi, MM-12 içeriği sorgulaması, hemokromatozis taraması gibi öneriler doktor tarafından zaten değerlendirildi.

**Sadece 3 soru doktora gitti, cevap bekleniyor** (ablası iletecek):
- NADH dozu
- NAC tek/iki seferli
- Probiyotik markası

Bu 3 cevap geldiğinde plan + ilgili SYNTHESIS dosyaları güncellenir.

### 2. Acnelyse = Tretinoin (retinol değil)
Reçeteli retinoid. Hassas ciltte 2x/hafta sandwich tekniği. AHA/Vit C aynı gece bindirme YASAK. Mezoterapi öncesi 5 gün kes.

### 3. Tret + Gym esnek kuralı
Gym sabit gün yok. Tret günleri Sal + Paz (düşük aktivite akşamları). Çar + Cum 18:00 pilates dersi akşamları **bariyer** günleri (tret YASAK). Yoğun terleme/duş sonrası tret skip.

### 4. Acıkana kadar kahvaltı bekle
Doktor talimatı: Uyanış 08:00, kahvaltı SAAT vermedi, acıkma sinyaline göre (genelde 09:00-11:00). Supplement saat çizelgesi bu esnekliğe göre.

### 5. Egzersiz switch sistemi
Her ağırlık/kardiyo gün için Ev (2-3 kg DB + bant + magic circle + pilates topu + mat) / Dışarı (yürüyüş + park) / Gym (tam erişim) alternatifi. Çar + Cum 18:00 pilates dersi sabit (Begümnaz öğrencisiyle).

### 6. Sıcak su mecbur
Doktor protokolünde **soğuk su YASAK**. Günde 5+ bardak ılık/sıcak su, cam termos, plastik yok. Tüm içecekler sıcak (gül+zeytin yaprağı, aynı safa, melissa+papatya — sadece bu 3 çay izinli).

### 7. Yasaklar 17 madde
Pirinç (jasmin/basmati hariç haşlama), beyaz un, tatlı içecek, hazır gıda, salam-sosis-sucuk, **dana eti, tavuk**, dondurma, soğuk su, **çiğ sebze**, **süt ürünleri**, karabiber-acıbiber, salça, büyük dip balık, çay-kahve (siyah/yeşil), yer fıstığı, **patlıcan**. İzinli protein: kuzu/koyun/hindi 3x/hafta.

### 8. Cycle awareness (endo özel)
Menstrüel 1-5: aktif iyileşme. Foliküler 6-12: peak antrenman. Ovulasyon 13-15: heavy. Luteal erken 16-22: sürdür. Luteal geç PMS 23-28: %20-30 düşür. **Endo flare** (faz fark etmez): 24-48 saat downshift + heating pad + ekstra ayak banyosu.

## Klasör Yapısı

```
skin-ultimate/        — Cilt (Begümnaz'ın #1 önceliği)
supplements-ultimate/ — 16 ürün doktor reçetesi
workout-ultimate/     — Egzersiz programı
diet-ultimate/        — Mizaç temelli beslenme
lifestyle-ultimate/   — Ayak banyosu + sıcak vücut + ıtır + uyku + saç
medical-documents/    — Kan testleri + cilt fotoları + body + period
```

Tüm klasörlerde `SYNTHESIS.md` (master sentez) + alt detay dosyaları + `agent-XX-*.md` uzman perspektifleri.

## PWA Mimarisi

**Tek dosya `index.html`** (~9700 satır, Bengisu reposundan adapte). Backend yok, framework yok. Vanilla JS + inline CSS. localStorage'da ~30+ key.

**7 sekme**: Dashboard, Cycle, Supplements (Begümnaz için yeni), Diet, Workout, Skin, Measurements.

**Cycle engine**: 3 helper fonksiyon (faz tespit, log durumu, PMS pencere). Diet macro hedefleri, skincare rotation, workout şiddet ayarı bu motora bağlı.

**Profile system**: Çoklu profil arşivleme (Bengisu reposundan miras kaldı, korunur).

**AI integration**: Anthropic API direkt veya Cloudflare Worker proxy üzerinden. 9 AI çağrısı (Recipe, Food analysis, Health Photo, Skin Photo comparison, Apple Health screenshot OCR vs.).

## Geliştirme Kuralları (PWA)

- Tüm değişiklikler `index.html`'de (sw.js, manifest.json, cloudflare-worker.js istisna)
- Buton onayları kullan (`confirm()` dialog yok)
- iOS Safari'de manuel test
- Her sürümde service worker cache versiyon güncelle
- Her AI prompt'unda cycle context + remaining macros ekle
- Yeni localStorage key'leri `BACKUP_KEYS` whitelist'e ekle

## Temel Referans

**Önce `PROGRESS.md`** oku — repo durumu, commit geçmişi, localStorage keys, bekleyen kararlar, teknik mimari.

**Sonra ilgili klasörün `SYNTHESIS.md`** oku — o konunun master sentezi.

## Source-of-Truth

`/Users/agent9/.claude/plans/haftalik-program-olarak-kardesim-golden-clarke.md` — Begümnaz programının tam içerik kaynağı. Bu repo'daki SYNTHESIS dosyaları buradan üretildi. Değişiklik olursa önce orada güncellenir, sonra repo'ya yansıtılır.
