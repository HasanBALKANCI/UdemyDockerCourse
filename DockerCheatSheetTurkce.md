[A'dan Z'ye Docker](https://ozgurozturk.net/docker-udemy) eğitimimdeki öğrencilerimin yararlanabilmesi adına Docker Cheat Sheet yani Türkçeleştirirsek "Docker komutlarının nasıl kullanıldığının bir listesi" hazırladım. Yararlı bir derleme olduğunu düşünüyorum. Daha geniş bir kitleye ulaşabilmesi için de burada yayınlıyorum. Kolay gelsin.  

***Docker Cheat Sheet (Türkçe)***
___

* ***Container***

**Container çalıştırma:**

`docker container run image:tag`

Örnek: `docker container run nginx:latest`
___
**Detach modda container çalıştırma (-d):**

`docker container run -d image:tag`

Örnek: `docker container run -d nginx:latest`
___
**Varsayılan uygulama yerine başka uygulama ile container başlatma:**

`docker container run image:tag uygulama`

Örnek: `docker container run ubuntu:latest ping 127.0.0.1`
___
**Container'a bir isim vererek çalıştırma**

`docker container run --name isim image:tag`

Örnek: `docker container run --name container1 -d nginx:latest`
___
**Çalışan bir container içerisinde başka bir uygulama çalıştırma:**

`docker container exec container_id|ya da|container_ismi uygulama`

Örnek: `docker container exec 12a793b3fec0 ping 127.0.0.1`
___
**Çalışan bir container'a shell bağlantısı oluşturma:**

`docker container exec -it container_id|ya da|container_ismi sh`

Örnek: `docker container exec -it 12a793b3fec0 sh`
___
**Container'ı detach modda ve shell bağlantısı ile oluşturma (dit):**

`docker container run -dit image:tag sh`

Örnek: `docker container run -dit nginx:latest sh`
___
**Detach modda ve shell bağlantısı ile oluşturulmuş container'a bağlanma:**

`docker attach container_id|ya da|container_ismi`

Örnek: `docker attach 12a793b3fec0`
___
**Container durdurma:**

`docker container stop container_id|ya da|container_ismi`

Örnek: `docker container stop 12a793b3fec0`
___
**Container silme:**

`docker container rm container_id|ya da|container_ismi`

Örnek: `docker container rm 12a793b3fec0`
___
**Çalışan containerı silme (-f):**

`docker container rm -f container_id|ya da|container_ismi`

Örnek: `docker container rm -f 12a793b3fec0`
___
**Container kapatıldığı zaman aynı zamanda silinmesi (-rm):**

`docker container run -rm image:tag`

Örnek: `docker container run -rm nginx:latest` (-rm ile container kapandığı zaman otomatik olarak silinmesini söylüyoruz)
___
**Container ile ilgili detayları inceleme:**

`docker container inspect container_id|ya da|container_ismi`

Örnek: `docker container inspect 12a793b3fec0`
___
**Sistemdeki tüm containerları (çalışan ve durdurulmuş) silme**

`docker container rm -f $(docker ps -aq)`
___
**Sistemdeki çalışan containerları listeleme:**

`docker container ls` ya da 

`docker container ps`
___
**Sistemdeki tüm containerları listeleme:**

`docker container ls -a` ya da 

`docker container ps -a`
___
**Çalışan container'daki processleri listeleme:**

`docker top container_id|ya da|container_ismi`

Örnek: `docker top 12a793b3fec0`
___
**Çalışan container'ın Cpu, Ram, I/O kullanımını görme:**

`docker stats container_id|ya da|container_ismi`

Örnek: `docker stats 12a793b3fec0`
___
**Container'ın memory kullanımını sınırlama (--memory, --memory-swap):**

`docker container run --memory=rakam(b,k,m,g) --memory-swap=rakam(b,k,m,g) image:tag`

Örnek: `docker container run --memory=1g --memory-swap=2g nginx:latest` (memory-swap ile swap alanı da tanımlayabiliriz.b=byte k=kilobyte m=megabyte g=gigabyte)
___
**Container'ın cpu kullanımını sınırlama (--cpus, --cpuset-cpus):**

`docker container run --cpus="core_adeti" image:tag`

Örnek: `docker container run --cpus="3" nginx:latest` (sistemden kaç core'a erişebileceğini belirledik)

`docker container run --cpuset-cpus="core_numarası" image:tag`

Örnek: `docker container run --cpuset-cpus="0,4" nginx:latest` (sistemdeki hangi corelara erişebileceğini belirledik)
___
**Container'a enviroment variable tanımlama:**

`docker container run --env enviroment_variable=değeri image:tag`

Örnek: `docker container run --env VAR1=deneme1 --env VAR2=deneme2 nginx:latest`
___
**Containerdan hosta ya da tam tersi dosya kopyalama:**

`docker cp container_id|ya da|container_ismi:path host_path`

Örnek: `docker cp 12a793b3fec0:/usr/src/uygulama/ .`

___
___
___

* ***Image***

**Docker CLI aracılığıyla registery'de oturum açma:**

`docker login registery_url`

Örnek: `docker login localhost:8080`
___
**Sisteme bir imaj çekme:**

`docker image pull image:tag`

Örnek: `docker image pull nginx:latest`
___
**Docker hub'a (ya da başka bir repository) image gönderme:** 

`docker image push repository/image:tag`

Örnek: `docker image push ozgurozturknet/adanzyedocker:latest`
___
**Mevcut bir imaja yeni tag ekleme**

`docker image tag image:tag yeniimage:tag`

Örnek: `docker image tag nginx:latest ozgurozturknet\nginx:v1`
___
**Image ile ilgili detayları inceleme:**

`docker image inspect image:tag`

Örnek: `docker image inspect nginx:latest`
___
**Image layerlarını listeleme:**

`docker image history image:tag`

Örnek: `docker image history nginx:latest`
___
**Dockerfile kullanarak yeni bir imaj yaratma:** 

`docke image build -t image:tag .`

Örnek: `docker image build -t ozgurozturknet\merhaba-dunya:latest .` (Dockerfile dosyası komutun çalıştırıldığı folder'da bulunmalı)
___
**Image oluştururken build arg kullanma:**

`docker image build --build-arg arg=deger -t image:tag .`

Örnek: `docker image build --build-arg VERSION=3.7.1 -t nginx:latest .`
___
**Sistemdeki tüm imageleri listeleme:**

`docker image ls`
___
**Sistemden bir imajı silme:**

`docker image rm image:tag`

Örnek: `docker image rm nginx:latest`
___
**Containerdan image yaratma:**

`docker commit container_id|ya da|container_ismi image:tag`

Örnek: `docker commit 12a793b3fec0 ozgurozturknet/img:latest`
___
**Image'i bir dosyaya kaybetmek ve kaydedilmiş bir dosyadan image oluşturmak:**

`docker save image:tag -o dosyaadi.tar`

Örnek: `docker save ozgurozturknet/img:latest -o image.tar`

`docker load -i dosyaadi.tar`

Örnek: `docker load -i imagecon1.tar`

___
___
___

* ***Volume***

**Volume oluşturma:**

`docker volume create volume_ismi`

Örnek: `docker volume create ilkvolume`
___
**Volume ile ilgili detayları inceleme:**

`docker volume inspect volume_id|ya da|volume_ismi`

Örnek: `docker volume inspect ilkvolume`
___
**Sistemdeki tüm volumeleri listeleme:**

`docker volume ls`
___
**Volume'u container'a bağlama (-v):**

`docker container run -v volume_ismi:container_icindeki_path image:tag`

Örnek: `docker container run -v ilkvolume:/var/www/html image:tag`
___
**Volume'u container'a sadece okunur şekilde bağlama (:ro):**

`docker container run -v volume_ismi:container_icindeki_path:ro image:tag`

Örnek: `docker container run -v ilkvolume:/var/www/html:ro image:tag`
___
**Host üstündeki bir klasör ya da dosyayı bind mount olarak bağlama:**

`docker container run -v host_klasör_path:container_icindeki_path image:tag`

`docker container run -v c:\websitesi:/usr/share/nginx/html nginx:latest `
___
**Volume silme:**

`docker volume rm volume_ismi`

Örnek: `docker volume rm ilkvolume`

___
___
___

* ***Network***

**Kullanıcı tanımlı bridge network oluşturma (bridge):**

`docker network create --driver=bridge network_ismi`

Örnek: `docker network create --driver=bridge kopru`
___
**Kullanıcı tanımlı bridge network oluşturma (ip bilgilerini belirleyerek):**

`docker network create --driver=bridge --subnet=cidr --ip-range=cdir --gateway=ip_adresi network_ismi `

Örnek: `docker network create --driver=bridge --subnet=10.10.0.0/16 --ip-range=10.10.10.0/24 --gateway=10.10.10.10 kopru`
___
**Sistemdeki tüm volumeleri listeleme:**

`docker network ls`
___
**Volume ile ilgili detayları inceleme:**

`docker network inspect network_ismi`

Örnek: `docker network inspect kopru`
___
**Container'ı varsayılan dışında bir network'e bağlayarak çalıştırma:**

`docker container run --network network_ismi image:tag`

Örnek: `docker container run --network kopru nginx:latest`
___
**Çalışan bir container'ı başka bir network'e bağlama:**

`docker network connect network_ismi container_id|ya da|container_ismi`

Örnek: `docker network connect kopru 12a793b3fec0`
___
**Çalışan bir container'ın bağlı olduğu networkle bağlantısını kesme:**

`docker network disconnect network_ismi container_id|ya da|container_ismi`

Örnek: `docker network disconnect kopru 12a793b3fec0`
___
**Port publish ederek bir container çalıştırma (-p):**

docker container run -p host_portu:container_portu/tcp_yada_udp image:tag

Örnek: docker container run -p 8080:80 -p 53:53/udp nginx:latest

___
___
___

* ***Logging***

**Container tarafından oluşturulan logları görmek:**

`docker logs container_id|ya da|container_ismi`

Örnek: `docker logs 12a793b3fec0`
___
**Container tarafından oluşturulan logları uzun formatta detaylı görmek:**

`docker logs --details container_id|ya da|container_ismi`

Örnek: `docker logs --details 12a793b3fec0`
___
**Container tarafından oluşturulan logları belirli tarih aralığında görmek:**

`docker logs --since tarih_saat --until tarih_saat container_id|ya da|container_ismi`

Örnek: `docker logs --since 2020-01-13T11:34:43.154304300Z 12a793b3fec0` (since verilen andan itibaren olanları, until ise verilen ana kadar olanları listeler)
___
**Container tarafından oluşturulan logların belirli sayıda son oluşanlarını görmek:**

`docker logs --tail sayı container_id|ya da|container_ismi`

Örnek: `docker logs --tail 10 12a793b3fec0` (son 10 log çıktısını listeler)
___
**Container tarafından oluşturulan logları anlık olarak izlemek:**

`docker logs -f container_id|ya da|container_ismi`

Örnek: `docker logs -f 12a793b3fec0` (loglar oluştukça ekranda gözükecektir. Ctrl-C ile bağlantı kesilebilir)

Note to Self:

1. Container Temelleri-2 :

   * Her container imajinda o imajdan bir container yarattigimiz zaman varsayilan olarak calismasi icin ayarlanmis bir uygulama vardir. Bu uygulama calistigi surece container ayakta kalir. uygulama calismayi biraktiginda container da kapanir.

   * Imajlarin icinde istenilen sayida uygulama koyulabilir.

   * Birden fazla uygulama olsada container create edilirken sadece tek uygulama secilebilir. Varsayilan olarak secilir. (servis olarak adlandirilir)

   * Bu uygulamayla calismaya baslayan containerda daha sonra farkli uygulamada calistirilabilir.

   * Container create yapilirke hangi uygulamayi calistirmasini istedigimizi belirtebiliriz. Belirtilmezse varsayilan uygulama calisir.

   * names ler --name tagiyle olusturulabilir, yoks default olarak sistem kendi atart. ismin ilk kelimesi sifat ikincisi IT dunyasina hizmet etmis unlu birinin ismidir.

   * calisan konteyner silinemez once stop yapilmali. yada rm -f kullanilir.


   Commands:

   * docker container run -p 80:80 ozgurozturknet/adanzyedocker

   * docker container ls

   * docker container logs eb4 # <container id, ilk uc harf genelde yeterli, names de yazilabilirdi bu durumda  tamami yazilmali.>

   * docker container run --name denemecon ozgurozturk/adanzyedocker java app1

   * docker container stop eb

   * docker container run -d ozgurozturknet/adanzyedocker

   * docker container rm -f 07

   * docker container stop 07

   * docker container rm 07 aa 50 eb 07

2. Container Temelleri-3
   
   * Imajlar ideal olarak tek uygulama calistirilacak sekilde dizayn edilmesi ve imaj asamasinda tamamlanmasi gerekir.

   * Container in icinde birden fazla uygulama calisabilir. Sadece conteiner run edilirken biz sadece bir uygulamanin calismasini isaret edebiliriz. 

   * ayni imajdan sonsuz container olusturabiliriz. A containerrinda imajda yapilan bir degisiklik, o imajdan olusturulan B containerini etkilemez. Her konteiner bagimsizdir. Isoledir.

     - 

   Commands:

   * docker container run --name websunucu -p 80:80 -d ozgurozturknet/adanzyedocker

   * docker container exec -it 00 sh (calisan contianerin icine girme, baglanma)

   * java app1.java  ( container icinde baska bir uygulama calistirabildik)

   * ps (containera bagliyken icinde calisan tum uygulamalari gösterir)

   * exit (containerdan cikar shelle geliriz ama arka planda container exited dir stop eder.)

   * container ps

   * ctrl + d +a (containerdan cikariz ama container arka planda calisir)

   * kill 1 ( containerin icinde 1 nolu calisan uygulama herzaman contanira baglidir. o uygulama kapatilirsa kontainer otomatik kapanir. ve bizi shell e atar)

   * docker container start websunucu

   * docker container stop websunucu

3.  * Docker Katmanli Dosya Sistemi Yapisi
     - docker depolama altyapisinda union file system kullanir. Her degisiklik ayri bir katmanda depolanir. 

     - Bu katmanlarin bir araya gelerek olusturduklari da image olur.

     - bir image dan container olusturulurken, docker bu imaji R/O read only olarak tutar. Ustune bir katman daha ekler. Bu katmana Container yazilabilir katmani (R/W) denir. Containerdaki tum degisiklikler bu yazilabilir katmanda olur. Image de degisiklik olmaz R/o olarak kalir.

     - Dosyalarin ayri katmanlarda olmasina ragmen bir arada gormemizi saglayan union file systemdir. ls yaptigimizda ayni yerdedir.

     - (Copy on Write) Image icindeki R/O layerdan birini degistirmek istersek, R/O katmandaki file i R/W katmanina kopyalayip degisikligi burda yaparak islemi gerceklestirir.

     - farkli imagelerde ortak layerlar tekrar indirilmez, o layerlar birbirine map edilerek kullanilir.

    * Command:
       - docker container prune
       - docker image ls
       - docker image prune -a (-a all)
       - docker image pull alpine (tek katman)
       - docker image pull ozgurozturnet/hello-app (iki katman)

4. Docker Volume:
  * Container gibi ayri bir structure der. Containera baglayip ayirabiliriz.

  * containeri silsek bile volume ve icindeki dosyalar silinmez.

  * bir volume birden fazla containera baglanabilir. Ve containerdaki dosyalara erisebilir.

  * bos-dolu container baglandiginda davranis farklari vardir. 

  * eger bir volume mount edildigi klasor mevcut degilse bu klasoru olusturur. Ve o anda volume icinde hangi dosyalar varsa bu klasorde de o dosyalar görulur.

  * eger bir volume imaj icerisinde bulunan mevcut bir klasore mount edilirse:
    - A: Klasör bossa o anda volume icerisinde hangi dosyalar varsa bu klasörde de o dosyalari görursunuz.
    - B: Klasörde dosya varsa ve volume bossa klasördeki dosyalar volume kopyalanir.
    - C: Klasörde dosya var ya da yok fakat volume'de dosyalar varsa yani volume bos degilse, volumedeki dosyalari klasörde göruruz. DIKKAT! Hem klasör hem de volumedeki dosyalar degil, sadece volumedeki dosyalar görulur.

  * Commands :
    - docker volume create ilkvolume

    - docker volume inspect ilkvolume

    - docker container run  -it -v ilkvolume:/deneme3:ro centos sh

    - docker container run -it -v ilkvolume:/uygulama alpine sh (volume adi:/container icinde volume baglamak istedigimiz klasor, yoksa olusturur)

    - docker container run -it -v ilkvolume:/readonly:ro centos sh (raed only oldugu icin burda file olusturulamaz, ama volume bagli baska containerlarda olusturulan filelari gorebilirsin)

    - docker container run --rm -it ozgurozturknet/adanzyedocker sh

    - docker volume create deneme1

    - docker container run --rm -it -v deneme1:/test ozgurozturknet/adanzyedocker sh
    
    - cd /
    - docker container run --rm -it -v deneme1:/usr/src/myapp ozgurozturknet/adanzyedocker sh
    - docker container run --rm -it -v deneme1:/bosklasor alpine sh


5. Bind Mounts:
   * Test ortaminda veya kendi bilgisyarimizda kullanilabilir
   * Host ustundeki bir klasör ya da dosyayi container icerisine map edebiliriz. 
   * Docker Desktop ayarlari duzenlenmeli:
     - hardike erisim izni verilmeli
     - https://hub.docker.com/_/nginx (kullanim bilgilerine ulasilabilir)
       . Hosting some simple static content

$ docker run --name some-nginx -v /some/content:/usr/share/nginx/html:ro -d nginx
Alternatively, a simple Dockerfile can be used to generate a new image that includes the necessary content (which is a much cleaner solution than the bind mount above):

FROM nginx
COPY static-html-directory /usr/share/nginx/html
Place this file in the same directory as your directory of content ("static-html-directory"), run docker build -t some-content-nginx ., then start your container:

$ docker run --name some-nginx -d some-content-nginx
   
   Commands:
     -  docker container run -d -p 80:80 --name ilkweb nginx

     - docker container run -d -p 80:80 -v /Users/hasanbalkanci/DevOps/AdanZyeDocker/kisim3/bolum28/websitesi:/usr/share/nginx/html nginx

     - 

6. Docker Network Driver

  * Bridge, Host, Macvlan, None, Overlay
  * Docker kuruldugu anda otomatik uc network nesnesi olusur: Bridge, Host, None

  * Bridge:
    - Varsayilan driverdir.
    - Container create yapildigi anda ve driver belirtilmezse otomatik secilir.
    - Birden fazla agdan birlesik tek ag olusmasini destekler.
    - container1<--> docker0 <-->container2
      -p 8000:80 dis dunya erisimi .. port publish dis dunyadan containera erisim icin kullanilir. -p . yada --publish
      disdunya --> docker engine makine (ipsi192.168.1.10)(port 80)  --> docker0 (port 5000) --> container2 
    - Bridge; otomatik Docker0 adinda sanal network interface olusturur, 172.17.0.1/16 ip adresini ona verir. Default gatewayde bu docker0 dir, yani paketler buraya teslim edilir ve burdan ana network interface teslim edilir. Yeni olusturulan containerlar sirasiyla 172.17.0.2 vs diye ip alirlar. 
    -  ayni bridge teki containerlar birbiriyle docker0 aracigiyla haberlesebilir. ping 172.17.0.3.
    - bridge disindan dis dunyadan containerin icindeki uygulamaya erismek icin pot tanimlamak gerekir. -p 80:80 (-p host(engine makine):container)
    - default olarak portlar TCP protokolunde acilir. UDP kullanmak icin -p 53:53/udp

    - Kullanici tanimli Bridge:
      . Containerlar arasi network izolasyonu saglar
      . Varsayilan disinda IP araliklari tanimlanabilir
      . Kullanici tanimli bridge network'e bagli containerlar birbirleriyle isimler uzerinden haberlesebilirler. DNS cozumlemesi saglar.
      . Containerlar calisir durumdayken de kullanici tanimli bridge networklere baglanip, baglantiyi kesebilirler.
      . ip adres blogu 172.18.0.0/16 olur. 18,19,20.. olarak devam eder.
  * Host:
    - Her sistemde host driver ile olusturulmus "Host" adinda bir network bulunur.
    - Bu networke bagli container da network izolasyonu olmaz. Sanki o host uzerinde calisan bir prosedd gibi host'un ag kaynaklarini kullanir.
    - 
  
  * MacVlan:

    - Bo driver ile olusturulan network objeleri sayesinde containerlar fiziksel aglara kendi MAC adreslerine sahip olurlar. Birer fiziksel ag adaptorune sahipmiscesine aga baglanabilirler.

  * None
    - Container a hicbir sekilde ag erisimi almamasi istenirse kullanilir.
  
  * Overlay
    - Ayri/Farkli hostlar uzerindeki containerlarin ayni agda calisiyormus gibi davranmasi istendiginde kullanilir.

  * Commands:
    - docker info
    - docker network ls
    - docker network inspect bridge
    - docker exec -it containerid
    - ifconfig
    - pin 8.8.8.8
    - ctrl + p + q (kontainerla baglantiyi keser ama kontainer kapanmaz)
    - docker container run -it --name deneme1 --net host ozgurozturknet/adanzyedocker sh
    - docker network create kopru1 (kullanici tanimli bridge network)
    - docker network create --driver host --name myhost
    - docker network ls
    - docker attach websunucu
    - docker network create --driver=bridge --subnet=10.10.0.0/16 --ip-range=10.10.10.0/24 --gateway=10.10.10.10 kopru2
    - docker network connect kopru2 database (kullanici tanimli networke calisan bir containeri baglama, default bridge de bu islem olmaz, boylece container birsen fazla bridge e baglanmis oldu)
    - docker network rm kopru2




   
     






