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
- Feature engineering (`rooms_per_household`, `bedrooms_per_room`, `population_per_household`)
- One-Hot Encoding (`ocean_proximity`)
- Korelasyon tabanlı feature selection
- Train / Validation / Test ayrımı (%70 / %15 / %15)
- StandardScaler (yalnızca training verisi üzerinde fit edilmiştir)
- 5-fold Cross-Validation
- GridSearchCV ile hiperparametre ayarlama

## Kullanılan Modeller
- Linear Regression
- Ridge Regression
- Random Forest Regressor

## Model Karşılaştırması

Validation veri seti üzerinde modellerin performansı:

| Model | MAE | RMSE | R² |
|---|---:|---:|---:|
| Linear Regression | 47.399,98 | 64.300,31 | 0,58 |
| Ridge | 47.391,73 | 64.288,14 | 0,58 |
| Random Forest | 38.418,87 | 54.800,13 | 0,70 |

Validation sonuçlarına göre en başarılı model Random Forest Regressor olmuştur.

## Hiperparametre Ayarlama

Random Forest modeli için `GridSearchCV` kullanılarak hiperparametre optimizasyonu yapılmıştır.

**En iyi parametreler:**

- `max_depth`: None
- `min_samples_leaf`: 2
- `n_estimators`: 100

**En iyi CV RMSE:** 54.742,67

## En İyi Model

**Random Forest Regressor**

Final test veri seti üzerindeki sonuçlar:

- **Test MAE:** 38.740,33
- **Test MSE:** 3.039.053.211,81
- **Test RMSE:** 55.127,61
- **Test R²:** 0,6895

En önemli öznitelikler:

- `median_income`
- `ocean_proximity_INLAND`
- `latitude`

## Sonuç

Random Forest, doğrusal modellere kıyasla gelir ve konum gibi değişkenler arasındaki doğrusal olmayan ilişkileri daha iyi yakalayarak belirgin şekilde daha iyi performans göstermiştir.

Modelin R² değeri 0,6895 olduğundan, test verisindeki ev fiyatlarındaki değişimin yaklaşık %69'unu açıklayabildiği görülmektedir. Kalan açıklanamayan kısım; veri setinde bulunmayan konut kalitesi, yenilenme durumu ve benzeri faktörlerden kaynaklanabilir.

## Kurulum
```bash
git clone https://github.com/Hayrunnisa64/ev_fiyat-_tahmini.git
cd ev_fiyat-_tahmini
pip install -r requirements.txt
```

## Çalıştırma
1. `ev_fiyati_tahmini_final_odev (2).ipynb` dosyasını Jupyter Notebook, VS Code veya Google Colab ile açın.
2. Tüm hücreleri baştan sona sırayla çalıştırın (Colab: Çalışma Zamanı → Tümünü Çalıştır).
3. İnternet bağlantısı gereklidir (veri seti otomatik indirilir).

## Kullanılan Kütüphaneler
pandas, numpy, matplotlib, seaborn, scikit-learn
