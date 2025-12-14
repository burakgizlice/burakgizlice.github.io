---
title: "🇹🇷 AdSphere'da Bu Hafta: HOH Development Modeli"
date: 2025-12-13T11:36:51+03:00
draft: false
tags: ["TR", "devlog", "software-engineering", "adsphere", "thesis", "development", "docker", "git"]
author: ["Burak Gizlice"]
showToc: true                     # Show Table of Contents?
TocOpen: false                    # Auto-expand the Table of Contents?
hidemeta: false                   # Hide date/author/read-time?
comments: false                   # Disable comments for specific post?
description: "3 hafta önce analiz işlerini bitirmiş, 250'nin üzerinde gereksinimlerimizi çıkartmıştık. Ancak bir türlü hızlanmayan ve hatta başlamayan development biraz canımızı sıkmıştı. Bu hafta bu çarkı döndürmenin bir yolunu bulduk diyebiliriz."         # Metadata description for SEO
disableHLJS: true                 # Disable code highlighting?
disableShare: false               # Hide share buttons?
hideSummary: false                # Hide summary from list page?
searchHidden: false               # Hide from site search?
ShowReadingTime: true             # Show "5 min read"?
showWordCount: true               # Show "1200 words"?
cover:
    image: "/images/adsphere/signup2.png"     # Image path/url
    relative: false               # To use relative path for cover image, set this to true
    hidden: false                 # Hide on the single page, but show on list?
series: ["adsphere"]           # Groups posts together (e.g., "DevLogs")
---

# Giriş ve Kısa Bilgilendirme
## Merhaba, nedir bu 'Devlog'lar ve neden bu yazıyı yazıyorum?

AdSphere projesi için ve aslında genel olarak da ilk yazdığım devlog bu. Şu anda 4. Sınıf bir Bilgisayar Mühendisliği öğrencisi olmam gerekirdi aslında, ancak ben sistemde ve aslında gerçekten de 3. Sınıf bir Bilgisayar Mühendisliği öğrencisiyim. 

Bunun nedeni Erasmus+ ile 9 aylık bir Polonya ve 2 aylık bir İspanya serüveni geçirmiş olmam. Okulu uzattığım için pişman değilim, ancak çok pişman olduğum bir şey var.

Ben üniversite sınavının hemen ardından, henüz daha yerleştirmeler bile açıklanmadan Bilgisayar Mühendisliği alanında çalışmalarıma başlamıştım. Harvard'ın CS50 kursuyla birlikte en temelden Bilgisayar Bilimini kavradım, sonrasında Native Android geliştirmeden oyun geliştirmeye, ReactJS projelerinden Flutter'a, ve son olarak Avrupa'ya gidişimle veri bilimine kadar şuan aklıma bile gelmeyen birçok farklı şeyi kurcaladım. Bazılarına haftalar, bazılarına aylar bazılarına yıllar harcadım ve şuan bu yaptıklarımın hiçbirinde ısrarcı olmayıp doğru düzgün belgelememem nedeniyle kendim bile nerede neyle ne seviye ilerlediğimi %100 hatırlayamıyorum.

Uzun lafın kısası, bu durumu değiştirmek adına geliştirdiğimiz AdSphere projesinde hafta hafta neler öğrendiğimi ne sorun yaşadığımı ne kullanarak nasıl çözdüğümü düşünce yapımı ve mühendisliğimi belgelemek ve bu belgelemeden en başta kendim faydalanmak istiyorum. Tüm bu nedenlerle inşallah biz bu projeyi bitirene kadar haftada en az bir yazı paylaşacağım.


## Kısaca AdSphere projesi nedir?

AdSphere büyük çapta e-ticaret yapan şirketlerin/markaların büyük ölçekli bir biçimde Influencer havuzlarına ulaşmasını, kendi ürün havuzlarıyla kendilerine özel kampanyalar oluşturmalarını, serbest piyasa mantığı ile Influencer'ların X kampanyası kapsamında Y ürününe Z fiyatıyla talip olabilmesini amaçlıyor.

Böylece markalar influencer'lar ile teklifleşme, havuzdan kendi şirketi ve ürününe uygun influencer seçme, verimsiz sonuçlar aldığı influencer'lar ile tekrar çalışmama, olumlu sonuç aldığı influencer'lara daha çok bütçe ayırma gibi lükslere sahip olabilecekler. Yani en azından projenin amacı bu. 

Marka ve Influencer'lar arasında köprü olma fikri aklımıza geldikten ve çalışmalara başladıktan yaklaşık 1-2 hafta sonra yaptığımız araştırmada "Teamfluencer" adında halihazırda hayata geçirilmiş bir proje olduğunu fark ettik. AdSphere fikrinden vazgeçmedik çünkü bu bize fazlasıyla küçük ölçekli ve bu işi el ile tek tek yapan işletmelere yönelik geldi. Bizim fikrimizin halihazırda herhangi bir uygulamanın kaplamadığı alanları kapladığına inandığımızdan projemize devam ediyoruz.

# Şuan Hangi Aşamadayız ve Bu Hafta Neler Yaşandı?

## Analiz Süreci

Yaklaşık üç ay süren derin bir analiz sürecimiz oldu, bu süreçte birçok iş kararı hakkında tartışmalar yaptık. Mentörümüzün de katkılarıyla işe yarar bir yapı ortaya çıkarabildik.

Veritabanı için tablolarımızı ve ER diyagramımızı ortaya çıkardık. Senaryo(lar) yazdık ve kurduğumuz yapı üzerinden senaryoları veritabanında nasıl gerçekleştiririz bunlara kafa yorduk.

Influencer ve Brand taraflarında sırasıyla üç ve dört rol olması gerektiğine karar kıldık ve 7 farklı rolün (aslında 5 diyebiliriz çünkü 2 tanesi tüm rolleri kapsayıcı konumda) farklı işlemlerini göstermesi için "Swimlane" adında güzel bir diyagram üzerine çalıştık. 

!["swimlane"](/images/adsphere/SWIMSWIM.png)

Şimdi ana süreçlerimiz, ve bu süreçlerin altındaki alt süreçler, her süreçte her rolün hangi işlemi hangi mantıkla gerçekleştirebileceği gibi bilgilerin hepsi elimizde güzelce belgelenmiş durumda.

Bunun üzerine mock up olarak ekranlarımızı, ve ekranlarla birlikte de 'functional', 'non functional', 'cosmetic', ve 'constraint' olmak üzere sınıflandırdığımız 250'den fazla gereksinim yazdık.

Yani epey analiz yaptık diyebiliriz, bunun bize geliştirmeye başladığımızda tekrar tekrar ana planda değişiklik yapmama gibi bir lüks sağlayacağına inanıyoruz ve ümit ediyoruz.

## Geliştirme Sürecine Geçişte Neden Bu Kadar Oyalandık?

Yaklaşık üç hafta önce analizimiz resmi olarak bittikten sonra hemen geliştirmeye geçmeye karar verdik. Geliştirme için güzel bir mono-repo, containerized yapı kurmaya karar verdim. Ben bu işlemleri yaparken takım arkadaşım İrem de bizim için Figma üzerinden mock-up'larımızı tasarımlara dönüştürüyordu.

### 1. Hafta

İlk hafta yapıyı kurdum; frontend, backend, database ayrı ayrı container'lar olarak tek bir docker compose komutu ile sorunsuzca ayağa kalkıp birbirine bağlanıyordu. Frontend uygulamamız Backend'e istek gönderiyor, Backend'imiz de Database'den 'Selam Dünya' değerini alıp Frontend'e gönderiyordu. Tüm bu kurulumu Google Cloud Platform üzerinden bir E2 Instance oluşturup uzak sunucuya da kurduk ve test ettik. Yani teknik olarak hem geliştirme yapmaya, hem de haftalık 'deploy'larımıza başlamaya hazırdık.

İrem bazı tasarımları hazırladı, 'swimlane'de bahsettiğim bir alt süreci gözümüze kestirdik ve bu hafta bunu yapıyoruz dedik.

### 2. Hafta

Ben bir ikileme düştüm, kodlama yaparken yapay zeka kullanımında ekstrem derecede kısıtlayıcı bir yaklaşımım var. Sanırım yapay zeka yokken kod yazmış en son nesildenim çünkü 1 ve 2. Sınıftayken geliştirdiğim projeler sırasında LLM'ler ortada yoktu. Sonrasında olanlar ortada.

Ancak şunu da çok iyi algılıyorum ki hiç yapay zeka kullanmamak da sadece yapay zekaya kod yazdırıp hiçbir şey bilmemekle benzer seviyede başka bir ekstremlik. 

Bir hafta boyunca Figma'da nasıl efektif şekilde tasarım hazırlarız, oradan LLM'in oluşturduğu React projesini kendi projemize 'kontrollü' bir şekilde nasıl taşırız buna kafa yordum. Çünkü ne iş yaptığını algılamadığım bir yapıyı bırakın, tek bir parçayı bile projeme eklemek istemiyorum.

Nihayetinde 'shadcn/ui' kütüphanesi ve 'tailwindcss' ile ilgili takip etmesi gereken kuralları net bir biçimde belirttiğimiz bir 'prompt'u Figma'nın 'Make' kısmından koda dönüştürüp, tüm yapıyı ya da işlevselliği değilse bile ayrı ayrı 'component'ları çekebileceğimiz sonrasında parçaları elimizle birleştirebileceğimiz adım adım takip edilecek bir protokolü oluşturdum ve pratikte test ettim.

Bu ne kadar bir kazanım gibi görünse de bu hafta geliştirmeye başlamalı ve ilk sürecimizi her anlamda tamamlamış olmalıydık.

Ayrıca İrem'le birlikte Figma'nın Make kısmından yapılan tasarımların birbirine aşırı benzemesi, tam istediğimizi yansıtamaması nedeniyle artık tasarımları en baştan İrem'in elle yapmasına karar verdik.

### 3. Hafta

Yani bu şuan bırakın olmamız gereken yeri, başlayabileceğimiz sıfır noktasından bile gerideydik demek oluyordu. Figma'dan projeye nasıl taşırız, tasarımı nasıl yaparız konularıyla 2. Haftanın tamamını, 3. Haftanın da yarısını çöpe atmıştık.

> Burada şunu belirtmeliyim: bizim haftalarımız Cuma günü mesai çıkışında sona eriyor, ve yeni hafta başlıyor. Yani Cuma günleri bizim 'deployment' günlerimiz.

### 3. Haftanın Çarşamba Günü

Günlük SCRUM'lar yapmaya karar vermiştik yani her gün hızlıca, on beş dakika içerisinde hangi işte ne aşamaya geldim ve bugün neye odaklanacağım sorularını cevaplıyorduk.

Birkaç gündür aksattığımız bu hızlı toplantılardan birini İrem'le Mühendislik Fakültesi kantininde yaptık. Kelimenin tam anlamıyla hiçbir ilerleme olmaması iyice gün yüzüne çıkmış oldu. Cuma günü 2 numaralı alt aşamayı bitirmiş olmalıydık ve biz az önce de bahsettiğim gibi ilk aşamaya bile başlama noktasında değil, sıfırın da gerisindeydik.

Hızlı toplantımızın sonunda İrem kütüphaneye gitti ve arayüzlerin tasarımı ile ilgili işine başlayacağını söyledi. 

Aslında benim o günkü planım eve gitmekti ancak içim rahat etmedi, tüm bu zaman kaybını ortadan kaldırıp asıl işe başlamamız gerektiğini düşünüyordum bu nedenle yoldan dönüp ben de kütüphaneye gittim. O andan itibaren bizim ekibimiz için HOH Development modeline geçiş başladı ve geliştirmenin 3.haftasının kaderi tamamen değişti.

# HOH Development Modeli Nedir?

### HOH Nereden Geliyor?

2024 yazında Galatasaray'ın orta sahasında geçtiğimiz sezondan kalan ve bir sonraki sezonda hiç randıman vermeyecek olan Sergio Oliveira, Frederik Midtsjo gibi oyuncular vardı. Mükemmel performans veren Lucas Torreira'nın yanına sağlam, fizikli, ve becerikli bir orta saha oyuncusu aranıyordu. Bu orta saha oyuncusu için kulüp tarihinin en büyük bonservisi verileceği dedikoduları hakimdi, o yüzden epey süre boyunca birçok isim geçti.

Ben de aynı yazın hemen başında Erasmus+ kapsamındaki stajım için Polonya'ya gitmiş, iş ortamıma ve yurduma yeni alışırken yalnız olduğum anlarda yürürken ya da bisiklet sürerken YouTube'dan bu konu ile ilgili yorumları dinliyordum.

Bu yeni transfer için o kadar isim yazıldı ve iptal oldu ki Uğur Karakullukçu'nun kanalındaki canlı yayınlarda artık Galatasaray kadrosu yazılırken Lucas Torreira'nın yanına HOH8 yazılıp geçiliyordu. 

Bu takıma lazım olan şeyler sıralanırken ve transfer listesi yazılırken HOH8 en başa yazılır, sonra kalan yerlere aday oyuncular doldurulurdu.

Yolda yürürken nedir bu HOH8 deyip durduğumu ve canlı yayının sohbetinde ***'hayvan oğlu hayvan sekiz numara'*** yazısını gördüğümü hatırlıyorum.

> Bu arada o yaz bunca kaosun arasında Galatasaray Okan Buruk'un çok istediği Scott McTominay yerine Championship'ten Gabriel Sara'yı getirdi. Bugünlerde McTominay'in Napoli'de yaptığı şovun ardından bu kararın ne kadar büyük bir rezalet olduğunu daha net görüyoruz.

### Kütüphanede Ne Oldu Da Haftanın Kaderi Değişti?

Ne kadar hoş bir açılımı olmasa da İrem'e 'HOH Development Modeli'ne geçtiğimizi ve başlamak üzere olduğu görevi tamamen boş vermesini istediğimi söyledim. Asıl işimize odaklanıp hızlı hareket etmeye başladık.

**Çarşamba günü** İrem veri yapısını oluşturmayı bitirdi, senaryomuzdaki tüm süreci veri yapısı üzerinden başarıyla yürüttüğü bir test gerçekleştirdi.

Ben de dünyanın en düz, dümdüz varsayılan HTML elementlerinden oluşan arayüzümüz ile sadece işlevselliği yürütebileceğimiz şekilde React'te basit birkaç sayfa ve component yazdım. Ardından Flask'ta ihtiyacımız olan API'ları yazmaya başladım.

![](/images/adsphere/signup2.png)

> Çarşamba akşamı arabamın arızalanmasıyla Perşembe gününün tamamını evde AdSphere üzerinde çalışarak geçireceğim kesinleşmiş oldu.

**Perşembe günü** 1. Alt aşamamızın tamamını kurguladım, hangi sayfa hangi API'ye istek atacak, hangi API hangi Query'i çalıştıracak. Hangi sayfaya geçilecek? Veri yapısı nasıl birbirine uydurulacak? Bu gibi soruların tamamını kurguladım ve çalıştım.

Bu kurguyu kurarken kafam o kadar doluyordu ki pek çok detayı hemen o anda unutabiliyordum. İrem'e ondan istediğim Query'lerin girdilerini, istediğim çıktıları, hangi API'de ne için kullanılacağını, bu API'nin hangi sayfalarda kullanılacağı ile ilgili bilgileri aktaran bir PDF yolladım.

### Ticket Sistemine Geçiş

Yolladığım PDF sayesinde tekrar tekrar toplantılar yapmaktan kurtulduk, ben de bu PDF gibi bir görev 'template'i ile Asana üzerinden İrem için 'ticket'lar oluşturmaya başladım. 

**Cuma günü**, Perşembe geceye kadar çalıştığımız halde yakaladığımız ivmeyi sürdürmek için sabah 8'de ofisteydik. Mesai saatlerinin sonuna kadar 1. Aşamamızın neredeyse her detayını geliştirdik ve test ettik. Bitirmeden önce de oluşan problemlerin her birinin çözümü ile alakalı Asana'ya detaylı 'ticket'lar yazdık.

Sürekli olarak 'git' kullanmaya, 'Conflict'leri çözmeye, gerçekten hızlı bir biçimde geliştirme yapmaya iyice alıştık.

Tekrar tekrar toplantılar yapmak, neyi nereye nasıl bağlayacağımı unutmak, İrem'den istediğim query'leri, girdileri, çıktıları, bağlanacakları noktaları unutup durmak yerine Asana üzerinden böyle bir sisteme geçmek bizi hem çok hızlandırdı hem çok rahatlattı.

Artık sistem mimarisini çok daha rahat bir şekilde kurguluyor ve yürütebiliyoruz.

# Önümüzdeki Hafta İçin Hedefler ve Plan Ne?

Bu haftanın sonunda 2. Alt aşamamızı bitirmiş olmalıydık, şuan buna başlama noktasındayız.

Projemiz için James Clear'ın Atomik Alışkanlıklar kitabında okuduklarım doğrultusunda hedefler koymak ve planlar yapmaya gayret ediyorum.

Nihayetinde yakaladığımız ivmeye ve sistemimize odaklanıyoruz, üç günde karmaşık bir alt aşamayı tamamladık. Aynı ivmeyi sürdürerek önümüzdeki haftanın sonunda nispeten daha az karmaşık olan 2 ve 3. alt aşamaları da tamamlamayı hedefliyoruz.

Hedefimize yönelik bir çalışma ve ivmemiz olduğu için, olduğumuz yere de büyük bir hız ve gelişmeyle geldiğimiz için olumlu hissediyorum. Bu fazlasıyla uzun ve epey gereksiz bilgi barındıran ilk devlog'u burada noktalıyorum. Önümüzdeki devlog'ların çok daha kısa ve sade olmasını umuyorum. Bu haftalık, görüşmek üzere.