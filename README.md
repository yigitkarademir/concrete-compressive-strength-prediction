# Beton Basınç Dayanımı Tahmini

Bu proje, betonun karışım bileşenlerine ve yaşına bağlı olarak basınç dayanımını tahmin etmeyi amaçlayan bir makine öğrenmesi regresyon çalışmasıdır. Random Forest ve XGBoost modelleri kurulup karşılaştırılarak en başarılı model belirlenmiştir.

## Proje Hakkında

Beton basınç dayanımının doğru tahmin edilmesi, inşaat sektöründe yapı güvenliği ve tasarım güvenilirliği açısından önemlidir. Bu projede veri seti tamamen sürekli sayısal değişkenlerden oluştuğu için regresyon problemine uygun bir zemin sunmaktadır.

Yapılan keşifsel veri analizinde bağımsız değişkenler ile hedef değişken arasında doğrusal olmayan, karmaşık ilişkiler gözlemlenmiş, VIF analizinde ise bazı değişkenler arasında çoklu doğrusallık tespit edilmiştir. Bu nedenle hem çoklu bağlantı problemlerinden etkilenmeyen hem de doğrusal olmayan ilişkileri yakalayabilen ağaç tabanlı modeller (Random Forest ve XGBoost) tercih edilmiştir.

## Kullanılan Veri Seti

Veri seti, betonun karışımındaki bileşenleri ve yaşını içeren 1030 gözlemden oluşmaktadır:

| Değişken | Açıklama |
|---|---|
| cement | Çimento miktarı |
| blast_furnace_slag | Yüksek fırın cürufu miktarı |
| fly_ash | Uçucu kül miktarı |
| water | Su miktarı |
| superplasticizer | Süper akışkanlaştırıcı miktarı |
| coarse_aggregate | İri agrega miktarı |
| fine_aggregate | İnce agrega miktarı |
| age | Betonun yaşı (gün) |
| concrete_compressive_strength | Beton basınç dayanımı (hedef değişken) |

## Kullanılan Yöntemler

- Veri ön işleme ve tekrarlayan kayıtların temizlenmesi
- Keşifsel veri analizi (dağılım grafikleri, scatter plotlar)
- Korelasyon analizi
- VIF (Variance Inflation Factor) ile çoklu doğrusallık kontrolü
- Random Forest ve XGBoost modelleri ile GridSearchCV kullanılarak hiperparametre optimizasyonu
- Model performans değerlendirmesi (R², RMSE, MAE)
- Feature importance analizi
- Gerçek ve tahmin edilen değerlerin karşılaştırılması
- Residual analizi

## Sonuçlar

| Model | Veri Seti | R² | RMSE | MAE |
|---|---|---|---|---|
| Random Forest | Train | 0.984 | 2.03 | 1.38 |
| Random Forest | Test | 0.906 | 5.30 | 3.64 |
| XGBoost | Train | 0.992 | 1.40 | 0.83 |
| XGBoost | Test | 0.941 | 4.21 | 2.76 |

XGBoost modeli, hem cross validation skorunda hem de test seti performansında Random Forest'a kıyasla daha başarılı sonuçlar vermiştir. Her iki modelde de **age** (beton yaşı) ve **cement** (çimento miktarı) değişkenleri, dayanımı belirleyen en önemli iki değişken olarak öne çıkmıştır. Bu sonuç, betonun kürlenme süresi arttıkça dayanımının artması ve çimentonun betonun temel bağlayıcı bileşeni olması gibi bilinen mühendislik gerçekleriyle örtüşmektedir.

## Kullanılan Kütüphaneler

- pandas, numpy
- matplotlib, seaborn
- statsmodels
- scikit-learn
- xgboost

## Dosya Yapısı

```
.
├── concrete_data.csv          # Veri seti
├── concrete_strength_model.ipynb   # Analiz ve modelleme notebook'u
└── README.md
```

## Nasıl Çalıştırılır

```bash
pip install pandas numpy matplotlib seaborn statsmodels scikit-learn xgboost
jupyter notebook concrete_strength_model.ipynb
```

## Geliştirme Fikirleri

- LightGBM veya CatBoost gibi farklı ağaç tabanlı modellerin denenmesi
- Stacking/ensemble yaklaşımlarının kullanılması
- Aykırı değer analizi yapılması
