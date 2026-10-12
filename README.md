# İstanbul Ev Fiyatı Tahmini

Satılık konut ilanlarından bir evin fiyatını özelliklerine bakarak tahmin eden bir model.

> **Durum:** Veri temizliği sürüyor. Model, sonuç ve eksikler bölümleri proje ilerledikçe dolacak.

## Veri

- Kaynak: [Kaggle – House Price Dataset](https://www.kaggle.com/datasets/aselasel/house-price-dataset). Bir emlak ilan sitesinden Mart 2022'de toplanmış, ön işleme yapılmamış ilan verisi.
- İstanbul'un 39 ilçesinden 25.155 satılık konut ilanı, 37 sütun.
- İlanların son güncellenme tarihi Eylül 2021 ile Mart 2022 arasında; fiyatlar o dönemin fiyatları.

## Veri temizliği

Her madde aynı sırayı izliyor: sorun ne, ne yaptım, düzeldiğini nasıl anladım.

- **Fiyat:** Fiyatlar `3,100,000TL` biçiminde metin olarak geliyor. 1333 ilanda sitedeki indirim rozetinin metni fiyata yapışmış: `34,550,000TLarrow_downward%3`. Sondaki `%3` indirim oranı, fiyatın parçası değil. Bu yüzden `TL`'den önceki kısmı alıp virgülleri sildim ve sayıya çevirdim. İki biçim için de test yazdım.
- **Metrekare** (brüt, net, hol, WC, banyo, balkon): Değerler `160 m2` biçiminde metin. Burada nokta ondalık değil, binlik ayırıcı: `2.250 m2` aslında 2250 m². Doğrudan sayıya çevrilince 2,25 m² okunuyor; bu, brüt alanda 246, net alanda 140 ilanı etkiliyor. Noktaları silip çevirdim. Noktalı 387 değerin hepsinde noktadan sonra tam üç rakam geldiğini kontrol ettim, yani ondalıklı metrekare yok. İlk versiyonumda bu hata vardı ve 105 ilanda net alan brütten büyük görünüyordu; düzeltmeden sonra hiç yok.

## Model

_Eklenecek._

## Sonuç

_Eklenecek._

## Bildiğim eksikler

- Fiyatlar 2021-2022'ye ait. Aradaki enflasyon yüzünden model bugünkü fiyatları tahmin etmek için kullanılamaz.
- Metrekare temizliği bu verinin biçimine göre yazıldı. Ondalıklı metrekare içeren bir veride kontrol hata verir.
- Fiyatlar ilanlarda istenen fiyatlar, gerçekleşen satış fiyatları değil.