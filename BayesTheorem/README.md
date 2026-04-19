# YZM212 - Bayes Theorem

Projede gürültülü astronomik gözlem verileri kullanılarak bir gök cisminin gerçek parlaklığı ve gözlem hatası Bayesyen çıkarım yöntemiyle tahmin edilmiştir. Posterior dağılımdan örnekleme yapmak için Markov Chain Monte Carlo (MCMC) yaklaşımı ve `emcee` kütüphanesi kullanılmıştır.

## Dosyalar

- `src/bayes.ipynb`: çalıştırılmış analiz notebook'u
- `report/bayes_report.pdf`: ödev raporu

## Veri

Veri sentetik olarak normal dağılımdan üretilmiştir.

- Gerçek parlaklık: `true_mu = 150.0`
- Gerçek gözlem hatası: `true_sigma = 10.0`
- Gözlem sayısı: `n_obs = 50`
- Rastgelelik için `seed = 42` kullanılmıştır.

Üretilen veri için örnek ortalaması yaklaşık `147.745`, örnek standart sapması ise yaklaşık `9.337` bulunmuştur.

## Yöntem

Modelde iki parametre tahmin edilmiştir:

- `mu`: ortalama parlaklık
- `sigma`: gözlem hatasının standart sapması

Likelihood normal dağılım varsayımıyla kurulmuştur. Parametreler için geniş prior aralıkları kullanılmıştır:

- `0 < mu < 300`
- `0 < sigma < 50`

MCMC ayarları:

- Walker sayısı: `32`
- Adım sayısı: `2000`
- Burn-in: `500`
- Thinning: `15`

## Ana Sonuçlar

| Değişken | Gerçek Değer | Tahmin Edilen Median | Alt Sınır (%16) | Üst Sınır (%84) | Mutlak Hata |
|---|---:|---:|---:|---:|---:|
| `mu` (Parlaklık) | 150.0 | 147.728 | 146.385 | 149.053 | 2.272 |
| `sigma` (Hata Payı) | 10.0 | 9.503 | 8.614 | 10.618 | 0.497 |

Ana deneyde posterior örnek sayısı `3200`, ortalama kabul oranı ise yaklaşık `0.712` olarak elde edilmiştir. Sonuçlar gerçek değerlere yakın çıkmıştır. `mu` değerinin 150'nin biraz altında tahmin edilmesi, üretilen veri setinin örnek ortalamasının da 150'nin altında olmasından kaynaklanmaktadır.

## Ek Deneyler

Prior etkisini incelemek için `mu` parametresi dar ve hatalı bir aralığa, `100 < mu < 110`, sınırlandırılmıştır. Bu durumda `mu` tahmini yaklaşık `109.440` değerine sıkışmış, `sigma` tahmini ise yaklaşık `40.286` değerine yükselmiştir. Bu sonuç yanlış prior seçiminin posterior tahminlerini ciddi biçimde bozabileceğini göstermektedir.

Veri miktarının etkisini görmek için gözlem sayısı `n_obs = 5` yapılmıştır. Bu durumda `mu` için 68% aralık genişliği `2.668` değerinden `8.395` değerine, `sigma` için ise `2.004` değerinden `8.109` değerine çıkmıştır. Yani gözlem sayısı azaldığında posterior belirsizliği belirgin şekilde artmıştır.

## Grafikler

Notebook çalıştırıldığında aşağıdaki grafikler `figures/` klasörüne kaydedilmiştir:

- `01_sentetik_veri_histogram.png`
- `02_trace_plot_ana_deney.png`
- `03_corner_plot_ana_deney.png`
- `04_prior_etkisi_karsilastirma.png`
- `05_veri_miktari_karsilastirma.png`
- `06_corner_plot_n_obs_5.png`

## Çalıştırma

Gerekli paketler:

```python
numpy
pandas
matplotlib
emcee
corner
```

Eksik paket varsa Jupyter içinde şu komut çalıştırılabilir:

```python
%pip install numpy matplotlib pandas emcee corner
```

Analizi yeniden üretmek için `bayes.ipynb` dosyası baştan sona çalıştırılabilir.
