## A3. Proje Kısa Tanıtımı

### Kuruluş Kısa Tanıtımı 1500

### Projenin Amacı 1000

CoronaBuster Projesinin amacı, bir virüs salgınında temas izlemesi (contact tracing) yapmayı kolaylaştırmaktır. Temas izlemesi, hasta olduğu belli olan bir kişinin kimlerle fiziksel olarak temasta bulunduğunu tespit etmek anlamına gelir. 

Temas izlemesi, salgınların yayılma hızını ciddi ölçüde azaltan halk sağlığı uygulamalarının başında gelir; çünkü temas izlemesi yoluyla, hastalık taşıma şüphesi bulunan insanlar, semptomlar ortaya çıkmadan ve hastaneye ulaşmadan, ortaya çıkarılabilir. 

Bizim önerdiğimiz proje, temas izlemesi yapmayı hem son derece düşük maliyetli ve otomatik bir hale getiriyor, hem de bunu yaparken insanların kişisel mahremiyet haklarını koruyor. Bunun için önerdiğimiz çözüm, cep telefonlarının bluetooth sinyallerini kullanmaya dayanıyor. 

### Anahtar Kelimeler 255

Contact tracing, temas izleme

### Yenilikçi Yönleri 700

Mevcut koşullarda temas izleme, DSÖ ve sağlık kurumları tarafından manuel bir şekilde yapılıyor. Bu yüzden, ancak salgının başlangıç aşamasında uygulanabiliyor. Hastalık, binlerce insana bulaştıktan sonra, kaynak yetersizliğinden dolayı temas izlemesi yapılamıyor.

Bizim projemiz, temas izlemesi yapmayı hem son derece ucuzlatıyor, hem de doğru temas bilgisine ulaşmak açısından son derece çok kaliteli bir hale getiriyor. Hemen herkesin üzerinde bulunan cep telefonlarının bluetooth sinyallerini kullanarak ve bazı akıllı istatistiksel puanlama algoritmalarıyla, bir kişiye hastalık bulaşma ihtimalini uzaktan tespit edebilir hale geleceğiz.

### Kullanılacak/Geliştirilecek Teknik ve Teknolojiler ile Özgün Katkıları

### Ekonomik ve Ulusal Kazanımlar 1000

Corona salgınından dolayı milyonlarca insan çalışamıyor. Temas izleme otomasyonu sayesinde, potansiyel hastaların tespiti son derece kolay ve neredeyse sıfır maliyetli bir hale gelecek. Bu sayede, hasta olsun olmasın herkesin eve kapanması zorunluluğu hafifleyecek. Sadece hasta olanlar ve potansiyel hastalık şüphesi taşıyanları tecrit edilmesi ve test edilmesiyle, salgın kontrol altına alınabilecek.

### Proje Görseli (5 Resim)

CoronaBuster_Architecture-AdminPanel.png
CoronaBuster_Architecture-Batch Processes.png
CoronaBuster_Architecture-EventCollectors.png

### Sunum Materyali (Powerpoint)

# B. Projenin Endüstriyel Arge İçeriği, Teknoloji Düzeyi ve Yenilikçi Yönü

## B1. Projenin Çağrı Konusuyla İlişkisi ve Hedefleri

### Projenin Çağrı Konusu ile İlişkisi 10000

CoronaBuster projesi, çağrı metninde belirtilen şartları şu gerekçelerle sağlamaktadır:

1. Korona virüs salgınının yayılma hızını doğrudan azaltmayı kolaylaştıracaktır, çünkü: 

a) Hasta kişiyle yoğun bir şekilde temas etmiş, potansiyel hastaları hızlı bir şekilde tespit etmeyi sağlayacak.

b) Hastalığın en çok yayıldığı ortamları tespit etmeyi sağlayacak.

Bu gerekçelerle, CoronaBuster projesi, salgının doğrudan veya dolaylı sonuçlarına etki edebilecek bir bilişim uygulamasıdır.

2. Burada toplanan veriler ve yapılan analizlerle, dolaylı olarak başka halk sağlığı ve epidemiyolojik araştırmalar için veri kümesi oluşturacaktır:

a) Hastalığı kesinleşmiş bir kişinin, hastalığı kimden aldığını tahminlemeyi mümkün hale getirecek. Bu da süper yayıcıların (super spreaders) tespit edilmesini ve bu kişilerin ortak davranış özelliklerini çıkarmayı kolaylaştıracaktır.

b) Hastalığın bulaşmasına dair etkileşim dinamiklerini görselleştirmeyi mümkün hale getirecek. Bu da idarecilerin politika oluşturmasına yardımcı olacaktır.

3. Sağlık Bakanlığının ve mülki idarenin hastalıkla önleyici mücadele yapmasını kolaylaştıracak, çünkü:

a) Spesifik olarak potansiyel hasta kişilerin tespit edilmesi sayesinde, sadece bu kişileri tecrit edilmesiyle, hastalığın yayılması yavaşlatılabilecek. Böylece, ekonominin ve tedarik zincirlerinin bir bütün olarak durdurulması gerekmeyecek. Tedarik zincirlerindeki öngörülemeyen aksamalardan dolayı, sağlık, gıda gibi kritik ikmal hatlarında bir aksaklık yaşanması durumu önlenmiş olacak.

### Problem Tanımı 10000

Mevcut izolasyon ve sosyal mesafe uygulamaları, korona hastalığının yayılmasını belirli ölçüde yavaşlatmış olmakla birlikte, hastalanmış popülasyon yine de her 2-3 günde bir, katlanarak büyümeye devam etmektedir. 

Sokağa çıkma yasağı getirilmesi durumunda, hasta popülasyonunun üstel bir şekilde azalması beklenmektedir. Ancak hastalık tamamen yok olmayacağından, yasak kaldırıldığında, hastalığın tekrar hızla yayılması ihtimali söz konusudur. Imperial College Profesörü Neil Ferguson'ın yaptığı simülasyonlara göre, salgının sönümlenmesi 18 ayı bulacaktır (bkz: "Impact of non-pharmaceutical interventions (NPIs) to reduce COVID- 19 mortality and healthcare demand" https://t.co/srbBS7F1s5). 18 ay boyunca sokağa çıkma yasağı veya #EvdeKal kampanyası uygulanamayacağına göre, bir yerden sonra, hastalığın yayılması önündeki izolasyondan kaynaklı yavaşlama tamamen ortadan kalkacaktır.

Eğer hastalığı kesinleşmiş bir kişinin, yoğun temas içinde bulunduğu kişilerin tümünü otomatik ve mevcut KVKK hukukuna uygun bir yolunu bulursak, toplumun sadece çok ufak bir kısmını tecrit altına almak yoluyla, salgının kontrol alınması mümkündür. Odaklanmamız gereken hedef, hasta olsun olmasın herkesi tecrit etmek değil, sadece kesinleşmiş hastaları ve bunların temasta bulunduğu muhtemel hastaları tecrit etmek olmalı. Böylece, ekonomi aksamadan yürüyebilir ve hastalık çok yüksek bir maliyet etkin bir şekilde kontrol altına alınıp, tamamen sönümlendirilebilir.

Bizim önerdiğimiz proje, temas izlemesi yapmayı hem son derece düşük maliyetli ve otomatik bir hale getiriyor, hem de bunu yaparken insanların kişisel mahremiyet haklarını koruyor. Bunun için önerdiğimiz çözüm, cep telefonlarının bluetooth sinyallerini kullanmaya dayanıyor. 

### Çözüm Önerisi 10000

Şu an, neredeyse herkesin üzerinde bluetooth destekli bir akıllı telefon bulunuyor. Telefonların yaydığı bluetooth sinyalinin yaklaşık 10 metrelik bir menzili bulunuyor. Telefonlara yükleyeceğimiz bir yazılım modülüyle, her bir kişinin yakın çevresindeki insanların şifrelenmiş güvenli kaydını tutacağız. Daha sonra, bir kişinin hasta olduğu bilgisi bize ulaştığında, bu kişiyle yakın temasta bulunmuş diğer insanları tespit edeceğiz ve bu insanlara uyarı mesajı göndereceğiz.

Bütün bu işlemleri yaparken, hem Türkiye'nin KVKK (Kişisel Verileri Koruma Kurumu) mevzuatıyla, hem de AB'nin GDPR (General Data Protection Regulation) mevzuatıyla uyumlu bir şekilde, insanların kişisel bilgilerinin mahremiyetini koruyacak bir çözüm tasarlıyoruz. 

Bilgi mahremiyetini korumak için sistem tasarımımızda şu iki kritik kısıt bulunuyor:

- Temasların tespit edilmesi için gerekli olan minimum seviyede bilgi sunucu tarafına gönderilecek.
- Telefonların birbirlerine gönderecekleri mesajlarda (beacon mesajı), gönderen telefonun kimliğini ortaya çıkaracak veri bulunmayacak.

Yazılım sisteminin çalışması temel olarak, iki ana modülden oluşur:

- Mobil istemci SDK (Akıllı telefonda)
- EventCollector Workers (Backend sunucularda)
- Spark Batch Processes (Backend sunucularda)

Mobil istemciyi, bir SDK modülü olarak dağıtacağız, esas olarak. Bu SDK, hali hazırda insanların yaygın bir şekilde kullandığı, teslimat (getir, banabi, yemeksepeti gibi), bankacılık (İşBankası, Enpara gibi) gibi uygulamaların (host uygulama) içine gömülecek.

Mobil istemciyi hazırladıktan sonra, popüler uygulama üreticileriyle bağlantıya geçeceğiz. Bunların arasından hızlı bir şekilde öncü partner olmak isteyen partnerleri seçeceğiz. İlk etapta, SDK'yı bu partnerlerin uygulamalarına ekleyeceğiz. Uygulama canlı ortamda bir süre test edildikten sonra, geniş yayılım için, yeni partnerlerle bağlantı kurup uygulamanın yayılımını olabildiğince artırmaya çalışacağız.

Mobil istemci, BLE (bluetooth light energy) ile diğer cihazlara dakikada bir kendisini tanıtan bir mesaj (Beacon mesajı) yollayacak. Bu mesajı bluetooth üzerinden alan etraftaki telefonlarda bulunan mobil istemciler, bu temas verisini telefonun hafızasına kaydedecek. Bu kayıt (Beacon Contact Log) şu verilerden oluşacak:

- Timestamp (zaman damgası)
- Gönderen telefonun tekil kimliği (id)
- RSS (receiver signal strength): Gönderen telefonun yaklaşık mesafesini tespit etmek için.
- Coarse location: Yaklaşık 1-2 km hassasiyetinde (değişebilir) konum verisi. 

Beacon Contact Log'ları sunucuya gönderilmez. Bunlar sadece kişinin kendi telefonunda saklanır. 

Daha sonra, Sağlık Bakanlığı gibi resmi bir kaynaktan, belirli bir kişinin hasta olduğu bilgisi, bizim sistemimize AdminPanel arayüzü veya API üzerinden girildiğinde, bu bilgiyi Postgres veritabanına kaydedeceğiz. Sistem, hasta kişilerin mobil istemci SDK'larından bu telefonlarda tutulan kayıtları (Beacon Contact Logs) ister. 

Mobil istemci SDK'sı, bu kayıtları bir JSON dosyası olarak, backend tarafındaki EventCollector sunucusuna gönderir. Bu sunucular farklı kişilerden gelen JSON dosyalarını toplayıp, saklama alanını optimize ederek lokaline Parquet formatında kaydeder. EventCollector sunucuları, belli aralıklarla bu lokal Parquet dosyalarını, S3 gibi merkezi bir depolama servisine kaydederler.

Bu arada, EventCollector'larla asenkron bir şekilde çalışan Spark tabanlı bir batch process, S3'teki Parquet dosyaları üzerinde veri işlemesi yapar. Bu işlem sırasında, veriyi indeksler (coarse location, timestamp, "beacon encrypted contact id" alanlarına göre).

Bu yukarıdaki proseslerle asenkron bir şekilde, tüm mobil istemci SDK'ları, saatte bir, backend sunucusundan, S3'teki kendi ziyaret ettiği mekanlara (coarse location) ait, Parquet dosyalarını çeker. Her bir mobil istemci, kendi kimliğini (id), bu kayıtlarda arar. 

Daha sonra, mobil istemci, parquet dosyasında kendisiyle eşleşen hasta temaslarının skorlamasını yapar. Bu skorlamadan amaç, örneğin çok kısa süreli veya çok uzaktan gerçekleşen temasları elemek, gerçekten bulaşma riski oluşturan temas örneklerini ayıklamaktır.

Bu skor hesaplamasının sonunda, bir kişiye hastalık bulaşma ihtimali ortaya çıkar. Eğer kullanıcının riski eşik değerin üstündeyse, kullanıcıya uyarı bilgisi gönderilir. Kullanıcıya mobil istemci SDK'sını kullanarak, ekstra sorular sorarız. Bu sorular, CDC'nin ve Apple'ın hastalık tanısı amacıyla kullandığı semptom sorularıdır (https://www.cdc.gov/coronavirus/2019-ncov/downloads/pui-form.pdf).

Semptom bilgilerini, hastalık şüphesi taşıyan kullanıcılara her gün sorarak backend tarafındaki Postgres veritabanına kaydederiz. Buna göre her gün yeniden skor hesaplarız. Belli bir eşik değeri geçerse, bir sonraki aksiyona geçeriz: 

- Şüpheli hasta bilgisini Sağlık Bakanlığına bildirmek
- Kullanıcıyı hastaneye gitmesi için uyarmak

Güvenlik Gereksinimleri:

Bütün bu işlemleri yaparken, hem KVKK hem GDPR mevzuatıyla uyumlu bir şekilde, insanların kişisel bilgilerinin mahremiyetini koruyacağız. Bunun için şu iki kritik kısıta göre sistemi dizayn ediyoruz:

- Temasların tespit edilmesi için gerekli olan minimum seviyede bilgi sunucu tarafına gönderilecek.
- Telefonların birbirlerine gönderecekleri mesajlarda (beacon mesajı), gönderen telefonun kimliğini ortaya çıkaracak veri bulunmayacak.

Beacon mesajlarında, gönderici telefonun kimliği, saatte bir değişen bir şifrelemeyle kodlanacak. Aslında her bir telefon için iki tür id kullanacağız:

- Private device id
- Beacon encrypted contact id 

Private device id, her bir telefonu tanımlayan sabit kimlik. Bu kimlik verisini, her bir telefon sadece kendisi bilecek. Biz sunucu tarafında bile, bu kimliğin hangi telefona veya kişiye ait olduğunu saklamayacağız. 

Mobil istemci SDK'sı ilk çalıştığında, Turkcell gibi mobil operatörlerin sunduğu Mobile Connect servisindan, kendi telefon numarası için tekil bir private device id talep edecek. Biz sunucu tarafında, bu private device id verisini saklayacağız. Dolayısıyla, bunun ait olduğu telefon numarasını kendi veritabanımızda bulunmayacak. Bu kimliğin ait olduğu telefon numarası bilgisi sadece, mobil operatörün Mobile Connect servisinde tutulacak. Ancak Mobile Connect de, kimin hasta olduğu bilgisine sahip olmadığından, kullanıcıların kişisel bilgileri, biz de dahil tüm paydaşlardan saklanmış olacak.

Beacon encrypted contact id, mobil istemcilerin birbirlerine gönderdikleri beacon mesajlarına konulacak. Bu kimlik, saat başı değişen bir kimlik olacak. Bunun için saat başı, KDF (key derivation function) kullanarak, aşağıdaki verileri girdi olarak alarak, şifrelenmiş kimlik verisi üretilecek:

- Private device id
- Coarse timestamp (significant birim olarak saat alınacak)
- Rastgele bir salt string

Böylece, dışarıdan birisinin etrafta dolaşan beacon mesajlarını takip ederek, bir telefonu takip etmesi imkansız hale gelecek; çünkü saat başı her bir telefonun gönderdiği beacon mesajındaki kendi kimliği değişecek.

### Proje Hedefleri 10000

@Mert

### Hedef Kitle 10000

@Mert

### Yöntem 10000

@Mert

## B2. Projenin Teknoloji Düzeyi

### Teknolojinin Bilinen Güncel Durumu 3000

### Teknik Özgün Katkılar Tablosu

### Teknolojik Belirsizlik ve Zorluklar 3000

## B3. Projenin Somut/Ölçülebilir Hedeflerle Tanıtımı ve Çözüm Yaklaşımları

### Proje Hedefleri Tablosu (maks 5 adet)

### Proje Hazırlık Çalışmaları 

### Literatür araştırması (doküman)

### Faydalı model/patent araştırması (doküman)

### Ön fizibilite özet bulguları 1500

### Proje çıktısıyla ilgili standartlar 1500

### Arge Sürecinde Kullanılacak Yöntemler

## B4. Projenin Yenilikçi Yönleri

### Yenilikler 3000

# C. Proje Planı ve Kuruluş Alt Yapısı

## C1. İş Planı

### İş paketi faaliyetleri 3000

### İş paketinde kullanılan yöntemler ve özgün katkılarınız 3000

### Teknik ara çıktılar (Ekle)

## C2. Proje Yönetimi ve Organizasyonu

### Proje Personel Listesi (doküman): özgeçmişler

## C3. Kuruluş Altyapısı

### Kuruluşun Arge Olanakları

# D. Projenin Ekonomik Yarara ve Ulusal Kazanıma Dönüşebilirliği

## D1. Ekonomik Öngörüler

### Ticari Başarı Potansiyeli: Kullanım alanları, pazar büyüklüğü, müşteriler, rakipler 3000

### Ticari Başarı Potansiyeli: Çıktının ticarileşmesi, önemli maliyet kalemleri, nasıl finanse edilecek. İlave yatırım. 3000

### Kara Geçiş Noktası 3000

## D2. Ulusal Kazanımlar

### Ulusal kazanımlar. Teknolojiye katkısı. Yeni arge projeleri başlatma potansiyeli. Yeni istihdam. Sektöre katkısı. Sosyo kültürel katkısı. Bilimsel yayına katkı. 5000

# E. Risk ve Finansman Yapısı

## E1. Risk ve Finansman Yönetimi

### Yürütme: Riskler ve Önlemler (ekle)

### Ticarileştirme: Riskler ve Önlemler (ekle)

### Finansman Yönetimi 3000

F. Proje Bütçesi

F1. M011 Personel Giderleri

F2. M012 Seyahat Giderleri

F3. M013 Alet/Teçhizat/Yazılım/Yayın Alımları

F4. M014 Arge ve Test Kuruluşlarına Yaptırılan İşler

F5. M015 Hizmet Alımları

F6. M016 Malzeme Alımları

F7. M017 Dönemsel Giderler Tablosu

G. Ekler

G1. Proje Önerisi Ekleri



