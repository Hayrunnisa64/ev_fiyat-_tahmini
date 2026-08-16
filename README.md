# Ev Fiyat Tahmini

## Proje Amacı
Kaliforniya'daki mahallelere ait demografik ve coğrafi özelliklerden (gelir, konum, hane büyüklüğü vb.) yola çıkarak bölgedeki evlerin medyan satış fiyatını (`median_house_value`) tahmin eden uçtan uca bir regresyon projesi.

## Veri Seti
**California Housing Prices** veri seti kullanılmıştır (1990 ABD nüfus sayımı verilerinden türetilmiştir, 20.640 satır). Veri seti kod içinde aşağıdaki adresten otomatik olarak indirilir, ayrıca dosya indirmeye gerek yoktur:

`https://raw.githubusercontent.com/ageron/handson-ml2/master/datasets/housing/housing.csv`

Hedef değişken: `median_house_value` (mahalledeki evlerin medyan fiyatı, USD).

## Kullanılan Yöntemler
- Eksik değer analizi ve doldurma (medyan)
- Aykırı değer incelemesi (IQR, boxplot)
- Feature engineering (rooms_per_household, bedrooms_per_room, population_per_household)
- One-Hot Encoding (`ocean_proximity`)
- Korelasyon tabanlı feature selection
- Train / Validation / Test ayrımı (%70 / %15 / %15)
- StandardScaler (yalnızca training verisi üzerinde fit edilerek, veri sızıntısı önlenmiştir)
- 5-fold Cross-Validation
- GridSearchCV ile hiperparametre ayarlama

## Kullanılan Modeller
- Linear Regression
- Ridge Regression
- Random Forest Regressor

## Model Karşılaştırması
| Model | MAE | RMSE | R² |
|---|---|---|---|
| Linear Regression | 47.399,98 | 64.300,31 | 0,58 |
| Ridge | 47.391,73 | 64.288,14 | 0,58 |
| Random Forest | 38.418,87 | 54.800,13 | 0,70 |

## En İyi Model
**Random Forest Regressor**
- Test MAE: 38.740,33
- Test RMSE: 55.127,61
- Test R²: 0,6895

En önemli öznitelikler: `median_income`, `ocean_proximity_INLAND`, `latitude`.

## Sonuç
Random Forest, doğrusal modellere kıyasla gelir ve konum gibi değişkenler arasındaki doğrusal olmayan ilişkileri daha iyi yakalayarak belirgin şekilde daha iyi performans göstermiştir. Model, fiyat değişiminin yaklaşık %69'unu açıklayabilmektedir; kalan kısım veri setinde bulunmayan etkenlerden (konut kalitesi, yenilenme durumu vb.) kaynaklanmaktadır.

## Kurulum
```bash
git clone <repo-linki>
cd <repo-klasoru>
pip install -r requirements.txt
```

## Çalıştırma
1. `ev_fiyati_tahmini_final_odev.ipynb` dosyasını Jupyter Notebook, VS Code veya Google Colab ile açın.
2. Tüm hücreleri baştan sona sırayla çalıştırın (Colab: Çalışma Zamanı → Tümünü Çalıştır).
3. İnternet bağlantısı gereklidir (veri seti otomatik indirilir).

## Kullanılan Kütüphaneler
pandas, numpy, matplotlib, seaborn, scikit-learn
