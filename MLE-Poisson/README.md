# MLE ile Akilli Sehir Planlamasi

Bu klasor, Poisson dagilimi kullanilarak trafik yogunlugu verisi uzerinde Maximum Likelihood Estimation (MLE) uygulanmasi icin hazirlanan odev teslimini icerir.

## Icerik

- `mle_poisson.ipynb`: Python ile gorsellestirme ve outlier analizi, Notebook formatinda duzenlenmis cozum
- `report/rapor.pdf`: Odev raporunun PDF surumu
- `report/poisson_fit_original.png`: Orijinal veri seti icin histogram + Poisson PMF grafigi
- `report/poisson_fit_outlier.png`: Outlier eklendikten sonraki histogram + Poisson PMF grafigi

## Odev Ozeti

Bu calismada 1 dakikada gecen arac sayisini modellemek icin Poisson dagilimi kullanilmistir. Amac, trafik yogunlugu parametresi olan `lambda` degerini MLE ile tahmin etmektir.

Calisma su adimlari kapsar:

1. Poisson likelihood ve log-likelihood fonksiyonunun teorik turetilmesi
2. `scipy.optimize.minimize` ile sayisal MLE hesabi
3. Gercek veri histogrami ile Poisson PMF grafiginin karsilastirilmasi
4. Veri setine `200` degerli bir outlier eklenerek MLE hassasiyetinin incelenmesi

## Kullanilan Veri

Orijinal trafik verisi:

```python
[12, 15, 10, 8, 14, 11, 13, 16, 9, 12, 11, 14, 10, 15]
```

## Sonuclar

- Analitik MLE: `12.142857`
- Sayisal MLE: `12.142857`
- Outlier sonrasi MLE: `24.666667`

Sonuclar, Poisson dagiliminda MLE tahmininin ornek ortalamasina esit oldugunu ve aykiri degerlere duyarli oldugunu gostermektedir.

## Calistirma

Gerekli kutuphaneler:

- `numpy`
- `scipy`
- `matplotlib`

Scripti calistirmak icin:

```bash
jupyter notebook mle_poisson.ipynb
```
