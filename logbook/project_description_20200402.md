
# CoronaBuster Projesi

## Amaç ve Gerekçe

CoronaBuster Projesinin amacı, bir virüs salgınında temas izlemesi (contact tracing) yapmayı kolaylaştırmaktır. Temas izlemesi, hasta olduğu belli olan bir kişinin kimlerle fiziksel olarak temasta bulunduğunu tespit etmek anlamına gelir. 

Temas izlemesi, salgınların yayılma hızını ciddi ölçüde azaltan halk sağlığı uygulamalarının başında gelir; çünkü temas izlemesi yoluyla, hastalık taşıma şüphesi bulunan insanlar, semptomlar ortaya çıkmadan ve hastaneye ulaşmadan, ortaya çıkarılabilir. 

Mevcut koşullarda, bu uygulama DSÖ (Dünya Sağlık Örgütü) ve dünya devletlerinin ilgili sağlık kurumları tarafından büyük ölçüde manuel süreçlerle yürütülüyor. Bu yüzden, ancak salgının başlangıç aşamasında uygulanabiliyor. Hastalık, binlerce insana bulaştıktan sonra, kaynak yetersizliğinden dolayı temas izlemesinin yapılma ihtimali kalmıyor. Bu durumda, Covid-19 salgınında olduğu gibi, halk sağlığı kurumlarının elinde salgını durdurmak için, tek araç olarak hastalığın yoğun olduğu merkezleri (epicenter) kapatmak (lockdown) kalıyor. Ne var ki, bu çözüm ancak kısa süreli uygulanabilecek bir çözüm. Eğer salgın 4-6 hafta içinde, kapatma sonucunda yok edilemezse, bu durumda ekonominin ve tedarik süreçlerinin aksamaması için, kapatmayı kaldırmak gerekiyor. Bu ise, doğal olarak, salgının ömrünün uzamasına ve hem ekonomi hem de halk sağlığı üzerinde bedelin katlanarak artmasına neden oluyor. 

Bizim önerdiğimiz proje, temas izlemesi yapmayı hem son derece düşük maliyetli ve otomatik bir hale getiriyor, hem de bunu yaparken insanların kişisel mahremiyet haklarını koruyor. Bunun için önerdiğimiz çözüm, cep telefonlarının bluetooth sinyallerini kullanmaya dayanıyor. 

## Faydalar

Corona salgınından dolayı milyonlarca insan çalışamıyor. Temas izleme otomasyonu sayesinde, potansiyel hastaların tespiti son derece kolay ve neredeyse sıfır maliyetli bir hale gelecek. Bu sayede, hasta olsun olmasın herkesin eve kapanması zorunluluğu hafifleyecek. Sadece hasta olanlar ve potansiyel hastalık şüphesi taşıyanları tecrit edilmesi ve test edilmesiyle, salgın kontrol altına alınabilecek.

## Çözümün Özet Tarifi

Şu an, neredeyse herkesin üzerinde bluetooth destekli bir akıllı telefon bulunuyor. Telefonların yaydığı bluetooth sinyalinin yaklaşık 10 metrelik bir menzili bulunuyor. Telefonlara yükleyeceğimiz bir yazılım modülüyle, her bir kişinin yakın çevresindeki insanların şifrelenmiş güvenli kaydını tutacağız. Daha sonra, bir kişinin hasta olduğu bilgisi bize ulaştığında, bu kişiyle yakın temasta bulunmuş diğer insanları tespit edeceğiz ve bu insanlara uyarı mesajı göndereceğiz.

Bütün bu işlemleri yaparken, hem Türkiye'nin KVKK (Kişisel Verileri Koruma Kurumu) mevzuatıyla, hem de AB'nin GDPR (General Data Protection Regulation) mevzuatıyla uyumlu bir şekilde, insanların kişisel bilgilerinin mahremiyetini koruyacak bir çözüm tasarlıyoruz. 

Bilgi mahremiyetini korumak için sistem tasarımımızda şu iki kritik kısıt bulunuyor:

- Temasların tespit edilmesi için gerekli olan minimum seviyede bilgi sunucu tarafına gönderilecek.
- Telefonların birbirlerine gönderecekleri mesajlarda (beacon mesajı), gönderen telefonun kimliğini ortaya çıkaracak veri bulunmayacak.

## Nasıl Çalışır?

### Tüm Süreç

Önkoşul: 

- Mobil istemci telefona yüklenmiş ve gerekli izinler verilmiş olmalı.

#### Normal Akış (Normal Flow)

1. Telefon

## Gereksinimler

### Fonksiyonel Olmayan Gereksinimler

NFR001: Telefonun piline eklenecek ekstra yük, %1'i geçmeyecek.

NFR002: Telefonun hafızasına günlük en fazla 5 MB veri yazılacak.

NFR003: Sunucu tarafında en fazla 6 haftalık veri saklanacak. 

Kişisel bilgilerin mahremiyetini korumak için, olabildiğince az veri tutmamız gerekiyor.

Eski verinin üzerine kademeli (incremental) bir şekilde yeni veriyi yazacağız (overwrite).

NFR004: Telefonun lokasyon, bluetooth servislerini kullanma izini alınacak.

SDK'nın gömüldüğü host uygulamanın bu izinleri kullanıcıdan alması gerekiyor. Partner firmaların  uygulamaları, bu izinleri zaten kendi işleyişleri için muhtemelen almış olacaktır. 

NFR005: Partner uygulamalar

## Teknik Çözüm

### Mobil İstemci

Mobil istemciyi, bir SDK modülü olarak dağıtacağız, esas olarak. Bu SDK, hali hazırda insanların yaygın bir şekilde kullandığı, teslimat (getir, banabi, yemeksepeti gibi), bankacılık (İşBankası, Enpara gibi) gibi uygulamaların (host uygulama) içine gömülecek.

Mobil istemciyi hazırladıktan sonra, popüler uygulama üreticileriyle bağlantıya geçeceğiz. Bunların arasından hızlı bir şekilde öncü partner olmak isteyen partnerleri seçeceğiz. İlk etapta, SDK'yı bu partnerlerin uygulamalarına ekleyeceğiz. Uygulama canlı ortamda bir süre test edildikten sonra, geniş yayılım için, yeni partnerlerle bağlantı kurup uygulamanın yayılımını olabildiğince artırmaya çalışacağız.

## 

