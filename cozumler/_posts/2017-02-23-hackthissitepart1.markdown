---
layout: post
title: HackThis Web Walkthrough Part 1
date: '2017-02-23 15:15:50 +0300'
categories: cozumler
---
 
 Merhabalar 
 
 Bu ilk walkthrough yazımda oldukça eski olan fakat benim daha geçenlerde keşfettiğim
 [hackthis.co.uk](https://www.hackthis.co.uk/) sitesindeki bazi soruları inceleyecegiz.
 Soru zorluklarının kademeli olarak arttığı bu site yeni başlayanlar, bir temel oluşturmak ve pratik
 yapmak isteyenler için gayet ideal.

 Main level soruları genel olarak sitelerin kaynak kodlarından doğabilecek zaafiyetleri ve sitede
 saklanmış bazi gizli dizinler üzerindeki zaafiyetleri kavratmayı amaçlamış.

Ilk soruyla başlayalım 




__Main level 1__

![]({{ AUCyberClub.github.io }}/assets/img/hackthis/1.png)



Amacımız buraya giriş yapmak.
Ilk cümlelerinde belirttiğim gibi yeterince güvenlik önlemi alınmamış ve/veya bazı ufak ayrıntıların 
gözden kaçırıldığı web sitelerinin kaynak kodlarında çok kritik bilgiler bulunabiliyor. 
O yüzden **ctrl + u** kombinasyonu ile kaynak koda bir göz atalım;

   -```(Kaynak kod = Herhangi bir yazılımın işlenip makina diline çevrilmeden önce insanların okuyup
   üzerinde çalışabildiği programlama diliyle yazılmış hali.Websiteleri icin , php,html,javascript ...)```
   


![]({{ AUCyberClub.github.io }}/assets/img/hackthis/soru1-2.png)



**Ctrl + F** kombinasyonu ile çok temel bir şekilde **password** keywordunu arattım ve  karşımıza
çıkan ilk şey bir kullanıcı ismi ve parola bilgisi oldu **username = in , password=out**.
Tabiki bu şuan gözünüze çok basit gelmiş olabilir ama gerçek hayatta da böyle durumlarla karışılaşılabiliyor.
Source kodunun önemini bir nebze daha anladığımıza göre çözümlere devam edelim.




__Main level 2__

![]({{ AUCyberClub.github.io }}/assets/img/hackthis/2.png)




 Artık source kodun önemini biraz daha kavradığımıza göre , bu bölüm içinde source kodumuza bir
 göz gezdirelim.



![]({{ AUCyberClub.github.io }}/assets/img/hackthis/3.png)



Ilk bolumden farkli olarak bu sefer password ve username bilgisini gözden kaçırma ihtimaliniz
biraz daha yüksek. Hem sayfanın en altlarında bulunuyor hem de yanında yazını tipini rengini
belirleyen bir kaç kod ile iç içe verilmiş. Burdaki **resu** ve **ssap** kelimelerini dikkatli
bakmazsanız gözden kaçırabilirsiniz. Tabiki her zaman bu durum böyle olmayacak fakat bunlar
temel durumlar ve dikkat edilmeli.




__Main level 3__

![]({{ AUCyberClub.github.io }}/assets/img/hackthis/4.png)



Bu sorumuzda , önceki ilk iki sorudan farklı olarak bir JavaScript zaafiyeti var. JavaScript komutları
düzgün kullanılmaz ve gizlenilmez ise tıpkı source kodda olduğu gibi oldukça kritik bilgileri ifşa edebilir.
Burdaki javascript kodunu incelemek için source koda bakmak yerine , **username** boşluğuna gelip sağ tıklayarak
**inspect element(öğeyi incele)** özelliğini kullanıyorum. Bu bir nebze olsun daha pratik.

 -```Inspect Element : "ctrl + u" kombinasyonuna ek olarak , websitesinin source kodunu görebileceğiniz ve değişiklikler
    yapabileceğiniz bir tool.```




![]({{ AUCyberClub.github.io }}/assets/img/hackthis/5.png)



Ve javascript kodunu incelediğimizde bir **if else** statement ti karşımıza çıkıyor.Bu statementı
anlamak için herhangi bir programlama bilgisine gerek bile yok.

-```Eğer if statement’inin sonucu “1(true)” ise altında belirtilen işlemi yap, eğer “0(false)” ise “else”
kısmının altında belirtilen işlemini yap.```

Burdaki statement'a göre  eğer **username == Heaven ve password == Hell** koşulu sağlanırsa giriş
kabul edilir.




__Main level 4__

![]({{ AUCyberClub.github.io }}/assets/img/hackthis/6.png)



Artık biraz pratik yaptığımıza ve dikkatimizi topladığımıza göre, hadi direk source koddan bir bilgi
elde edebiliyor muyuz bu soru için inceleyelim.



![]({{ AUCyberClub.github.io }}/assets/img/hackthis/7.png))



Source kodda levelimizin olduğu bölmeye indiğimiz zaman ilk başta herhangi bir password yada
username bilgisi görünmüyor. Eğer dikkatli bakarsak **../../extras/ssap.xml** detayındaki anormalliği
görebiliyoruz.
Bu soru sitedeki kritik bilgi içeren gizli dizinlerle ilgili. Direkt olarak uzantıyı kopyalayıp linke
yapıştırdığımızda bizim için gerekli olan username ve password bilgisini ele geçirmiş oluyoruz.


![]({{ AUCyberClub.github.io }}/assets/img/hackthis/8.png)




__Main level 5__

![]({{ AUCyberClub.github.io }}/assets/img/hackthis/9.png)



Soruya girer girmez bizi bir prompt pop-up karşılıyor. ```Prompt javascript ile yazılmış
kullanıcıdan bilgi alan bir pop’up.``` Yine bizden bir password bilgisi bekleniyor önceki sorulardan da
geliştirdiğimiz bilgi birikimiyle hadi source koda bir göz atalım ;

Ve işte prompt komutu ve birde if statementi. 


![]({{ AUCyberClub.github.io }}/assets/img/hackthis/10.png)


Önceki sorudada bahsettiğimiz gibi burdada
passwordun **9286jas** ya eşit olması durumunda bizim bölümü tamamlamamızı sağlıyor.




__Main level 6__

![]({{ AUCyberClub.github.io }}/assets/img/hackthis/11.png)


Bu soruda bizden siteye Ronald olarak giriş yapmamızı istiyor ama seçeneklerde Ronald yok.
Şimdi bizim yapmamız gereken tek şey eğer source kodda gizlenmediyse bu isimlerden birini
Ronald ile değiştirmek ve/veya aynı kodu Ronald içinde eklemek. Böyle değiştirme işlemleri için
ctrl+u yapıp source koda bakmak yerine **inspect element(öğeyi incele)** özelliğini kullanıyoruz.


![]({{ AUCyberClub.github.io }}/assets/img/hackthis/12.png)


User seçimiyle ilgili kod açık şekilde görülüyor. Şimdi tek yapmamız gereken şey userlardan birini
değiştirmek;

Değiştirmek için koda tıklıyorum ve ardından herhangi bir userin üzerine gelip **F2** tuşuna basarak
ismi tekrar düzenliyorum.


![]({{ AUCyberClub.github.io }}/assets/img/hackthis/13.png)


Ve artık Ronald diye bir user var .
**inspect element(öğeyi incele)** özelliği **client side** çalıştığı için sayfayı yenilediğinizde yaptığınız 
değişiklikler silinecek ve dolayısıyla **Ronald** seçeneğide kaybolucak.

 -```Client Side : Web tarayıcıları üzerinde çalışan istemci taraflı programlamalar.```


__Main level 7__

![]({{ AUCyberClub.github.io }}/assets/img/hackthis/14.png)

Bu bölüm diğerlerine nazaran biraz daha deneyim isteyen bir bölüm ve beni en çok uğraştıran bölüm.
Source kodunda herhangi bir bilgi bulamadım , hatta dirbuster(directory fuzzing) programi
ile gizli dizin bile aradım ama yine sonuç alamadım (aslında sonuç alamama sebebim dizini yanlış
uzantıya göre aratmamdı. "/level/mains/7" yerine direk olarak hackthis.co.uk/ olarak aratsam bulurdum.)

 -```( “Directory Fuzzing = Bir web sitesindeki gizli dizinleri elle ve/veya bir wordlist ve script ile
 deneme yanılma (brute force) yöntemiyle bulmak ve gizli dizinleri ortaya çıkarmak icin kullanılan
 bir yöntem. Örnek olarak = Dirbuster.” )```
 

![]({{ AUCyberClub.github.io }}/assets/img/hackthis/15.png)


Ve bir kaç saat sonra boş boş film izlerken kafama bir dosya dank etti **Robots.txt** !

 -```“Robots.txt” arama motoru tarayıcılarının web sitelerinin  erişilmesi istenmeyen  yerlerini gösteren
 ve sitenin “kök dizininde”  bulunan bir dosyadır. Normal şartlarda bu dosyaya dışardan erişim
 engellidir ama çoğu durumda burdan kritik bilgiler elde edebilirsiniz.```


![]({{ AUCyberClub.github.io }}/assets/img/hackthis/16.png)


Gördüğünüz üzere bu dosya sadece 7.soruyla alakali değil farkli bilgiler de barındırıyor. Benim
gözüme çarpan ilk şey **/levels/extras/userpass.txt** oldu  ve o dizine gittim.
Ve gerekli username ve password burdan geldi.


![]({{ AUCyberClub.github.io }}/assets/img/hackthis/17.png)





__Main level 8__

![]({{ AUCyberClub.github.io }}/assets/img/hackthis/18.png)

Bu sorumuzda hintten yola çıkara yine ilk olarak bi source koda göz atıyoruz;

![]({{ AUCyberClub.github.io }}/assets/img/hackthis/19.png)

Ve yine açıkta kalmış bir gizli dizin gözümüze çarpıyor.
Dizine gittiğimizde bizi encrypt edilmiş 2 satır bilgi karşılıyor;

![]({{ AUCyberClub.github.io }}/assets/img/hackthis/20.png)

Bunu uzun uzadıya aramak istemediğim için hint kısmına baktım ve hintte **base16** da okumak daha
basit gibi bir ifade vardı . Google’a binary to hexadecimal(base16) converter yazarak ilk siteye
girdim;

![]({{ AUCyberClub.github.io }}/assets/img/hackthis/21.png)
![]({{ AUCyberClub.github.io }}/assets/img/hackthis/22.png)


Ilk satırı çevirdiğimde **B00B** ve ikinci satırı çevirdiğimde ise **FEED** değerleri
geldi.Böylece sitedeki dizinlerin önemini bir kez daha görmüş olduk.


__Main level 9__

![]({{ AUCyberClub.github.io }}/assets/img/hackthis/23.png)

Bu soruda developerin kendine password erişimi için yazdığı kodu exploit edip passwordu almamız
isteniyor;

Request details’e tıkadıkdan sonra gelen email gönderme formuna sağ tıklayıp **inspect element(öğeyi incele)**
dediğimde developerin eklediği kodu açıkca görebiliyoruz.

![]({{ AUCyberClub.github.io }}/assets/img/hackthis/24.png)

Eğer **value**deki email adresini kendi emailimiz yaparsak şifre bize gelmiş olucak.

![]({{ AUCyberClub.github.io }}/assets/img/hackthis/25.png)

**F2** ye basarak düzenleme bölmünü açıyorum ve emaili kendiminkiyle değiştiriyorum. Ve emailimi
yazip submit diyorum;

![]({{ AUCyberClub.github.io }}/assets/img/hackthis/26.png)

Bu levelimizde burda bitmiş oluyor.



__Main level 10__

Ve main seviyesinin son bölmüne geldik.

![]({{ AUCyberClub.github.io }}/assets/img/hackthis/27.png)

Edindiğimiz bilgi birikimlerinden yola çıkarak yine önce sayfanın kaynak kodunu inceleyerek
başlıyoruz. Fakat bu sefer **ctrl + u**  yapmak yerine direkt olarak sağ tıklayıp **öğeyi incele**
diyorum (tamamen şahsi isteğime bağli).

![]({{ AUCyberClub.github.io }}/assets/img/hackthis/28.png)

Ve yine bir gizli dizin ile karşılaşıyorum **level10pass.txt**.
Dizine gittiğimide karşımıza 2 adet **hash** cıkıyor .

 -```Basit olarak Hash'i encrypt edilmiş bilgi olarak tanımlayabiliriz.``` 

![]({{ AUCyberClub.github.io }}/assets/img/hackthis/29.png)

Google’a hash cracker yazarak çıkan ilk siteye giriyorum ve hash’lerı kırmaya çalışıyorum;


![]({{ AUCyberClub.github.io }}/assets/img/hackthis/30.png)

![]({{ AUCyberClub.github.io }}/assets/img/hackthis/31.png)


Tabiki hash kırma işlemini offline olarak yapan araçlarda mevcut ama ben bulabileceğinden emin
olduğumdan dolayi online bakmayı tercih ettim ve göründüğü gibi bu sorumuzu da burda bitirmiş
oluyoruz.Bunları yapmak oldukça eğlenceliydi umarım sizde okurken güzel vakit geçirmişsinizdir.

---  
**[Engin Demirbilek](https://twitter.com/Hyal0id)**
