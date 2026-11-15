# 🛡️ AERO-SHIELD
### Mikro Yerçekimi Anomali ve Yapay Zekâ Tabanlı Yangın Tahmin Matrisi

![NASA Space Apps Challenge 2026](https://img.shields.io/badge/NASA_Space_Apps_Challenge-2026-blue?style=for-the-badge&logo=nasa)
![Kategori](https://img.shields.io/badge/Kategori-Flame_in_Free_Fall-orange?style=for-the-badge)
![Takım](https://img.shields.io/badge/Takım-ARGE_EĞİTİMCİLERİ-success?style=for-the-badge)
![Mimari](https://img.shields.io/badge/Edge_JS-Offline_&_Otonom-lightgrey?style=for-the-badge)

> **"Erken Farkındalık. Daha Güvenli Uzay Görevleri."**  
> Yardımın günler uzakta olduğu derin uzay görevlerinde (Artemis, Lunar Gateway, Mars) kazanılan her saniye mürettebatı korur[cite: 14].

---

## 🚀 Proje Hakkında

**AERO-SHIELD**, mikro yerçekimi ortamlarında (uzay istasyonları, derin uzay kapsülleri ve gezegenler arası yaşam alanları) meydana gelebilecek görünmez ve yavaş ilerleyen yangınları duman oluşumunu beklemeden tespit etmek amacıyla geliştirilmiş **çevrimdışı, otonom ve çoklu sensör füzyonuna dayalı** bir erken uyarı ve izolasyon sistemidir[cite: 8, 9, 11, 12].

---

## 01 / Gerçek Problem: Uzayda Alevler Görünmez Yanar

Dünya'daki yerçekimi kaynaklı konveksiyon akımları uzayda bulunmadığı için yangın dinamikleri tamamen farklı işler[cite: 9]:

* **Küresel ve Yavaş Alev:** Sıcak gaz yükselmez; duman ve ısı tavan dedektörlerine çok geç ulaşır[cite: 9].
* **Görünmez Soğuk Alevler:** 500–800 K sıcaklık bandında issiz ve çıplak gözle görülemeyecek şekilde yanar; klasik optik dedektörler bu duruma karşı kör kalır[cite: 9, 13].
* **Zehirli Gaz Riski:** Görünür alev sönse bile yanma reaksiyonu devam ederek kabin içine karbonmonoksit ($CO$) ve formaldehit gibi ölümcül gazlar yayar[cite: 9].

---

## 02 / Bilimsel Temel ve NASA Veri Kalibrasyonu

Sistemin karar eşikleri ve anomali modelleri, **30 TB Açık NASA PSI (Physical Sciences Informatics)** veri tabanındaki gerçek uçuş deneyleriyle kalibre edilmiştir[cite: 10]:

| Parametre / Veri Kaynağı | Değer / Standart | Açıklama |
| :--- | :--- | :--- |
| **ACME Deneyi** | ~1.500 | ISS üzerinde yakılan deney alevi verileri[cite: 10] |
| **FLEX Deneyi** | 500 - 800 K | Görünmez soğuk alev sıcaklık eşikleri[cite: 10] |
| **NASA-STD-3001** | 3 mmHg | ISS saatlik maksimum $CO_2$ güvenlik sınırı[cite: 10] |
| **Saffire & PSI** | 30 TB Veri | Katı yakıt yangın yayılımı ve kabin güvenlik modellemesi[cite: 10, 13] |

---

## 03 / Çözüm Mimarisi: Çoklu Sensör Füzyonu

AERO-SHIELD, dumanın sensöre ulaşmasını beklemek yerine üç bağımsız fiziksel sinyali eşzamanlı analiz ederek anlık bir **Risk Skoru ($R$)** hesaplar[cite: 11]:

1. **IR Termal Isınma (%40 Ağırlık):** Görünmez soğuk alevlerin yaydığı düşük yoğunluklu termal radyasyonu ve yüzey ısınmasını yakalar[cite: 11].
2. **Gaz Gradyanı (%35 Ağırlık):** Kabin içi oksijen ($O_2$) tüketimini ve $CO / CO_2$ konsantrasyon artış hızını ölçer[cite: 11].
3. **Lazer Partikül Algılama (%25 Ağırlık):** Aşırı ısınan elektronik devrelerden ve Kapton kablolardan çıkan mikro partikülleri anında saptar[cite: 11, 13].

---

## 04 / Teknoloji ve Uç İşleme (Edge JS Mimarisi)

Sistem, harici bir sunucuya veya Dünya ile iletişime ihtiyaç duymadan **düşük donanımlı uç düğümlerde (Edge Nodes)** sıfır bağımlılıkla saniyeler içinde otonom karar üretir[cite: 12]:

```text
[ ADIM 01: Sensör Okuma ] ──► IR termal, gaz gradyanı ve lazer partikül verileri toplanır.
         │
         ▼
[ ADIM 02: Risk Hesaplama ] ──► R ≥ 45: DİKKAT Uyarısı | R ≥ 75: KRİTİK Alarm[cite: 12]
         │
         ▼
[ ADIM 03: Otomatik İzolasyon ] ──► Kritik eşikte kabin oksijen/gaz akışı ve havalandırma anında kesilir.[cite: 12]
