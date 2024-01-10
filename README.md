# Twitter Oppenheimer Filmi Tweetleri Duygu Analizi
Twitter'da Oppenheimer filmi hakkında atılmış tweetlerin, olumlu veya olumsuz duygu taşıyıp taşımadığını tahmin eden Doğal Dil İşleme sınıflandırma projesidir. Karar Ağacı, Naive Bayes ve Support Vector Machine algoritmaları kullanılmıştır.

## Twitter'dan Tweetlerin Çekilmesi
### Tweetleri Çekerken Yararlandığım Video: https://www.youtube.com/watch?v=MNEw3Mplm7E <br>
Twitter'dan veri çekilme işlemi "<b>scrapper.ipynb</b>" dosyası içinde yer almaktadır.
Twitter'dan tweetlerin çekilebilmesi için Nitter denilen bir scrapper kullanılmıştır. Tweetler çekilirken hangi verilerin istendiği açıkça belirtilebilir.(örneğin beğenme sayısı, tarih).
Tweetler çekilirken sadece metin içeriğinin çekilmesi tercih edildi. Veriler çekilirken Oppenheimer filminin vizyon tarihi olan 21 Temmuz'dan günümüze ve ingilizce olacak şekilde arama sorguları girildi. Dil olarak İngilizce seçilme nedeni daha fazla sayıda veriye ulaşabilmektir
### Örnek Bir Sorgu:
![arama sorgusu](https://github.com/AlperenAkgul/Twitter_Oppenheimer_Duygu_Analizi/assets/97761889/e59f7e2e-bb5a-4ceb-be5f-74e2422d21d4)

Çekilen tweetler bir "<b>.csv</b>" dosyasına kaydedildi.
Tweetlerin daha zengin olabilmesi için manuel olarak da eklemeler yapıldı.Toplamda 2319 tweet elde edildi.

![verilerin eklenmesi](https://github.com/AlperenAkgul/Twitter_Oppenheimer_Duygu_Analizi/assets/97761889/5a1568be-0228-4b8c-98a3-76222f7f5d5e)

## Verileri Etiketleme
Tweetlerin her biri 1, 0 ya da -1 olacak şekilde etiketlendi. 1 'Pozitif', 0 'Negatif' tweet anlamına gelirken, -1 ise kesin bir duygu içermeyen veya konudan alakasız tweetler için kullanıldı.

## Verilerin Okunması

Buradan sonraki bütün adımlar <b>main.ipynb</b> dosyas içinde yer almaktadır.

İlk olarak gerekli kütüphaneler eklendi.
### Gerekli Kütüphaneler:
![kutuphaneler](https://github.com/AlperenAkgul/Twitter_Oppenheimer_Duygu_Analizi/assets/97761889/b98a6f05-b348-4fed-b5a7-661cd9aea67f)

Daha sonra etiketlenmiş "<b>.csv</b>" dosyası programa yüklendi.
1 veya 0 ile etiketlenmiş olan satırlar diğerlerinden ayırıldı. 589 tane 1 ile etiketlenmiş (pozitif) ve 136 tane 0 ile etiketlenmiş (negatif) olmak üzere toplam <b>725</b> duygu içeren tweet bulunmaktadır.

Bir sonraki işlem tweetlerin dolgu sözcüklerinden, noktalama işaretlerinden vb. temizlenmesidir. Temizlenen tweetler "<b>clean</b>" adında bir sütun olarak DataFrame'ye eklendi. Daha sonra metinde hala bulunan harf dışındaki özel karakterlerin temizlenmesi ile birlikte sadece harflerden ve rakamlardan oluşan bir metin elde edildi.
### Eski ve Temizlenmiş Metinin Arasındaki Fark:
![temizlenmismetin](https://github.com/AlperenAkgul/Twitter_Oppenheimer_Duygu_Analizi/assets/97761889/64bbc345-76dc-44a3-b205-c0dcb5de38f0)

## Modelin Eğitimi ve Skorlar
Verilerin metin kısımları X, etiketler Y dizisi olacak şekilde ayırıldı ve numpy dizisi haline dönüştürüldü.
Verilerin %20'si test verisi olacak şekilde ayırıldı.
X dizisinin eğitim ve test kısmı TF-IDF kullanılarak vektörleştirildi.

### Karar Ağacı:

![karar](https://github.com/AlperenAkgul/Twitter_Oppenheimer_Duygu_Analizi/assets/97761889/c2b89308-fb21-4773-82d9-7f081b36c006)

Karar Ağacı modelini kullandığımızda %88 başarı oranı elde edilmektedir.

### Naive Bayes:

![nb](https://github.com/AlperenAkgul/Twitter_Oppenheimer_Duygu_Analizi/assets/97761889/29e50e9f-68ea-4e16-9cac-22dc39687e03)

Naive Bayes modeli kullanıldığında %86 başarı oranı elde edilmektedir.

### Support Vector Machine:

![svm](https://github.com/AlperenAkgul/Twitter_Oppenheimer_Duygu_Analizi/assets/97761889/d8799665-00fd-442b-83df-854333fd93f3)

SVM modeli kullanıldığında ise %93 başarı oranı elde edilmektedir.

## Örnek Cümle Girişi

Modeli test etmek için aşağıdaki resimde bulunan örnek cümleler girildi. Kodun çıktısında cümlelerin temizlenmiş hali görülebilir. Model olarak Karar Ağacı kullanılmıştır. Karar Ağacı'nın verdiği sonuç doğrudur.

![ornekler](https://github.com/AlperenAkgul/Twitter_Oppenheimer_Duygu_Analizi/assets/97761889/f731af82-dd04-4c2c-acc9-8b276aa8dd09)

## Sonuç:
Üç algoritma da başarılı sonuç vermiştir. Fakat Support Vector Machine algoritmasının diğer algoritmalardan daha iyi olduğu görülebilmektedir. 
