# İstanbul Ev Fiyatı Tahmini

Satılık konut ilanlarından bir evin fiyatını özelliklerine bakarak tahmin eden bir model.

> **Durum:** Veri temizliği bitti, sırada özellikler ve model var. Model ve sonuç bölümleri proje ilerledikçe dolacak.

## Veri

- Kaynak: [Kaggle – House Price Dataset](https://www.kaggle.com/datasets/aselasel/house-price-dataset). Bir emlak ilan sitesinden Mart 2022'de toplanmış, ön işleme yapılmamış ilan verisi.
- İstanbul'un 39 ilçesinden 25.155 satılık konut ilanı, 37 sütun.
- İlanların son güncellenme tarihi Eylül 2021 ile Mart 2022 arasında; fiyatlar o dönemin fiyatları.

## Veri temizliği

Her madde aynı sırayı izliyor: sorun ne, ne yaptım, düzeldiğini nasıl anladım.

- **Fiyat:** Fiyatlar `3,100,000TL` biçiminde metin olarak geliyor. 1333 ilanda sitedeki indirim rozetinin metni fiyata yapışmış: `34,550,000TLarrow_downward%3`. Sondaki `%3` indirim oranı, fiyatın parçası değil. Bu yüzden `TL`'den önceki kısmı alıp virgülleri sildim ve sayıya çevirdim. İki biçim için de test yazdım.
- **Metrekare** (brüt, net, hol, WC, banyo, balkon): Değerler `160 m2` biçiminde metin. Burada nokta ondalık değil, binlik ayırıcı: `2.250 m2` aslında 2250 m². Doğrudan sayıya çevrilince 2,25 m² okunuyor; bu, brüt alanda 246, net alanda 140 ilanı etkiliyor. Noktaları silip çevirdim. Noktalı 387 değerin hepsinde noktadan sonra tam üç rakam geldiğini kontrol ettim, yani ondalıklı metrekare yok. İlk versiyonumda bu hata vardı ve 105 ilanda net alan brütten büyük görünüyordu; düzeltmeden sonra hiç yok.
- **Tekrar eden satırlar:** Veride birebir aynı 171 satır vardı. Aynı ilanın bir kopyası eğitim, diğeri test verisine düşerse model cevabı önceden görmüş olur ve başarısı olduğundan iyi görünür. Hepsini attım; ardından tekrar eden satır kalmadığını kontrol ettim.
- **Aykırı değerler:** Üç kural koydum:
  1. Brüt m² fiyatı 1.000–150.000 TL dışında kalan 160 ilan. Bunlar 120 m²'lik bir eve 16 milyar TL gibi giriş hataları.
  2. Brüt alanı netin 3 katından büyük 138 ilan. Bunlarda alanlardan biri yanlış girilmiş (73 m² net, 9720 m² brüt gibi).
  3. Brüt alanı 1.000 m²'den büyük 219 ilan. Bir kısmı 1 oda ya da 2+1 gibi alanla çelişen hatalı girişler, bir kısmı gerçek büyük mülkler; modeli 1.000 m²'ye kadar konutla sınırladım.

  Bazı ilanlar birden fazla kurala takıldığı için üçü birlikte 438 ilanı (%1,8) attı; geriye 24.546 ilan kaldı. Fiyat ile brüt metrekare arasındaki korelasyon temizlikten önce 0,03'tü, sonra 0,62'ye çıktı: aradaki ilişki aykırı değerler yüzünden görünmüyordu.

## Model

_Eklenecek._

## Sonuç

_Eklenecek._

## Bildiğim eksikler

- Fiyatlar 2021-2022'ye ait. Aradaki enflasyon yüzünden model bugünkü fiyatları tahmin etmek için kullanılamaz.
- Fiyatlar ilanlarda istenen fiyatlar, gerçekleşen satış fiyatları değil.
- Metrekare temizliği bu verinin biçimine göre yazıldı. Ondalıklı metrekare içeren bir veride kontrol hata verir.
- Aykırı değer kurallarından biri fiyatı kullanıyor. Yeni bir ilanın fiyatı bilinmediği için bu kural tahmin sırasında uygulanamaz.
- İlan tarihi ve mahalle bilgisi henüz kullanılmıyor.