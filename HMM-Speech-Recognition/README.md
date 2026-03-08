Projede Hidden Markov Model kullanılarak basit bir izole kelime tanıma sistemi tasarlanmıştır. Amaç, verilen bir gözlem dizisinin hangi kelimeye daha uygun olduğunu belirlemektir. Çalışmada iki farklı kelime için ayrı HMM modelleri oluşturulmuş ve yeni gelen test verisinin hangi modele daha yüksek olasılık verdiği incelenmiştir.

## Veri

Projede gerçek ses kaydı yerine temsili gözlem dizileri kullanılmıştır. Gözlemler iki sembol ile ifade edilmiştir:

- `0 = Low`
- `1 = High`

Bu semboller, ses sinyalinden elde edilebilecek basitleştirilmiş akustik özellikleri temsil etmektedir.

Testlerde kullanılan örnek gözlem dizileri şunlardır:

- `[1, 0]`
- `[1, 1, 0, 0]`
- `[1, 0, 1, 0]`

## Yöntem

Projede `hmmlearn` kütüphanesi kullanılarak iki ayrı HMM modeli tanımlanmıştır:

- `EV` kelimesi için 2 durumlu model
- `OKUL` kelimesi için 4 durumlu model

Her model için şu parametreler belirlenmiştir:

- başlangıç olasılıkları
- durum geçiş olasılıkları
- emisyon olasılıkları

Daha sonra her test verisi için her iki modelin log-likelihood skoru hesaplanmıştır. Daha yüksek skor üreten model, test dizisine daha uygun kabul edilmiştir.

## Sonuçlar

Uygulama sonucunda test verileri her iki model üzerinde değerlendirilmiş ve log-likelihood puanları karşılaştırılmıştır. Bu karşılaştırma sayesinde her test dizisinin `EV` veya `OKUL` kelimesinden hangisine daha yakın olduğu belirlenmiştir.

Elde edilen sonuçlar, HMM yaklaşımının küçük ve kontrollü örneklerde temel sınıflandırma mantığını göstermede yararlı olduğunu göstermiştir.

Çalışma, gerçek konuşma tanıma sisteminin basitleştirilmiş bir simülasyonudur. Gerçek sistemlerde doğrudan `Low` ve `High` gibi semboller yerine ses sinyalinden çıkarılan daha karmaşık özellikler kullanılır. Ayrıca gerçek verilerde gürültü, konuşmacı farklılığı ve kelime çeşitliliği gibi etkenler sistemin performansını etkiler.


