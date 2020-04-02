
Ilgazla mülakat 20200331

# Mimari

# Modüller

		Landinpage (CoronaBuster)
			Statik sayfa
			S3’de + cloudfront’ da host edilecek
			React kullanılacak
			Route53 ayarları ,SSL
		API - EventCollector
			Sbt scala projesi ,akka http
			Auto-scale group kullanılacak
			Network LB olacak
			Route53 ayarlaması
			S3 bucket’ ı oluşturulacak DB için
			AkkaStream, Akka cluster olacak
		Spark Stream Processing
		İstemci (Client)
			Admin Panel
			React , SPA
			S3 + cloudfront
			Route53
		Mobil çıktılar (deliverables)
			Android SDK
			Android App
			IOS SDK
			IOS App
		Veritabanları
			S3 + Parquet
			PostgreSQL

# Sistem nasıl çalışıyor?

İlgili komponentler:

- Landing page: projenin ne olduğunu anlatacak

- API - EventCollector

Cep telefonlarından gelen datayı kaydediyor. Sunucu tarafında çalışacak.

Bunun önünde Network Loadbalancer var. IP taraflı. IP tarafındaki event collectorlardan hangisinie bağlanacağını

Aynı workera yazılıyor, hbir istemci her zaman. IP taraflı olunca daha hızlı oluyor. 

Auto-scale group: yük arttığında, arka taraftaki API sunucu tarafının artması gerekiyor. 

Ortalama CPU kullanımı %80'i aştığında yeni makine açılıyor. 

Amazon'un auto-scale group servisi var. O yapıyor bunu. Makine satın alma ve LB'ye register etme olayını yapıyor. 

Route53: API'nin DNS kaydı. LB'ye kayıt ediliyor. 

DNS sunucu var. Arka tarafta birden fazla LB var. Ama bunu biz görmüyoruz. LB'ler bozulabiliyor. Bozulunca, DNS sunucu doğru yere forward ediyor. Bunun arkasında da birden fazla API sunucular var, yani event collector'lar.

Worker'ların arkasında, lokal diski var. Gelen bütün datayı parquet formatında buraya kaydediyoruz. 

20 MB'yi geçtiğinde, bu S3'e upload dosya ediliyor. 

parquet column tabanlı bir dosya formatı. 

AkkaStream: API sunucu yaparken, scala + akka kullanıyoruz. Event tabanlı mesaj işlemek için, reactive gibi çalışıyor. Workerda çalışacak.

Akka, Akka HTTP, AkkaStream arasındaki fark? 

Akka, Erlang'daki Actor modelini uyguluyor. Çok hafif threadler gibi. 

Akka: HTTP server. 

Önce lokalde workerlar parquet dosyasını oluşturacak. S3'te doğru yapıda kaydetmeliyiz. Ana folder var. Onun altında worker id'si var. Onun altında da gün tabanlı tarih klasörleri var. En altında da birden fazla dosya var. 

Doğru formatta yazarsan, Hadoop ekosistemine dahil uygulamalar Spark gibi, kök dizini algılayıp, filtreleme gibi işlevleri hızlıca yapabiliyor. 

EventCollector'lar sadece datayı kaydediyor. İşleme kısmını bu yapıyor:

Spark Stream Processing: 

Bu birkaç şey yapıyor: 

- Farklı formatlara çevirmek veya farklı indekslemeler yapıyoruz.
- Corona virüsü olan birisini öğrendiğimiz zaman, bu kullanıcının kimlerle temasta bulunduğunu data içinde arıyoruz. 

Ya önceden SQL'e çevirebiliriz, ya da doğrudan tüm data içinde arama yapabiliriz.

Her seferinde yapmak yerine, batch process olarak günde n kez yapmak lazım. 

parquet column tabanlı olduğundan, number encoding formatlarıyla 64 bitlik 1000 tane sayıyı, 64 * 1000 yapmak yerine her birini n bit yapıyoruz. Time stampler sürekli arttığından, sadece increment kısmını tutuyoruz.

Hem veri miktarını azaltıyoruz, hem de processing kısmını azaltıyor. 

Tekrar sorgulama yaparken, normal time stamp'e çevirmemiz gerekecek. Ama sorgulamada zaten esas darboğaz S3'ten datayı çekme oluyor. 

Bazı veriler için postgres kullanabiliriz. Kimlere virüs bulaştı? Bunları kaydetmek için. 

Bu tablodan sparka gidecek. 

## Admin Panel: 

Landing page statik sayfa. Önde cloudfront var. 

React kullanılıyor. 

Admin paneli, API'nin önündeki admin paneli. Debug etmek ve data girmek için. 

Sağlık Bakanlığı, Belediyeler, hastane personeli olabilir. 

## Data girişi: 

Hangi dataların girişini öngördün?

CDC'nin PUI (person under investigation). WHO da bu formu kullanıyor. Hasta hakkında demografik veriler, test yapıldı mı, nerede yapıldı, sonucu ne, semptomlar ne. Bayağı detaylı. Bu kadar bilgi bize gerekmiyor. 

İkinci sayfada semptomlar var. Bunu muhtemelen kullanıcıdan alacağız. 

Yetkililerden alacağımız bilgi, kullanıcıya virüs bulaşıp bulaşmadığı bilgisi. 

Cep telefonu numarasıyla ilişkilendirerek yetkili kullanıcıdan kimlik bilgisini alabiliriz. Veya kullanıcının app'inde, kullanıcı kendi inisayatifiyle "bana bulaştı" diyebilir.

Neden S3'e veriyi kaydediyoruz? js kodları için.

## Android/iphone

opt01: app

opt02: SDK

getir.com, banka uygulamalarını arka tarafta. Manuel data girişi olmayabilir. Bir diyalog açılabilir. Yeni bir sayfa açılıyor sadece. 

Kullanıcı uygulamalarının, yeni izin alması gerekiyor. Lokasyon ve bluetooth kullanma izni alması gerekiyor. 

Bunları zaten birçok app hali hazırda istiyor. Lokasyon alınca, zaten bluetooth (BLE) buna dahil oluyor. BLE çok az pil harcıyor.

Cep telefonun piline ekstradan %1 yük oluşturacağız.

SDK'nın boyutu 10 MB-20 MB gibi olur. 

Günde 1 Mb altı veri saklama.

Gönderilecek veri, daha az olacak. Bütün data 6 haftalık data istemci tarafında saklanacak.

Eski datayı incremental bir overwrite edeceğiz. 

## Datayı bizim sunucuya ne zaman aktaracağız?

Birkaç alternatif:

opt01: Dakikada bir log alırsın sunucuya yollarız. En basit hali. (Mahremiyeti dikkate almazsak)

opt02: Kullanıcı dakikada bir koordinat logu alıyor. Etrafta dolaşırken, bluetooth beacon mesajı broadcast ediyor. Diğer kullanıcılar da bu beacon mesajlarını topluyor. Hangi kontaktları gördüğü, kendi dosyasına kaydedioyr timestamp ile beraber. Daha sonra, bu kullanıcılardan birinin hasta olduğunu öğrendiğimizde, kullanıcının tüm kendi telefonunda sakladığı datayı upload ediyoruz. 

Adam hasta olmadıysa, hiç o dataya erişmiyoruz bile. 

Bizim sunucuya upload edilince, biz hangi bluetooth kontakt id'leri var. Nerelerden geçmiş kullanıcı? Bulunduğu lokasyonlar. İki haftalık.

Bu bilgiyi, bluetooth id'lerinin kime ait olduğunu biliyoruz. Bu kullanıcılara notification yolluyoruz.

Bluetooth mesajı: timestamp, bir tane id, karşı taraf mesajı alırken RSS (receiver signal strength): kaç desibelde bu mesaj geldi. Ama standardı olmadığı için, değişkenlik gösterebiliyor. 

### ID

ID: saatte bir id değişebiliyor. bunu biz kendimiz üretiyoruz. bizim sunucuya kayıt olduğunda, bunu biz üretiyoruz. cep telefonu gibi bir id olursa, birisi app yazar. Rastgele birisini takip eder. Saatte bir değiştirirsek, takip etse bile, yeni bir kullanıcı gibi görünür.

App de sdk'yi kullanacak. sdk ilk bizim sunucuya register olduğunda, telefona unique bir id atıyor. Telefon, saatte bir kendisi geçici id oluşturuyor. Kendi orjinal id'si var. Bizim sunucu, her kullanıcıya özel shared secret biliyor. Kendi unique id'si, shared secret, o anki timestamp'in saat kısmı, bunu string gibi toplayıp, crypto hash'ini alıyorsun. sha256 gibi. 

Bize yollanan datanın içinde şifrelenmiş id'ler olacak.

### Veriyi nasıl saklayacağız?

Açık haliyle saklayacağız. Sadece hasta olduğunda alacağız bu datayı zaten.

Bluetooth Beacon: Fener. Etrafa sinyal saçmak. Bir mesaj oluyor. Tek yönlü bir broadcast bu. "Ben buradayım". İçine istediğimiz şeyi koyabiliyoruz.

O mesajı aldıysan, o kişi çok yakındadır. Açık havada 10 metre. Fakat cihaza göre değişebiliyor. Kapalı alanda, duvara bağlı azalabiliyor. 

Geometrik bir hesaplama yapmaya gerek yok.

### Lokasyon

opt03: Lokasyon bilgisini hiç almayabiliriz. Telefonlar, adam hasta olsa da, olmasa da, coarse lokasyon yollayabilir. 5 km içindeki lokasyonu yollar. Bu niye lazım olabilir. Hangi bölgede ne kadar hasta var? İnsanlar nereden nereye hareket ediyor? 

Eğer lokasyon bilgisi almıyorsak, daha iyi. Daha çok güven verir. 

Otobüs gibi araçlara biniyorsun. Bu konuştuğumuz şeyler, havadan nefes yoluyla hastalığın bulaşmasını önlemek için. Ama düşün ki, adam taksiye bindi. Bir saat önce binen adam da sana hastalığı bulaştırabilir. Bu app'i yüklerken, taksici ve otobüs şoförlerine, özel olarak, bu taksinin ve otobüsün hangi otobüs olduğunu, plakasıyla ilişkilendirerek bilgiyi toplayabiliriz. Taksiciler app'i yüklerken, özellikle taksici olduğunu ve plakasını bildirirse, bu sorunu çözeriz. Otobüs, metro vs. araçları için de bu geçerli.

Faydaları konusunda: Nefes yoluyla bulaşmak ve dokunma yoluyla bulaşmanın ikisini de kapsıyoruz, diye yollamak lazım. 

Bununla başka araştırmalar yapabiliyorsun. Hangi bölgede daha çok var? Otobüsten mi bulaşıyor, evden mi? Datayı akademisyenlerle paylaşıp, başka güzel şeyler çıkartabilirler. 

Belki başta bunu eklemeyiz. Sonradan ekleyebiliriz. 

Verinin çokluğundan ziyade kullanımın yaygınlığı daha önemli.

Zamandan bağımsız bulaşmayla ilgili, toplu gidilen yerler var. Açık havada bir yere dokunmuyorsun. Ofis, araç. Sokağa çıkma yasağı geri çekildikten sonra kafeler yeniden açılacak. Şu anın çözümü, ayrıca bir yıllık bir sorunun çözümü gibi düşün. 

Şoför app'leri özel olur. Plaka ve sefer numaralarını biliyor oluruz. Kullanıcının taksi, metroya binip binmediğini kontrol edebiliriz. 

Kamu personeline devlet yapın derse yaparlar. Doğrulanması da kolay, yani şoförün şoför olması da.

opt-in tarzı olabilir. Bluetooth her zaman opt-in olur. Ekstradan da lokasyon bilgisini paylaşmak istiyor musun, ekstra faydası şu olacak. Fakat lokasyon bilgisi elimizde olursa, güvenlik bilgisini çok daha iyi yönetmemiz gerekir. Datanın sızdırılması çok büyük problem. 

İnsanların güvenilirliğini kazandıktan sonra, gerekirse daha fazla veri de toplanır. 

Birisi hasta olduktan sonra şüpheli listesi çıkıyor. Belli exposure time üstü insanlar. Uzaklık ve süre.

Son 2 hafta içinde, toplam 20 dakika virüslü bir insanın dibindeydin. Sağlığa zararlı ortamda, hiç korunma önlemi almadan, en fazla 30 saniye veya 1 dakika kalabiliyorsun. Radyasyonda da öyle. Kalma demiyorlar, şu dozda kalabilirsin diyorlar. Maskelerin çarpanı oluyor. Tavsiye edilenin 10 katı daha kalabilirsin. N95 maskeler, 10x koruma sağlıyor. Tamamen yüzü kapatanlar 100x koruma sağlıyor. 

Bu mesaj attıklarımıza bir form doldurmalarını söyleyeceğiz. O formlarda semptomları soracağız. CDC'nin PUI formundaki soruları soracağız. 

O bilgiyi alacağız, adamın hasta olup olmadığını göreceğiz. Training datası olacak. 

Herkesi korumak zorunda değiliz. %90'ı korusak toplumu kurtaran bir şey. 

Bireyin yapması gereken tek şey dışarı çıkmamak. Biz adama bulaştıysa, başkasına bulaşmasını önlemeye çalışıyoruz. 

Market, kafe, kargo: 4sq'de bu data var. Herkes kredi kartı kullanıyor. Hangi tarihte kullanıcı neredeydi? Bunu bankalardan veya migrostan alabiliriz.

İş yerleri:

Devlet daireleri, hastaneler: Bütün hastane lokasyonlarını googledan çekebiliriz. Geofence koyabiliyorsun. Şu alana girdiğinde şu API'yi çalıştır gibi.

Açık hava:

Q: Yalancı negatif veya pozitiflik olur mu?

Balkonnda sigara içiyorsun. Dipdibe değilsiniz, ama temas varmış gibi görünecek. Kaldırımda da bu olacak. Evde cep telefonu sabit duruyor. Accelerometer datasını kullanabiliriz. 

Adamın yürüyüp yürümediğini anlayabiliriz. Pedometerler çalışma şeklinde. 

Adam arabasındaydı. Hasta birinin yanından geçti. Süreye bakıyoruz. 

Sunucuya bildirmeden, kullanıcı arabada mı, evinde mi, açık havada yürüyor mu? Bunun bilgisini çıkartırız. 

Ekstra izin gerektirmiyor bu accelerometer datası. 

İki kişi özel arabadaysa, bunları algılamamız gerekiyor. Servisler için de bu geçerli. 

Büyük otobüste ne olur? Arkadakini kaçırabiliriz. Birden fazla temas esas mesele. Tek temastan dolayı.

Etrafa bluetooth ile paket yolluyoruz. 100 kişiyi aşınca, telefon kendisi oranın kalabalık olduğunu bilebiliyor. O bölgeleri işaretleyebiliriz. Sadece o bölgenin konumunu bizim sunucuya yollayabilir. 

## KVKK ve Mahremiyet Hakları

Bunu olabildiğince iyi yapmak hedeflerimizden bir tanesi. Çok fazla veri alırsan, kullanıcılar rahatsız olur. Evimin adresini niye bileceksin? Olaylar bittikten sonra bu verilere ne olacak?

Sunucu tarafında olabildiğince az data saklanacak. Gerekmedikçe data almamayı, kullanıcıyı identify edebilecek olabildiğince az data tutmak. 

Not: Mahremiyet

Q: Veri analizi? 

## Kilometre taşları

Tübitak projesi

İlk prototipi hızlıca yapmak. Ekibi olgunlaştırmak. Yapamayanları başka kişilere vereceğiz.

İlk kendi appimizi yapacağız. SDK değil. Oluyor mu test edeceğiz. 

Düzgün çalışıyorsa, getir.com ceo'larıyla konuşacağız. Bazıları hızlı hareket edecek, bazıları avukatlarla konuşacak.

O sırada Tübitak belli olur. O belli olursa, Sağlık Bakanlığı da bizi ciddiye alır. Onlar ayrıca doktorlarla görüştürür. SB ile entegrasyonu soracaklar.

Tüm lokasyon datasını alalım diyecekler. Bunun neden yanlış olduğunu anlatacağız.

## Deployment

Q: Deployment nasıl olacak? Host yazılımla etkileşim.

Dokümantasyon sayfasını yapacağız. Projeye şu maven bağımlılığını yerleştir. Şu izinleri eklemeniz gerekiyor. Main activity kısmında, program ilk açıldığında, şu satırı yazacaksınız.

## Ne kadar veri akışı olacak?

Lokasyon verisini almazsak, veri akışı az oluyor. 

Lokasyon verisini bir miktar coarse data almak. 6 km'lik kutulara böldüğümüzü düşün. 

Günde TB'lerce

Q: 
Bir timestamp var. 128 bit lokasyon. 64 bit kullanıcı id. 2*64: bluetooth kontaktları (günde 100 temas oluyordur). 

Dakikada bir bu event loglanıyor. 

//bunların hepsi bit 8 e bölünecek
const userPerMin = 64 + 64 + 128 + 2*64 + 64
undefined
userPerMin * 60  * 24
645120
const dataUserPerDay = userPerMin * 60  * 24
undefined
const eventPerUserDay = 60*24
undefined
const allUserCount = 80000000
undefined
allUserCount * dataUserPerDay / 1e9
51609.6 GB /8
10e9
10000000000
1e9
1000000000
const allDataPerDayGB = allUserCount * dataUserPerDay / 1e9
undefined
4*7*allDataPerDayGB / 1000 
1445.0688

Aylık 10 TB civarında merkezi sunucuda data tutacağız. 

1 TB'lık SQL tablosu yapmak çok zor.

Q: Hosting maliyeti ne kadar olur?

S3 data: 1-2 ay saklayacağız. 20 TB.

Gelen veri miktarı: 10 TB

API sunucuları: EventConnectorlar. 80 M kullanıcı için. 

Spark ile batch process yapmak pahalı olur. 

Günde kaç kullanıcıdan data alırız.

## Next

Bunu başkalarına nasıl anlatacağız? Ona göre de yazalım.

Singapurluların projesi: Trace Together. 

Nefesle bulaşmayı engellemek için. Taksiye bir saat önce adam dokunacak, onun için çözüm kullanmamışlar. 

Çin: devlet her şeyi app'den takip ediyorlar. Bir sürü yere girerken, vatandaşlık numarası alıyorlar. İstihbarat servisleri falan takip ediyor adamları.

Kore ve Tayvan örneklerini de çıkartalım.

Bu salgın bittikten sonra, 2-3 yıl sonra tekrar aynı şey olacak. Çünkü nüfus artıyor ve hayvanlarla temas giderek yaygınlaşıyor. Bu virüs zaten ortalıkta dolaşıyor olacak. İlk günden bunu kursaydık, bu kadar olmazdı.

## EventCollector Backend

json doğrudan gelecek

cep telefonu: hızlı bağlan

oauth gibi bir şey. turkcell'in hizmeti. cep telefonu bilgisi bize gelmiyor. turkcell'e gidiyor. biz telefon numarasını göstermiyor. o kullanıcıyı tanımlayan bir id var. biz bunu kaydediyoruz sadece. 

kullanıcının tıbbi geçmişini de istersek, cep telefonu + tıbbi geçmişin yanyana durması pek güzel değil.

sonradan bunu kullanıp kullanmamaya karar veririz.

cep telefonu bilgisi, sadece turkcell'e gidiyor. telefona id'yi gönderiyor. onu sadece değiştiriyoruz.

Mobile Connect. Turkcell Hızlı Giriş.

C5 önce parquet dosyalarını lokal kaydediyor. sonra yukarı iletiyor. 

---

CDN ve EC2 arasında LB olsun. Sadece statik sayfalar CDN üzerinden geçiyor. Diğerleri LB üzerinden geçer. 

Auto-scale olacak.

---

S3 yanına bucket isimlerini yaz: Event Buckets

Öbürüne de static files bucket.

Bucket isimlendirmesini ağaç yapısını gösteririz.

---

## Batch Processing 20200402  

Batch processing:

Cluster olunca. Birden çok bilgisayardan oluşuyor. Parçalayarak işi yapacaklar. Paralel.

Spark'ı biz yönetmek zorunda değiliz. 

Elastic MapReduce (Spark Cluster)

Çıktıyı, S3'e de koyacak, hem de yine parquet formatında postgres koyacağız. Normal tablo şeklinde. Postgresten data da okuyacağız.

Mesela, kimler hasta olan kullanıcılar?

---

100 hasta verisi geldi parquet dosyası olarak yazıldı. 

Datanın üzerindeki tüm işlemleri spark ile işleyeceğiz. Application kısmı için. Niye normal düz yazılım yapmadık? Çünkü spark daha kolay olduğu için. S3 dosyalarına erişim otomatik oluyor. Tek yaptığı data processing.

Birisi hasta olduğunda, onu AdminPanel'den gelebilir. Veya excel tablosuyla upload mu ederiz? Veya cep telefonundan kendisi girecek. 

Bir tane API'dan geliyor, net. Postgres'e koyacağız bunu.

Spark, postgres'ten bu hasta bilgilerini okuyacağız. 

API'dan id ve bluetooth kontaktlarının id'leri geliyor. 126 bitlik UUID kullanıcı idsi (düz id). Buna private device id. Kullanıcının kontakt listesi geliyor. Bu bir array. Timestamp (saat çözünürlüğünde), encrypted user id (encrypted bluetooth contact id), RSS, device model idsi (debug etmek için. bazen bluetooth'ta sorun çıkar, coarse location. kulaklık bozuk oluyor falan diyecek.) Bunları parquet dosyası olarak kaydedilecek.

Parquet: iki şey yazacağız:

- Hastalandıktan sonra telefondaki logları tuttuğumuz şeyler
- Coarse location datası.

Spark, bluetooth contact bilgilerine bakıyor. 

Sıralama yapıyor: coarse location, Timestamp, beacon encrypted contact id (bluetooth encrypted contact id).

Bir tane dosya haline getiriyoruz. 

Diğer clientlar, bir saatte bir bu dosyayı çekecek. Bu dosya orta boyutta bir dosya olacak. Bu kısmı optimize edebiliriz. Coarse location'a göre grupladığımızı düşün. Client kendi coarse location'ındaki dosyaları çekecek.

Bu listede kendi id'si var mı yok mu onu arıyor. Burada trick var: Saatte bir, kullanıcının private id'si vardı. Bu private id başka client'lara gitmiyor. Sadece biz görebiliyoruz. Private id + coarse timestamp (significantı saat), rastgele bir salt string. Bunları topluyorsun. hash'ini alıyorsun. 

[11:55 PM, 4/1/2020] Ilgaz: KDF(userprivate_id, salt + timestamp_hour_resolution)
[11:55 PM, 4/1/2020] Ilgaz: Key derivation function
In cryptography, a key derivation function (KDF) is a cryptographic hash function. MD5 gibi bir fonksiyon.

Niye bu şifrelemeyi yaptık? Birisi rasgele bir program yazar. Tüm etraftaki bluetooth id'lerini takip eder. Bu şekilde bulamaz. Saat başı çünkü değişecek.

Timestamp, salt'ın yanında duruyor. Bunu yolluyoruz çünkü telefonların saatleri aynı olmayabilir. Telefon saatini, tüm kullanıcılar indiriyor ya, saati kullanarak kendi id'sini bulmak için kullanıyor. Yine KDF'e sokuyor. Benim bu saatteki id'im neydi? Tüm saatler için kendi id'sini buluyor. Bunları dosyada arıyor.

Kullanıcı diyelim ki, kendisini buldu. Ne yapacak?

Bize bir notification gönderiyor. Ben şu saatte, bu bluetooth id bana aitti. API'dan bunu alıyoruz. Bunların toplamını alıyoruz. Şu saat, bu saat, bu saat. Tüm listeyi alıyoruz. Hangi saatte kaç dakika virüslü biriyle kontaktta bulundu? Azıcık bir dakikalık temas olabilir. Bu durumda, iki hafta kendini kapat demeyeceğiz. Belli bir eşiği geçenleri kapatacağız.

Bu listeyi alıp, skorlama algoritmasını, kullanıcının lokalinde çalıştırabiliriz. Veya sunucuda yapabiliriz.

Kullanıcıya ekstra sorular soruyoruz. Semptom soruları. CDC'nin soruları.

Apple soruları: https://drive.google.com/drive/folders/12u1bjSNCsHJJb0HNzNbozmxRfblueG6B

Bu bilgiyi sunucuya her gün sorarak alacağız. Buna göre her gün yeniden skor hesaplayacağız. Hasta olduğunu düşünüyorsak, diğer aksiyonu söyleyeceğiz: SB'ye söylemek ya da kullanıcıyı yönlendirmek.

- SB'ye kullanıcının id'sini söylemek. 
- Kullanıcıyı hastaneye git diye uyarmak

Kullanıcı kendi loglarında zaten en detay timestamp çözünürlüğünde temaslarını görüyorlar. Oradan kaç dakika temas ettiğini oradan bulabilir.

---

Q: Turkcell id veriyor. 

Bizim app için, tüm kullanıcıları tekil tanımlayacak id olacak. O id'nin kime ait olduğu. Turkcell'i kullanırsak, private device id.

gdrive'daki sözlüğe ekleyelim bu terimleri.

Q: Hasta kişinin kimlik bilgisiyle telefon numarasını nasıl eşleştiriyorduk? Hasta birine mesaj gönderip, onun loglarını almamız için gerekiyordu bu.
