# Twitter Oppenheimer Tweetleri Duygu Analizi
Twitter'da Oppenheimer filmi hakkında atılmış tweetlerin, olumlu veya olumsuz duygu taşıyıp taşımadığını tahmin eden Doğal Dil İşleme projesidir.
## Twitter'dan Tweetlerin Çekilmesi
Yararlandığım Video: https://www.youtube.com/watch?v=MNEw3Mplm7E <br>
Twitter'dan veri çekilme işlemi <b>scrapper.ipynb</b> dosyası içinde yer almaktadır.
Twitter'dan tweetlerin çekilebilmesi için Nitter denilen bir scrapper kullanılmıştır. Tweetler çekilirken hangi verilerin istendiği açıkça belirtilebilir.(örneğin beğenme sayısı, tarih).
Tweetler çekilirken sadece metin içeriğinin çekilmesi tercih edildi. Veriler çekilirken Oppenheimer filminin vizyon tarihi olan 21 Temmuz'dan günümüze olacak şekilde arama sorgusu girildi.
### Örnek Bir Sorgu:

Çekilen tweetler bir .csv dosyasına kaydedildi.
Toplamda 2319 tweet çekildi. Tweetlere manuel olarak eklemeler yapıldı.
### tweet sayısı resmi

## Verileri Etiketleme
Tweetlerin her biri 1, 0 ya da -1 olacak şekilde etiketlendi. 1 'Pozitif', 0 'Negatif' tweet anlamına gelirken, -1 ise kesin bir duygu içermeyen veya konudan alakasız tweetler için kullanıldı.

## Verilerin Okunması

Buradan sonraki bütün adımlar <b>main.ipynb</b> dosyas içinde yer almaktadır.
İlk olarak gerekli kütüphaneler eklendi
### Gerekli Kütüphaneler:

Daha sonra oluşturulan ve etiketlenmiş <b>.csv</b> dosyası programa yüklendi.
1 veya 0 ile etiketlenmiş olan satırlar diğerlerinden ayırıldı. Toplam 589 tane 1 ile etiketlenmiş (pozitif) ve 136 tane 0 ile etiketlenmiş (negatif) olmak üzere toplam 725 duygu içeren tweet bulunmaktadır.

Bir sonraki işlem tweetlerin deolgu sözcüklerinden, noktalama işaretlerinden vb. temizlenmesidir. Temizlenen tweetler <b>clean</b> adında bir sütun olarak DataFrame'ye eklendi. Daha sonra metinde hala bulunan harf dışındaki özel karakterlerin temizlenmesi ile birlikte sadece harflerden ve rakamlardan oluşan bir metin elde edildi.
### Eski ve Temizlenmiş Metinin Arasındaki Fark:

## Modelin Eğitimi ve Skorlar
Verilerin %20'si test verisi olacak şekilde ayırıldı. TF-IDF kullanılarak vektörleştirildi.

### Karar Ağacı:

Karar Ağacı modelini kullandığımızda %88 başarı oranı elde edilmektedir.

### Naive Bayes:

Naive Bayes modeli kullanıldığında %86 başarı oranı elde edilmektedir.

### Support Vector Machine:

SVM modeli kullanıldığında ise %93 başarı oranı elde edilmektedir.

## Örnek Cümle Girişi

Modeli test etmek için aşağıdaki resimde bulunan örnek cümleler girildi. Kodun çıktısında cümlelerin temizlenmiş hali görülebilir. Model olarak Karar Ağacı kullanılmıştır. Karar Ağacı'nın verdiği sonuç doğrudur.
