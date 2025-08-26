.. image:: /_static/logo.png
  :width: 600
  :align: center



.. raw:: pdf

   PageBreak

Yazar
+++++
- Bayram KARAHAN
- Celalettin AKARSU

Paket Derleme
+++++++++++++
- Bayram KARAHAN
- Celalettin AKARSU


.. raw:: pdf

   PageBreak

Ön Söz
======


Bu kitap, açık kaynak ve özgür yazılım dünyasına ilgi duyan herkes için hazırlanmıştır. Amacı, Türkçe kaynak eksikliğini gidermek ve kendi Linux dağıtımını oluşturmak isteyenlere yol göstermektir.

İçerdiği adımları dikkatle takip ederek, sıfırdan bir sistem derleyebilir ve son kullanıcıların kolayca kurup kullanabileceği bir ISO dosyası haline getirebilirsiniz. Bu rehber, basit düzeyde bir dağıtım inşa etmekten kurulabilir bir medya (ISO) hazırlamaya kadar tüm süreci adım adım açıklamaktadır.

Açık kaynak bir sistem, kullanıcıya yalnızca bir işletim sistemi sunmakla kalmaz; aynı zamanda yazılım bağımsızlığının kapılarını aralar. Kapalı kaynak sistemlerde kullanıcılar, üretici firmaların belirlediği sınırlar içinde hareket etmek zorundadır. Bu durum, hem güvenlik hem de esneklik açısından ciddi kısıtlamalar doğurur. Oysa açık kaynak dünyasında, kullanılan her bileşenin kaynağına erişebilir, üzerinde değişiklik yapabilir ve sistemi kendi ihtiyaçlarınıza göre uyarlayabilirsiniz. Bu özgürlük, özellikle kurumlar ve geliştiriciler için bağımsız bir ekosistem yaratmanın temel taşlarından biridir.

Kendi dağıtımınızı geliştirmek ise bu bağımsızlığı bir adım öteye taşır. Kullandığınız her paket, yapılandırma ve araç zinciri tamamen sizin kontrolünüzdedir. Bu sayede dışa bağımlılığı azaltabilir, sisteminizin işlevlerini kendi güvenlik ve performans kriterlerinize göre şekillendirebilirsiniz. Ayrıca, yerelleştirme ve özgün ihtiyaçlara özel optimizasyonlar yaparak sadece bir kullanıcı değil, aynı zamanda kendi yazılım ekosisteminizin yöneticisi haline gelirsiniz. Açık kaynak bu anlamda yalnızca bir tercih değil, uzun vadede teknolojik egemenliğin anahtarıdır.

.. raw:: pdf

   PageBreak

İçindekiler
===========

.. list-table::
   :widths: 60 10

   * - 1- :ref:`giris`
     - 5
   * - 3- :ref:`temelsistem`
     - 8
   * - 4- :ref:`paketderleme`
     - 11
   * - 5- :ref:`paketsistemi`
     - 94
   * - 6- :ref:`isohazirlama`
     - 107
   * - 7- :ref:`sistemkurulumu`
     - 114
   * - 9- :ref:`yardimcikonular`
     - 121
   * - 10- :ref:`kaynaklar`
     - 122
   * - 11- :ref:`gelistiricimesaji`
     - 123
 
.. raw:: pdf

   PageBreak

.. footer:: ###Page###

.. toctree::

Bu dokümanda, bir cihazı açan, kendini kurulabilen ve kullanıcıyla etkileşime giren bir sistemin nasıl tasarlanacağı anlatılmaktadır. Adımları uygularken ve araştırmalarınız sırasında sıkça karşılaşacağınız temel kavramları https://tr.wikipedia.org/wiki/Linux adresini inceleyip basit bir dille açıklayarak ilerleyelim. 

Linux Nedir?
============

Linux, Linus Torvalds’ın öncülüğünde geliştirilen ve tamamen açık kaynak kodlu bir çekirdek mimarisidir. Unutulmamalıdır ki Linux ifadesi, teknik olarak sadece çekirdek bileşenine karşılık gelir. Tam bir işletim sistemi deneyimi için GNU araç seti ve kütüphanelerle birleştirilir. Bu birleşime **GNU/Linux** denir. Bugün Linux, bilgisayarlar, telefonlar, sunucular ve birçok farklı cihazda yaygın olarak kullanılmaktadır.

GPL Nedir?
==========

GPL (Genel Kamu Lisansı), yazılımların özgürce kullanılmasına, değiştirilmesine ve paylaşılmasına izin veren bir lisanstır. Bu lisans sayesinde herkes yazılımların kaynak koduna erişebilir ve kendi ihtiyaçlarına göre düzenleyebilir.

GNU Nedir?
==========

**GNU**, özgür yazılım hareketinin bir parçası olarak başlatılmış bir projedir. Kısaltması “GNU’s Not Unix” (GNU Unix değildir) anlamına gelir. GNU araçları, Linux çekirdeğiyle birleşerek bugün kullandığımız GNU/Linux sistemlerini oluşturur.

Açık Kaynak Nedir?
==================

Açık kaynak, bir yazılımın kaynak kodlarının herkesin erişimine açık olmasıdır. Böylece isteyen herkes kodları inceleyebilir, geliştirebilir ve başkalarıyla paylaşabilir. Bu yaklaşım, yazılımların daha hızlı gelişmesini ve daha güvenli hale gelmesini sağlar.

Dağıtım Nedir?
==============

Bir GNU/Linux dağıtımı; Linux çekirdeği, GNU araçları, kütüphaneler ve çeşitli uygulamaların bir araya gelmesiyle oluşan tam bir işletim sistemidir. Farklı dağıtımlar, farklı ihtiyaçlara göre şekillendirilir ve özelleştirilir.

Yazılım Bağımsızlığı
====================

Açık kaynak yazılımlar, kullanıcıların bir şirkete bağlı kalmadan yazılım geliştirmesine ve kullanmasına imkan tanır. Bu sayede lisans maliyetleri ortadan kalkar, güvenlik artar ve yazılımlar daha esnek bir şekilde geliştirilebilir.


.. raw:: pdf

   PageBreak


.. _giris:
Temel Kavramlar
================

Bu bölümde **Linux çekirdeği** kullanarak çalışan temel bir Linux sistemi oluşturacağız. Amacımız, dağıtım geliştirme sürecinde bir başlangıç noktası hazırlamak. Sistemi hazırlamak için **kernel, initrd.img, grub.cfg** olması yeterlidir.

Bu sistemi hazırlarken debian üzerinde kurulu paketlere ihtiyacımız var. Bunlar;

- **busybox-static:**
	BusyBox temel linux komutlarını içerisinde barındıran bir uygulamadır.
- **grub-mkrescue:**  
  	 Bir dizini ISO dosyasına dönüştüren araç.
- **qemu-system-x86:**  
  	ISO dosyasını test edebileceğimiz sanal bir makine uygulaması.

Debian tabanlı bir sistemde bu uygulamaları şu komutla yükleyebilirsiniz::

    # Paketleri kuralım
    sudo apt install busybox-static grub-mkrescue qemu-system-x86 -y


Adım Adım Hazırlama
-------------------

**1. Çalışma Dizini Hazırlama**

İlk olarak sistem dosyalarını barındıracak bir dizin oluşturalım::

    mkdir -p $HOME/temellinux/rootfs
    cd $HOME/temellinux/rootfs

**2. BusyBox’u Kopyalama**

BusyBox ikili dosyasını kök dosya sistemine kopyalayın::

    cp /bin/busybox ./busybox

**3. `init` Betiğini Oluşturma**

Sistem açıldığında kernel’in çalıştıracağı init betiğini oluşturun::

    nano init

İçerik::

    #!/busybox sh
    PATH=/bin
    /busybox --install -s /bin
    exec /bin/sh

Dosyayı kaydedip çıkın, ardından çalıştırılabilir hale getirin::

    chmod +x init

.. raw:: pdf

   PageBreak
   
**4. initrd.img Dosyasını Paketleme**

Tüm kök dosya sistemi içeriğini initramfs imajına dönüştürün::

    find . | cpio -H newc -o > ../initrd.img
    gzip -9 ../initrd.img

**5. Kernel’i Kopyalama**

Mevcut sisteminizdeki kernel’i kopyalayın::

    cp /boot/vmlinuz-$(uname -r) ../vmlinuz

**6. GRUB Yapılandırmasını Hazırlama**

GRUB’un boot edebilmesi için gerekli dosya yapısını oluşturun::

    mkdir -p ../iso/boot/grub
    nano ../iso/boot/grub/grub.cfg

İçerik::

    set timeout=5
    set default=0

    menuentry "Temel Linux" {
        linux /boot/vmlinuz
        initrd /boot/initrd.img
    }

Kernel ve initrd’yi iso dizinine kopyalayın::

    cp ../vmlinuz ../iso/boot/vmlinuz
    cp ../initrd.img ../iso/boot/initrd.img

**7. ISO Dosyası Oluşturma**

Boot edilebilir ISO dosyasını oluşturun::

    grub-mkrescue -o temellinux.iso ../iso

**8. Sistemi Test Etme**

QEMU ile sistemi test edin::

    qemu-system-x86_64 -cdrom temellinux.iso -m 1024M

Başarılı bir şekilde açılırsa, BusyBox’un sağladığı temel komutları çalıştırabilirsiniz.

Sonuç
-----

Bu adımlar sonunda, yalnızca **BusyBox** ve **Kernel** ile çalışan basit bir Linux sistemi elde etmiş olacaksınız. Bu temel sistem, daha gelişmiş bir dağıtım hazırlamak için sağlam bir temel sağlar.

.. raw:: pdf

   PageBreak

.. _temelsistem:
**Temel Linux Sistemi Oluşturma**
=================================

Bir önceki bölümde, temel bir sistem hazırlamayı adım adım öğrenmiştik. O çalışmada, temel işlevselliğe sahip, kendi kendine açılabilen, küçük ama işlevsel bir Linux ortamı kurduk. Bu süreç, hepimiz için oldukça öğretici ve motive ediciydi. Şimdi ise bu yolculuğu bir adım daha ileri taşıyoruz!

Artık daha güçlü, daha esnek ve daha geniş özelliklere sahip bir sistem inşa etmenin zamanı geldi. Bu bölümde, **GNU araçlarıyla** nasıl bir dağıtım hazırlayabileceğimizi detaylı şekilde anlatacağız. Peki neden busybox'la yetinmeyip GNU araçlarına geçiyoruz? İşte tam da burada kararımızın nedenlerini birlikte keşfedelim.

BusyBox: Küçük Dev ama Sınırlı
-------------------------------

**BusyBox**, bize temel sistem oluşturmada büyük kolaylık sağladı. Tek bir binary ile onlarca temel komutu çalıştırabildik, disk alanından tasarruf ettik ve bağımlılıklarla uğraşmadık. Busybox özellikle gömülü sistemlerde ve kurtarma ortamlarında adeta bir hayat kurtarıcı.

Avantajlar (Artıları)
......................

- **Küçük boyut**, **Taşınabilirlik** : Tek binary ile onlarca komut.
- **Düşük bağımlılık**: Ekstra kütüphane gerektirmez.
- **Kolay kurulum**: Derlemesi ve kurulumu oldukça basit.
- **Çok amaçlı kullanım**: Tek dosyada tüm temel araçlar.

Dezavantajlar (Eksileri)
.........................

- **Sınırlı özellikler**: Gelişmiş parametre seçenekleri yok.
- **Standart dışı davranışlar**, **Script uyumsuzluğu**: GNU araçlarıyla tam uyumlu değil. Karmaşık bash scriptleri çalışmayabilir.
- **Performans sınırlamaları**: Büyük veri işlemlerinde yetersiz.
- **Hata ayıklama zorlukları**: Detaylı debug için yetersiz.

İşte bu nedenle, artık GNU araçlarıyla donatılmış daha güçlü bir sistem hazırlama zamanı geldi.

Yeni Hedef: Tam Teşekküllü Bir Linux Dağıtımı
----------------------------------------------

Bu yolculukta, aşağıdaki yeteneklere sahip bir sistem kurmayı hedefliyoruz:

- Temel **Linux komutlarını** eksiksiz şekilde çalıştırabilmek
- **Bash kabuğu** ile tam işlevli bir TTY ortamı sunmak
- Farklı **sıkıştırma formatlarıyla** dosya işlemleri yapmak
- **Kernel modüllerini** yönetebilmek
- **Initrd** (Initial RAM Disk) oluşturabilmek
- **GRUB** ile sistem önyüklemesi yapabilmek
- Sistemi hem **kurulabilir** hem de **live (canlı)** modda çalıştırabilmek
- **İnternete bağlanabilir** olmak
- **SSH** ile uzaktan yönetim imkanı sağlamak
- Metin düzenlemek için bir **editör (nano)** sunmak

.. raw:: pdf

   PageBreak
   
**Kurulum Dizini: Dağıtımın Oluşacağı Yer**
-------------------------------------------

Dağıtım sürecinde tüm çalışma dosyalarımızı saklayacağımız bir hedef dizin belirlemeliyiz.

Bu doküman boyunca varsayılan çalışma dizini olarak şunu kullanacağız:

``$HOME/distro/rootfs``

Burada **$HOME** ne demek?  
Bu, Linux ortamında aktif olan kullanıcının ev dizinini ifade eden standart bir değişkendir. Örneğin, sistemde giriş yapan kullanıcı adınız **uzman** ise; **$HOME = /home/uzman** konumunu belirtir.Bu sayede doküman boyunca paylaşılan tüm komutlarda **$HOME** ifadesi sizin kendi kullanıcı dizininize göre otomatik olarak uyarlanacak.

Artık ortam hazır!

Ortamın hazırlanmasından sonra bazı konuları bilmemiz gerelmektedir. Bunlar; 

1. Derleme(Dinamik/Static) 
2. chroot Kullanımı 
3. Kernel/Modül Derleme
4. İso Oluşturma
5. Canlı Sistem Oluşturma Kullanma
6. qemu Kullanmı
7. cfdisk Kullanımı
8. Canlı Sistemden Kurulum Yapma


Burada liste halinde verilen konu başlıkları bu dokümanın **Yardımcı Konular** bölümünde anlatılmaktadır. 

Bundan sonraki adımlarda kendi dağıtımımızı şekillendirmeye başlayacağız!

.. raw:: pdf

   PageBreak


İşte Tüm Bu Yapı İçin İhtiyacımız Olan Paketler
-----------------------------------------------

.. list-table::
   :widths: 25 25 50

   * - 0- :ref:`base-file`
     - 25- :ref:`elfutils`
     - 50- :ref:`popt`
   * - 1- :ref:`glibc`
     - 26- :ref:`libselinux`
     - 51- :ref:`icu`
   * - 2- :ref:`readline`
     - 27- :ref:`tar`
     - 52- :ref:`iproute2`
   * - 3- :ref:`ncurses`
     - 28- :ref:`zlib`
     - 53- :ref:`net-tools`
   * - 4- :ref:`bash`
     - 29- :ref:`brotli`
     - 54- :ref:`dhcp`
   * - 5- :ref:`openssl`
     - 30- :ref:`curl`
     - 55- :ref:`openrc`
   * - 6- :ref:`acl`
     - 31- :ref:`shadow`
     - 56- :ref:`rsync`
   * - 7- :ref:`attr`
     - 32- :ref:`file`
     - 57- :ref:`kbd`
   * - 8- :ref:`libcap`
     - 33- :ref:`eudev`
     - 58- :ref:`kernel`
   * - 9-  :ref:`libpcre2`
     - 34- :ref:`cpio`
     - 59- :ref:`dialog`
   * - 10- :ref:`gmp`
     - 35- :ref:`libsepol`
     - 60- :ref:`live-boot`
   * - 11- :ref:`coreutils`
     - 36- :ref:`kmod`
     - 61- :ref:`live-config`
   * - 12- :ref:`util-linux`
     - 37- :ref:`audit`
     - 62- :ref:`parted`
   * - 13- :ref:`grep`
     - 38- :ref:`libxcrypt`
     - 63- :ref:`busybox`
   * - 14- :ref:`sed`
     - 39- :ref:`libnsl`
     - 64- :ref:`nano`
   * - 15- :ref:`mpfr`
     - 40- :ref:`libbsd`
     - 65- :ref:`grub`
   * - 16- :ref:`gawk`
     - 41- :ref:`libtirpc`
     - 66- :ref:`efibootmgr`
   * - 17- :ref:`findutils`
     - 42- :ref:`e2fsprogs`
     - 67- :ref:`efivar`
   * - 18- :ref:`gcc`
     - 43- :ref:`dostools`
     - 68- :ref:`libssh`
   * - 19- :ref:`libcap-ng`
     - 44- :ref:`initramfs-tools`
     - 69- :ref:`openssh`
   * - 20- :ref:`sqlite`
     - 45- :ref:`libxml2`
     - 70- :ref:`pam`
   * - 21- :ref:`gzip`
     - 46- :ref:`expat`
     - 71- 
   * - 22- :ref:`xz-utils`
     - 47- :ref:`libmd`
     - 72- 
   * - 23- :ref:`zstd`
     - 48- :ref:`libaio`
     - 73-    
   * - 24- :ref:`bzip2`
     - 49- :ref:`lvm2`
     - 74-

Bağımlılıklar Zinciri: Doğru Sıralama Şart!
-------------------------------------------

Unutmamak gerekir ki, bir Linux paketinin sorunsuz çalışabilmesi için **bağımlı olduğu tüm paketlerin önceden derlenmiş olması gerekir**. 

Örneğin; **bash** paketini çalıştırmak için: **readline** ve **ncurses** paketleri gereklidir. **readline** ve **ncurses** için ise **glibc** paketi gereklidir. Bu sayfadaki liste bağımlılıklarına göre sıralandı. Liste sırasına göre ilerlemek oldukça önemlidir. Her paketin derleme aşaması, ayrı başlıklar altında detaylı bir şekilde anlatılacaktır.

Hazırlık: Gerekli Derleme Araçlarını Kurun!
-------------------------------------------

Paket derleme işlemine başlamadan önce, aşağıdaki temel araçları sisteminize kurmalısınız.

.. code-block:: bash

	sudo apt update
	sudo apt-get install debootstrap xorriso mtools make squashfs-tools gcc wget unzip xz-utils tar zstd \
	autoconf automake autotools-dev make meson cmake ninja-compile_packages pkgconf patch libtool grub-pc grub-pc-bin
	
.. raw:: pdf

   PageBreak


.. _base-file:
base-file
+++++++++

Linux sistemimiz için öncelikle temel ayarlamalar ve gerekli dosya-dizin yapıları oluşturulmalıdır. Bu yapıyı hazırladıktan sonra, diğer tüm paketleri ve sistemi bu temel üzerine inşa edeceğiz.

Aslında bir Linux sisteminin en temel paketi **glibc**'dir. Ancak, **glibc** derlenip yüklenmeden önce, sistem için gerekli temel dizin yapısının hazır olması gerekir. Bu nedenle **base-file** adında özel bir paket oluşturduk.

**base-file Komutları**
-----------------------

Aşağıdaki komutlarla temel dosya ve dizin yapısını hazırlıyoruz:

.. code-block:: shell

	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -n 1)"	# Açık ekran tespiti
	user=$(who | grep '('$display')' | awk '{print $1}')	# Ekranı açan kullanıcı tespiti
	mkdir -p /home/$user/distro/build 	# Derleme dizini yoksa oluşturuluyor
	mkdir -p /home/$user/distro/rootfs  	# Sistemin oluşturulacağı dizin yoksa oluşturuluyor
	rm -rf /home/$user/distro/build/* 	# İçeriği temizleniyor
	cp -prfv files/* /home/$user/distro/build/ 	# Ek dosyalar kopyalanıyor
	cd /home/$user/distro/build 	# Derleme dizinine geçiliyor

	mkdir -p bin dev etc home lib64 proc root run sbin sys usr var etc/kly tmp tmp/kly/kur \
	var/log var/tmp usr/lib64/x86_64-linux-gnu usr/lib64/pkgconfig \
	usr/local/{bin,etc,games,include,lib,sbin,share,src}
	ln -s lib64 lib
	cd var && ln -s ../run run && cd -
	cd usr && ln -s lib64 lib && cd -
	cd usr/lib64/x86_64-linux-gnu && ln -s ../pkgconfig pkgconfig && cd -

	bash -c "echo -e \"/bin/sh \n/bin/bash \n/bin/rbash \n/bin/dash\" >> /home/$user/distro/build/etc/shell"
	bash -c "echo 'tmpfs /tmp tmpfs rw,nodev,nosuid 0 0' >> /home/$user/distro/build/etc/fstab"
	bash -c "echo '127.0.0.1 kly' >> /home/$user/distro/build/etc/hosts"
	bash -c "echo 'kly' > /home/$user/distro/build/etc/hostname"
	bash -c "echo 'nameserver 8.8.8.8' > /home/$user/distro/build/etc/resolv.conf"
	echo root:x:0:0:root:/root:/bin/sh > /home/$user/distro/build/etc/passwd
	chmod 755 /home/$user/distro/build/etc/passwd
	cp -prfv /home/$user/distro/build/* /home/$user/distro/rootfs/

Yukarıdaki işlemleri daha düzenli ve fonksiyonel hale getirmek için aşağıdaki şablon script yapısını kullanacağız.

.. raw:: pdf

   PageBreak
   
**Şablon Script Yapısı**
------------------------

Aşağıda, tüm paketlerde kullanılacak şablon script yapısı örneği verilmiştir:

.. code-block:: shell

	#!/usr/bin/env bash
	version=""
	name=""
	depends=""
	source=""
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -n 1)"	# Açık ekran tespiti
	user=$(who | grep '('$display')' | awk '{print $1}')	# Kullanıcı tespiti
	ROOTBUILDDIR="/home/$user/distro/build" 	# Derleme konumu
	BUILDDIR="/home/$user/distro/build/build-${name}-${version}" 	# Paket derleme dizini
	DESTDIR="/home/$user/distro/rootfs" 	# Yüklenecek dizin
	PACKAGEDIR=$(pwd) 	# Derleme talimatının bulunduğu dizin
	SOURCEDIR="/home/$user/distro/build/${name}-${version}" 	# Kaynak dizini

	initsetup(){
		mkdir -p $ROOTBUILDDIR
		rm -rf $ROOTBUILDDIR/*
		cd $ROOTBUILDDIR
		wget ${source}
		dowloadfile=$(ls | head -1)
		filetype=$(file -b --extension $dowloadfile | cut -d'/' -f1)
		if [ "${filetype}" == "???" ]; then unzip ${dowloadfile}; else tar -xvf ${dowloadfile}; fi
		director=$(find ./* -maxdepth 0 -type d)
		directorname=$(basename ${director})
		if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version}; fi
		mkdir -p $BUILDDIR && mkdir -p $DESTDIR && cd $BUILDDIR
	}

	setup(){	# Derleme öncesi kaynak dosyaların hazırlanması	}
	build(){	# Paketin derlenmesi	}
	package(){	# Derlenen dosyaların yüklenmesi	}

	initsetup
	setup
	build
	package

**Şablonda Kullanılan Sabit Bilgiler**
--------------------------------------

Şablon script içinde geçen bazı sabit değişkenler şunlardır:

- **ROOTBUILDDIR:** /home/$user/distro/build → Derleme dizini
- **BUILDDIR:** /home/$user/distro/build/build-${name}-${version} → Paket derleme dizini
- **DESTDIR:** /home/$user/distro/rootfs → Yükleme dizini
- **PACKAGEDIR:** $(pwd) → Derleme scriptinin bulunduğu dizin
- **SOURCEDIR:** /home/$user/distro/build/${name}-${version} → Kaynak dizin

Bu değişkenler sayesinde uzun dizin yolları yerine sadece kısaltmaları kullanıyoruz. Bu aslında bir çeşit takma ad (alias) kullanımına benzer. Örneğin, kaynak dizinde işlem yapmak için sadece **$SOURCEDIR** kullanmanız yeterlidir. Bu yapılar tüm paketlerde geçerli olacak.

**base-file** scriptine benzer şekilde, diğer paketler için de aynı şablon yapısı kullanılacaktır. Böylece her paket için aynı temel adımları tekrar tekrar yazmanıza gerek kalmayacak. Ayrıca, hata olması durumunda ilgili fonksiyon üzerinden doğrudan müdahale ederek kolayca çözüm sağlayabileceksiniz.

.. raw:: pdf

   PageBreak

**Şablon Scripte Uygun base-file Scripti**
------------------------------------------

Aşağıda **base-file** paketine ait tam script örneği verilmiştir:

.. code-block:: shell

	#!/usr/bin/env bash
	version="1.0"
	name="base-file"
	depends=""
	description="sistemin temel yapısı"
	source=""

	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -n 1)"
	user=$(who | grep '('$display')' | awk '{print $1}')
	ROOTBUILDDIR="/home/$user/distro/build"
	BUILDDIR="/home/$user/distro/build/build-${name}-${version}"
	DESTDIR="/home/$user/distro/rootfs"
	PACKAGEDIR=$(pwd)
	SOURCEDIR="/home/$user/distro/build/${name}-${version}"
	initsetup(){
		mkdir -p $ROOTBUILDDIR
		rm -rf $ROOTBUILDDIR/*
		cd $ROOTBUILDDIR
		mkdir -p $BUILDDIR && mkdir -p $DESTDIR && cd $BUILDDIR
	}
	setup(){
		cp -prfv $PACKAGEDIR/files/* $BUILDDIR/
	}
	build(){	
		echo ""
	}
	package(){
		mkdir -p bin dev etc home lib64 proc root run sbin sys usr var etc/kly \ 
		tmp tmp/kly/kur var/log var/tmp usr/lib64/x86_64-linux-gnu \ 
		usr/lib64/pkgconfig usr/local/{bin,etc,games,include,lib,sbin,share,src}
		ln -s lib64 lib
		cd var && ln -s ../run run && cd -
		cd usr && ln -s lib64 lib && cd -
		cd usr/lib64/x86_64-linux-gnu && ln -s ../pkgconfig pkgconfig && cd -
		printf "/bin/sh\n/bin/bash\n/bin/rbash\n/bin/dash\n" >> "$BUILDDIR/etc/shell"
		echo 'tmpfs /tmp tmpfs rw,nodev,nosuid 0 0' >> "$BUILDDIR/etc/fstab"
		echo '127.0.0.1 kly' >> "$BUILDDIR/etc/hosts"
		echo 'kly' > "$BUILDDIR/etc/hostname"
		echo 'nameserver 8.8.8.8' > "$BUILDDIR/etc/resolv.conf"
		echo 'root:x:0:0:root:/root:/bin/sh' > "$BUILDDIR/etc/passwd"
		chmod 755 $BUILDDIR/etc/passwd
		cp -prfv $BUILDDIR/* $DESTDIR/
	}
	initsetup
	setup
	build
	package

**Not:** Yukarıdaki scriptin sorunsuz çalışabilmesi için ek dosyaları `indirin. <https://kendilinuxunuyap.github.io/_static/files/base-file/files.tar>`_ İndirdiğiniz **files.tar** dosyasını istediğiniz bir konumda **base-file** adında bir dizin oluşturarak oraya açınız. **base-file** dizini içine yukarıdaki script kodlarını build adlı bir dosya oluşturup yapıştırın ve kaydedin. **base-file** dizininde bir terminal açarak aşağıdaki komutları sırasıyla çalıştırın.

.. code-block:: shell

	chmod 755 build
	sudo ./build

.. raw:: pdf

   PageBreak

**Paket Derleme Yöntemi**
=========================

**base-file** paketi ilk olduğu için detaylı anlatıldı. Bundan sonraki paketlerde sadece **şablon bir script dosyası** verilecek. Eğer paketin ek dosyaları varsa, bunlar **files.tar** şeklinde sunulacak.

Her paket için istediğiniz bir konumda yeni bir dizin oluşturun. Varsa, ilgili **files.tar** arşivini dizin içinde açın.

Aşağıda, test amaçlı derlediğim bazı paketler ile **base-file** için oluşturulan dizin yapısı görülmektedir:

.. image:: /_static/images/base-file-0.png
   :width: 600

**Derleme Scripti Kullanımı**
-----------------------------

Her paket için **build** adında bir dosya oluşturup, script kodlarını içine yapıştırın ve kaydedin.

Sonrasında, o dizin içinde terminal açarak aşağıdaki komutları çalıştırabilirsiniz:

.. code-block:: shell

	chmod 755 build
	sudo ./build

.. raw:: pdf

   PageBreak


.. _glibc:
glibc
+++++

**glibc** linux dağıtımlarında bütün uygulamaların çalışmasını sağlayan en temel C kütüphanesidir. **glibc** dışında diğer C standart kütüphaneler şunlardır: Bionic libc, dietlibc, EGLIBC, klibc, musl, Newlib ve uClibc. **glibc** temel kütüphane olduğu için ilk bu paketi derleyeceğiz.

glibc Script Dosyası
--------------------

Debian ortamında bu paketin derlenmesi için;
**sudo apt install make bison gawk diffutils gcc gettext grep perl sed texinfo libtool** komutuyla paketin kurulması gerekmektedir.

.. code-block:: bash

	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	version="2.39"
	name="glibc"
	description="temel kütüphane"
	source="https://ftp.gnu.org/gnu/libc/${name}-${version}.tar.gz"
	export CC="gcc"
	export CXX="g++"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -n 1)" 
	user=$(who | grep '('$display')' | awk '{print $1}')  # Detect the user using such display
	ROOTBUILDDIR="/home/$user/distro/build" # Derleme konumu
	BUILDDIR="/home/$user/distro/build/build-${name}-${version}" #Derleme yapılan paketin derleme konumu
	DESTDIR="/home/$user/distro/rootfs" #Paketin yükleneceği sistem konumu
	PACKAGEDIR=$(pwd) #paketin derleme talimatının verildiği konum
	SOURCEDIR="/home/$user/distro/build/${name}-${version}" #Paketin kaynak kodlarının olduğu konum
	initsetup(){
	mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
	rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
	cd $ROOTBUILDDIR #dizinine geçiyoruz
	wget ${source}
	for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
	dowloadfile=$(ls|head -1)
	filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
	if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
	director=$(find ./* -maxdepth 0 -type d)
	directorname=$(basename ${director})
	if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
	mkdir -p $BUILDDIR && mkdir -p $DESTDIR && cd $BUILDDIR
	}
	setup() {
	cp -prvf $PACKAGEDIR/files $BUILDDIR/            
	echo "slibdir=/lib64" >> configparms
	echo "rtlddir=/lib64" >> configparms
	$SOURCEDIR/configure --prefix=/usr --mandir=/usr/share/man --infodir=/usr/share/info --enable-bind-now \
	--enable-multi-arch --enable-stack-protector=strong --enable-stackguard-randomization --disable-crypt \
	--disable-profile --disable-werror --enable-static-pie --enable-static-nss --disable-nscd \
	--host=x86_64-pc-linux-gnu --libdir=/lib64 --libexecdir=/lib64/glibc
	}
	build(){
	make $DESTDIR all
	}
	package(){
	mkdir -p ${DESTDIR}/lib64
	cd $DESTDIR
	ln -s lib64 lib
	cd $BUILDDIR
	make install DESTDIR=$DESTDIR
	mkdir -p ${DESTDIR}/etc/ld.so.conf.d/ ${DESTDIR}/etc/sysconf.d/ ${DESTDIR}/bin
	install $BUILDDIR/files/ld.so.conf ${DESTDIR}/etc/ld.so.conf
	install $BUILDDIR/files/usr-support.conf ${DESTDIR}/etc/ld.so.conf.d/
	install $BUILDDIR/files/x86_64-linux-gnu.conf ${DESTDIR}/etc/ld.so.conf.d/
	rm -f ${DESTDIR}/etc/ld.so.cache
	install $BUILDDIR/files/locale-gen ${DESTDIR}/bin/locale-gen
	install $BUILDDIR/files/revdep-rebuild ${DESTDIR}/bin/revdep-rebuild
	install $BUILDDIR/files/tr_TR ${DESTDIR}/usr/share/i18n/locales/tr_TR
	sed -i "s|#!/bin/bash|#!/bin/sh|g" ${DESTDIR}/usr/bin/ldd	#fix ldd shebang
	cd ${DESTDIR}/lib64/ && mkdir -p x86_64-linux-gnu && cd x86_64-linux-gnu
	while read -rd '' file; do
	ln -s $file $(basename "$file")
	done < <(find "../" -maxdepth 1 -type f -iname "*" -print0)
	${DESTDIR}/sbin/ldconfig -r ${DESTDIR}	# sistem guncelleniyor
	}
	initsetup; setup; build;package;
	
Ek dosyayı indirmek için `tıklayınız. <https://kendilinuxunuyap.github.io/_static/files/glibc/files.tar>`_  **Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.

.. raw:: pdf

   PageBreak

**glibc Test Etme**
-------------------

glibc kütüphanemizi **$HOME/distro/rootfs** komununa yüklendi. Şimdi bu kütüphanenin çalışıp çalışmadığını test edelim. Aşağıdaki c kodumuzu derleyelim ve **$HOME/distro/rootfs** konumuna kopyalayalım. **$HOME/** (ev dizinimiz) konumuna dosyamızı oluşturup aşağıdaki kodu içine yazalım.

.. code-block:: shell

	#include<stdio.h>
	void main(){
	puts("Merhaba Dünya");
	}

**Program Derleme**
...................

.. code-block:: shell
	
	cd $HOME
	gcc -o merhaba merhaba.c #merhaba.c dosyası derlenir.

**Program Yükleme**
...................

Derlenen çalışabilir merhaba dosyamızı **glibc** kütüphanemizin olduğu dizine yükleyelim. 

.. code-block:: shell
	
	cp merhaba $HOME/distro/rootfs/merhaba # derlenen merhaba ikili dosyası $HOME/distro/rootfs/ konumuna kopyalandı.

**Programı Test Etme**
......................

**glibc** kütüphanemizin olduğu dizin dağıtımızın ana dizini oluyor.  **$HOME/distro/rootfs/** konumuna **chroot** ile erişelim.

Aşağıdaki gibi çalıştırdığımızda bir hata alacağız.

.. code-block:: shell

	sudo chroot $HOME/distro/rootfs/ /merhaba
	chroot: failed to run command ‘/merhaba’: No such file or directory
	
**Hata Çözümü**
...............

.. code-block:: shell
	
	# üstteki hatanın çözümü sembolik bağ oluşturmak.
	cd $HOME/distro/rootfs/
	ln -s lib lib64

#merhaba dosyamızı tekrar chroot ile çalıştıralım. Aşağıda görüldüğü gibi hatasız çalışacaktır.

.. code-block:: shell
	
	sudo chroot $HOME/distro/rootfs/ /merhaba
	Merhaba Dünya

**Merhaba Dünya** mesajını gördüğümüzde glibc kütüphanemizin  ve merhaba çalışabilir dosyamızın çalıştığını anlıyoruz. 
Bu aşamadan sonra **Temel Paketler** listemizde bulunan paketleri kodlarından derleyerek **$HOME/distro/rootfs/** dağıtım dizinimize yüklemeliyiz.

Derlemede **glibc** kütüphanesinin derlemesine benzer bir yol izlenecektir. **glibc** temel kütüphane olması ve ilk derlediğimiz paket olduğu için detaylıca anlatılmıştır. Diğer paketlerimizde de **glibc** için paylaşılan script dosyası gibi dosyalar hazırlayıp derlenecektir.

.. raw:: pdf

   PageBreak



.. _readline:
readline 
+++++++++++

libreadline, Linux işletim sistemi için geliştirilmiş bir kütüphanedir. Bu kütüphane, kullanıcıların komut satırında girdi almasını ve düzenlemesini sağlar. Bir programcı olarak, libreadline'i kullanarak kullanıcı girdilerini okuyabilir, düzenleyebilir ve işleyebilirsiniz. Debian ortamında bu paketin derlenmesi için;
**sudo apt install libreadline-dev** komutuyla paketin kurulması gerekmektedir.

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	version="8.2"
	name="readline"
	depends="glibc"
	description="readline kütüphanesi"
	source="https://ftp.gnu.org/pub/gnu/readline/${name}-${version}.tar.gz"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  
	user=$(who | grep "(${display})" | awk '{print $1}')	# kullanıcı tespit
	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                		# Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     		# Yükleme dizini
	PACKAGEDIR=$(pwd)                          		# Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" 		# Kaynak dizini
	initsetup(){
		mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		cd $ROOTBUILDDIR #dizinine geçiyoruz
		wget ${source}
		#isimde boşluk varsa silme işlemi yapılıyor
		for f in *\ *; do mv "$f" "${f// /}"; done 
		dowloadfile=$(ls|head -1)
		filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; \
		else tar -xvf ${dowloadfile};fi
		director=$(find ./* -maxdepth 0 -type d)
		directorname=$(basename ${director})
		if [ "${directorname}" != "${name}-${version}" ]; \
		then mv $directorname ${name}-${version};fi
		mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup(){
		cp -prvf $PACKAGEDIR/files $SOURCEDIR/
		./configure --prefix=/usr --libdir=/usr/lib64
	}
	build(){
		make SHLIB_LIBS="-L/tools/lib -lncursesw"
	}
	package(){
		make SHLIB_LIBS="-L/tools/lib -lncursesw" DESTDIR="$DESTDIR" \
		 install pkgconfigdir="/usr/lib64/pkgconfig"
		install -Dm644 $SOURCEDIR/files/inputrc "$DESTDIR"/etc/inputrc
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

Ek dosyaları indirmek için `tıklayınız. <https://kendilinuxunuyap.github.io/_static/files/readline/files.tar>`_ **Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.

.. raw:: pdf

   PageBreak


.. _ncurses:
ncurses
+++++++

ncurses, Linux işletim sistemi için bir programlama kütüphanesidir. Bu kütüphane, terminal tabanlı kullanıcı arayüzleri oluşturmak için kullanılır. ncurses, terminal ekranını kontrol etmek, metin tabanlı menüler oluşturmak, renkleri ve stil özelliklerini ayarlamak gibi işlevlere sahiptir.

ncurses, kullanıcıya metin tabanlı bir arayüz sağlar ve terminal penceresinde çeşitli işlemler gerçekleştirmek için kullanılabilir. Örneğin, bir metin düzenleyici, dosya tarayıcısı veya metin tabanlı bir oyun gibi uygulamalar ncurses kullanarak geliştirilebilir.

Derleme
-------

Debian ortamında bu paketin derlenmesi için;
**sudo apt install libncurses-dev** komutuyla paketin kurulması gerekmektedir.


.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	version="6.4"
	so_ver="6"
	name="ncurses"
	depends="glibc"
	description="ncurses kütüphanesi"
	source="https://ftp.gnu.org/pub/gnu/ncurses/${name}-${version}.tar.gz"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		cd $ROOTBUILDDIR #dizinine geçiyoruz
		wget ${source}
		#isimde boşluk varsa silme işlemi yapılıyor
		for f in *\ *; do mv "$f" "${f// /}"; done 
		dowloadfile=$(ls|head -1)
		filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; \
		else tar -xvf ${dowloadfile};fi
		director=$(find ./* -maxdepth 0 -type d)
		directorname=$(basename ${director})
		if [ "${directorname}" != "${name}-${version}" ]; \
		then mv $directorname ${name}-${version};fi
		mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

.. raw:: pdf

   PageBreak


.. code-block:: bash

	#--------------------------------------------------------------------------------------------------------------------
	# ncurses devamı
	setup(){
		./configure --prefix=/usr --libdir=/lib64 --with-shared \
		    --disable-tic-depends --with-versioned-syms --enable-widec \
		    --with-cxx-binding --with-cxx-shared --enable-pc-files \
		    --mandir=/usr/share/man --with-manpage-format=normal \
		    --with-xterm-kbs=del --with-pkg-config-libdir=/usr/lib64/pkgconfig
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
		cd $DESTDIR/lib64

		ln -s libncursesw.so.6 libtinfow.so.6
		ln -s libncursesw.so.6 libtinfo.so.6
		ln -s libncursesw.so.6 libncurses.so.6

		# Paket config dosyaları linkleniyor
		for lib in ncurses ncurses++ form panel menu; do
		    if [ ! -f "$DESTDIR/usr/lib64/pkgconfig/${lib}.pc" ]; then
		        ln -sv ${lib}w.pc "$DESTDIR/usr/lib64/pkgconfig/${lib}.pc"
		    fi
		done

		for lib in tic tinfo tinfow ticw; do
		    if [ ! -f "$DESTDIR/usr/lib64/pkgconfig/${lib}.pc" ]; then
		        ln -sv ncursesw.pc "$DESTDIR/usr/lib64/pkgconfig/${lib}.pc"
		    fi
		done

		# Eski sürüm desteği için sembolik linkler
		for lib in libncursesw libncurses libtinfo libpanelw libformw libmenuw; do
		    ln -sv ${lib}.so.${so_ver} ${lib}.so.5
		done

		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak



.. _bash:
bash
++++

Bash, Linux ve diğer Unix tabanlı işletim sistemlerinde kullanılan bir kabuk programlama dilidir. Kullanıcıların komutlar vererek işletim sistemini yönetmelerine olanak tanır. Bash, kullanıcıların işlemleri otomatikleştirmesine ve betik dosyaları oluşturmasına olanak tanır. Özellikle sistem yöneticileri ve geliştiriciler arasında yaygın olarak kullanılan güçlü bir araçtır.

.. code-block:: bash

	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	version="5.2.21"
	name="bash"
	depends="glibc,readline,ncurses"
	description="GNU/Linux dağıtımında ön tanımlı kabuk"
	source="https://ftp.gnu.org/pub/gnu/bash/${name}-${version}.tar.gz"
	# Display adı  # Display kullanıcısı
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)" 
	user=$(who | grep "(${display})" | awk '{print $1}')                    

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		cd $ROOTBUILDDIR #dizinine geçiyoruz
		wget ${source}
		#isimde boşluk varsa silme işlemi yapılıyor
		for f in *\ *; do mv "$f" "${f// /}"; done 
		dowloadfile=$(ls|head -1)
		filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; \
		else tar -xvf ${dowloadfile};fi
		director=$(find ./* -maxdepth 0 -type d)
		directorname=$(basename ${director})
		if [ "${directorname}" != "${name}-${version}" ]; \
		then mv $directorname ${name}-${version};fi
		mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup()	{
        ./configure --prefix=/usr --libdir=/usr/lib64 --bindir=/bin 
        --with-curses --enable-readline --without-bash-malloc
	}
	build()	{
		 make 
	}
	package()	{
		make install DESTDIR=$DESTDIR
		cd $DESTDIR/bin
		ln -s bash sh
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}	# sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.

.. raw:: pdf

   PageBreak




.. _openssl:
openssl
+++++++

OpenSSL, açık kaynaklı bir kriptografik kütüphanedir ve SSL/TLS protokollerini uygulamak, şifreleme, dijital sertifikalar oluşturma ve doğrulama gibi işlemleri gerçekleştirmek için yaygın olarak tercih edilir. coreutils için gerekli olan paket.

Derleme
--------

Debian ortamında bu paketin derlenmesi için; **sudo apt install perl** komutuyla paketin kurulması gerekmektedir.

.. code-block:: bash

	#--------------------------------------------------------------------------------------------------------------------	
	#!/usr/bin/env bash
	version="3.2.0"
	name="openssl"
	depends="glibc,zlib"
	description="openssl"
	source="https://www.openssl.org/source/${name}-${version}.tar.gz"

	# Display adı ve kullanıcı
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"
	user=$(who | grep "(${display})" | awk '{print $1}')

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                    # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}"  # Alt dizin
	DESTDIR="$ROOT/rootfs"                         # Yükleme dizini
	PACKAGEDIR=$(pwd)                             # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}"   # Kaynak dizini

	initsetup(){
		mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		cd $ROOTBUILDDIR #dizinine geçiyoruz
		wget ${source}
		#isimde boşluk varsa silme işlemi yapılıyor
		for f in *\ *; do mv "$f" "${f// /}"; done 
		dowloadfile=$(ls|head -1)
		filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; \
		else tar -xvf ${dowloadfile};fi
		director=$(find ./* -maxdepth 0 -type d)
		directorname=$(basename ${director})
		if [ "${directorname}" != "${name}-${version}" ]; \
		then mv $directorname ${name}-${version};fi
		mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup(){
		cp -prfv "$PACKAGEDIR/files/"* "$SOURCEDIR"
		wget -O "$SOURCEDIR/files/cacert.pem" https://curl.haxx.se/ca/cacert.pem
		patch -Np1 -i "$SOURCEDIR/files/ca-dir.patch"
		./config --prefix=/usr --openssldir=/etc/ssl \
		    --libdir=/usr/lib64 shared linux-x86_64
	}

	build(){
		make depend
		make
	}

	package(){
		mkdir -p "${DESTDIR}/etc/ssl/" "${DESTDIR}/sbin/"
		install "$SOURCEDIR/files/update-certdata" "${DESTDIR}/sbin/update-certdata"
		install "$SOURCEDIR/files/cacert.pem" "${DESTDIR}/etc/ssl/cert.pem"
		make DESTDIR="${DESTDIR}" install_sw install_ssldirs install_man_docs
		"${DESTDIR}/sbin/ldconfig" -r "${DESTDIR}"    # sistem güncelleniyor
	}

	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

Ek dosyaları indirmek için `tıklayınız. <https://kendilinuxunuyap.github.io/_static/files/openssl/files.tar>`_ **Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.

.. raw:: pdf

   PageBreak




.. _acl:
acl
+++

ACL (Access Control List), dosya sistemlerinde veya ağ cihazlarında erişim kontrolünü yönetmek için kullanılan bir mekanizmadır. ACL'ler, belirli kullanıcıların veya kullanıcı gruplarının belirli dosya veya kaynaklara erişim düzeylerini tanımlamak için kullanılır. Bu, dosyalara veya kaynaklara erişim izinlerini hassas bir şekilde kontrol etmeyi sağlar. Örneğin, bir dosyaya sadece belirli kullanıcıların yazma izni vermek için ACL'ler kullanılabilir. Bu şekilde, güvenlik ve erişim kontrolü daha ayrıntılı bir şekilde yapılabilmektedir.coreutils için gerekli olan paket.

Derleme
--------

Debian ortamında bu paketin derlenmesi için;
**sudo apt install libattr1-dev** komutuyla paketin kurulması gerekmektedir.

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="acl"
	version="2.3.1"
	description="The acl package contains utilities to administer Access Control Lists"
	source="https://download.savannah.nongnu.org/releases/acl/acl-$version.tar.xz"
	depends="attr"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		cd $ROOTBUILDDIR #dizinine geçiyoruz
		wget ${source}
		#isimde boşluk varsa silme işlemi yapılıyor
		for f in *\ *; do mv "$f" "${f// /}"; done 
		dowloadfile=$(ls|head -1)
		filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; \
		else tar -xvf ${dowloadfile};fi
		director=$(find ./* -maxdepth 0 -type d)
		directorname=$(basename ${director})
		if [ "${directorname}" != "${name}-${version}" ]; \
		then mv $directorname ${name}-${version};fi
		mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup(){
	    ./configure --prefix=/usr --libdir=/usr/lib64
	}
	build(){
	     make
	}
	package(){
	    make install DESTDIR=$DESTDIR
	    ${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak




.. _attr:
attr
++++

coreutils için gerekli olan paket.

attr, dosya özniteliklerini ayarlamak veya görüntülemek için kullanılan bir komuttur. Bu komut, dosya veya dizinlerin özelliklerini (izinler, sahiplik, erişim zamanları vb.) yönetmek için kullanılır. Örneğin, bir dosyanın izinlerini değiştirmek veya bir dosyanın sahibini görmek için attr komutunu kullanabilirsiniz.

Derleme
--------

Debian ortamında bu paketin derlenmesi için;
**sudo apt install libattr1-dev** komutuyla paketin kurulması gerekmektedir.

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="attr"
	version="2.5.1"
	description="The attr package contains utilities to administer the extended attributes on filesystem objects."
	source="https://mirror.rabisu.com/savannah-nongnu/attr/attr-${version}.tar.gz"
	depends=""
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		cd $ROOTBUILDDIR #dizinine geçiyoruz
		wget ${source}
		#isimde boşluk varsa silme işlemi yapılıyor
		for f in *\ *; do mv "$f" "${f// /}"; done 
		dowloadfile=$(ls|head -1)
		filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; \
		else tar -xvf ${dowloadfile};fi
		director=$(find ./* -maxdepth 0 -type d)
		directorname=$(basename ${director})
		if [ "${directorname}" != "${name}-${version}" ]; \
		then mv $directorname ${name}-${version};fi
		mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup(){
	    ./configure --prefix=/usr --sysconfdir=/etc --libdir=/usr/lib64
	}

	build(){
	    make
	}

	package(){
	    make install DESTDIR=$DESTDIR
	    ${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak





.. _libcap:
libcap
++++++

libcap paketi, Linux işletim sistemlerinde kullanıcı ve grup yetkilendirmelerini yönetmek için kullanılan bir kütüphanedir. Bu kütüphane, sistem kaynaklarına erişim kontrolü sağlamak amacıyla çeşitli yetki seviyeleri tanımlamaktadır. coreutils için gerekli olan paket.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	version="2.69"
	name="libcap"
	depends="glibc,acl,openssl"
	description="shell ve network copy"
	source="https://mirrors.edge.kernel.org/pub/linux/libs/security/linux-privs/libcap2/${name}-${version}.tar.xz"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		cd $ROOTBUILDDIR #dizinine geçiyoruz
		wget ${source}
		#isimde boşluk varsa silme işlemi yapılıyor
		for f in *\ *; do mv "$f" "${f// /}"; done 
		dowloadfile=$(ls|head -1)
		filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; \
		else tar -xvf ${dowloadfile};fi
		director=$(find ./* -maxdepth 0 -type d)
		directorname=$(basename ${director})
		if [ "${directorname}" != "${name}-${version}" ]; \
		then mv $directorname ${name}-${version};fi
		mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	_common_make_options=(
	  CGO_CPPFLAGS="$CPPFLAGS"
	  CGO_CFLAGS="$CFLAGS"
	  CGO_CXXFLAGS="$CXXFLAGS"
	  CGO_LDFLAGS="$LDFLAGS"
	  CGO_REQUIRED="1"
	  GOFLAGS="-buildmode=pie -mod=readonly -modcacherw"
	  GO_BUILD_FLAGS="-ldflags '-compressdwarf=false -linkmode=external'"
	)
	setup(){ echo ""   
	}
	build(){
        make "${_common_make_options[@]}" SUDO="" prefix=/usr KERNEL_HEADERS=include lib=lib64 \ 
        sbindir=bin RAISE_SETFCAP=no  DYNAMIC=yes
	}
	package(){
		make "${_common_make_options[@]}" DESTDIR="$DESTDIR" RAISE_SETFCAP=no prefix=/usr \ 
		lib=lib64 sbindir=bin install
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak




.. _libpcre2:
libpcre2
++++++++

libpcre2 paketi, Perl Compatible Regular Expressions (PCRE) kütüphanesinin ikinci versiyonunu temsil eder ve düzenli ifadelerle çalışmak için kullanılan bir araçtır. Bu kütüphane, özellikle metin işleme ve arama işlemlerinde yaygın olarak kullanılmaktadır.

Derleme
--------

.. code-block:: bash

	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	version="10.40"
	name="libpcre2"
	description="Perl-compatible regular expression library"
	source="https://github.com/PCRE2Project/pcre2/releases/download/pcre2-${version}/\
	pcre2-${version}.tar.gz"
	depends="readline"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		cd $ROOTBUILDDIR #dizinine geçiyoruz
		wget ${source}
		#isimde boşluk varsa silme işlemi yapılıyor
		for f in *\ *; do mv "$f" "${f// /}"; done 
		dowloadfile=$(ls|head -1)
		filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; \
		else tar -xvf ${dowloadfile};fi
		director=$(find ./* -maxdepth 0 -type d)
		directorname=$(basename ${director})
		if [ "${directorname}" != "${name}-${version}" ]; \
		then mv $directorname ${name}-${version};fi
		mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup()	{
	    ./configure --prefix=/usr --enable-shared --enable-static --enable-pcre2-16 \
	    --enable-pcre2-32 --enable-jit --enable-pcre2test-libreadline 
	}
	build()	{
		make
	}
	package(){
		make install DESTDIR=$DESTDIR
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}

	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak




.. _gmp:
gmp
++++

GMP (GNU Multiple Precision Arithmetic Library) paketi, yüksek hassasiyetli aritmetik işlemler gerçekleştirmek için kullanılan bir kütüphanedir. Özellikle büyük sayılarla çalışırken, standart veri türlerinin yetersiz kaldığı durumlarda devreye girer.

Derleme
--------

.. code-block:: bash

	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	version="6.3.0"
	name="gmp"
	depends="glibc"
	description="Library for arbitrary-precision arithmetic on different type of numbers"
	source="https://gmplib.org/download/gmp/gmp-${version}.tar.xz"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini
	
	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup()
	{
		./configure --prefix=/usr --libdir=/usr/lib64 \
			$(use_opt cxx --enable-cxx --disable-cxx) \
		--enable-fat
	}
	build()
	{
		make
	}
	package()
	{
		make install DESTDIR=${DESTDIR}
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.

.. raw:: pdf

   PageBreak





.. _coreutils:
coreutils
+++++++++

coreutils, Linux işletim sistemlerinde temel dosya yönetimi ve sistem komutlarını içeren bir paket olup, kullanıcıların dosyalarla etkileşimde bulunmalarını sağlayan temel araçları sunar. Bu paket, dosya kopyalama, taşıma, silme, listeleme gibi işlemleri gerçekleştiren komutları içerir. Örneğin, cp, mv, rm, ls gibi komutlar coreutils paketinin bir parçasıdır.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="coreutils"
	version="9.5"
	description="The basic file, shell and text manipulation utilities of the GNU operating system"
	source="https://ftp.gnu.org/gnu/coreutils/coreutils-$version.tar.xz"
	depends="acl,attr,gmp,libcap,openssl"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	export CFLAGS="-static-libgcc -static-libstdc++ -fPIC"
	setup(){
    	export FORCE_UNSAFE_CONFIGURE=1 
    	./configure --prefix=/usr \
        --libdir=/usr/lib64 \
        --libexecdir=/usr/libexec \
        --enable-largefile \
        --enable-single-binary=symlinks \
        --enable-no-install-program=groups,hostname,kill,uptime \
        --without-selinux --without-openssl
	}

	build(){
	    make
	}
	package(){
	    make install DESTDIR=$DESTDIR
	    ${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.

.. raw:: pdf

   PageBreak




.. _util-linux:
util-linux
++++++++++

Util-linux paketi, Linux tabanlı sistemlerde kritik öneme sahip bir bileşendir. Bu paket, dosya sistemleri, disk yönetimi, kullanıcı yönetimi ve sistem izleme gibi çeşitli işlevleri yerine getiren bir dizi araç içerir. Örneğin, mount ve umount komutları, dosya sistemlerini bağlamak ve ayırmak için kullanılırken, fdisk ve parted disk bölümlerini yönetmek için kullanılır. Ayrıca, login, su, ve passwd gibi komutlar, kullanıcı kimlik doğrulama ve yönetimi için önemli işlevler sunar.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="util-linux"
	version="2.40.1"
	description="Various useful Linux utilities"
	source="https://mirrors.edge.kernel.org/pub/linux/utils/util-linux/v${version%.*}/util-linux-${version}.tar.gz"
	depends=""
	buildepend="libcap-ng,python,eudev,sqlite,eudev,cryptsetup,libxcrypt"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		cd $ROOTBUILDDIR #dizinine geçiyoruz
		wget ${source}
 		for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		dowloadfile=$(ls|head -1)
		filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		director=$(find ./* -maxdepth 0 -type d)
		directorname=$(basename ${director})
		if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup(){
		cp -prvf $PACKAGEDIR/files/ $SOURCEDIR/
		patch -Np1 -i $SOURCEDIR/files/0001-util-linux-tmpfiles.patch
		./configure --prefix=/usr --libdir=/usr/lib64 --bindir=/usr/bin --enable-shared --enable-static \
		--disable-su --disable-runuser --disable-chfn-chsh --disable-login --disable-sulogin  \
		--disable-makeinstall-chown --disable-makeinstall-setuid --disable-pylibmount \
		--disable-raw --without-systemd --without-libuser --without-utempter --without-econf \
		--with-python --with-udev
	}
	build(){
		make
	}
	package(){
		make install DESTDIR=$DESTDIR
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.
	
	
Ek dosyaları indirmek için `tıklayınız. <https://kendilinuxunuyap.github.io/_static/files/util-linux/files.tar>`_ **Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.

.. raw:: pdf

   PageBreak




.. _grep:
grep
++++

Grep, Linux işletim sistemlerinde metin arama işlemleri için kullanılan güçlü bir komut satırı aracıdır. Kullanıcıların belirli bir desen veya kelimeyi dosyalar içinde hızlı bir şekilde bulmalarını sağlar.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="grep"
	version="3.11"
	description="GNU regular expression matcher"
	source="https://ftp.gnu.org/gnu/grep/grep-$version.tar.xz"
	depends="libpcre2"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup(){
		./configure --prefix=/usr --libdir=/usr/lib64/
	}

	build(){
	    make
	}

	package(){
	    make install DESTDIR=$DESTDIR
	    ${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak




.. _sed:
sed
+++

sed, "stream editor" anlamına gelen bir Linux komut satırı aracıdır. Temel görevi, metin akışını düzenlemek ve dönüştürmektir. sed, dosyalar üzerinde arama, değiştirme, silme ve ekleme işlemleri yaparak metin verilerini işlemek için kullanılır.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="sed"
	version="4.9"
	description="Super-useful stream editor"
	source="https://ftp.gnu.org/gnu/sed/sed-$version.tar.xz"
	depends="acl"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini


	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	
	setup(){
	   ./configure --prefix=/usr \
		--libdir=/usr/lib64/
	}

	build(){
	    make
	}

	package(){
	    make install DESTDIR=$DESTDIR
	    ${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak




.. _mpfr:
mpfr
++++

MPFR (Multiple Precision Floating-Point Reliable) paketi, yüksek hassasiyetli kayan nokta hesaplamaları yapmak için kullanılan bir kütüphanedir. Bu kütüphane, matematiksel hesaplamalarda doğruluğu artırmak amacıyla tasarlanmıştır.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	version="4.2.0"
	name="mpfr"
	depends="glibc,gmp"
	description="multiple precision floating-point computation"
	source="https://ftp.gnu.org/gnu/mpfr/mpfr-${version}.tar.xz"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini


	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup()
	{
		./configure --prefix=/usr \
		--libdir=/usr/lib64 \
		--enable-shared \
		--enable-static \
		--disable-maintainer-mode \
		--enable-thread-safe
	}
	build()
	{
		make
	}
	package()
	{
		make install DESTDIR=${DESTDIR}
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.

.. raw:: pdf

   PageBreak





.. _gawk:
gawk
++++

gawk, GNU projesinin bir parçası olarak geliştirilmiş bir metin işleme aracıdır. "awk" dilinin GNU versiyonu olan gawk, özellikle metin dosyalarındaki verileri analiz etmek, düzenlemek ve raporlamak için kullanılır. gawk, satır ve sütun bazında veri işleme yeteneği ile kullanıcıların karmaşık metin manipülasyonları gerçekleştirmesine olanak tanır.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="gawk"
	version="5.3.0"
	description="GNU awk pattern-matching language"
	source="https://ftp.gnu.org/gnu/gawk/gawk-$version.tar.xz"
	depends="mpfr,readline"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini


	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup(){
	    ./configure --prefix=/usr \
		--libdir=/usr/lib64/ \
		--sysconfdir=/etc \
		--without-libsigsegv
	}

	build(){
	    make
	}

	package(){
	    make install DESTDIR=$DESTDIR
	    ${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.

.. raw:: pdf

   PageBreak




.. _findutils:
findutils
+++++++++

Finutils paketi, Linux işletim sistemlerinde dosya ve dizin yönetimi ile ilgili çeşitli işlevler sunan bir araç setidir. Bu paket, özellikle dosya sistemleri üzerinde işlem yaparken kullanıcıların işini kolaylaştırmayı hedefler.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="findutils"
	version="4.9.0"
	description="GNU utilities for finding files"
	source="https://ftp.gnu.org/gnu/findutils/findutils-$version.tar.xz"
	depends=""
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini


	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup(){
	   	./configure --prefix=/usr --libdir=/usr/lib64/
	}

	build(){
	    make
	}

	package(){
	    make install DESTDIR=$DESTDIR
	    ${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak




.. _gcc:
gcc
+++

gcc paketi, GNU Compiler Collection (GCC) ile birlikte gelen ve C, C++ gibi dillerde yazılmış programların çalışması için gerekli olan temel kütüphaneleri içeren bir bileşendir. Debian ortamında derlemek için **sudo apt install libmpc-dev libmpfr-dev libgmp-dev libisl-dev** paketleri kurmalıyız.

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	version="13.1.0"
	name="gcc"
	depends="glibc,gmp,mpfr,libmpc,zlib,libisl"
	builddepend="flex,elfutils,curl,linux-headers"
	description="DOS filesystem tools - provides mkdosfs, mkfs.msdos, mkfs.vfat"
	source="https://ftp.gnu.org/gnu/gcc/gcc-${version}/gcc-${version}.tar.xz"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini
	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $BUILDDIR
	}
	export CFLAGS="-O2 -s"
	export CXXFLAGS="-O2 -s"
	unset LDFLAGS
	setup(){
	case $(uname -m) in
	  x86_64)
	    sed -i.orig '/m64=/s/lib64/lib/' gcc/config/i386/t-linux64
	  ;;
	esac
	    cd $SOURCEDIR
	    mkdir build
	    cd build
	    ../configure --prefix=/usr --libexecdir=/usr/libexec --mandir=/usr/share/man --infodir=/usr/share/info  \
	    --enable-languages=c,c++ --with-linker-hash-style=gnu --with-system-zlib --enable-__cxa_atexit --enable-cet=auto \
	    --enable-checking=release --enable-clocale=gnu --enable-default-pie --enable-default-ssp \ 
	    --enable-gnu-indirect-function --enable-gnu-unique-object --enable-libstdcxx-backtrace --enable-link-serialization=1 \
	    --enable-linker-build-id --enable-lto --disable-multilib --enable-plugin --enable-shared --enable-threads=posix \
	    --disable-libssp --disable-libstdcxx-pch --disable-werror --without-zstd --disable-nls	--libdir=/usr/lib64 \ 
	    --target=x86_64-pc-linux-gnu 	
	}
	build(){
		cd $SOURCEDIR/build
		make
	}
	package(){
		cd $SOURCEDIR/build
		make install DESTDIR=${DESTDIR}
		mkdir -p ${DESTDIR}/usr/lib64/
		ln -s gcc ${DESTDIR}/usr/bin/cc
		ln -s g++ ${DESTDIR}/usr/bin/cxx
		cd $DESTDIR
		while read -rd '' file; do
		case "$(file -Sib "$file")" in
		    application/x-executable\;*)     # Binaries
		        strip "$file" ;;
		    application/x-pie-executable\;*) # Relocatable binaries
		        strip "$file" ;;
		esac
	    done< <(find "./" -type f -iname "*" -print0)	 
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.


**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.

.. raw:: pdf
   PageBreak

.. _libcap-ng:
libcap-ng
+++++++++

libcap-ng paketi, Linux işletim sistemlerinde yetki yönetimi ve güvenlik uygulamaları için kullanılan bir kütüphanedir. Bu kütüphane, kullanıcıların ve süreçlerin sahip olduğu yetkileri daha esnek bir şekilde yönetmelerine olanak tanır.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	version="0.8.3"
	name="libcap-ng"
	depends="glibc,acl,openssl,libtool"
	description="shell ve network copy"
	source="https://github.com/stevegrubb/libcap-ng/archive/refs/tags/v${version}.zip"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini


	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup()
	{	
        ./autogen.sh
        ./configure --prefix=/usr \
          --libdir=/lib64 \
         --with-python \
   		--with-python3
		
	}
	build()
	{
		make 
	}
	package()
	{
		make install DESTDIR=$DESTDIR
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.

.. raw:: pdf

   PageBreak


.. _sqlite:
sqlite
++++++

SQLite, C dilinde yazılmış ve gömülü bir veritabanı motoru olarak bilinen bir yazılımdır. Özellikle hafifliği ve taşınabilirliği ile dikkat çeker. SQLite, bir dosya sistemi üzerinde çalışarak verileri depolar ve bu sayede herhangi bir sunucuya ihtiyaç duymadan uygulama içinde kullanılabilir.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="sqlite"
	version="3.45.2"
	description="A C library that implements an SQL database engine"
	srcver="3450200"
	source="https://www.sqlite.org/2024/sqlite-autoconf-$srcver.tar.gz"
	depends="zlib,readline"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini


	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}


	setup(){
	    ./configure --prefix=/usr --libdir=/usr/lib64 --enable-fts3 --enable-fts4 --enable-fts5 --enable-rtree \
		CPPFLAGS="-DSQLITE_ENABLE_FTS3=1            \
		          -DSQLITE_ENABLE_FTS4=1            \
		          -DSQLITE_ENABLE_COLUMN_METADATA=1 \
		          -DSQLITE_ENABLE_UNLOCK_NOTIFY=1   \
		          -DSQLITE_ENABLE_DBSTAT_VTAB=1     \
		          -DSQLITE_SECURE_DELETE=1          \
		          -DSQLITE_ENABLE_FTS3_TOKENIZER=1"
	}

	build(){
	    make
	}

	package(){
	    make install DESTDIR=$DESTDIR
	    ${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak




.. _gzip:
gzip
++++

Gzip, "GNU zip" ifadesinin kısaltmasıdır ve dosyaları sıkıştırmak için kullanılan bir yazılımdır. Temel amacı, dosya boyutunu azaltarak depolama alanından tasarruf sağlamak ve veri iletimini hızlandırmaktır. Gzip, genellikle metin dosyaları gibi tekrarlayan verilerde yüksek sıkıştırma oranları sunar.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	version="1.13"
	name="gzip"
	depends=""
	description="Standard GNU compressor"
	source="https://ftp.gnu.org/gnu/gzip/${name}-${version}.zip"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini


	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	
	setup()
	{
		export DEFS="NO_ASM"
		./autoreconf -fvi
		./configure --prefix=/usr \
		--libdir=/usr/lib64/
	}
	build()
	{
		make 
	}
	package()
	{
		make install DESTDIR=$DESTDIR
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak





.. _xz-utils:
xz-utils
++++++++

xz-utils, Linux işletim sistemlerinde dosyaları sıkıştırmak ve açmak için kullanılan bir yazılım paketidir. Bu paket, LZMA (Lempel-Ziv-Markov chain algorithm) algoritmasını temel alarak yüksek sıkıştırma oranları sağlar. xz-utils, genellikle büyük dosyaların depolanması ve aktarılması sırasında disk alanından tasarruf sağlamak amacıyla tercih edilir.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="xz-utils"
	version="5.4.5"
	description="lzma compression utilities"
	source="https://tukaani.org/xz/xz-${version}.tar.gz"
	md5sums="66f82a9fa24623f5ea8a9ee6b4f808e2"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup(){
	    ./configure --prefix=/usr \
		--libdir=/usr/lib64 \
		--enable-static \
		--enable-shared \
		--enable-doc \
		--enable-nls
	}
	build(){
	    make
	}
	package(){
	    make install DESTDIR=$DESTDIR
	    ${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak




.. _zstd:
zstd
++++

Zstd (Zstandard), Facebook tarafından geliştirilen bir veri sıkıştırma algoritmasıdır. Bu paket, verilerin boyutunu azaltarak depolama alanından tasarruf sağlamak ve veri iletimini hızlandırmak amacıyla kullanılır. Zstd, hem sıkıştırma hem de açma işlemlerinde yüksek hız ve verimlilik sunar. Özellikle büyük veri setleri ile çalışırken, Zstd'nin sunduğu sıkıştırma oranları, diğer geleneksel algoritmalara göre daha üstündür.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	version="1.5.5"
	name="zstd"
	depends="glibc,readline,ncurses"
	description="şıkıştırma kütüphanesi"
	source="https://github.com/facebook/zstd/releases/download/v1.5.5/${name}-${version}.tar.gz"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup()
	{
		echo ""
	}
	build()
	{
		make 
	}
	package()
	{
		make prefix=/usr install DESTDIR=$DESTDIR
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}

	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak




.. _bzip2:
bzip2
+++++

bzip2, dosyaları sıkıştırmak için kullanılan bir yazılımdır ve genellikle Unix tabanlı sistemlerde tercih edilmektedir.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	version="1.0.8"
	name="bzip2"
	depends="glibc,readline,ncurses"
	description="şıkıştırma kütüphanesi"
	source="https://sourceware.org/pub/bzip2/${name}-${version}.tar.gz"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
		    wget ${source}
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup(){
		    cp -prvf $PACKAGEDIR/files/ $SOURCEDIR
		    sed -i -e 's:\$(PREFIX)/man:\$(PREFIX)/share/man:g' -e 's:ln -s -f $(PREFIX)/bin/:ln -s :' Makefile
		    sed -i -e "s:1\.0\.4:$version:" bzip2.1 bzip2.txt Makefile-libbz2_so manual.*
	}
	build(){
		     make -f Makefile-libbz2_so all
		     make all
	}
	package(){
		    cd $SOURCEDIR
		    make DESTDIR=$DESTDIR/usr install
		    install -D libbz2.so.$version "$DESTDIR"/usr/lib64/libbz2.so.$version
		    ln -s libbz2.so.$version "$DESTDIR"/usr/lib64/libbz2.so
		    ln -s libbz2.so.$version "$DESTDIR"/usr/lib64/libbz2.so.${version%%.*}
		    mkdir -p "$DESTDIR"/usr/lib64/pkgconfig/
		    install -Dm644 files/bzip2.pc -t "$DESTDIR"/usr/lib64/pkgconfig
		    ${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

Ek dosyaları indirmek için `tıklayınız. <https://kendilinuxunuyap.github.io/_static/files/bzip2/files.tar>`_ **Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak





.. _elfutils:
elfutils
++++++++

elfutils, ELF dosyalarının oluşturulması, düzenlenmesi ve incelenmesi için gerekli araçları sağlayan bir yazılım paketidir. Bu paket, özellikle derleyiciler ve bağlantı editörleri tarafından üretilen ikili dosyaların yapısını anlamak ve analiz etmek için kullanılır.

Paket, readelf, objdump, eu-strip gibi araçları içerir. Örneğin, readelf komutu, bir ELF dosyasının içeriğini detaylı bir şekilde görüntülemeye olanak tanırken, objdump ise ikili dosyaların iç yapısını analiz etmek için kullanılır. Bu araçlar, geliştiricilerin yazılımlarını optimize etmelerine ve hata ayıklama süreçlerini kolaylaştırmalarına yardımcı olur.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="elfutils"
	version="0.190"
	description="Libraries/utilities to handle ELF objects (drop in replacement for libelf)"
	source="https://sourceware.org/elfutils/ftp/${version}/elfutils-${version}.tar.bz2"
	depends="bzip2,xz-utils,zstd,zlib"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup(){
	    ./configure --prefix=/usr --libdir=/usr/lib64 \
			--enable-shared --disable-debuginfod --enable-libdebuginfod=dummy --disable-thread-safety \
			--disable-valgrind --disable-nls --program-prefix="eu-" --with-bzlib --with-lzma 
	}
	build(){
	    make
	}
	package(){
	    make install DESTDIR=$DESTDIR
	    ${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak




.. _libselinux:
libselinux
++++++++++

libselinux paketi, Linux işletim sistemlerinde güvenlik politikalarının uygulanmasına yardımcı olan bir kütüphanedir. Bu kütüphane, SELinux (Security-Enhanced Linux) mekanizmasının temel bileşenlerinden biridir.

Derleme
--------

Debian ortamında bu paketin derlenmesi için; **sudo apt install libpcre2-dev libsepol-dev** komutuyla paketin kurulması gerekmektedir.

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	version="3.6"
	name="libselinux"
	depends=""
	description="lib"
	source="https://github.com/SELinuxProject/selinux/releases/download/3.6/${name}-${version}.tar.gz"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
			mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
			rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
			cd $ROOTBUILDDIR #dizinine geçiyoruz
			wget ${source}
			for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
			dowloadfile=$(ls|head -1)
			filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
			if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
			director=$(find ./* -maxdepth 0 -type d)
			directorname=$(basename ${director})
			if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
			mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup()	{
			cp -prvf $PACKAGEDIR/files/ $SOURCEDIR
	}
	build()	{
		    patch -Np1 -i files/lfs64.patch
		    make FTS_LDLIBS="-lfts"
	}
	package()	{
		    make install DESTDIR=$DESTDIR
		    ${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.	

Ek dosyaları indirmek için `tıklayınız. <https://kendilinuxunuyap.github.io/_static/files/libselinux/files.tar>`_ **Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak





.. _tar:
tar
+++

Tar paketi, Unix ve Linux sistemlerinde dosya arşivleme ve sıkıştırma işlemleri için kullanılan bir dosya formatıdır. "tar" kelimesi, "tape archive" ifadesinin kısaltmasıdır ve başlangıçta manyetik bantlarda veri saklamak amacıyla geliştirilmiştir.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="tar"
	version="1.35"
	description="Utility used to store, backup, and transport files"
	source="https://ftp.gnu.org/gnu/tar/tar-$version.tar.xz"
	depends="glibc,acl"
	builddepend=""
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup(){
		export FORCE_UNSAFE_CONFIGURE=1
		./configure --prefix=/usr \
			--libdir=/usr/lib64 \
			--sbindir=/usr/bin \
			--libexecdir=/usr/lib64/tar \
			--localstatedir=/var \
			--enable-backup-scripts
	}
	build(){
		make 
	}
	package(){
		make DESTDIR=$DESTDIR install
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.


**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak





.. _zlib:
zlib
++++

Zlib, veri sıkıştırma ve açma işlemleri için geliştirilmiş açık kaynaklı bir kütüphanedir. Genellikle, Gzip ve PNG gibi formatların temelini oluşturur. Zlib, Deflate algoritmasını kullanarak verileri sıkıştırır ve bu sayede dosya boyutunu önemli ölçüde azaltır. Bu özellik, özellikle ağ üzerinden veri transferi sırasında bant genişliğinden tasarruf sağlamak için oldukça faydalıdır.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	version="1.3"
	name="zlib"
	depends="glibc,readline,ncurses,flex"
	description="Compression library implementing the deflate compression method found in gzip and PKZIP"
	source="https://github.com/madler/zlib/archive/refs/tags/v$version.tar.gz"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup(){
		./configure --prefix=/usr
	}
	build(){
		make 
	}
	package(){
		make install pkgconfigdir="/usr/lib64/pkgconfig" DESTDIR=$DESTDIR
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak





.. _brotli:
brotli
++++++

Brotli, Google tarafından geliştirilen ve özellikle web tarayıcıları için optimize edilmiş bir veri sıkıştırma algoritmasıdır. Bu algoritma, HTTP/2 ve HTTPS protokolleri ile birlikte kullanıldığında, web sayfalarının daha hızlı yüklenmesine olanak tanır. Brotli, gzip'e göre daha yüksek sıkıştırma oranları sunarak, veri transferini optimize eder.

Derleme
--------


Debian ortamında bu paketin derlenmesi için;

- **sudo apt install cmake** komutuyla paketin kurulması gerekmektedir.


.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	version="1.1.0"
	name="brotli"
	depends="glibc,zlib"
	description="Generic-purpose lossless compression algorithm"
	source="https://github.com/google/brotli/archive/refs/tags/v$version.tar.gz"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup(){
	    cmake \
		-DCMAKE_INSTALL_PREFIX=/usr \
		-DBUILD_SHARED_LIBS=True
	}
	build(){
		make 
	}
	package(){
		make install DESTDIR=$DESTDIR
		mkdir -p $DESTDIR/lib
		mkdir -p $DESTDIR/lib/pkgconfig
		cp -prfv $DESTDIR/usr/lib/x86_64-linux-gnu/* $DESTDIR/lib/
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.


**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak





.. _curl:
curl
++++

Curl, "Client URL" ifadesinin kısaltmasıdır ve internet protokolleri üzerinden veri transferi yapabilen bir komut satırı aracıdır. Özellikle HTTP, HTTPS, FTP gibi protokollerle çalışarak, web sunucularına istek göndermek ve yanıt almak için kullanılır. Linux sistemlerinde yaygın olarak kullanılan bu araç, geliştiricilere ve sistem yöneticilerine API'lerle etkileşim kurma, dosya indirme veya yükleme gibi işlemleri kolaylaştırır.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	version="8.4.0"
	name="curl"
	depends="glibc,acl,openssl"
	description="shell ve network copy"
	source="https://curl.se/download/${name}-${version}.tar.xz"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		        mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		        rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		        cd $ROOTBUILDDIR #dizinine geçiyoruz
		        wget ${source}
		        dowloadfile=$(ls|head -1)
		        filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		        if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		        director=$(find ./* -maxdepth 0 -type d)
		        directorname=$(basename ${director})
		        if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		        mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup(){
		    opts=(
		    --prefix=/usr --libdir=/usr/lib64 --disable-ldap --disable-ldaps --disable-versioned-symbols
		    --enable-doh --enable-ftp --enable-ipv6 --with-ca-path=/etc/ssl/certs --with-ca-bundle=/etc/ssl/cert.pem
		    --enable-threaded-resolverl --enable-websockets --without-libidn2 --without-libpsl --without-nghttp2)
		      #--without-zstd --without-zlib --without-brotli --without-libssh)
		    ./configure ${opts[@]} --with-openssl
	}
	build(){
		    make
	}
	package(){
			make install DESTDIR=$DESTDIR
		    cd $DESTDIR
		    for ver in 3 4.0.0 4.1.0 4.2.0 4.3.0 4.4.0 4.5.0 4.6.0 4.7.0; do
		    ln -s $DESTDIR/lib/libcurl.so.4.8.0 $DESTDIR/lib/libcurl.so.${ver}
			done
			${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak





.. _shadow:
shadow
++++++

Shadow paketi, Linux işletim sistemlerinde kullanıcı hesaplarının şifrelerini güvenli bir şekilde saklamak için kullanılan bir mekanizmadır. Bu paket, kullanıcı bilgilerini ve şifrelerini içeren dosyaların yönetiminde önemli bir rol oynamaktadır.

Derleme
--------

Debian ortamında bu paketin derlenmesi için; **sudo apt install libreadline-dev libcap-dev libcap2-bin** komutları çalıştırıldıktan sonra derleme yapılmalıdır.

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="shadow"
	version="4.13"
	description="Password and account management tool suite with support for shadow files and PAM"
	source="https://github.com/shadow-maint/shadow/releases/download/$version/shadow-$version.tar.xz"
	depends="pam,libxcrypt,acl,attr"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		cd $ROOTBUILDDIR #dizinine geçiyoruz
		wget ${source}
		for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		dowloadfile=$(ls|head -1)
		filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		director=$(find ./* -maxdepth 0 -type d)
		directorname=$(basename ${director})
		if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup(){
		cp -prvf $PACKAGEDIR/files/ $SOURCEDIR/
		autoreconf -fiv      
		./configure --prefix=/usr --libdir=/usr/lib64 --sysconfdir=/etc --bindir=/usr/bin --sbindir=/usr/sbin \
		--disable-account-tools-setuid --without-sssd --with-fcaps --with-libpam --without-group-name-max-length \
		--with-bcrypt --with-yescrypt --without-selinux
	}

	build(){
	    make
	}
	package(){
		make install DESTDIR=$DESTDIR
		mkdir -p "${DESTDIR}/etc" "${DESTDIR}/etc/default/"
		sed -i "/.*selinux.*/d" ${DESTDIR}/etc/pam.d/*
		install -vDm 600 $SOURCEDIR/files/useradd.defaults "${DESTDIR}/etc/default/useradd"
		install -vDm 600 $SOURCEDIR/files/system-auth "${DESTDIR}/etc/pam.d/system-auth"
		if [ ! -f ${DESTDIR}/etc/group ] ; then install -vDm 600 $SOURCEDIR/files/group "${DESTDIR}/etc/group"; fi
		if [ ! -f ${DESTDIR}/etc/shadow ] ; then echo "root:*::0:::::" > ${DESTDIR}/etc/shadow; fi
		chmod 600 ${DESTDIR}/etc/shadow
		chmod 644 ${DESTDIR}/etc/group
		chown root ${DESTDIR}/etc/group  ${DESTDIR}/etc/shadow
		chgrp root ${DESTDIR}/etc/group  ${DESTDIR}/etc/shadow

		if [ ! -f "${DESTDIR}/etc/passwd" ]; then echo -e "root:x:0:0:root:/root:/bin/sh">${DESTDIR}/etc/passwd; fi
		    ${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

Ek dosyaları indirmek için `tıklayınız. <https://kendilinuxunuyap.github.io/_static/files/shadow/files.tar>`_ **Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak




.. _file:
file
++++

Linux'ta "file" komutu, dosyaların türlerini tanımlamak için kullanılan bir araçtır. Bu komut, dosyanın içeriğini analiz ederek, dosyanın ne tür bir veri içerdiğini belirler. Örneğin, bir dosyanın metin dosyası mı, ikili dosya mı yoksa bir resim dosyası mı olduğunu tespit edebilir.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="file"
	version="5.45"
	description="Identify a files format by scanning binary data for patterns"
	source=("http://ftp.astron.com/pub/file/file-${version}.tar.gz")
	depends=""
	
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
		    wget ${source}
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup(){
	    opts=(
	    	--prefix=/usr
		--libdir=/usr/lib64
		--enable-static
		--enable-elf
		--enable-elf-core
	    )
	    ./configure ${opts[@]} \
		$(use_opt zlib --enable-zlib --disable-zlib) \
		$(use_opt lzma --enable-xzlib --disable-xzlib) \
		$(use_opt bzip2 --enable-bzlib --disable-bzlib) \
		$(use_opt seccomp --enable-libseccomp --disable-libseccomp)
	}

	build(){
	    make
	}

	package(){
	    make install DESTDIR=$DESTDIR
	    ${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak




.. _eudev:
eudev
+++++

Eudev, Linux tabanlı sistemlerde cihaz yönetimi için kullanılan bir kullanıcı alanı aracı olan udev'in bir fork'udur. Udev, sistemdeki donanım bileşenlerinin tanınması, yönetilmesi ve olay bildirimlerinin gerçekleştirilmesi için kritik bir rol oynar. Debian ortamında bu paketin derlenmesi için; **sudo apt install libkmod-dev l libgperf-dev** paketlerin kurulması gerekmektedir.


.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	version="3.2.14"
	name="eudev"
	depends="glibc,readline,ncurses,gperf"
	description="modül ve sistem iletişimi sağlayan paket"
	source="https://github.com/eudev-project/eudev/releases/download/v3.2.14/${name}-${version}.tar.gz"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		cd $ROOTBUILDDIR #dizinine geçiyoruz
		wget ${source}
		for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		dowloadfile=$(ls|head -1)
		filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		director=$(find ./* -maxdepth 0 -type d)
		directorname=$(basename ${director})
		if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup(){
		cp $PACKAGEDIR/files/eudev.hook $SOURCEDIR
		cp $PACKAGEDIR/files/eudev.init-bottom $SOURCEDIR
		cp $PACKAGEDIR/files/eudev.init-top $SOURCEDIR

		./configure --prefix=/usr --bindir=/sbin --sbindir=/sbin --libdir=/lib64 --disable-manpages \ 
		--disable-static --disable-selinux --enable-modules --enable-kmod --sysconfdir=/etc --exec-prefix=/ \
		--with-rootprefix=/ --with-rootrundir=/run --with-rootlibexecdir=/lib64/udev --enable-split-usr 
	}
	build(){
		make 
	}
	package(){
		make install DESTDIR=$DESTDIR
		mkdir -p ${DESTDIR}/usr/share/initramfs-tools/{hooks,scripts}
	  	mkdir -p ${DESTDIR}/usr/share/initramfs-tools/scripts/init-{top,bottom}
	  	install $SOURCEDIR/eudev.hook         ${DESTDIR}/usr/share/initramfs-tools/hooks/udev
	    install $SOURCEDIR/eudev.init-top         ${DESTDIR}/usr/share/initramfs-tools/scripts/init-top/udev
	    install $SOURCEDIR/eudev.init-bottom         ${DESTDIR}/usr/share/initramfs-tools/scripts/init-bottom/udev
	    	
		cd ${DESTDIR}
		mkdir -p bin
		cd bin
		ln -s ../sbin/udevadm udevadm
		ln -s ../sbin/udevd udevd
		mkdir -p  ${DESTDIR}/usr/lib64/pkgconfig/
		cd ${DESTDIR}/usr/lib64/pkgconfig/
		ln -s ../../../lib64/pkgconfig/libudev.pc libudev.pc
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}

	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

Ek dosyaları indirmek için `tıklayınız. <https://kendilinuxunuyap.github.io/_static/files/eudev/files.tar>`_ **Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.

.. raw:: pdf

   PageBreak




.. _cpio:
cpio
++++

CPIO (Copy In and Out), Unix ve Linux işletim sistemlerinde dosyaları arşivlemek ve taşımak için kullanılan bir komut satırı aracıdır. CPIO, dosyaları bir arşiv dosyası içinde saklayarak, bu dosyaların daha sonra kolayca geri yüklenmesini sağlar. CPIO, genellikle tarayıcılar ve diğer arşivleme araçları ile birlikte kullanılır.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="cpio"
	version="2.15"
	description="A tool to copy files into or out of a cpio or tar archive"
	source="https://ftp.gnu.org/gnu/cpio/cpio-$version.tar.gz"
	depends="glibc"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup(){
	    CFLAGS+=' -fcommon'
	    ./configure --prefix=/usr
	}
	build(){
	    make
	}

	package(){
	    make install DESTDIR=$DESTDIR
	    ${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.

.. raw:: pdf

   PageBreak




.. _libsepol:
libsepol
++++++++

libsepol, SELinux'un güvenlik politikalarını oluşturmak, düzenlemek ve uygulamak için gerekli olan temel bir kütüphanedir. SELinux, Linux çekirdeği üzerinde güvenlik katmanları ekleyerek sistemin güvenliğini artırmayı amaçlar. libsepol, bu güvenlik politikalarının tanımlanması ve yönetilmesi için gerekli olan araçları sağlar.

Derleme
--------

Debian ortamında bu paketin derlenmesi için;

- **sudo apt install flex** 

komutuyla paketin kurulması gerekmektedir.



.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	version="3.6"
	name="libsepol"
	depends=""
	description="lib"
	source="https://github.com/SELinuxProject/selinux/releases/download/3.6/${name}-${version}.tar.gz"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup()	{
		echo ""
	}
	build()	{
		make 
	}
	package()	{
		make install DESTDIR=$DESTDIR
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.

.. raw:: pdf

   PageBreak





.. _kmod:
kmod
++++

Linux çekirdeği ile donanım arasındaki haberleşmeyi sağlayan kod parçalarıdır. Bu kod parçalarını kernele eklediğimizde kerneli tekrardan derlememiz gerekmektedir. Her kod ekleme ve her kod çıkartma işleminden sonra kernel derlemek ciddi bir iş yükü ve karmaşa oluşturacaktır.

Bu sorunların çözümü için modul vardır. Moduller kernele istediğimiz kod parçalarını ekleme ya da çıkartma yapabilmemizi sağlar. Bu işlemleri yaparken kernel derleme işlemi yapmamıza gerek yoktur. Bu süreçleri yöneten uygulamalarının bulunduğu pakettir.

Derleme
--------

Debian ortamında bu paketin derlenmesi için;

- **sudo apt install libkmod-dev** 

komutuyla paketin kurulması gerekmektedir.

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="kmod"
	version="32"
	description="library and tools for managing linux kernel modules"
	source="https://mirrors.edge.kernel.org/pub/linux/utils/kernel/kmod/kmod-$version.tar.xz"
	depends="zlib,xz-utils"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup(){
	    touch libkmod/docs/gtk-doc.make
	    ./configure --prefix=/usr --libdir=/usr/lib64/ --bindir=/bin --with-rootlibdir=/lib --with-zlib --with-openssl
	}
	build(){
	    make
	}
	package(){
	    make install DESTDIR=$DESTDIR
	    mkdir -p ${DESTDIR}/sbin
	    for i in lsmod rmmod insmod modinfo modprobe depmod; do
			ln -sf ../bin/kmod "$DESTDIR"/sbin/$i
		done
		for i in lsmod modinfo; do
			ln -s kmod "$DESTDIR"/bin/$i
		done
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.


**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
 
.. raw:: pdf

   PageBreak




.. _audit:
audit
+++++

Audit paketi, Linux sistemlerinde güvenlik denetimlerini gerçekleştirmek için tasarlanmış bir yazılımdır. Bu paket, sistemdeki önemli olayları, kullanıcı aktivitelerini ve dosya erişimlerini kaydederek, sistem yöneticilerine kapsamlı bir denetim ve izleme imkanı sunar. Debian ortamında bu paketin derlenmesi için; **sudo apt install libaudit-dev** komutuyla paketin kurulması gerekmektedir.

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="audit"
	version='3.1.1'
	depends=""
	description="servis yöneticisi"
	source="https://github.com/linux-audit/audit-userspace/archive/refs/tags/v$version.tar.gz"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		        mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		        rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		        cd $ROOTBUILDDIR #dizinine geçiyoruz
		        wget ${source}
		        for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		        dowloadfile=$(ls|head -1)
		        filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		        if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		        director=$(find ./* -maxdepth 0 -type d)
		        directorname=$(basename ${director})
		        if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		        mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup(){
		cp -prvf $PACKAGEDIR/files/ $SOURCEDIR
		./autogen.sh
		./configure --prefix=/usr --sysconfdir=/etc --libdir=/usr/lib64 --disable-zos-remote --disable-listener \
		--disable-systemd --disable-gssapi-krb5 --enable-shared=audit --with-arm --with-aarch64 --without-python \
		--without-python3 --with-libcap-ng=no
	}
	build(){
		    make
	}
	package(){
		make install DESTDIR=$DESTDIR
		install -Dm755 files/auditd.initd "$DESTDIR"/etc/init.d/auditd
		install -Dm755 files/auditd.confd "$DESTDIR"/etc/conf.d/auditd
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.


Ek dosyaları indirmek için `tıklayınız. <https://kendilinuxunuyap.github.io/_static/files/audit/files.tar>`_ **Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak





.. _libxcrypt:
libxcrypt
+++++++++

libxcrypt, Unix benzeri sistemlerde parolaların şifrelenmesi için kullanılan bir kütüphanedir. Bu kütüphane, geleneksel crypt() fonksiyonunun yerini alarak daha güvenli ve esnek bir şifreleme yöntemi sunar. libxcrypt, çeşitli şifreleme algoritmalarını destekler; bunlar arasında bcrypt, scrypt ve Argon2 gibi modern algoritmalar bulunmaktadır.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="libxcrypt"
	version="4.4.36"
	description="libxcrypt"
	source=("https://github.com/besser82/libxcrypt/releases/download/v4.4.36/libxcrypt-4.4.36.tar.xz")
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		   mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup() {
	    ./configure --prefix=/usr --libdir=/usr/lib64/ --sbindir=/usr/bin 
	}
	build() {
	    make -C $SOURCEDIR
	}
	package() {
	    make -C $SOURCEDIR install DESTDIR=$DESTDIR
	    ${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.

.. raw:: pdf

   PageBreak




.. _libnsl:
libnsl
++++++

libnsl, "Network Services Library" anlamına gelen bir kütüphanedir ve genellikle Unix sistemlerinde ağ hizmetleri ile ilgili işlevsellik sağlamak amacıyla kullanılır. Bu kütüphane, uzaktan prosedür çağrıları (RPC) ve diğer ağ iletişim protokollerinin uygulanmasında kritik bir bileşendir. libnsl, özellikle eski sistemlerde ve uygulamalarda yaygın olarak bulunur ve modern sistemlerde de bazı uygulamalar için gereklidir.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="libnsl"
	version="2.0.0"
	url="https://github.com/thkukuk/libnsl"
	description="Public client interface library for NIS(YP)"
	source="https://github.com/thkukuk/libnsl/releases/download/v$version/libnsl-$version.tar.xz"
	depends="libtirpc"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup(){
	    ./configure --prefix=/usr --libdir=/usr/lib64
	}
	build(){
	    make
	}
	package(){
	    make install DESTDIR=$DESTDIR
	    ${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak




.. _libbsd:
libbsd
++++++

libbsd, geliştiricilere daha güvenli ve taşınabilir kod yazma imkanı tanırken, aynı zamanda BSD sistemlerinde yaygın olarak kullanılan işlevlerin Linux üzerinde de kullanılmasını sağlar. Bu kütüphane, sistem programlama ve ağ programlama gibi alanlarda sıkça tercih edilmektedir.

Derleme
--------

Derlemek için **sudo apt-get install libbsd-dev** paketi kurulmalı.

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="libbsd"
	version="0.11.7"
	description="Library to provide useful functions commonly found on BSD systems"
	source="https://libbsd.freedesktop.org/releases/libbsd-$version.tar.xz"
	depends=""
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
		    wget ${source}
		    for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup(){
		autoreconf -fvi
		./configure --prefix=/usr --libdir=/usr/lib64
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}

	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.

.. raw:: pdf

   PageBreak




.. _libtirpc:
libtirpc
++++++++

libtirpc, UNIX sistemlerinde yaygın olarak kullanılan bir RPC kütüphanesidir. Bu kütüphane, istemci ve sunucu uygulamaları arasında uzaktan prosedür çağrıları yapmayı mümkün kılar. libtirpc, özellikle dağıtık sistemlerde veri paylaşımını ve iletişimi kolaylaştırmak amacıyla geliştirilmiştir.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="libtirpc"
	version="1.3.3"
	description="Transport Independent RPC library (SunRPC replacement)"
	source="https://downloads.sourceforge.net/libtirpc/libtirpc-$version.tar.bz2"
	depends=""
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}


	setup(){
		./configure --prefix=/usr \
		--libdir=/usr/lib64 \
		--sysconfdir=/etc \
		--disable-gssapi
	}

	build(){
	    make
	}

	package(){
	    make install DESTDIR=$DESTDIR
	    ${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak




.. _e2fsprogs:
e2fsprogs
+++++++++

e2fsprogs, Linux tabanlı sistemlerde yaygın olarak kullanılan bir dosya sistemi yönetim aracıdır. Bu paket, ext2, ext3 ve ext4 dosya sistemleri üzerinde çeşitli işlemler yapabilmek için gerekli olan araçları içerir. Örneğin, dosya sistemi oluşturma, onarma, kontrol etme ve boyutlandırma gibi işlemler e2fsprogs ile gerçekleştirilebilir.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	version="1.47.0"
	name="e2fsprogs"
	depends="glibc,readline,ncurses"
	description="modül ve sistem iletişimi sağlayan paket"
	source="https://mirrors.edge.kernel.org/pub/linux/kernel/people/tytso/e2fsprogs/v${version}/${name}-${version}.tar.xz"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup(){
		./configure --sbindir=/usr/bin --libdir=/usr/lib64/  
	}
	build(){
		make 
	}
	package(){
		make install DESTDIR=$DESTDIR
		rm -rf $DESTDIR/usr/share/man/man8/fsck.8
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak





.. _dostools:
dostools
++++++++

Dostools, Linux işletim sistemlerinde kullanılan bir dizi araç ve komut setidir. Bu araçlar, sistem yöneticilerine ve geliştiricilere, sistem yönetimi, dosya işlemleri ve ağ yönetimi gibi çeşitli görevleri daha verimli bir şekilde gerçekleştirme imkanı sunar.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	version="4.2"
	name="dosfstools"
	depends="glibc"
	description="DOS filesystem tools - provides mkdosfs, mkfs.msdos, mkfs.vfat"
	source="https://github.com/dosfstools/dosfstools/archive/refs/tags/v$version.tar.gz"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup(){
		./autogen.sh
		./configure --prefix=/usr --libdir=/usr/lib64/ --enable-compat-symlinks
	}
	build(){
		make 
	}
	package(){
		make install DESTDIR=$DESTDIR
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak





.. _initramfs-tools:
initramfs-tools
+++++++++++++++

initramfs-tools, Debian tabanlı sistemlerde kullanılan bir araçtır ve initramfs (initial RAM file system) oluşturmak için kullanılır. Bu araç, sistem açılırken kullanılan geçici bir dosya sistemini oluşturur ve gerekli modülleri yükler. initramfs için farklı araçlarda kullanılabilir.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	version="0.142"
	name="initramfs-tools"
	depends="glibc,readline,ncurses"
	description="initramfs  generate sağlayan paket"
	source="https://salsa.debian.org/kernel-team/initramfs-tools/-/archive/v$version/initramfs-tools-v$version.tar.gz"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		        mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		        rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		        cd $ROOTBUILDDIR #dizinine geçiyoruz
		        wget ${source}
		        for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		        dowloadfile=$(ls|head -1)
		        filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		        if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		        director=$(find ./* -maxdepth 0 -type d)
		        directorname=$(basename ${director})
		        if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		        mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup()	{
		    cp -prfv $PACKAGEDIR/files/* $SOURCEDIR/
		    patch -Np1 < $SOURCEDIR/patches/remove-zstd.patch
		    patch -Np1 < $SOURCEDIR/patches/remove-logsave.patch
		    patch -Np1 < $SOURCEDIR/patches/non-debian.patch
	}
	build()	{
	echo ""
	}
	package()	{
		    cat debian/*.install | sed "s/\t/ /g" | tr -s " " | while read line ; do
		    file=$(echo $line | cut -f1 -d" ")
		    target=$(echo $line | cut -f2 -d" ")
		    mkdir -p ${DESTDIR}/$target
		    cp -prvf $file ${DESTDIR}/$target/
		    done
		    # install mkinitramfs
		    cp -pvf mkinitramfs ${DESTDIR}/usr/sbin/mkinitramfs
		    sed -i "s/@BUSYBOX_PACKAGES@/busybox/g" ${DESTDIR}/usr/sbin/mkinitramfs
		    sed -i "s/@BUSYBOX_MIN_VERSION@/1.22.0/g" ${DESTDIR}/usr/sbin/mkinitramfs
		    # Remove debian stuff
		    rm -rvf ${DESTDIR}/etc/kernel
		    # install sysconf
		    mkdir -p ${DESTDIR}/etc/sysconf.d
		    install $SOURCEDIR/initramfs-tools.sysconf ${DESTDIR}/etc/sysconf.d/initramfs-tools
		    install $SOURCEDIR/zzz-busybox ${DESTDIR}/usr/share/initramfs-tools/hooks/
		    install $SOURCEDIR/modules ${DESTDIR}/usr/share/initramfs-tools/
		    install $SOURCEDIR/modules ${DESTDIR}/etc/initramfs-tools/

		    mkdir -p ${DESTDIR}/usr/share/initramfs-tools/conf-hooks.d
		    install $SOURCEDIR/conf-hooks.d/busybox ${DESTDIR}/usr/share/initramfs-tools/conf-hooks.d/
		    mkdir -p ${DESTDIR}/etc/initramfs-tools/scripts
			${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	  }
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.


.. raw:: pdf

   PageBreak

Ek dosyaları indirmek için `tıklayınız. <https://kendilinuxunuyap.github.io/_static/files/initramfs-tools/files.tar>`_ **Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.

**/etc/initramfs-tools/modules**
---------------------------------

**modules** dosyası initrd oluşturulma ve güncelleme durumunda isteğe bağlı olarak modullerin eklenmesisini ve **initrd** açıldığında modülün yüklenmesini istiyorsak **/etc/initramfs-tools/modules** komundaki dosyayı  aşağıdaki gibi düzenlemeliyiz. Bu dosya içinde **ext4**, **vfat** ve diğer yardımcı moduller eklenmiş durumdadır. 

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	### This file is the template for /etc/initramfs-tools/modules.
	### It is not a configuration file itself.
	###
	# List of modules that you want to include in your initramfs.
	# They will be loaded at boot time in the order below.
	#
	# Syntax:  module_name [args ...]
	#
	# You must run update-initramfs(8) to effect this change.
	#
	# Examples:
	#
	# raid1
	# sd_mod
	vfat
	fat
	nls_cp437
	nls_ascii
	nls_utf8
	ext4
 
**initramfs-tools Ayarları**
----------------------------

**/usr/share/initramfs-tools/hooks/** konumundaki dosyaları dikkatlice düzenlemek gerekmektedir.
Dosyaları alfabetik sırayla çalıştırdığı için **busybox** **zzz-busybox** şeklinde ayarlanmıştır.

**initrd Oluşturma/Güncelleme**
-------------------------------

Sistemin initrd.img dosyasının güncellenmesi/oluşturulması için çalıştığınız sistemde  aşağıdaki komutlarla yapılabilir. 

.. code-block:: shell

	/usr/sbin/update-initramfs -u -k $(uname -r) #initrd günceller

Eğer bir dizin içinde bir sisteme initrd oluşturlacaksa, yani chroot ile sisteme erişiliyorsa yukarıdaki komut yeterli olmayacaktır. chroot öncesinde sistemin **dev sys proc run** dizinlerinin  bağlanılması gerekmektedir. Dizindeki sistemimizin dizin konumu **/$HOME/distro/rootfs** olsun. Buna göre aşağıda sisteme yukarıdaki komutu çalıştırmadan önce çalıştırılması gereken komutlar aşağıda verilmiştir. Dikkat edilmesi gereken en önemli noktalardan biriside bu komutlar **root** yetkisiyle çalıştırılmalıdır.

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	rootfs="$HOME/distro/rootfs"
	distro="$HOME/distro"
	mkdir -p $rootfs/dev
	mkdir -p $rootfs/sys
	mkdir -p $rootfs/proc 
	mkdir -p $rootfs/run
	mkdir -p $rootfs/tmp
	mount --bind /dev $rootfs/dev
	mount --bind /sys $rootfs/sys
	mount --bind /proc $rootfs/proc
	mount --bind /run$rootfs/run
	mount --bind /tmp $rootfs/tmp
	
	### update-initrd
	fname=$(basename $rootfs/boot/config*)
	kversion=${fname:7}
	mv $rootfs/boot/config* $rootfs/boot/config-$kversion
	cp $rootfs/boot/config-$kversion $rootfs/etc/kernel-config
	
	chroot $rootfs update-initramfs -u -k $kversion
	
	umount -lf -R $rootfs/dev 2>/dev/null
	umount -lf -R $rootfs/sys 2>/dev/null
	umount -lf -R $rootfs/proc 2>/dev/null
	umount -lf -R $rootfs/run 2>/dev/null
	umount -lf -R $rootfs/tmp 2>/dev/null
	#### Copy initramfs
	cp -pf $rootfs/boot/initrd.img-* $distro/iso/boot/initrd.img
	 
Güncelleme ve oluşturma aşamasında **/usr/share/initramfs-tools/hooks/** konumundaki dosyarı çalıştırarak yeni initrd dosyasını oluşturacaktır.
Oluşturma **/var/tmp** olacaktır. Ayrıca **/boot/config-6.6.0-amd64** gibi sistemde kullanılan kernel versiyonuyla config dosyası olmalıdır. Burada verilen **6.6.0-amd64** örnek amaçlı verilmiştir.

**initrd açılma Süreci**
------------------------

Sistemin açılması için **vmlinuz**, **initrd.img** ve **grub.cfg** dosyalarının olması yeterlidir. **initrd.img** sistemin açılma sürecini yürüten bir kernel yardımcı ön sistemidir. **initrd.img** açıldığında aşğıdaki gibi bir dizin yapısı olur. Bu dizinler içindeki **script** dizini çok önemlidir. Bu dizin içindeki scriptler belirli bir sırayla çalışarak sistemin açılması sağlanır.

.. image:: /_static/images/initrd-2.png
  	:width: 600

**initrd script İçeriği**
-------------------------
**script** içerindeki dizinler  aşağıdaki gibidir. Bu dizinler içinde scriptler vardır. Bu dizinlerin içeriği sırayla şöyle çalışmaktadır.

1. init-top
2. init-premount
3. init-bottom

.. image:: /_static/images/initrd-3.png
  	:width: 600
  	
Oluşan initrd.img dosyası sistemin açılmasını sağlayamıyorsa script açılış sürecini takip ederek sorunları çözebilirsiniz.

.. raw:: pdf

   PageBreak

.. _libxml2:
libxml2
+++++++

libxml2, özellikle XML ve HTML belgeleri ile çalışmak için tasarlanmış, yüksek performanslı bir C kütüphanesidir. Geliştiricilere, XML belgelerini analiz etme, oluşturma ve düzenleme gibi işlemleri gerçekleştirme imkanı sunar. libxml2, DOM (Document Object Model) ve SAX (Simple API for XML) gibi iki farklı API ile çalışabilme yeteneğine sahiptir. Bu sayede, hem bellek dostu hem de hızlı bir şekilde veri işleme imkanı sağlar.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	version="2.12.6"
	name="libxml2"
	depends="glibc,acl,openssl,libtool,icu"
	builddepend="python3"
	description="XML C parser and toolkit"
	source="https://github.com/GNOME/libxml2/archive/refs/tags/v${version}.tar.gz"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup(){
        ./autogen.sh
       	./configure --prefix=/usr --libdir=/usr/lib64 --with-history --with-icu --with-legacy --with-threads
	}
	build(){
		make 
	}
	package(){
		make install DESTDIR=$DESTDIR
		mkdir -p $DESTDIR/usr/lib64/python3.11
		mv $DESTDIR/usr/lib/* $DESTDIR/usr/lib64/
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak





.. _expat:
expat
+++++

Expat, özellikle C dilinde geliştirilmiş bir XML ayrıştırma kütüphanesidir. Bu kütüphane, XML belgelerini okuma ve işleme süreçlerini kolaylaştırmak amacıyla tasarlanmıştır. Expat, olay tabanlı bir ayrıştırma modeli kullanarak, XML belgelerinin içeriğini parçalara ayırır ve bu parçaları işlemek için geliştiricilere bir dizi geri çağırma (callback) fonksiyonu sunar. Bu sayede, büyük XML dosyaları ile çalışırken bellek verimliliği sağlanır.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="expat"
	version="2.6.2"
	vrsn="2_6_2"
	description="An XML parser library"
	#source="https://github.com/libexpat/libexpat/archive/refs/tags/R_${version}.tar.gz"
	source="https://github.com/libexpat/libexpat/releases/download/R_${vrsn}/expat-${version}.tar.bz2"
	depends=""
	builddepend=""
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup(){
	    cmake -DCMAKE_INSTALL_PREFIX=/usr \
		-DCMAKE_INSTALL_LIBDIR=lib64 \
		-DCMAKE_BUILD_TYPE=None \
		-DEXPAT_BUILD_DOCS=false \
		-W no-dev \
		-B $BUILDDIR
	}
	build(){
	    make -C $BUILDDIR
	}
	package(){
	    make DESTDIR="$DESTDIR" install -C $BUILDDIR
	    ${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.


**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak




.. _libmd:
libmd
+++++

libmd, özellikle BSD tabanlı sistemlerde bulunan bir kütüphanedir ve çeşitli kriptografik hash fonksiyonlarını (MD5, SHA-1, SHA-256 gibi) destekler. Bu kütüphane, veri bütünlüğünü sağlamak ve şifreleme işlemlerini gerçekleştirmek için kullanılır. Örneğin, bir dosyanın hash değerini hesaplamak, dosyanın değiştirilip değiştirilmediğini kontrol etmek için yaygın bir yöntemdir.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="libmd"
	version="1.1.0"
	description="Message Digest functions from BSD systems"
	depends=""
	source="https://archive.hadrons.org/software/libmd/libmd-$version.tar.xz"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup(){
	    ./configure --prefix=/usr --libdir=/usr/lib64/
	}
	build(){
	    make 
	}
	package(){
	    make install DESTDIR=$DESTDIR
	    ${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak




.. _libaio:
libaio
++++++

Libio, C dilinde girdi/çıktı işlemlerini kolaylaştıran bir kütüphanedir. Temel olarak, dosya okuma ve yazma işlemlerini, bellek yönetimini ve veri akışını yönetmek için kullanılır. Libio, performansı artırmak amacıyla tamponlama (buffering) mekanizmaları kullanır. Bu sayede, verilerin daha verimli bir şekilde işlenmesini sağlar. Örneğin, bir dosyadan veri okurken, veriler önce bir tampon belleğe alınır ve ardından işlenir. Bu, disk erişimlerini azaltarak programın genel performansını artırır.

Derleme
-------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="libaio"
	version="0.3.113"
	description="Asynchronous input/output library that uses the kernels native interface"
	source="https://pagure.io/libaio/archive/libaio-$version/libaio-libaio-$version.tar.gz"
	depends=""
	builddepend=""
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup (){
		echo ""
	}
	build(){
		
	    make
	}
	package(){
	    make install DESTDIR=$DESTDIR
	    ${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak




.. _lvm2:
lvm2
++++

LVM2 (Logical Volume Manager 2), Linux işletim sistemlerinde disk alanını yönetmek için kullanılan bir araçtır. LVM2, fiziksel disklerin mantıksal birimlere dönüştürülmesine olanak tanır. Bu sayede, disk alanı dinamik olarak genişletilebilir veya daraltılabilir. LVM2, sistem yöneticilerine disk alanını daha verimli bir şekilde kullanma imkanı sunar. Örneğin, bir fiziksel disk üzerinde birden fazla mantıksal birim oluşturabilir ve bu birimlerin boyutlarını ihtiyaçlara göre değiştirebilirsiniz.

Debian ortamında derlemek lvm2 paketinde sorunlar çıkmaktadır. Bunun sebebi kernel derlenmesi sırasında lvm ile ilgili özellikleri aktif etmek gerekiyor. Bundan dolayı isteyen aşağıda derleme bölümünde verilen derleme talimatını kullanarak başka dağıtımlarda derleme yapabilir. Burada geliştirilmesi anlatılan sistem üzerinde derlenen paketi indirip hazırladığımız sisteme kuran script aşağıda verilmiştir.

lvm2 Kurma Scripti
------------------

.. code-block:: shell

	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="lvm2"
	version="2_03_21"
	description="User-land utilities for LVM2 (device-mapper) software"
	source=""
	depends="libaio"
	builddepend=""
	group="sys.fs"

	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -n 1)"	#Detect the name of the display in use
	user=$(who | grep '('$display')' | awk '{print $1}')	#Detect the user using such display
	ROOTBUILDDIR="/home/$user/distro/build" # Derleme konumu
	BUILDDIR="/home/$user/distro/build/build-${name}-${version}" #Derleme yapılan paketin derleme konumun
	DESTDIR="/home/$user/distro/rootfs" #Paketin yükleneceği sistem konumu
	PACKAGEDIR=$(pwd) #paketin derleme talimatının verildiği konum
	SOURCEDIR="/home/$user/distro/build/${name}-${version}" #Paketin kaynak kodlarının olduğu konum

	initsetup(){
		mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		cd $ROOTBUILDDIR #dizinine geçiyoruz
		wget ${source}
 		for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		dowloadfile=$(ls|head -1)
		filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		director=$(find ./* -maxdepth 0 -type d)
		directorname=$(basename ${director})
		if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup(){
		mkdir -p $SOURCEDIR
		cd $SOURCEDIR
		#dosya indiriliyor
		wget -O lvm2.kly https://kendilinuxunuyap.github.io/_static/files/lvm2/lvm2-2_03_21.kly 				
		# tar -xf lvm2.kly
		tar -xf lvm2.kly
		tar -xf rootfs.tar.xz
	}
	build(){
		echo ""
	}
	package(){
		cd $SOURCEDIR
		cp -prfv etc  ${DESTDIR}/
		cp -prfv usr  ${DESTDIR}/
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.


**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak
 
Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="lvm2"
	version="2_03_21"
	description="User-land utilities for LVM2 (device-mapper) software"
	source="https://github.com/lvmteam/lvm2/archive/refs/tags/v$version.tar.gz"
	depends="libaio"
	builddepend=""
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup(){
			./configure --prefix=/usr --libdir=/usr/lib64/  CONFIG_SHELL=/bin/bash --sbindir=/usr/bin \ 
			--sysconfdir=/etc --localstatedir=/var \
			--enable-cmdlib --enable-dmeventd --enable-lvmpolld --enable-pkgconfig --enable-readline \
			--enable-udev_rules --enable-udev_sync --enable-write_install --disable-systemd \
			--with-cache=internal --with-default-dm-run-dir=/run --with-default-locking-dir=/run/lock/lvm \
			--with-default-pid-dir=/run --with-default-run-dir=/run/lvm --with-thin=internal \
			--with-udev-prefix=/usr
	}
	build(){
	    make
	}
	package() {
	    make install DESTDIR=$DESTDIR
	    ${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}

	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.


**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak




.. _popt:
popt
++++

Popt, "Portable Options Parsing Library" ifadesinin kısaltmasıdır ve özellikle C programlama dilinde geliştirilmiş bir kütüphanedir. Bu kütüphane, komut satırı argümanlarını analiz etmek ve yönetmek için kullanılır. Popt, kullanıcıların programlarına daha anlaşılır ve esnek bir seçenek yönetimi eklemelerine olanak tanır.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="popt"
	version="1.19"
	description="A commandline option parser"
	source="http://ftp.rpm.org/popt/releases/popt-${version%.*}.x/popt-${version}.tar.gz"
	depends=""
	builddepend=""
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup(){
		CFLAGS+=" -ffat-lto-objects" ./configure --prefix=/usr
	}

	build(){
	    make
	}

	package(){
	    make install DESTDIR=$DESTDIR
	    ${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak




.. _icu:
icu
+++

ICU, çok dilli uygulamalar geliştirmek için gerekli olan metin işleme, tarih ve saat formatlama, sayı biçimlendirme gibi işlevleri sağlayan bir kütüphanedir. Unicode standardını destekleyerek, farklı dillerdeki karakterlerin doğru bir şekilde işlenmesini ve görüntülenmesini mümkün kılar. Özellikle, uluslararasılaşma (i18n) ve yerelleştirme (l10n) süreçlerinde kritik bir rol oynar.

Derleme
--------

.. code-block:: shell

	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="icu"
	version="74-2"
	description="icu International Components for Unicode"
	source=("https://github.com/unicode-org/icu/releases/download/release-${version}/icu4c-74_2-src.tgz")
	depends=()
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup(){
	    cd source
	    ./configure --prefix=/usr \
		--libdir=/usr/lib64/
	}

	build(){
	    make
	}

	package(){
	    make install DESTDIR=$DESTDIR
	    chmod +x "$DESTDIR"/usr/bin/icu-config
	    ${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak




.. _iproute2:
iproute2
++++++++

iproute2, Linux tabanlı sistemlerde ağ yönetimi için geliştirilmiş bir araç setidir. Bu araç seti, özellikle ağ yönlendirmesi ve trafik kontrolü gibi karmaşık işlemleri gerçekleştirmek için kullanılır. iproute2, ip komutu ile birlikte gelir ve bu komut, ağ arayüzlerini, yönlendirme tablolarını ve diğer ağ yapılandırmalarını yönetmek için kapsamlı bir arayüz sunar.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="iproute2"
	version="6.10.0"
	description="GNU regular expression matcher"
	source="https://mirrors.edge.kernel.org/pub/linux/utils/net/iproute2/iproute2-6.10.0.tar.xz"
	depends=""
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup(){
		cp -prvf ${PACKAGEDIR}/files/ $SOURCEDIR/
		patch -Np1 -i $SOURCEDIR/files/0001-make-iproute2-fhs-compliant.patch
		patch -Np1 -i $SOURCEDIR/files/0002-bdb-5-3.patch
		sed -i 's/-Werror//' Makefile
		export CFLAGS+=' -ffat-lto-objects'
		./configure
	}
	build(){
	   make DBM_INCLUDE='/usr/include/db5.3'
	}
	package(){
		make DESTDIR=$DESTDIR SBINDIR="/sbin" install
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

Ek dosyaları indirmek için `tıklayınız. <https://kendilinuxunuyap.github.io/_static/files/iproute2/files.tar>`_ **Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.

.. raw:: pdf

   PageBreak




.. _net-tools:
net-tools
+++++++++

net-tools, Linux tabanlı sistemlerde ağ yönetimi için kullanılan klasik bir araçlar paketidir. Bu paket, ifconfig, route, netstat, arp gibi komutları içerir. ifconfig komutu, ağ arayüzlerinin durumunu görüntülemek ve yapılandırmak için kullanılırken, route komutu yönlendirme tablolarını yönetmekte kullanılır. netstat ise ağ bağlantılarını ve istatistiklerini gösterir.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="net-tools"
	version="2.10"
	description="GNU regular expression matcher"
	source="https://sourceforge.net/projects/net-tools/files/net-tools-2.10.tar.xz"
	depends=""
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup(){
		export BINDIR='/usr/bin' SBINDIR='/usr/bin'
	}

	build(){
	   yes "" | make
	}

	package(){
	    make install DESTDIR=$DESTDIR
	    # the following is provided by yp-tools
	  	rm "${DESTDIR}"/usr/bin/{nis,yp}domainname
	  	# hostname is provided by inetutils
	  	rm "${DESTDIR}"/usr/bin/{hostname,dnsdomainname,domainname}
	  	rm -r "${DESTDIR}"/usr/share/man/man1
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak




.. _dhcp:
dhcp
++++

Bu protokol, bir istemci cihazın ağa bağlandığında, DHCP sunucusuna bir istek göndererek IP adresi talep etmesiyle başlar. Sunucu, istemciye uygun bir IP adresi, alt ağ maskesi, varsayılan ağ geçidi ve DNS sunucusu gibi bilgileri iletir.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="dhcp"
	version="4.4.3"
	description="GNU regular expression matcher"
	source="https://downloads.isc.org/isc/dhcp/4.4.3/dhcp-4.4.3.tar.gz"
	depends=""
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup(){
		cp -prvf ${PACKAGEDIR}/files $SOURCEDIR/
    	./configure --prefix=/usr --libdir=/usr/lib64/
	}
	build(){
	    make
	}
	package(){
		mkdir -p $DESTDIR/sbin/
	    make install DESTDIR=$DESTDIR
	    install  $SOURCEDIR/client/scripts/linux $DESTDIR/sbin/dhclient-script
	    mkdir -p $DESTDIR/etc/init.d    
	    for level in boot default nonetwork shutdown sysinit ; do
	    mkdir -p ${DESTDIR}/etc/runlevels/$level
	    done
		install -Dm755  $SOURCEDIR/files/dhclient.init.d $DESTDIR/etc/init.d/dhclient
		install -Dm755  $SOURCEDIR/files/dhclient.init.d ${DESTDIR}/etc/runlevels/default/dhclient
	    ${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

Ek dosyaları indirmek için `tıklayınız. <https://kendilinuxunuyap.github.io/_static/files/dhcp/files.tar>`_ **Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak




.. _openrc:
openrc
++++++

OpenRC, sistem başlangıcını ve hizmetlerin yönetimini sağlamak amacıyla geliştirilmiş bir init sistemidir. Openrc'nin kullanımı için **Yardımcı Konular** bölümüne bakınız.

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="openrc"
	version="0.53"
	description="The OpenRC init system"
	source="https://github.com/OpenRC/openrc/archive/refs/tags/$version.zip"
	depends=""
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı
	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup(){
	cp -prfv $PACKAGEDIR/files $SOURCEDIR/
	cp -prfv $PACKAGEDIR/extras $SOURCEDIR/
	meson setup $BUILDDIR --sysconfdir=/etc --prefix=/ --libdir=/lib64 --includedir=/usr/include \ 
	-Ddefault_library=both -Dzsh-completions=true -Dbash-completions=true -Dpam=true -Dselinux=disabled -Dpkgconfig=true
	}
	build(){
	    meson compile -C $BUILDDIR
	}
	package(){
	    export DESTDIR=${DESTDIR}//
	    DESTDIR="$DESTDIR" meson install --no-rebuild -C $BUILDDIR
	    rm -f ${DESTDIR}/etc/runlevels/*/*	    # disable all services
	    rm ${DESTDIR}//etc/init.d/functions.sh
	    ln -s ../../lib/rc/sh/functions.sh ${DESTDIR}/etc/init.d/functions.sh
	    mkdir -p ${DESTDIR}/etc/sysconf.d/	    # install sysconf script
	    install $SOURCEDIR/files/openrc.sysconf ${DESTDIR}/etc/sysconf.d/openrc
	    mkdir -p ${DESTDIR}/usr ${DESTDIR}/sbin
	    mv ${DESTDIR}/{,usr}/share	    # move /share to /usr/share
	    install $SOURCEDIR/files/reboot ${DESTDIR}/sbin/reboot	    # reboot and poweroff script
	    install $SOURCEDIR/files/poweroff ${DESTDIR}/sbin/poweroff
	    ln -s openrc-shutdown ${DESTDIR}/sbin/shutdown
	    mkdir -p ${DESTDIR}/usr/libexec
	    install $SOURCEDIR/extras/disable-secondary-gpu.sh ${DESTDIR}/usr/libexec/disable-secondary-gpu
	    install $SOURCEDIR/extras/disable-secondary-gpu.initd ${DESTDIR}/etc/init.d
	    install $SOURCEDIR/extras/backlight-restore.initd ${DESTDIR}/etc/init.d
	    install $SOURCEDIR/files/0modules.init.d ${DESTDIR}/etc/init.d/0modules
	    for level in boot default nonetwork shutdown sysinit ; do
	    mkdir -p ${DESTDIR}/etc/runlevels/$level
	    done
	    touch ${DESTDIR}/etc/fstab
	    install $SOURCEDIR/files/0modules.init.d ${DESTDIR}/etc/init.d/0modules
	    install $SOURCEDIR/files/0modules.init.d ${DESTDIR}/etc/runlevels/default/0modules
	    install ${DESTDIR}/etc/init.d/hostname ${DESTDIR}/etc/runlevels/default/hostname
	    cd ${DESTDIR}/etc/init.d/
	    ln -s agetty agetty.tty1
	    install ${DESTDIR}/etc/init.d/agetty.tty1 ${DESTDIR}/etc/runlevels/default/agetty.tty1
	    ${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

Ek dosyaları indirmek için; 1. Ek `tıklayınız. <https://kendilinuxunuyap.github.io/_static/files/openrc/files.tar>`_ 2.Ek `tıklayınız.. <https://kendilinuxunuyap.github.io/_static/files/openrc/extras.tar>`_ **Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.

.. raw:: pdf

   PageBreak




.. _rsync:
rsync
+++++

rsync, dosya transferi ve senkronizasyonu için geliştirilmiş bir yazılımdır. Temel işlevi, yerel veya uzak sistemler arasında dosyaların ve dizinlerin hızlı ve verimli bir şekilde kopyalanmasını sağlamaktır. rsync, yalnızca değişen verileri transfer ederek bant genişliği kullanımını optimize eder. Bu özellik, büyük dosyaların veya dizinlerin güncellenmesi gerektiğinde önemli bir avantaj sunar.

Debian ortamında bu paketin derlenmesi için; **sudo apt install libzstd-dev libacl1-dev libacl1** komutuyla paketlerin kurulması gerekmektedir.


.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	version="3.2.7"
	name="rsync"
	depends="glibc,acl,openssl"
	description="shell ve network copy"
	source="https://download.samba.org/pub/rsync/src/${name}-${version}.tar.gz"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup(){
		./configure --prefix=/usr --libdir=/lib64/ --with-included-popt --with-included-zlib \
		--disable-xxhash --disable-lz4
	}
	build(){
		make 
	}
	package(){
		make install DESTDIR=$DESTDIR
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}

	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.


**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak




.. _kbd:
kbd
+++

KBD paketi, Linux tabanlı sistemlerde klavye ile etkileşimi yönetmek için kritik bir bileşendir. Bu paket, farklı klavye düzenlerini destekler ve kullanıcıların ihtiyaçlarına göre özelleştirilmiş tuş atamaları yapmalarına olanak tanır. Örneğin, bir kullanıcı farklı bir dilde yazmak istediğinde, KBD paketi sayesinde o dilin klavye düzenine geçiş yapabilir.


Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="kbd"
	version="2.6.4"
	description="Keytable files and keyboard utilities"
	source="https://www.kernel.org/pub/linux/utils/kbd/kbd-${version}.tar.gz"
	depends="pam"
	makedepend="flex,autoconf,automake"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		        mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		        rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		        cd $ROOTBUILDDIR #dizinine geçiyoruz
				wget ${source}
				for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		        dowloadfile=$(ls|head -1)
		        filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		        if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		        director=$(find ./* -maxdepth 0 -type d)
		        directorname=$(basename ${director})
		        if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		        mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup(){
		    cp -prfv $PACKAGEDIR/files $SOURCEDIR/
		autoreconf -fvi
		./configure --prefix=/usr --sysconfdir=/etc --datadir=/usr/share/kbd --enable-optional-progs
	}
	build(){
		make KEYCODES_PROGS=yes RESIZECONS_PROGS=yes
	}
	package(){
		make DESTDIR=${DESTDIR} install
		for level in boot default nonetwork shutdown sysinit ; do
		mkdir -p ${DESTDIR}/etc/runlevels/$level
		done
		install -Dm755 $SOURCEDIR/files/loadkeys.initd "$DESTDIR"/etc/init.d/loadkeys
		install -Dm755  $SOURCEDIR/files/loadkeys.initd ${DESTDIR}/etc/runlevels/default/loadkeys

		install -Dm644 $SOURCEDIR/files/loadkeys.confd "$DESTDIR"/etc/conf.d/loadkeys
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

Ek dosyaları indirmek için `tıklayınız. <https://kendilinuxunuyap.github.io/_static/files/kbd/files.tar>`_ **Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak




.. _kernel:
kernel
++++++

Kernel, bilgisayar sistemlerinde işletim sisteminin kalbini oluşturan bir yazılım katmanıdır. Donanım kaynaklarını yönetir, sistem çağrılarını işler ve uygulama yazılımlarının donanım ile etkileşimini sağlar. Linux işletim sisteminde, kernel, çoklu görev yönetimi, bellek yönetimi, dosya sistemi erişimi ve ağ iletişimi gibi kritik işlevleri yerine getirir.

Aşağıda nasıl derlendiği detaylıca anlatılmıştır. Derleme işlemi zaman ve tecrübe gerektirdiği için hazır derlenmiş olanı kullanacağız. Aslında debian, arch vb. dağıtımların kernelini derlemeden kullanabiliriz. Bir uyumsuzluk yaratmayacaktır. Bundan dolayı kendi derlediğimiz kernelini indirip kendi sistemimize yükleyen bir işlem yapacağız. Fakat derlemek isterseniz Derleme başlığı altında paylaşılan scripti kullanabilirsiniz. Kerneli hazırladığımız sistemem kurmak için aşağıda script verilmiştir.

Debian Kernel Kullanma
----------------------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	version="6.10.6"
	name="linux-image"
	depends=""
	description="temel dağıtım kernel dosyası ve moduller"
	source=""
	groups="sys.base"
	
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -n 1)"	#Detect the name of the display in use
	user=$(who | grep '('$display')' | awk '{print $1}')	#Detect the user using such display
	ROOTBUILDDIR="/home/$user/distro/build" # Derleme konumu
	BUILDDIR="/home/$user/distro/build/build-${name}-${version}" #Derleme yapılan paketin derleme konumun
	DESTDIR="/home/$user/distro/rootfs" #Paketin yükleneceği sistem konumu
	PACKAGEDIR=$(pwd) #paketin derleme talimatının verildiği konum
	SOURCEDIR="/home/$user/distro/build/${name}-${version}" #Paketin kaynak kodlarının olduğu konum

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup(){
		mkdir -p $SOURCEDIR
		cd $SOURCEDIR
		wget -O kernel.kly https://github.com/kendilinuxunuyap/kly-binary-packages/raw/master/kernel/kernel-6.10.8.kly
		tar -xf kernel.kly
		tar -xf rootfs.tar.xz
	}
	build(){
		echo ""
	}
	package(){
		cd $SOURCEDIR
		cp -prfv boot  ${DESTDIR}/
		cp -prfv lib/*  ${DESTDIR}/lib/
		find ${DESTDIR}/ -iname "*" -exec unxz {} \;
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.


.. raw:: pdf
   PageBreak

Kendi Kernelimiz Derleme
------------------------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="kernel-headers"
	version="6.9.9"
	description="Linux kernel"
	source="https://cdn.kernel.org/pub/linux/kernel/v6.x/linux-$version.tar.xz"
	depends="kernel"
	builddepend="rsync,bc,cpio,gettext,elfutils,pahole,perl,python,tar,xz-utils"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		cd $ROOTBUILDDIR #dizinine geçiyoruz
		wget ${source}
		for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		dowloadfile=$(ls|head -1)
		filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		director=$(find ./* -maxdepth 0 -type d)
		directorname=$(basename ${director})
		if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup(){
		cp -prvf $PACKAGEDIR/files/ $SOURCEDIR/
		patch -Np1 -i $PACKAGEDIR/files/patch-$version
		cp $PACKAGEDIR/files/config $SOURCEDIR/.config
		make olddefconfig
	}
	build(){
		make bzImage
		make modules
	}

.. raw:: pdf

   PageBreak
   
.. code-block:: bash
	  
	#--------------------------------------------------------------------------------------------------------------------
	# Kernel dereme scriptini devamı
	package(){
		arch="x86"
		kernelbuilddir="${DESTDIR}/lib/modules/${version}/build"
		# install bzImage
		mkdir -p "$DESTDIR/boot"
		install -Dm644 "$(make -s image_name)" "$DESTDIR/boot/vmlinuz-${version}"
		#make INSTALL_PATH=$DESTDIR install ARCH=amd64
		# install modules
		mkdir -p ${DESTDIR}/lib/modules/${version}
		mkdir -p $DESTDIR/usr/src
		mkdir -p ${DESTDIR}/lib/modules/${version}/build
		make INSTALL_MOD_PATH=$DESTDIR modules_install INSTALL_MOD_STRIP=1 -j$(nproc)
		rm "${DESTDIR}/lib/modules/${version}"/{source,build} || true
		depmod --all --verbose --basedir="$DESTDIR" "${version}" || true
		# install build directories
		install .config "$DESTDIR/boot/config-${version}"
		install -Dt "$kernelbuilddir/kernel" -m644 kernel/Makefile
		install -Dt "$kernelbuilddir/arch/$arch" -m644 arch/$arch/Makefile
		cp -t "$kernelbuilddir" -a scripts
		install -Dt "$kernelbuilddir/tools/objtool" tools/objtool/objtool
		mkdir -p "$kernelbuilddir"/{fs/xfs,mm}
		ln -s "../../lib/modules/${version}/build" "$DESTDIR/usr/src/linux-headers-${version}"
		install -Dt "$kernelbuilddir" -m644 Makefile Module.symvers System.map vmlinux
		# install libc headers
		mkdir -p "$DESTDIR/usr/include/linux"
		cp -v -t "$DESTDIR/usr/include/" -a include/linux/
		cp -v -t "$DESTDIR/usr/" -a tools/include	
		make headers_install INSTALL_HDR_PATH=$DESTDIR/usr

		mkdir -p "$kernelbuilddir" "$kernelbuilddir/arch/$arch"
		cp -v -t "$kernelbuilddir" -a include
	   	cp -v -t "$kernelbuilddir/arch/$arch" -a arch/$arch/include
		install -Dt "$kernelbuilddir/arch/$arch/kernel" -m644 arch/$arch/kernel/asm-offsets.*
		install -Dt "$kernelbuilddir/drivers/md" -m644 drivers/md/*.h
		install -Dt "$kernelbuilddir/net/mac80211" -m644 net/mac80211/*.h
		install -Dt "$kernelbuilddir/drivers/media/i2c" -m644 drivers/media/i2c/msp3400-driver.h
		install -Dt "$kernelbuilddir/drivers/media/usb/dvb-usb" -m644 drivers/media/usb/dvb-usb/*.h
		install -Dt "$kernelbuilddir/drivers/media/dvb-frontends" -m644 drivers/media/dvb-frontends/*.h
		install -Dt "$kernelbuilddir/drivers/media/tuners" -m644 drivers/media/tuners/*.h
		install -Dt "$kernelbuilddir/drivers/iio/common/hid-sensors" -m644 drivers/iio/common/hid-sensors/*.h 		
		# https://bugs.archlinux.org/task/71392
		find . -name 'Kconfig*' -exec install -Dm644 {} "$kernelbuilddir/{}" \;
		find -L "$kernelbuilddir" -type l -printf 'Removing %P\n' -delete					
		# clearing
		find "$kernelbuilddir" -type f -name '*.o' -printf 'Removing %P\n' -delete
		if [[ -d "$kernelbuilddir" ]] ; then
	    while read -rd '' file; do
		case "$(file -Sib "$file")" in
		    application/x-sharedlib\;*)      # Libraries (.so)
		        strip "$file" ;;
		    application/x-executable\;*)     # Binaries
		        strip "$file" ;;
		    application/x-pie-executable\;*) # Relocatable binaries
		        strip "$file" ;;
		esac
	    done < <(find "$kernelbuilddir" -type f -perm -u+x ! -name vmlinux -print0)
		fi
		if [[ -f "$kernelbuilddir/vmlinux" ]] ; then
	    strip "$kernelbuilddir/vmlinux"
		fi
		mkdir -p "$DESTDIR/usr/src"
		ln -sr "$kernelbuilddir" "$DESTDIR/usr/src/linux"
	    mv -vf System.map $DESTDIR/boot/System.map-$version
	    find ${DESTDIR}/ -iname "*" -exec unxz {} \;
	    depmod -b "$DESTDIR" -F $DESTDIR/boot/System.map-$version $version
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

Ek dosyaları indirmek için `tıklayınız. <https://kendilinuxunuyap.github.io/_static/files/kernel/files.tar>`_ **Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.

.. raw:: pdf

   PageBreak


.. _dialog:
dialog
++++++

Dialog paketi, terminal tabanlı uygulamalar için kullanıcı ile etkileşim kurmayı kolaylaştıran bir araçtır. Bu paket, kullanıcıdan bilgi almak veya kullanıcıya bilgi sunmak amacıyla çeşitli diyalog kutuları oluşturmanıza olanak tanır. Örneğin, metin kutuları, onay kutuları, seçim kutuları gibi farklı türde diyaloglar oluşturabilirsiniz.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	version="1.3-20230209"
	name="dialog"
	depends="glibc,readline,ncurses"
	description="shell box kütüphanesi"
	source="https://invisible-island.net/archives/dialog/${name}-${version}.tgz"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup(){
    	./configure --prefix=/usr --libdir=/lib64/ --with-ncursesw
	}
	build(){
		make 
	}
	package(){
		make install DESTDIR=$DESTDIR
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.


**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak





.. _live-boot:
live-boot
+++++++++

Live-boot paketi, kullanıcıların bir işletim sistemini kurmadan önce denemelerine olanak tanıyan bir araçtır. Genellikle bir USB bellek veya CD/DVD gibi taşınabilir bir ortamda bulunur. Bu paket, sistemin kurulu olduğu ortamdan bağımsız olarak çalışır ve kullanıcıların işletim sisteminin özelliklerini, performansını ve uyumluluğunu test etmelerine imkan tanır.

Debian ortamında bu paketin derlenmesi için; **sudo apt install po4a** komutuyla paketin kurulması gerekmektedir.

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	version="1230131"
	name="live-boot"
	depends="glibc,acl,openssl"
	description="shell ve network copy"
	source="https://salsa.debian.org/live-team/${name}/-/archive/debian/1%2520230131/${name}-debian-1%2520230131.tar.gz"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup(){
		echo ""
	}
	build(){
		make 
	}
	package(){
		make install DESTDIR=$DESTDIR
		sed -i "s/copy_exec \/bin\/mount \/bin/copy_exec \/usr\/bin\/mount \/bin/g" \
		$DESTDIR/usr/share/initramfs-tools/hooks/live
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.


**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak






.. _live-config:
live-config
+++++++++++

Live-Config, özellikle canlı CD veya USB ortamlarında kullanılan bir yapılandırma paketidir. Bu paket, sistemin başlangıçta otomatik olarak belirli ayarlarla başlatılmasını sağlar. Örneğin, ağ ayarları, kullanıcı hesapları ve diğer sistem yapılandırmaları gibi unsurlar, Live-Config aracılığıyla önceden tanımlanabilir.

Kullanıcılar, Live-Config ile özelleştirilmiş bir canlı sistem oluşturabilir ve bu sistemin her açılışında belirli ayarların otomatik olarak uygulanmasını sağlayabilir. Bu, özellikle eğitim, test veya kurtarma senaryolarında büyük bir avantaj sunar.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	version="11.0.4"
	name="live-config"
	depends="glibc,acl,openssl"
	description="shell ve network copy"
	source="https://salsa.debian.org/live-team/live-config/-/archive/debian/11.0.4/live-config-debian-11.0.4.tar.gz"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
			wget ${source}
			for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup(){
		echo ""
	}
	build(){
		make 
	}
	package(){
		make install DESTDIR=$DESTDIR
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.


**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak





.. _parted:
parted
++++++

Parted, Linux tabanlı sistemlerde disk bölümlerini oluşturmak, silmek, boyutlandırmak ve düzenlemek için kullanılan bir komut satırı aracıdır. Kullanıcıların disk alanlarını daha verimli bir şekilde yönetmelerine yardımcı olur. Parted, hem MBR (Master Boot Record) hem de GPT (GUID Partition Table) bölümlendirme şemalarını destekler.

Derleme
--------

Debian ortamında bu paketin derlenmesi için;

- **sudo apt install libparted-dev** 

komutuyla paketin kurulması gerekmektedir.

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	version="3.6"
	name="parted"
	depends="glibc"
	description="disks tools"
	source="https://ftp.gnu.org/gnu/parted/parted-${version}.tar.xz"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
		    wget ${source}
		    for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup(){
    	./configure --prefix=/usr --libdir=/usr/lib64/ --sbindir=/usr/bin --disable-rpath --disable-device-mapper	
	}
	build(){
		make 
	}
	package(){
		make install DESTDIR=$DESTDIR
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.


**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.

.. raw:: pdf

   PageBreak





.. _busybox:
busybox
+++++++

BusyBox, Linux tabanlı sistemlerde "İsviçre Çakısı" benzeri bir işlevsellik sunarak, çeşitli komutları tek bir ikili dosya altında toplar. 

BusyBox, ls, cp, mv, rm gibi temel komutların yanı sıra, ağ yönetimi, dosya sistemleri ve sistem yönetimi gibi birçok alanda işlevsellik sunar. Kullanıcılar, bu komutları BusyBox ile çağırarak bir dosyayı kopyalamak için aşağıdaki komut kullanılabilir:

.. code-block:: shell
	
	busybox cp kaynak_dosya hedef_dosya

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	version="1.36.1"
	name="busybox"
	depends="glibc"
	description="linux araç paketi static derlenmiş hali"
	source="https://busybox.net/downloads/${name}-${version}.tar.bz2"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		cd $ROOTBUILDDIR #dizinine geçiyoruz
		wget ${source}
		for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		dowloadfile=$(ls|head -1)
		filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		director=$(find ./* -maxdepth 0 -type d)
		directorname=$(basename ${director})
		if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup(){
		cp -prfv $PACKAGEDIR/files $SOURCEDIR/
		make defconfig
		sed -i "s|.*CONFIG_STATIC_LIBGCC .*|CONFIG_STATIC_LIBGCC=y|" .config
		sed -i "s|.*CONFIG_STATIC .*|CONFIG_STATIC=y|" .config
	}
	build(){ 
		make 
	}
	package(){
		mkdir -p $DESTDIR/bin
		install busybox ${DESTDIR}/bin/busybox
		mkdir -p ${DESTDIR}/usr/share/udhcpc/ ${DESTDIR}/etc/init.d/
		# install udhcpc script and service	
		install $SOURCEDIR/files/udhcpc.script ${DESTDIR}/usr/share/udhcpc/default.script
		install $SOURCEDIR/files/udhcpc.openrc ${DESTDIR}/etc/init.d/udhcpc
		cd $DESTDIR/bin&&ln -s busybox hostname
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

Ek dosyaları indirmek için `tıklayınız. <https://kendilinuxunuyap.github.io/_static/files/busybox/files.tar>`_ **Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak





.. _nano:
nano
++++

Nano, terminal tabanlı bir metin düzenleyici olup, GNU projesinin bir parçasıdır. Kullanıcıların metin dosyalarını kolayca oluşturmasına, düzenlemesine ve kaydetmesine olanak tanır. Nano, vi veya emacs gibi daha karmaşık metin düzenleyicilere göre daha basit bir kullanım sunar.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	version="7.2"
	name="nano"
	depends="glibc,readline,ncurses,file"
	description="şıkıştırma kütüphanesi"
	source="https://www.nano-editor.org/dist/v7/${name}-${version}.tar.xz"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
		    wget ${source}
		    for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup(){
		./configure --prefix=/usr
	}
	build(){
		make 
	}
	package(){
		make install DESTDIR=$DESTDIR
		cd $DESTDIR
		mkdir -p $DESTDIR/lib
		echo "INPUT(-lncursesw)" > $DESTDIR/lib/libncurses.so
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.


**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak





.. _grub:
grub
++++

GRUB (GRand Unified Bootloader), çoklu işletim sistemlerini destekleyen ve kullanıcıların sistemlerini başlatmalarını sağlayan bir önyükleyici yazılımıdır. GRUB yapılandırma dosyası genellikle /boot/grub/grub.cfg konumunda bulunur.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="grub"
	version="2.12"
	description="GNU GRand Unified Bootloader"
	source="https://ftp.gnu.org/gnu/grub/grub-$version.tar.xz"
	depends="glibc,readline,ncurses,xz-utils,efibootmgr"
	builddepend="rsync,freetype,ttf-dejavu"
	group="sys.boot"
	uses=(efi bios)
	uses_extra=(ia32)
	dontstrip=1
	efi_dp=(efibootmgr)
	ia32_dp=(efibootmgr)
	unset CFLAGS
	unset CXXFLAGS
	get_grub_opt(){ echo -n "--disable-efiemu "
		if [[ "$1" == "efi" ]] ; then echo -n "--with-platform=efi --target=x86_64"
		elif [[ "$1" == "ia32" ]] ; then echo -n "--with-platform=efi --target=i386"
		elif [[ "$1" == "bios" ]] ; then echo -n "--with-platform=pc"
		fi
		}
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı
	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		        mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		        rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		        cd $ROOTBUILDDIR #dizinine geçiyoruz
		        wget ${source}
		        for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		        dowloadfile=$(ls|head -1)
		        filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		        if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		        director=$(find ./* -maxdepth 0 -type d)
		        directorname=$(basename ${director})
		        if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		        mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup(){	cd $ROOTBUILDDIR
	 echo depends bli part_gpt > $SOURCEDIR/grub-core/extra_deps.lst
		for tgt in ${uses[@]} ; do cp -prfv $name-$version $tgt; done
		for tgt in ${uses[@]} ; do
		    cd $tgt
		    autoreconf -fvi
		    ./configure --prefix=/usr --sysconfdir=/etc --libdir=/usr/lib64/ --disable-nls --disable-werror \
		    --disable-grub-themes $(get_grub_opt $tgt)
		    cd ..
		done
	}
	build(){ for tgt in ${uses[@]} ; do make -C $tgt; done	}
	package(){
		for tgt in ${uses[@]} ; do make $jobs -C $tgt install DESTDIR=$DESTDIR; done
		mkdir -p $DESTDIR/etc/default $DESTDIR/usr/bin/
		install $PACKAGEDIR/files/grub $DESTDIR/etc/default/grub
		install -vDm 755  $PACKAGEDIR/files/update-grub $DESTDIR/usr/bin/update-grub
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

Ek dosyaları indirmek için `tıklayınız. <https://kendilinuxunuyap.github.io/_static/files/grub/files.tar>`_ **Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak




.. _efibootmgr:
efibootmgr
++++++++++

efibootmgr, UEFI (Unified Extensible Firmware Interface) tabanlı sistemlerde önyükleme yöneticisi olarak işlev gören bir Linux aracıdır. Bu paket, UEFI önyükleme seçeneklerini yönetmek için kullanılır ve sistemin önyükleme sırasını, önyükleme girişlerini ve diğer ilgili ayarları düzenlemeye olanak tanır.

Derleme
--------

Debian ortamında bu paketin derlenmesi için;

- **sudo apt install libefiboot-dev** 
- **sudo cp -prfv /usr/include/efivar/* /usr/include/**

komutuyla paketin kurulması gerekmektedir.

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="efibootmgr"
	version="16"
	description="Linux user-space application to modify the Intel Extensible Firmware Interface (EFI) Boot Manager."
	source="https://github.com/rhboot/efibootmgr/archive/refs/tags/$version.tar.gz"
	depends="efivar,popt"
	builddepend=""
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup(){
		echo ""
	}
	build(){
	    make sbindir=/usr/bin EFIDIR=/boot/efi PCDIR=/usr/lib64/pkgconfig
	}
	package(){
		EFIDIR="/boot/efi" sbindir=/usr/bin make DESTDIR="$DESTDIR" install
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}

	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.

.. raw:: pdf

   PageBreak




.. _efivar:
efivar
++++++

efivar paketi, UEFI tabanlı sistemlerde, firmware ile işletim sistemi arasında veri alışverişini sağlamak için kritik bir rol oynamaktadır. UEFI, BIOS'un yerini alarak daha modern bir arayüz sunmakta ve sistem başlangıcında daha fazla esneklik sağlamaktadır. efivar, UEFI değişkenlerini okuma, yazma ve silme işlemlerini gerçekleştirmek için bir dizi komut sunar.

Derleme
--------

Debian ortamında bu paketin derlenmesi için; **sudo apt install libefivar-dev** komutuyla paketin kurulması gerekmektedir.

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="efivar"
	version="39"
	description="Tools and libraries to work with EFI variables"
	source="https://github.com/rhboot/efivar/archive/refs/tags/$version.tar.gz"
	depends=""
	builddepend=""
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup(){
		export ERRORS=''
		export PATH=$PATH:$HOME
	    echo "exit 0" > $HOME/mandoc		# fake mandoc for ignore extra dependency
	    chmod +x $HOME/mandoc
	}
	build(){
	    make
	}
	package(){
		local make_options=(V=1 libdir=/usr/lib64/ bindir=/usr/bin/ mandir=/usr/share/man/ includedir=/usr/include/)
	    make DESTDIR=$DESTDIR "${make_options[@]}" install
	    ${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak





.. _libssh:
libssh
++++++

libssh, SSH protokolünü uygulamak için kullanılan açık kaynaklı bir C kütüphanesidir. Bu kütüphane, geliştiricilere güvenli bir şekilde veri iletimi, uzaktan erişim ve dosya transferi gibi işlevleri gerçekleştirme imkanı tanır. libssh, hem istemci hem de sunucu tarafında kullanılabilir ve çoklu platform desteği sunar.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="libssh"
	version="0.10.4"
	description="C library implenting the SSHv2 protocol on client and server side"
	source=("https://www.libssh.org/files/0.10/libssh-${version}.tar.xz")
	depends="openssl,zlib"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup() {
	    cmake -S $SOURCEDIR -B $BUILDDIR -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_INSTALL_LIBDIR=/usr/lib64 \
		-DWITH_EXAMPLES=NO -DBUILD_SHARED_LIBS=YES -DBUILD_STATIC_LIB=YES -DWITH_NACL=OFF \
		-DWITH_GCRYPT=OFF -DWITH_MBEDTLS=OFF -DWITH_GSSAPI=OFF \
		-DWITH_PCAP=OFF -DWITH_SERVER=ON -DWITH_SFTP=ON -DWITH_ZLIB=ON
	}
	build() {
	    make -C $BUILDDIR
	}
	package() {
	    make -C $BUILDDIR install DESTDIR=$DESTDIR
	    install $BUILDDIR/src/libssh.a ${DESTDIR}/usr/lib64/
	    ${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.
  
.. raw:: pdf

   PageBreak




.. _openssh:
openssh
+++++++

OpenSSH, Secure Shell (SSH) protokolünü uygulayan bir yazılım paketidir ve genellikle Linux ve Unix tabanlı sistemlerde kullanılır. Bu paket, kullanıcıların uzak sunuculara güvenli bir şekilde bağlanmalarını, dosya transferi yapmalarını ve uzaktan komut çalıştırmalarını sağlar. OpenSSH, veri iletimini şifreleyerek, ağ üzerinden yapılan iletişimlerin güvenliğini artırır.

OpenSSH, genellikle ssh, scp, sftp ve sshd gibi araçları içerir. 

Debian ortamında bu paketin derlenmesi için; **sudo apt install libssh2-1-dev libcrypt-dev** komutuyla paketlerin kurulması gerekmektedir.

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="openssh"
	version="9.6p1"
	description="OpenBSD ssh server & client"
	source="https://ftp.openbsd.org/pub/OpenBSD/OpenSSH/portable/openssh-$version.tar.gz"
	depends="zlib,libxcrypt,openssl,libmd,libssh"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		cd $ROOTBUILDDIR #dizinine geçiyoruz
		wget ${source}
		for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		dowloadfile=$(ls|head -1)
		filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		director=$(find ./* -maxdepth 0 -type d)
		directorname=$(basename ${director})
		if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup(){
		cp -prfv $PACKAGEDIR/files $SOURCEDIR/
		./configure --prefix=/usr --libdir=/usr/lib64/ --sysconfdir=/etc/ssh --without-pam --disable-strip \
		    --with-ssl-engine --with-privsep-user=nobody --with-pid-dir=/run  \
		    --with-default-path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
	}
	build(){
		make
	}
	package(){
		make install DESTDIR=$DESTDIR
		mkdir -p "$DESTDIR"/etc/{passwd,group,sysconf,init,conf}.d
		install -m755 -D $SOURCEDIR/files/sshd.initd "$DESTDIR"/etc/init.d/sshd
		install $SOURCEDIR/files/sshd.initd  ${DESTDIR}/etc/runlevels/default/sshd
		install -m755 -D $SOURCEDIR/files/sshd.confd "$DESTDIR"/etc/conf.d/sshd
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
		sed -i "/nobody/d"  ${DESTDIR}/etc/group
		sed -i "/nobody/d"  ${DESTDIR}/etc/passwd
		mkdir -p  ${DESTDIR}/var/empty
		chown root:root  ${DESTDIR}/var/empty
		chmod 755  ${DESTDIR}/var/empty
		echo "nobody:!:65534:" >>  ${DESTDIR}/etc/group
		echo "nobody:!:65534:65534::/var/empty:/usr/sbin/nologin" >>  ${DESTDIR}/etc/passwd
		sed -i "/PermitRootLogin/d" /etc/ssh/sshd_config
		echo -e "\nPermitRootLogin yes">> /etc/ssh/sshd_config
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

Ek dosyaları indirmek için `tıklayınız. <https://kendilinuxunuyap.github.io/_static/files/openssh/files.tar>`_  **Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.

.. raw:: pdf

   PageBreak




.. _pam:
pam
+++

PAM, "Pluggable Authentication Modules" ifadesinin kısaltmasıdır ve Linux işletim sistemlerinde kimlik doğrulama süreçlerini esnek bir şekilde yönetmek için tasarlanmıştır. PAM, sistem yöneticilerine, kimlik doğrulama yöntemlerini modüler bir yapıda değiştirme ve özelleştirme imkanı sunar. Örneğin, bir sistem yöneticisi, kullanıcıların şifre ile kimlik doğrulamasını sağlarken, aynı zamanda iki faktörlü kimlik doğrulama gibi ek güvenlik önlemleri de ekleyebilir.

Derleme
--------

.. code-block:: bash
	
	#--------------------------------------------------------------------------------------------------------------------
	#!/usr/bin/env bash
	name="pam"
	version="1.6.0"
	depends="libtirpc,libxcrypt,libnsl,audit"
	description="PAM (Pluggable Authentication Modules) library'"
	source="https://github.com/linux-pam/linux-pam/releases/download/v$version/Linux-PAM-$version.tar.xz"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -1)"  # Display adı
	user=$(who | grep "(${display})" | awk '{print $1}')                      # Display kullanıcısı

	ROOT="/home/$user/distro"
	ROOTBUILDDIR="$ROOT/build"                # Derleme dizini
	BUILDDIR="$ROOT/build/build-${name}-${version}" # Alt dizin
	DESTDIR="$ROOT/rootfs"                     # Yükleme dizini
	PACKAGEDIR=$(pwd)                          # Paket dizini
	SOURCEDIR="$ROOT/build/${name}-${version}" # Kaynak dizini

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup(){
	    ./configure --prefix=/usr --sbindir=/usr/sbin --libdir=/usr/lib64 \
		--enable-securedir=/usr/lib64/security --enable-static --enable-shared --disable-nls --disable-selinux
		}
	build(){
		make
	}
	package(){
		make install DESTDIR=$DESTDIR
		chmod +s "$DESTDIR"/usr/sbin/unix_chkpwd
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}

	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.


**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.

.. raw:: pdf

   PageBreak




.. _paketderleme:
**GNU Araçlarıyla Kendi Linux Dağıtımını Hazırlamak**
=====================================================

kernel-headers
++++++++++++++

Kernel-headers paketi, Linux çekirdeği başlık dosyalarını barındırır. Kernel-headers paketi derleme yaparsanız lazım olacaktır.

Derleme
--------

.. code-block:: shell
	
	#!/usr/bin/env bash
	name="kernel-headers"
	version="6.9.9"
	description="Linux kernel"
	source="https://cdn.kernel.org/pub/linux/kernel/v6.x/linux-$version.tar.xz"
	depends="kernel"
	builddepend="rsync,bc,cpio,gettext,elfutils,pahole,perl,python,tar,xz-utils"
	group="sys.kernel"
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -n 1)"	#Detect the name of the display in use
	user=$(who | grep '('$display')' | awk '{print $1}')	#Detect the user using such display
	ROOTBUILDDIR="/home/$user/distro/build" # Derleme konumu
	BUILDDIR="/home/$user/distro/build/build-${name}-${version}" #Derleme yapılan paketin derleme konumun
	DESTDIR="/home/$user/distro/rootfs" #Paketin yükleneceği sistem konumu
	PACKAGEDIR=$(pwd) #paketin derleme talimatının verildiği konum
	SOURCEDIR="/home/$user/distro/build/${name}-${version}" #Paketin kaynak kodlarının olduğu konum
	initsetup(){
		mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		cd $ROOTBUILDDIR #dizinine geçiyoruz
		wget ${source}
		for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		dowloadfile=$(ls|head -1)
		filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		director=$(find ./* -maxdepth 0 -type d)
		directorname=$(basename ${director})
		if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	setup(){
		cp -prvf $PACKAGEDIR/files/ $SOURCEDIR/
		patch -Np1 -i $PACKAGEDIR/files/patch-$version
		cp $PACKAGEDIR/files/config $SOURCEDIR/.config
		make olddefconfig
	}
	build(){
		make bzImage -j$(nproc)
		make modules -j$(nproc)
	}
	package(){
		arch="x86"
		kernelbuilddir="${DESTDIR}/lib/modules/${version}/build"
		# install bzImage
		mkdir -p "$DESTDIR/boot"
		install -Dm644 "$(make -s image_name)" "$DESTDIR/boot/vmlinuz-${version}"
		#make INSTALL_PATH=$DESTDIR install ARCH=amd64
		# install modules
		mkdir -p ${DESTDIR}/lib/modules/${version}
		mkdir -p $DESTDIR/usr/src
		mkdir -p ${DESTDIR}/lib/modules/${version}/build
		make INSTALL_MOD_PATH=$DESTDIR modules_install INSTALL_MOD_STRIP=1 -j$(nproc)
		rm "${DESTDIR}/lib/modules/${version}"/{source,build} || true
		depmod --all --verbose --basedir="$DESTDIR" "${version}" || true
		# install build directories
		install .config "$DESTDIR/boot/config-${version}"
		install -Dt "$kernelbuilddir/kernel" -m644 kernel/Makefile
		install -Dt "$kernelbuilddir/arch/$arch" -m644 arch/$arch/Makefile
		cp -t "$kernelbuilddir" -a scripts
		install -Dt "$kernelbuilddir/tools/objtool" tools/objtool/objtool
		mkdir -p "$kernelbuilddir"/{fs/xfs,mm}
		ln -s "../../lib/modules/${version}/build" "$DESTDIR/usr/src/linux-headers-${version}"
		install -Dt "$kernelbuilddir" -m644 Makefile Module.symvers System.map vmlinux
		# install libc headers
		mkdir -p "$DESTDIR/usr/include/linux"
		cp -v -t "$DESTDIR/usr/include/" -a include/linux/
		cp -v -t "$DESTDIR/usr/" -a tools/include	
		make headers_install INSTALL_HDR_PATH=$DESTDIR/usr
		mkdir -p "$kernelbuilddir" "$kernelbuilddir/arch/$arch"
		cp -v -t "$kernelbuilddir" -a include
	   	cp -v -t "$kernelbuilddir/arch/$arch" -a arch/$arch/include
		install -Dt "$kernelbuilddir/arch/$arch/kernel" -m644 arch/$arch/kernel/asm-offsets.*
		install -Dt "$kernelbuilddir/drivers/md" -m644 drivers/md/*.h
		install -Dt "$kernelbuilddir/net/mac80211" -m644 net/mac80211/*.h
		install -Dt "$kernelbuilddir/drivers/media/i2c" -m644 drivers/media/i2c/msp3400-driver.h
		install -Dt "$kernelbuilddir/drivers/media/usb/dvb-usb" -m644 drivers/media/usb/dvb-usb/*.h
		install -Dt "$kernelbuilddir/drivers/media/dvb-frontends" -m644 drivers/media/dvb-frontends/*.h
		install -Dt "$kernelbuilddir/drivers/media/tuners" -m644 drivers/media/tuners/*.h
		install -Dt "$kernelbuilddir/drivers/iio/common/hid-sensors" -m644 drivers/iio/common/hid-sensors/*.h 		# https://bugs.archlinux.org/task/71392
		find . -name 'Kconfig*' -exec install -Dm644 {} "$kernelbuilddir/{}" \;
		find -L "$kernelbuilddir" -type l -printf 'Removing %P\n' -delete					# clearing
		find "$kernelbuilddir" -type f -name '*.o' -printf 'Removing %P\n' -delete
		#-------------------------------------- 					install 										------------------------------------
		if [[ -d "$kernelbuilddir" ]] ; then
	    while read -rd '' file; do
		case "$(file -Sib "$file")" in
		    application/x-sharedlib\;*)      # Libraries (.so)
		        strip "$file" ;;
		    application/x-executable\;*)     # Binaries
		        strip "$file" ;;
		    application/x-pie-executable\;*) # Relocatable binaries
		        strip "$file" ;;
		esac
	    done < <(find "$kernelbuilddir" -type f -perm -u+x ! -name vmlinux -print0)
		fi
		if [[ -f "$kernelbuilddir/vmlinux" ]] ; then
	    strip "$kernelbuilddir/vmlinux"
		fi
		mkdir -p "$DESTDIR/usr/src"
		ln -sr "$kernelbuilddir" "$DESTDIR/usr/src/linux"
	    mv -vf System.map $DESTDIR/boot/System.map-$version
	    find ${DESTDIR}/ -iname "*" -exec unxz {} \;
	    depmod -b "$DESTDIR" -F $DESTDIR/boot/System.map-$version $version
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.

**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.

.. raw:: pdf

   PageBreak




lz4
+++

LZ4, yüksek hızda veri sıkıştırma ve açma işlemleri gerçekleştiren bir algoritmadır. Genellikle, büyük veri setlerini hızlı bir şekilde sıkıştırmak ve açmak için kullanılır. LZ4, özellikle performansın kritik olduğu durumlarda tercih edilir. Örneğin, oyun verileri, veri tabanları ve ağ iletişimi gibi alanlarda sıkça kullanılır.

Derleme
--------

Debian ortamında bu paketin derlenmesi için;

- **sudo apt install liblz4-dev** 

komutuyla paketin kurulması gerekmektedir.

.. code-block:: shell
		
	#!/usr/bin/env bash
	name="lz4"
	version="1.9.4"
	description="Extremely fast compression algorithm"
	source="https://github.com/lz4/lz4/archive/refs/tags/v1.9.4.tar.gz"
	depends=""
	builddepend=""
	group="app.arch"


	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -n 1)"      #Detect the name of the display in use
	user=$(who | grep '('$display')' | awk '{print $1}')    #Detect the user using such display
	ROOTBUILDDIR="/home/$user/distro/build" # Derleme konumu
	BUILDDIR="/home/$user/distro/build/build-${name}-${version}" #Derleme yapılan paketin derleme konumun
	DESTDIR="/home/$user/distro/rootfs" #Paketin yükleneceği sistem konumu
	PACKAGEDIR=$(pwd) #paketin derleme talimatının verildiği konum
	SOURCEDIR="/home/$user/distro/build/${name}-${version}" #Paketin kaynak kodlarının olduğu konum

	initsetup(){
		        mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		        rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		        cd $ROOTBUILDDIR #dizinine geçiyoruz
		wget ${source}
		for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		        dowloadfile=$(ls|head -1)
		        filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		        if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		        director=$(find ./* -maxdepth 0 -type d)
		        directorname=$(basename ${director})
		        if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		        mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup(){
		echo ""
	}

	build(){
		cd $SOURCEDIR
		make PREFIX=/usr
	}

	package(){
		make install DESTDIR=$DESTDIR PREFIX=/usr
		mv ${DESTDIR}/usr/{lib,lib64}
	}

	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.
	
**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.

.. raw:: pdf

   PageBreak




lzo
+++

LZO (Lempel-Ziv-Oberhumer), hızlı veri sıkıştırma ve açma işlemleri için tasarlanmış bir algoritmadır. Özellikle, yüksek hızda sıkıştırma ve açma işlemleri gerektiren uygulamalarda tercih edilir. LZO, kayıpsız bir sıkıştırma yöntemi sunar; yani, sıkıştırılmış veriyi açtığınızda orijinal veriyi tam olarak geri alırsınız.

Derleme
--------

Debian ortamında bu paketin derlenmesi için;

- **sudo apt install liblz4-dev** 

komutuyla paketin kurulması gerekmektedir.

.. code-block:: shell
		
	#!/usr/bin/env bash
	version="2.10"
	name="lzo"
	depends=""
	description="squashfs lzo"
	source="https://www.oberhumer.com/opensource/lzo/download/lzo-2.10.tar.gz"
	groups="app.shell"

	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -n 1)"      #Detect the name of the display in use
	user=$(who | grep '('$display')' | awk '{print $1}')    #Detect the user using such display
	ROOTBUILDDIR="/home/$user/distro/build" # Derleme konumu
	BUILDDIR="/home/$user/distro/build/build-${name}-${version}" #Derleme yapılan paketin derleme konumun
	DESTDIR="/home/$user/distro/rootfs" #Paketin yükleneceği sistem konumu
	PACKAGEDIR=$(pwd) #paketin derleme talimatının verildiği konum
	SOURCEDIR="/home/$user/distro/build/${name}-${version}" #Paketin kaynak kodlarının olduğu konum

	initsetup(){
		        mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		        rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		        cd $ROOTBUILDDIR #dizinine geçiyoruz
		wget ${source}
		for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		        dowloadfile=$(ls|head -1)
		        filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		        if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		        director=$(find ./* -maxdepth 0 -type d)
		        directorname=$(basename ${director})
		        if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		        mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup()
	{
		cd $SOURCEDIR
	  ./configure --prefix=/usr --enable-shared
	 
		
	}
	build()
	{
		make
	  # build minilzo
	  gcc $CPPFLAGS $CFLAGS -fpic -Iinclude/lzo -o minilzo/minilzo.o -c minilzo/minilzo.c
	  gcc $LDFLAGS -shared -o libminilzo.so.0 -Wl,-soname,libminilzo.so.0 minilzo/minilzo.o
	}
	package()
	{

	  make DESTDIR="${DESTDIR}" install

	  # install minilzo
	  install -m 755 libminilzo.so.0 "${DESTDIR}"/usr/lib
	  install -p -m 644 minilzo/minilzo.h ${DESTDIR}/usr/include/lzo
	  cd "${DESTDIR}"/usr/lib
	  ln -s libminilzo.so.0 libminilzo.so

	}


	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.
	
**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.

.. raw:: pdf

   PageBreak




squashfs-tools
++++++++++++++

squashfs-tools, Linux tabanlı sistemlerde sıkıştırılmış dosya sistemleri oluşturmak ve yönetmek için kullanılan bir araç setidir. SquashFS, özellikle depolama alanını verimli bir şekilde kullanmak amacıyla dosyaları sıkıştırarak depolayan bir dosya sistemidir. Bu paket, mksquashfs ve unsquashfs gibi komutları içerir. 

Derleme
--------

Debian ortamında bu paketin derlenmesi için;

- **sudo apt install liblz4-dev** 

komutuyla paketin kurulması gerekmektedir.

.. code-block:: shell
		
	#!/usr/bin/env bash
	version="4.6.1"
	name="squashfs-tools"
	depends="squashfs"
	description="squashfs"
	source="https://github.com/plougher/squashfs-tools/archive/refs/tags/4.6.1.tar.gz"
	groups="app.shell"

	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -n 1)"      #Detect the name of the display in use
	user=$(who | grep '('$display')' | awk '{print $1}')    #Detect the user using such display
	ROOTBUILDDIR="/home/$user/distro/build" # Derleme konumu
	BUILDDIR="/home/$user/distro/build/build-${name}-${version}" #Derleme yapılan paketin derleme konumun
	DESTDIR="/home/$user/distro/rootfs" #Paketin yükleneceği sistem konumu
	PACKAGEDIR=$(pwd) #paketin derleme talimatının verildiği konum
	SOURCEDIR="/home/$user/distro/build/${name}-${version}" #Paketin kaynak kodlarının olduğu konum

	initsetup(){
		mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		cd $ROOTBUILDDIR #dizinine geçiyoruz
		wget ${source}
		for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		dowloadfile=$(ls|head -1)
		filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		director=$(find ./* -maxdepth 0 -type d)
		directorname=$(basename ${director})
		if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}

	setup(){
		cd $SOURCEDIR/squashfs-tools
	}

	build(){
		make GZIP_SUPPORT=1 LZ4_SUPPORT=1 LZMA_XZ_SUPPORT=1 LZO_SUPPORT=1 XATTR_SUPPORT=1 XZ_SUPPORT=1 ZSTD_SUPPORT=1
	}
	package(){
	  	make INSTALL_PREFIX="$DESTDIR/usr" INSTALL_MANPAGES_DIR='$(INSTALL_PREFIX)/share/man/man1' install
	  	install -vDm 644 $SOURCEDIR/{ACTIONS-README,CHANGES,"README-$version",USAGE*} -t "$DESTDIR/usr/share/doc/$name/"
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.
	
**Paket Derleme Yöntemi** konusunda anlatıldığı gibi derleme işlemini yapınız.

.. raw:: pdf

   PageBreak




.. _paketsistemi:

**Paket Sitemi**
++++++++++++++++

Paket sistemi dağıtımların paketleri yükleme, kaldırma, güncelleme gibi temel işlemlerin yapılmasını sağlayan en önemli bileşenidir. 

Paket sistemeleri bir paketi yüklemek istediğinde, genellikle daha önceden derlenmiş paketleri veya yükeleme aşamasında derleyebilir. Önceden derlenmiş olan yapıya(binary==ikili), yükleme aşamasında derleme işleminede (source==kaynak) paket sistemi denir. 

Gnu/Linux deneyimi az olan kullanıcılar için  daha önceden hazırlanmış ikili paketler tercih edilmektedir.


Dağıtımlarda uygulamalar paketler halinde hazırlanır. Bu paketleri dağıtımda kullanabilmek için temel işlemler şunlardır;

1. Paket Oluşturma
2. Paket Liste İndexi Güncelleme
3. Paket Kurma
4. Paket Kaldırma
5. Paket Yükseltme gibi işlemleri yapan uygulamaların tamamı paket sistemi olarak adlandırılır.

Paket sisteminde, uygulama paketi haline getirilip sisteme kurulur. Genelde paket sistemi dağıtımın temel bir parçası olması sebebiyle üzerinde yüklü gelir.

Bazı dağıtımların kullandığı paket sistemeleri şunlardır.

- apt: Debian dağıtımının kullandığı paket sistemi.
- emerge :Gentoo dağıtımının kullandığı paket sistemi.

**kly Paket Sistemi**
---------------------

Bu dokümanda hazırlanan dağıtımın paket sistemi için ise **kly(KendiLinuxunuYap)** olarak ifade edeceğimiz paket sistemi adını kullandık. kly paket sistemindeki beş temel işlemin nasıl yapılacağı ayrı başlıklar altında anlatılacaktır. Paket sistemi derlemeli bir dil yerine bash script ile yapılacaktır. Bu dokumanı takip eden kişi, bu dokümanda yazılanları anlaması için orta seviye bash script bilmesi gerekmektedir.


.. raw:: pdf

   PageBreak


Paket Oluşturma
+++++++++++++++

Paket sisteminde en önemli kısımlardan birisi paket oluşturmadır. Bu işlem paketin derlenmesi ve derlenmiş paketin belirli bir yapıyla saklanması olayıdır. Bu saklanan paket daha sonra ihtiyaç halinde uzaktan(internet üzerinden) ve yerelden istediğimiz sisteme kurma işlemidir. Bu başlıkta paketin derlenmesi ve saklanması(paket oluşturma) anlatılacaktır.

Paket oluşturma işlemi sırayla şu aşamalardan oluşmaktadır.

1. Paketin indirilmesi
2. Paketin derleme öncesi hazırlanması(configure)
3. Paketin derlenmesi
4. Derlenmiş paketin bir dizine yüklenmesi
5. Yüklenen dizindeki dosya ve dizin yapısının konum listesini tutan file.index oluşturulması
6. Derlenmiş paketin bir dizinin sıkıştırılması
7. Sıkıştırılmış derlenmiş dizin, file.index ve derleme talimatının paket isim ve versiyonuyla tekrardan sıkıştırılması

Burada maddeler halinde anlatılan işlem adımlarını bir paket oluşturma amacıyla sırasıyla yapmamız gerekmektedir. 7. maddede anlatılan son sıkıştırılma öncesi yapı aşağıda gösterilmiştir.

.. image:: /_static/images/klypaketle-0.png
  	:width: 600


.. raw:: pdf

   PageBreak
   

**kly Paket Oluşturma**
-----------------------

kly paket sisteminin temel parçalarından en önemlisi paket oluşturma uygulamasıdır. Dokümanda temel paketlerin nasıl derlendiği **Paket Derleme** başlığı altında anlatılmıştı. Bir paket üzerinden(readline) örneklendirerek paketimizi oluşturacak scriptimizi yazalım.

Dokümanda readline paketi nasıl derleneceği aşağıdaki script olarak verilmiştir.

.. code-block:: shell

	#!/usr/bin/env bash
	version="8.2"
	name="readline"
	depends="glibc"
	description="readline kütüphanesi"
	source="https://ftp.gnu.org/pub/gnu/readline/${name}-${version}.tar.gz"
	groups="sys.apps"
	
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -n 1)"	#Detect the name of the display in use
	user=$(who | grep '('$display')' | awk '{print $1}')	#Detect the user using such display
	ROOTBUILDDIR="/home/$user/distro/build" # Derleme konumu
	BUILDDIR="/home/$user/distro/build/build-${name}-${version}" #Derleme yapılan paketin derleme konumun
	DESTDIR="/home/$user/distro/rootfs" #Paketin yükleneceği sistem konumu
	PACKAGEDIR=$(pwd) #paketin derleme talimatının verildiği konum
	SOURCEDIR="/home/$user/distro/build/${name}-${version}" #Paketin kaynak kodlarının olduğu konum

	initsetup(){
		    mkdir -p  $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		    rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		    cd $ROOTBUILDDIR #dizinine geçiyoruz
            wget ${source}
            for f in *\ *; do mv "$f" "${f// /}"; done #isimde boşluk varsa silme işlemi yapılıyor
		    dowloadfile=$(ls|head -1)
		    filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		    if [ "${filetype}" == "???" ]; then unzip  ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		    director=$(find ./* -maxdepth 0 -type d)
		    directorname=$(basename ${director})
		    if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		    mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $SOURCEDIR
	}
	
	setup(){
		cp -prvf $PACKAGEDIR/files $SOURCEDIR/
		./configure --prefix=/usr \
			--libdir=/usr/lib64
	}

	build(){
		make SHLIB_LIBS="-L/tools/lib -lncursesw"
	}

	package(){
		make SHLIB_LIBS="-L/tools/lib -lncursesw" DESTDIR="$DESTDIR" install pkgconfigdir="/usr/lib64/pkgconfig"
		
		install -Dm644 $SOURCEDIR/files/inputrc "$DESTDIR"/etc/inputrc
		${DESTDIR}/sbin/ldconfig -r ${DESTDIR}           # sistem guncelleniyor
	}
	initsetup       # initsetup fonksiyonunu çalıştırır ve kaynak dosyayı indirir
	setup           # setup fonksiyonu çalışır ve derleme öncesi kaynak dosyaların ayalanması sağlanır.
	build           # build fonksiyonu çalışır ve kaynak dosyaları derlenir.
	package         # package fonksiyonu çalışır, yükleme öncesi ayarlamalar yapılır ve yüklenir.


Bu script readline kodunu internetten indirip derliyor ve kurulumu yapıyor. Aslında bu scriptle **paketleme**, **paket kurma** işlemini bir arada yapıyor. Bu işlem mantıklı gibi olsada paket sayısı arttıkça ve rutin yapılan işlemleri tekrar tekrar yapmak gibi işlem fazlalığına sebep olmaktadır.

Bu sebeplerden dolayı **readline** paketleme scriptini yeniden düzenleyelim. Yeni düzenlenen halini  **klypaketle** ve **klybuild** adlı script dosyaları olarak düzenleyeceğiz. Genel yapısı aşağıdaki gibi olacaktır. Devamında ise **packageindex** ve **packagecompress** fonksiyonları klypaketle dosyasına eklenecektir.

**klybuild** Dosyası
--------------------

.. code-block:: shell
	
	setup()	{}
	build()	{}
	package() {}

**klypaketle** Dosyası
----------------------

.. code-block:: shell
	
	#genel değişkenler tanımlanır
	initsetup() {}
	
	#klybuild dosya fonksiyonları birleştiriliyor
	source klybuild # bu komutla setup build package fonsiyonları klybuild doyasından alınıp birleştiriliyor
	
	packageindex() {}
	packagecompress() {}

Aslında yukarıdaki **klypaketle** ve **klybuild** adlı script dosyaları tek bir script dosyası olarak **klypaketle** dosyası. İki dosyayı birleştiren **source klybuild** komutudur. **klypaketle** dosyası aşağıdaki gibi düşünebiliriz.

.. code-block:: shell
	
	#genel değişkenler tanımlanır
	initsetup() {}
	
	setup()	{} #klybuild dosyasından gelen fonksiyon, "source klybuild" komutu sonucu gelen fonksiyon
	build()	{} #klybuild dosyasından gelen fonksiyon, "source klybuild" komutu sonucu gelen fonksiyon
	package() {} #klybuild dosyasından gelen fonksiyon, "source klybuild" komutu sonucu gelen fonksiyon
	
	packageindex() {}
	packagecompress() {}

Bu şekilde ayrılmasının temel sebebi  **klypaketle** scriptinde hep aynı işlemler yapılırken **klybuild** scriptindekiler her pakete göre değişmektedir. Böylece paket yapmak için ilgili pakete özel **klybuild** dosyası düzenlememiz yeterli olacaktır. **klypaketle** dosyamızda **klybuild** scriptini kendisiyle birleştirip paketleme yapacaktır.

**klybuild** Dosyamızın Son Hali
----------------------------------

.. code-block:: shell

	#!/usr/bin/env bash
	version="8.2"
	name="readline"
	depends="glibc"
	description="readline kütüphanesi"
	source="https://ftp.gnu.org/pub/gnu/readline/${name}-${version}.tar.gz"
	groups="sys.apps"
	#2. madde, derleme öncesi hazırlık 
	setup(){
		cp -prvf $PACKAGEDIR/files $BUILDDIR/
		$SOURCEDIR/configure --prefix=/usr \
			--libdir=/usr/lib64
	}
	#3. madde, paketin derlenmesi 	
	build(){
		make SHLIB_LIBS="-L/tools/lib -lncursesw"
	}
	#4. madde, derlenen paketin bir dizine yüklenmesi 
	package(){
		make SHLIB_LIBS="-L/tools/lib -lncursesw" DESTDIR="$DESTDIR" install pkgconfigdir="/usr/lib64/pkgconfig"
		
		install -Dm644 files/inputrc "$DESTDIR"/etc/inputrc
	}



**klypaketle** Dosyamızın Son Hali
----------------------------------

.. code-block:: shell
	
	#!/usr/bin/env bash
	set -e
	paket=$1
	dizin=$(pwd)
	echo "Paket : $paket"
	source ${paket}/klybuild
	ROOTBUILDDIR="/tmp/kly/build"
	BUILDDIR="/tmp/kly/build/build-${name}-${version}" #Derleme yapılan dizin
	DESTDIR="/tmp/kly/build/rootfs-${name}-${version}" #Paketin yükleneceği sistem konumu
	PACKAGEDIR="$dizin/$paket"
	SOURCEDIR="/tmp/kly/build/${name}-${version}"
	# 1. madde, paketin indirilmesi
	initsetup(){
		mkdir -p $ROOTBUILDDIR #derleme dizini yoksa oluşturuluyor
		rm -rf $ROOTBUILDDIR/* #içeriği temizleniyor
		cd $ROOTBUILDDIR #dizinine geçiyoruz
		if [ -n "${source}" ]
		then
		wget ${source}
		dowloadfile=$(ls|head -1)
		filetype=$(file -b --extension $dowloadfile|cut -d'/' -f1)
		if [ "${filetype}" == "???" ]; then unzip ${dowloadfile}; else tar -xvf ${dowloadfile};fi
		director=$(find ./* -maxdepth 0 -type d)
		directorname=$(basename ${director})
		if [ "${directorname}" != "${name}-${version}" ]; then mv $directorname ${name}-${version};fi
		fi
		mkdir -p $BUILDDIR&&mkdir -p $DESTDIR&&cd $BUILDDIR
		cp $PACKAGEDIR/klybuild $ROOTBUILDDIR/
	}
	# 6. madde, paketlenecek dosların listesini tutan file.index dosyası oluşturulur
	packageindex()
	{
		rm -rf file.index
		cd /tmp/kly/build/rootfs-${name}-${version}
		find . -type f | while IFS= read file_name; do
		if [ -f ${file_name} ]; then echo ${file_name:1}>>../file.index; fi
		done
		find . -type l | while IFS= read file_name; do
		if [ -L ${file_name} ]; then echo ${file_name:1}>>../file.index; fi
		done
	}
	# paket dosyası oluşturulur;
	# rootfs.tar.xz, file.index ve klybuild dosyaları tar.gz dosyası olarak hazırlanıyor.
	# 7. madde, tar.gz dosyası olarak hazırlanan dosya kly ismiyle değiştirilip paketimiz hazırlanır.
	packagecompress()
	{
		cd /tmp/kly/build/rootfs-${name}-${version}
		tar -cf ../rootfs.tar ./*
		cd /tmp/kly/build/
		xz -9 rootfs.tar
		tar -cvzf paket-${name}-${version}.tar.gz rootfs.tar.xz file.index klybuild
		cp paket-${name}-${version}.tar.gz ${dizin}/${paket}/${name}-${version}.kly
	}
	# fonksiyonlar aşağıdaki sırayla çalışacaktır.
	initsetup #bu dosya içindeki fonksiyon (indirilmesi)
	setup #klybuild dosyasından gelen fonksiyon (derleme öncesi hazırlık)
	build #klybuild dosyasından gelen fonksiyon (derleme)
	package #klybuild dosyasından gelen fonksiyon (derlenen paketin dizine yüklenemesi)
	packageindex #bu dosya içindeki fonksiyon (dizine yüklelen paketin indexlenmesi)
	packagecompress #bu dosya içindeki fonksiyon (index.lst, derleme talimatı ve dizinin sıkıştırılmas)
	
Burada **readline** paketini örnek alarak **klypaketle** dosyasının ve **klybuild** dosyasının nasıl hazırlandığı anlatıldı.
Diğer paketler için sadece hazırlanacak pakete uygun şekilde **klybuild** dosyası hazırlayacağız. **klypaketle**  dosyamızda değişiklik yapmayacağız. Artık  **klypaketle**  dosyası paketimizi oluşturan script **klybuild** ise hazırlanacak paketin bilgilerini bulunduran script doyasıdır.


.. raw:: pdf

   PageBreak
   
**Paket Yapma**
---------------

Bu bilgilere göre readline paketi nasıl oluşturulur onu görelim. Paketlerimizi oluşturacağımız bir dizin oluşturarak aşağıdaki işlemleri yapalım. Burada yine **readline** paketi anlatılacaktır.


.. code-block:: shell

	mkdir readline
	cd readline
	# readline için hazırlanan klybuild dosyası, readline dizininin içine kopyalayın
	cd ..
	# klypaketle dosyamıza parametre olarak readline dizini verilmiştir.
	./klypaketle readline 

Komut çalışınca readline/readline-8.1.kly dosyası oluşacaktır. Aşağıda resimde nasıl yapıldığı gösterilmiştir. Burada anlatılan **klypaketle** script dosyasını **/bin/** konumuna oluşturnuz ve **chmod 755 /bin/klypaketle** komutuyla çalıştırma izni vermeliyiz. **kly** paket sistemi için yapılacak olan **bsppaketle, klyupdate, klykur, klykaldir** scriptlerinide **/bin/** konumunda oluşturulmalı veya kopyalanmalı ve çalıştırma izni verilmeli.

.. image:: /_static/images/klypaketle-2.png
  	:width: 600

Artık sisteme kurulum için ikili dosya, kütüphaneleri ve dizinleri barındıran paketimiz oluşturuldu. Bu paketi sistemimize nasıl kurarız? konusu **Paket Kurma** başlığı altında anlatılacaktır.

.. raw:: pdf

   PageBreak


**Depo indexleme**
++++++++++++++++++

Depo, paketlerimizin olduğu alandır. Depoda ne kadar paket varsa bunların isimleri sürüm numaraları gibi bilgiler ile adreslerini liste halinde oluşturma işlemine **depo indexleme** denir.
Depo indexlenirken genellikle bilgiler **paket derleme talimatı(klybuild)** dosyasından alınır.
Paketlerin listesi, paketler kurulurken, silinirken ve güncellenirken kullanılmaktadır.

**kly github Depo Yapma**
-------------------------

Bu doküman kullanılarak hazırlanan paketleri bilgisayarınızda bir dizinde tutabiliriz. Fakat bu çok kısıtlı bir sistem olmasına sebep olacaktır. Paketleri bir internet ortamında bir yerde saklayarak, kurmak istediğimizde internet(uzak) üzerinden kurulması daha doğru bir yöntemdir. Bu dağıtımda paketlerimizi github.com üzerinde oluşturulan bir repository üzerinden çekilmektedir. İnternetteki paketlerimizin listesi her yeni paketi yükleme sırasında güncellenmektedir. Bu işlem github hesabı üzerinden yapılmaktadır. github hakkında temel işlemler için :ref:`githubbilgi` konusunu okuyunuz.

**github üzerinde depolamak için;**

- github hesabı açılır(kendilinuxunuyap)
- github repository oluşturulur(kly-binary-packages)
- kly-binary-packages deposuna aşağıda verilen index dosyasını oluşturunuz.
- kly-binary-packages deposuna .github/workflows dizinini oluşturarak aşağıda verilen **main.yml** dosyasını oluşturunuz. **main.yml** dosyasısdaki **sh index** satırı **index** scriptimizi her githuba paket gönderdiğimizde(commit) çalışacak ve **index.lst** dosyasını oluşturacaktır.
- internet üzerinden kly-binary-packages reposunda settings->action->general->Workflow permissions->Read and write permissions  işaretlenmelidir.
- Yapılan paketler github üzerinde gönderilmelidir.

main.yml
--------

.. code-block:: shell

	#-------------------------------------------------------------------------------------------------------------
	name: CI

	on:
	  push:
		branches: [ master ]
	  schedule:
		- cron: "0 0 1 2 6"

	jobs:
		compile:
		    name: depoindex
		    runs-on: ubuntu-latest
		    steps:
		      - name: Check out the repo
		        uses: actions/checkout@v2
		      - name: Run the build process with Docker
		        uses: addnab/docker-run-action@v3
		        with:
		            image: debian:testing
		            options: -v ${{ github.workspace }}:/root -v /output:/output
		            run: |
		                cd /root
		                sh index
		      - uses: "marvinpinto/action-automatic-releases@latest"
		        with:
		            repo_token: "${{ secrets.GITHUB_TOKEN }}"
		            automatic_release_tag: "current"
		            prerelease: false
		            title: "Latest release"
		            files: |
		              /output/*



.. raw:: pdf

   PageBreak
   
**index Dosyası**
-----------------

Aşağıdaki script kly paket dosyalarımızı olduğu dizinde tek tek açarak içerisinden **klybuild** dosyalarını çıkartır. Paketle ilgili bilgileri alıp **index.lst** dosyası oluşturmaktadır. İstersek paketler local ortamdada index oluşturabiliriz. Bu dokümanda github üzerinde oluşturacak şekilde anlatılmıştır. Paket indeksi oluşturan **index.lst** dosyası aşağıdaki gibi olacaktır. Listede name, version ve depends(bağımlı olduğu paketler) bilgileri bulunmaktadır. Bilgilerin arasında **|** karekteri kullanılmıştır.

.. code-block:: shell

	#!/bin/sh
	#set -ex
	mkdir /output -p
	mkdir -p /klysource
	>index.lst
	find * -type f -name *.kly |
			while IFS= read file_name; do
				dosya="$(dirname $file_name)/klybuild"
				version=$(cat $dosya|grep version=)
				name=$(cat $dosya|grep name=)
				depends=$(cat $dosya|grep depends=)
				echo "$name|$version|$depends|$(dirname $file_name)">>index.lst
			done
	cp -rf index.lst /output

	# *****************************source files******************************
	cp -prfv ./* /klysource/

	find /klysource/* -type f -name *.kly |
			while IFS= read file_name; do
			rm -rf "$file_name"
			done
	tar -cf /output/klysourcepackage.tar /klysource/
	rm -rf /klysource


**index.lst İçeriği**
---------------------

https://github.com/kendilinuxunuyap/kly-binary-packages/releases/download/current/index.lst adresinde bulunan dosya aşağıdaki gibi liste oluşturacaktır.

.. code-block:: shell

	name="acl"|version="2.3.1"|depends="attr"|acl
	name="attr"|version="2.5.1"|depends=""|attr
	name="audit"|version='3.1.1'|depends=""|audit
	name="bash"|version="5.2.21"|depends="glibc,readline,ncurses"|bash


.. raw:: pdf

   PageBreak



index Güncelleme
++++++++++++++++

İndex güncelleme uzak(internet) depodaki paketlerin index listesinin yerelde tutulan index dosyasıyla eşitlemek işlemidir.
Depoda olan paketlerin listesi yerelde tutulan index.lst dosyasındada olması gerekmetedir. Bu işlemi yapan klyupdate dosya içeriği aşağıdadır.

**klyupdate** 
-------------

Debian sisteminde /etc/apt/source.list gibi bir yapı bulunmaktadır. Bu dosya içindeki depo adreslerine göre index oluşturmaktadır. Hazırladığımız paket sitemindede /etc/kly/source.list dosyası kullanılmaktadır. Birden fazla index dosyasını birleştiren ve güncelleyen scriptimiz aşağıdadır.
 
.. code-block:: shell
	
	#!/bin/sh
	target="$1"
	mkdir -p $target/etc/kly -p $target/tmp
	rm -rf $target/etc/kly/index.lst
	rm -rf $target/tmp/temp.lst
	curl -Lo $target/etc/kly/index.lst \
	https://github.com/kendilinuxunuyap/kly-binary-packages/releases/download/current/index.lst
		 
**klyupdate** Kullanma
----------------------

Script bir parametre almaktadır. Parametremiz --update veya -u olmalıdır. Bu scripti kullanarak /etc/kly/index.lst dosyasını github depomuzdaki paket listesiyle güncelleyecektir. 

.. code-block:: shell
	
	./klyupdate /home/user1/testiso
	# /home/user1/testiso konumu hazırladığımız dağıtım konumudur.
	# kendi siteminize uygun konum belirleyiniz. 


.. raw:: pdf

   PageBreak



Paket Kurma
+++++++++++

Hazırlanan dağıtımda paketlerin kurulması için  sırasıyla aşağıdaki işlem adımları yapılmalıdır.

1. Paketin indirilmesi
2. İndirilen paketin /tmp/kly/kur/ konumunda açılması
3. Açılan paket dosyalarının / konumuna yüklenmesi(kopyalanması)

	- Paketin bağımlı olduğu paketler varmı kontrol edilir
	- Yüklü olmayan bağımlılıklar yüklenir
	
4. Yüklenen paket bilgileri(name, version ve bağımlılık) yüklü paketlerin index bilgilerini tutan paket sistemi dizininindeki index dosyasına eklenir.	
5. Açılan paket içindeki yüklenen dosyaların nereye yüklendiğini tutan file.index dosyası paket sistemi dizinine yüklenir


Bu işlemler daha detaylandırılabilir. Bu işlemlerin detaylı olması paket sisteminin kullanılabilirliğini ve yetenekleri olarak ifade edebiliriz. İşlem adımlarını kolaylıkla sıralarken bunları yapacak script yazmak ciddi planlamalar yapılarak tasarlanması gerekmektedir.


Örneğin bir paketimiz zip dosyası olsun ve içinde dosya listesini tutan **file.index** adında bir dosyamız olsun. Paketi aşağıdaki gibi kurabiliriz.

.. code-block:: shell

	cd /tmp/kur/
	unzip /dosya/yolu/paket.zip
	cp -rfp ./* /
	cp file.index /paket/veri/yolu/paket.index

- Bu örnekte ilk satırda geçici dizine gittik 
- Paketi oraya açtık.
- Paket içeriğini kök dizine kopyaladık.
- Paket dosya listesini verilerin tutulduğu yere kopyaladık.

Bu işlemden sonra paket kurulmuş oldu.


.. raw:: pdf

   PageBreak

**kly Paket Kurma Scripti Tasarlama**
-------------------------------------
Burada basit seviyede kurulum yapan script kullanılmıştır. Detaylandırıldıkça doküman güncellenecektir. Kurulum scripti aşağıda görülmektedir.

Paket kurulurken paket içerisinde bulunan dosyalar sisteme kopyalanır.
Daha sonra istenirse silinebilmesi için paket içeriğinde dosyaların listesi tutulur.
Bu dosya ayrıca paketin bütünlüğünü kontrol etmek için de kullanılır.


**klykur** Scripti
------------------

.. code-block:: shell
	
	#!/bin/sh
	name="name=\"${1}\""
	target=$2
	mkdir -p $target
	paket=$(echo $(cat $target/etc/kly/index.lst|grep $name)|cut -d"\"" -f2)
	version=$(echo $(cat $target/etc/kly/index.lst|grep $name)|cut -d"\"" -f4)
	depends=$(echo $(cat $target/etc/kly/index.lst|grep $name)|cut -d"\"" -f6)
	# index dosyamızda paket aranıyor
	if [ ! -n "${paket}" ]; then
	echo "***********Paket Bulunamadı**********"; exit
	fi

	# 1. adım paketi indirme
	mkdir -p $target/tmp/kly $target/tmp/kly/kur
	rm -rf $target/tmp/kly/kur/*
	curl -Lo $target/tmp/kly/kur/${paket}-${version}.tar.gz \
	https://github.com/kendilinuxunuyap/kly-binary-packages/raw/master/${paket}/${paket}-${version}.kly
	mkdir -p $target/var/lib/kly
	cd $target/tmp/kly/kur/

	# 2. adım paketi açma
	tar -xf ${paket}-${version}.tar.gz
	mkdir -p rootfs
	tar -xf rootfs.tar.xz -C rootfs

	# 3. adım paketi kurma
	cp -prfv rootfs/* $target/

	# 4. adım name version depends /var/lib/kly/index.lst eklenmesi
	echo "name=\"${paket}\":"version=\"${version}\":"depends=\"${depends}\"">>$target/var/lib/kly/index.lst
	# 5. adım paket içinde gelen paket dosyalarının dosya ve dizin yapısını tutan
	# file index dosyanının /var/lib/kly/ konumuna kopyalanması
	cp file.index $target/var/lib/kly/${paket}-${version}.lst
	
**klykur** Scriptini Kullanma
-----------------------------

Script iki parametre almaktadır. İlk parametre paket adı. İkinci parametremiz ise nereye kuracağını belirten hedef olmalıdır. Bu scripti kullanarak readline paketi aşağıdaki gibi kurulabilir. 

.. code-block:: shell
	
	./klykur readline /home/user1/testiso
	# /home/user1/testiso konumu hazırladığımız dağıtım konumudur.
	# kendi siteminize uygun konum belirleyiniz. 

.. raw:: pdf

   PageBreak


**Paket Kaldırma**
++++++++++++++++++

Sistemde kurulu paketleri kaldırmak için işlem adımları şunlardır.

1. Paketin kullandığı bağımlılıkları başka paketler kullanıyor mu kontrol edilir. Eğer kullanılmıyorsa kaldırılır.
2. Paketin paket.LIST dosyası içerisindeki dosyalar, dizinler kaldırılır.
3. Kaldırılan dosyalardan sonra /paket/veri/yolu/paket.LIST dosyasından paket bilgisi kaldırılır.
4. sistemde kurulu paketler index dosyasından ilgili paket satırı kaldırılmalıdır.

**kly Paket Kaldırma Scripti Tasarlama**
----------------------------------------

Dokumanda örnek olarak verilen kly paket sistemi için yukarıdaki paket kaldırma bilgilerini kullanarak tasarlanmıştır.

**klykaldir** scripti
---------------------

.. code-block:: shell
	
	#-------------------------------------------------------------------------------------------------------------
	#!/bin/sh
	name="name=\"${1}\""
	target=$2
	mkdir -p $target
	paket=$(echo $(cat $target/etc/kly/index.lst|grep $name)|cut -d"\"" -f2)
	version=$(echo $(cat $target/etc/kly/index.lst|grep $name)|cut -d"\"" -f4)
	depends=$(echo $(cat $target/etc/kly/index.lst|grep $name)|cut -d"\"" -f6)
	# index dosyamızda paket aranıyor
	if [ ! -n "${paket}" ]; then
		echo "***********Paket Bulunamadı**********"; exit
	fi
	# Bağımlılıkları başka paketler kullanıyor mu kontrol edilir
	# Başka paketler kullanılıyorsa silinmemeli. Bu işlemin kodları yazılmadı.
	echo "${paket}-${version} bağımlılık kontrolü yapılacak"

	# Paketin file.lst dosyası içerisindeki dosyalar kaldırılır.
	if [ -f "$target/var/lib/kly/${paket}-${version}.lst" ]; then
		cat $target/var/lib/kly/${paket}-${version}.lst | while read dosya ;
		do
			if [[ -f "$target/$dosya" ]] ; then rm -f "$target/$dosya"; fi
		done
	fi
	# /var/lib/kly/paket-version.lst dosyasından paket bilgisi kaldırılır.
	rm -f $target/var/lib/kly/${paket}-${version}.lst

	# /var/lib/kly/index.lst dosyasından ilgili paket satırı kaldırılır.
	sed -i "/name=\"${paket}\"/d" $target/var/lib/kly/index.lst

	echo "********** ${paket}-${version}  Paketi Kaldırıldı **********"
		
Bu örnekte paket listesini satır satır okuduk. Önce dosya olanları sildik. Daha sonra tekrar okuyup boş kalan dizinleri sildik.
Son olarak paket listesi dosyamızı sildik. Bu işlem sonunda paket silinmiş oldu.

**klykaldir** Kullanma
----------------------

.. code-block:: shell
	
	./klykaldir readline /home/user1/testiso
	# /home/user1/testiso konumu hazırladığımız dağıtım konumudur.
	# kendi siteminize uygun konum belirleyiniz. 
.. raw:: pdf

   PageBreak


.. _paketsistemi:
**Paket Sistemi Tasarlama**
===========================

Önceki bölümlerde, gerekli paketlerin derlenmesi tamamlandı. Bu paketler, oturum açtığınız kullanıcının ev dizininde **$HOME/distro/rootfs** konumunda yer alacaktır. Burada **$HOME**, o anki kullanıcıya göre değişiklik gösterecektir. Örneğin, kullanıcı adımız **bd** ise, **$HOME** dizini **/home/bd/** olacaktır. Bu durumda, **$HOME/distro/rootfs** aslında **/home/bd/distro/rootfs** dizinini temsil eder.

ISO hazırlama süreci, yazının başında anlattığımız **Temel Linux Sistemi Oluşturma** ISO yapımına benzer bir şekilde ilerleyecektir. Oluşturulacak **iso** dosyasının temel yapısı aşağıdaki gibi olacaktır. Bu yapıyı oluşturan dört temel dosyanın her biri için hazırlık adımları tek tek açıklanacak ve en sonunda hepsini bir araya getiren bir ISO oluşturma scripti verilecektir.

.. code-block:: shell

   $HOME/distro/iso/boot/grub/grub.cfg
   $HOME/distro/iso/boot/initrd.img
   $HOME/distro/iso/boot/vmlinuz
   $HOME/distro/iso/live/filesystem.squashfs

**1-grub.cfg Hazırlama**
------------------------

Sistemin açılmasını sağlayan temel dosyalardan biri **grub.cfg** dosyasıdır. Genel olarak basit bir **grub.cfg** şu şekildedir:

.. code-block:: shell

   linux /boot/vmlinuz
   initrd /boot/initrd.img
   boot

Bu örnekteki sistem için **grub.cfg** dosyası aşağıdaki gibi düzenlenmiştir. Burada dikkat edilmesi gereken noktalar:

- Menü seçeneklerinde **live** ifadesinin kullanılması.
- Sistemin **openrc** ile başlatılmasını sağlamak için gerekli kernel parametrelerinin eklenmesi.
- Kurulum için özel bir **init=/bin/kur** satırı kullanılması.

İşte örnek **grub.cfg** oluşturma komutları:

.. code-block:: shell

   cat << EOF > "$HOME/distro/iso/boot/grub/grub.cfg"
   set timeout=3	# Timeout for menu
   set default=1	# Default boot entry
   set menu_color_normal=white/black	# Menu Colours
   set menu_color_highlight=white/blue	# Menu Colours
   insmod all_video; terminal_output console; terminal_input console
   
   menuentry "Canli(live) GNU/Linux(kly)" --class liveiso {
    linux /boot/vmlinuz boot=live init=/sbin/openrc-init net.ifnames=0 \
        biosdevname=0
    initrd /boot/initrd.img
   }
   menuentry "Kur GNU/Linux(kly)" --class liveiso {
      linux /boot/vmlinuz boot=live init=/bin/kur quiet
      initrd /boot/initrd.img 
      }
   EOF


.. raw:: pdf

   PageBreak
   
**2-initrd.img Oluşturma/Güncelleme**
-------------------------------------

**initrd.img** dosyasının güncellenmesi veya oluşturulması için aşağıdaki adımlar izlenebilir.

Varsayılan sistemde çalışıyorsanız doğrudan aşağıdaki komut yeterlidir:

.. code-block:: shell

   # initrd günceller
   /usr/sbin/update-initramfs -u -k $(uname -r)

Ancak bir **chroot** ortamında çalışıyorsanız (yani rootfs içine girip işlem yapacaksanız), önce **dev**, **sys**, **proc**, **run**, **tmp** dizinlerinin bağlanması gerekir. Bu işlemler root yetkisi ile yapılmalıdır.

Aşağıda örnek bir **initrd.img oluşturma scripti** yer almaktadır:

.. code-block:: shell

   #--------------------------------------------------------------------------
   rootfs="$HOME/distro/rootfs"
   distro="$HOME/distro"

   ## Gerekli dizinler oluşturuluyor
   for dir in dev sys proc run tmp; do
    mkdir -p "$rootfs/$dir"
   done
    
   ## Dizinler bağlanıyor
   # chroot ortamı için gerekli bind işlemleri
   for dir in dev sys proc run tmp; do 
   	mount --bind /$dir $rootfs/$dir
   done

   ## Kernel versiyonu tespiti
   fname=$(basename $rootfs/boot/config*)
   kversion=${fname:7}
   mv $rootfs/boot/config* $rootfs/boot/config-$kversion
   cp $rootfs/boot/config-$kversion $rootfs/etc/kernel-config

   ## initramfs oluşturuluyor
   chroot $rootfs update-initramfs -u -k $kversion

   ## Dizin bağlantıları kaldırılıyor
   for dir in dev sys proc run tmp; do
   	umount -lf -R $rootfs/$dir 2>/dev/null
   done
   
   ## initrd.img dosyası kopyalanıyor
   cp -pf $rootfs/boot/initrd.img-* $distro/iso/boot/initrd.img


.. raw:: pdf

   PageBreak
   
**3-vmlinuz Hazırlama**
-----------------------

Kernel dosyamız olan **vmlinuz**, ISO dizinine aşağıdaki komutla kopyalanır:

.. code-block:: shell

   #--------------------------------------------------------------------------
   rootfs="$HOME/distro/rootfs"
   distro="$HOME/distro"

   # Kernel dosyasını kopyala
   cp -pf $rootfs/boot/vmlinuz-* $distro/iso/boot/vmlinuz

   # Sistemde rootfs dışında boot bölümü olduğu için boot dizini silinebilir
   #rm -rf $rootfs/boot

**4-filesystem.squashfs Hazırlama**
-----------------------------------

Sistemin **live** olarak çalıştırılabilmesi ve kurulum için kayank oluşturacak **filesystem.squashfs** dosyası oluşturulur:

.. code-block:: shell

   #--------------------------------------------------------------------------
   cd $HOME/distro/
   mksquashfs $HOME/distro/rootfs $HOME/distro/filesystem.squashfs -comp xz -wildcards
   mv $HOME/distro/filesystem.squashfs $HOME/distro/iso/live/filesystem.squashfs

**5-ISO Dosyasının Oluşturulması**
----------------------------------

Tüm dosyalar konumlarına uygun hazırlandıktan sonra, **grub-mkrescue** aracı ile ISO dosyamızı oluşturabiliriz:

.. code-block:: shell

   #--------------------------------------------------------------------------
   cd $HOME/distro
   grub-mkrescue iso/ -o kly.iso

**6-ISO'nun Test Edilmesi**
---------------------------

Oluşturduğumuz ISO dosyasını **qemu** veya **VirtualBox** ile test edebiliriz. Linux üzerinde terminalden **qemu** kullanarak aşağıdaki şekilde test gerçekleştirebilirsiniz.

.. code-block:: shell

   # qemu ile ISO'nun test edilmesi
   qemu-system-x86_64 -cdrom $HOME/distro/kly.iso -m 1G

.. raw:: pdf

   PageBreak

**ISO Oluşturma Scripti**
-------------------------

Bu dokümanda anlatılan paketleri kurulduğu **/home/$user/distro/rootfs** dizini kullanarak, **/home/$user/distro/iso/** konumuna **kly.iso** dosyasını üretir. Bu bölümde anlatılan tüm aşamalar tek script halinde aşağıda verilmiştir.

.. code-block:: shell

   #!/bin/bash
   
   display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -n 1)"
   user=$(who | grep '('$display')' | awk '{print $1}')	# Kullanıcı&ekran bul
   distro="/home/$user/distro"; rootfs="$distro/rootfs"; rm -rf "$distro/iso"
   
   # chroot ortamı için gerekli bind işlemleri
   for dir in dev dev/pts proc sys; do mount -o bind /$dir $rootfs/$dir; done
   
   # Root parolası ve live kullanıcı eklenmesi
   chroot $rootfs echo -e "1\n1\n"|chroot $rootfs passwd root
   chroot $rootfs useradd live -m -s /bin/sh -d /home/live
   chroot $rootfs echo -e "live\nlive\n"|chroot $rootfs passwd live
   for grp in users tty wheel cdrom audio dip video plugdev netdev; do
       chroot $rootfs usermod -aG $grp live || true
   done
   # agetty ayarları
   sed -i "/agetty_options/d" $rootfs/etc/conf.d/agetty
   echo -e "\nagetty_options=\"-l /usr/bin/login\"" >> $rootfs/etc/conf.d/agetty
   # initrd güncellemesi
   fname=$(basename $rootfs/boot/config*)
   kversion=${fname:7}
   mv $rootfs/boot/config* $rootfs/boot/config-$kversion
   cp $rootfs/boot/config-$kversion $rootfs/etc/kernel-config
   chroot $rootfs update-initramfs -u -k $kversion
   # chroot bind dizinlerini ayır
   for dir in dev dev/pts proc sys ; do
       while umount -lf -R $rootfs/$dir 2>/dev/null ; do true; done
   done
   
   # ISO dizin yapısını oluştur
   mkdir -p "$distro/iso/boot/grub" "$distro/iso/live"
   cp -pf $rootfs/boot/initrd.img-* $distro/iso/boot/initrd.img	# initrd.img
   cp -pf $rootfs/boot/vmlinuz-* $distro/iso/boot/vmlinuz # vmlinuz kopyala
   mksquashfs $rootfs $distro/filesystem.squashfs -comp xz -wildcards # squashfs
   mv $distro/filesystem.squashfs $distro/iso/live/filesystem.squashfs
   # grub.cfg dosyasını yaz
   cat << EOF > "$distro/iso/boot/grub/grub.cfg"
   set timeout=3; set default=1; terminal_input console;
   menuentry "Canli(live) GNU/Linux 64-bit" --class liveiso {
      linux /boot/vmlinuz boot=live init=/sbin/openrc-init net.ifnames=0 \
      biosdevname=0
      initrd /boot/initrd.img
   }
   menuentry "Kur GNU/Linux 64-bit" --class liveiso {
      linux /boot/vmlinuz boot=live init=/bin/kur quiet
      initrd /boot/initrd.img 
      }
   EOF
   grub-mkrescue $distro/iso/ -o $distro/kly.iso   #iso oluşturuluyor

.. raw:: pdf

   PageBreak


**Dağıtıma Özgü ISO Hazırlama**
===============================

Dağıtıma özgü ISO oluşturmak için o dağıtımın paket sistemi kullanılır.  
Bu dokümanda anlatılan **kly** paket sistemi, önceki bölümde detaylıca açıklanmıştır.

Bu bölümde, **kly** paket sistemini kullanarak ISO oluşturma adımları basit ve anlaşılır şekilde verilecektir.  


.. note::

   Anlatılan yöntem, Debian gibi diğer dağıtımlarda da büyük oranda benzerdir. 
   Anlatılan yöntem genel Linux dağıtımlarının ISO oluşturma mantığına dayanır.
   Araçlar, dizinler ve komutlarda küçük farklılıklar olabilir, ancak iş akışı aynıdır.


   
**kly Paket Sistemiyle ISO Oluşturma Scripti**
----------------------------------------------

.. code-block:: shell

	#--------------------------------------------------------------------------------------------------------------------
	#!/bin/bash
	rootfs="/tmp/distro/rootfs"
	distro="/tmp/distro"
	rm -rf $rootfs
	mkdir -p $rootfs -p $rootfs/bin $rootfs/etc
	##Kurulum scripti
	cp -prf files/bin/* $rootfs/bin/
	cp -prf files/etc/* $rootfs/etc/
	
	# temel dizinler ve dosyalar oluşturuluyor
	cd $rootfs/
	mkdir  -p bin dev etc home lib64 proc root run sbin sys usr var etc/kly \
	tmp tmp/kly/kur var/log  var/tmp usr/lib64/x86_64-linux-gnu \
	usr/lib64/pkgconfig usr/local/{bin,etc,games,include,lib,sbin,share,src}
	ln -s lib64 lib
	cd var&&ln -s ../run run&&cd -
	cd usr&&ln -s lib64 lib&&cd -
	cd usr/lib64/x86_64-linux-gnu&&ln -s ../pkgconfig  pkgconfig&&cd -

	echo -e "/bin/sh\n/bin/bash\n/bin/rbash\n/bin/dash" >> "$rootfs/etc/shell"
	echo "tmpfs /tmp tmpfs rw,nodev,nosuid 0 0" >> "$rootfs/etc/fstab"
	echo "127.0.0.1 kly" >> "$rootfs/etc/hosts"
	echo "kly" > "$rootfs/etc/hostname"
	echo "nameserver 8.8.8.8" > "$rootfs/etc/resolv.conf"

	# paket adresi ekleniyor
	echo "kendilinuxunuyap/kly-binary-packages">$rootfs/etc/kly/sources.list

	### installing kly create_package in rootfs
	echo root:x:0:0:root:/root:/bin/sh > $rootfs/etc/passwd 
	chmod 755 $rootfs/etc/passwd

	### system chroot  bind/mount
	for dir in dev dev/pts proc sys; do mount -o bind /$dir $rootfs/$dir; done
	## paket listesi güncelleniyor
	$rootfs/bin/kly -u $rootfs

	## paketler kuruluyor
	for paket in glibc readline ncurses \bash openssl acl attr libcap libpcre2 gmp \
	 coreutils util-linux \grep \sed mpfr \gawk findutils libgcc libcap-ng sqlite \
	 \gzip xz-utils zstd \bzip2 \elfutils libselinux \tar \zlib brotli curl shadow \ 
	 \file eudev cpio libsepol kmod audit libxcrypt libnsl pam libtirpc e2fsprogs \
	 dosfstools  initramfs-tools libxml2 expat libmd libaio lvm2 popt icu iproute2 \
	 net-tools  dhcp openrc  rsync kbd busybox kernel kernel-headers live-boot \ 
	 live-config parted  nano grub dialog efibootmgr efivar libssh openssh
	do
	chroot $rootfs /bin/klykur $paket; 
	done

	#### system chroot umount
	for dir in dev dev/pts proc sys ; do    while umount -lf -R $rootfs/$dir \
	2>/dev/null ; do true; done done
	exit


.. raw:: pdf

   PageBreak

.. code-block:: shell

	#--------------------------------------------------------------------------------------------------------------------
	# scriptin devamı   
	chroot $rootfs useradd live -m -s /bin/sh  -d /home/live
	chroot $rootfs echo -e "live\nlive\n"|chroot $rootfs passwd live

	for grp in users tty wheel cdrom audio dip video plugdev netdev; do
		chroot $rootfs usermod -aG $grp live || true
	done

	sed -i "/agetty_options/d" $rootfs/etc/conf.d/agetty
	echo -e "\nagetty_options=\"-l /usr/bin/login\"" >> $rootfs/etc/conf.d/agetty

	### update-initrd
	fname=$(basename $rootfs/boot/config*)
	kversion=${fname:7}
	mv $rootfs/boot/config* $rootfs/boot/config-$kversion
	cp $rootfs/boot/config-$kversion $rootfs/etc/kernel-config

	chroot $rootfs update-initramfs -u -k $kversion
	#### system chroot umount
	for dir in dev dev/pts proc sys ; 
	do    while umount -lf -R $rootfs/$dir 2>/dev/null ; do true; done done

	mkdir -p "$distro/iso" "$distro/iso/boot" "$distro/iso/boot/grub"
	mkdir -p  "$distro/iso/live"
	#### Copy kernel and initramfs
	cp -pf $rootfs/boot/initrd.img-* $distro/iso/boot/initrd.img
	cp -pf $rootfs/boot/vmlinuz-* $distro/iso/boot/vmlinuz
	rm -rf $rootfs/boot

	#### Create squashfs
	mksquashfs $rootfs $distro/filesystem.squashfs -comp xz -wildcards
	mv $distro/filesystem.squashfs $distro/iso/live/filesystem.squashfs

	#### Write grub.cfg
	cat << EOF > "$distro/iso/boot/grub/grub.cfg"
	set timeout=3	# Timeout for menu
	set default=1	# Default boot entry

	# Menu Colours
	set menu_color_normal=white/black
	set menu_color_highlight=white/blue
	insmod all_video
	terminal_output console
	terminal_input console
	menuentry "Canli(live) GNU/Linux 64-bit" --class liveiso {
		linux /boot/vmlinuz boot=live init=/sbin/openrc-init net.ifnames=0 \
		biosdevname=0
		initrd /boot/initrd.img
	}
	menuentry "Kur GNU/Linux 64-bit" --class liveiso {
		linux /boot/vmlinuz boot=live init=/bin/kur quiet
		initrd /boot/initrd.img
	}
	EOF
	grub-mkrescue $distro/iso/ -o $distro/distro.iso

.. raw:: pdf

   PageBreak



.. _isohazirlama:
**ISO Hazırlama**
=================

.. _sistemkurma:

Sistem Kurulumu
===============

.. note::
   Bu doküman;
   
   [https://turkman.gitlab.io/devel/doc/wiki/01-sistem/04-kurulum/00-basit-kurulum.html]
   (https://turkman.gitlab.io/devel/doc/wiki/01-sistem/04-kurulum/00-basit-kurulum.html) 
   adresindeki çalışmadan kaynak alınarak türetilmiş ve özgünleştirilmiştir. 
   Teknik komutlar kamuya açık belgelerden derlenmiştir.

Bu bölümde, hazırlanan ISO dosyası ile sistem kurulumu için kullanılabilecek çeşitli yöntemler detaylandırılmaktadır. Kurulum işlemleri üç ana senaryoyu kapsayacak şekilde sunulmuştur:

1. Tek disk bölümü üzerine kurulum
2. İki disk bölümü (boot + sistem) üzerine kurulum
3. UEFI destekli sistem kurulumu

Her yöntemin avantajları ve dikkat edilmesi gereken noktalar açıklanmıştır. Böylece kullanıcılar, kendi sistem yapılarına en uygun kurulum yöntemini seçebilirler.

.. note::

   Kurulum sırasında otomatik senaryo tespiti yapılacak şekilde bir script hazırlanmıştır. Bu script, **Legacy BIOS** ve **UEFI** yapılandırmalarını algılayabilir ve kullanıcı hatalarını önlemek için gerekli kontrolleri sağlar.


.. raw:: pdf

   PageBreak
   
**1-Tek Bölüm Kurulumu**
========================

Bu yöntem, tüm sistemin tek bir disk bölümü üzerine kurulmasını sağlar. Özellikle basit sistemlerde tercih edilir.

**Hazırlıklar:**

- Disk işlemleri için `evdev` veya `udevd` servislerinin aktif olması gerekir.
- Gerekli çekirdek modüllerini yükleyin:

  .. code-block:: shell

     modprobe loop
     modprobe squashfs
     modprobe ext4

**Disk Bölümlendirme:**

.. code-block:: shell

    cfdisk /dev/sda

1. `dos` şemasını seçin
2. Tüm disk alanını tek bir `Linux system` bölümü olarak ayırın
3. Bölümü yazın ve çıkın

**Dosya Sistemi Oluşturma:**

.. code-block:: shell

    mkfs.ext4 /dev/sda1

**Kurulum Medyasını Bağlama ve Dosya Kopyalama:**

.. code-block:: shell

    mkdir -p /cdrom /kaynak
    mount -t iso9660 -o loop /dev/sr0 /cdrom
    mount -t squashfs -o loop /cdrom/live/filesystem.squashfs /kaynak

    mkdir -p /hedef
    mount /dev/sda1 /hedef

    cp -prfv /kaynak/* /hedef
    sync

**Chroot Ortamına Geçiş ve GRUB Kurulumu:**

.. code-block:: shell

    for dir in /dev /sys /proc /run /tmp; do
        mount --bind /$dir /hedef/$dir
    done

    chroot /hedef

    grub-install --boot-directory=/boot /dev/sda

    grub-mkconfig -o /boot/grub/grub.cfg


.. raw:: pdf

   PageBreak

**2-İki Bölüm Kurulumu**
========================

Bu senaryo, **/boot** ve **kök dosya sistemi** için ayrı bölümler oluşturur.

**Disk Bölümlendirme ve Formatlama:**

.. code-block:: shell

    cfdisk /dev/sda
    # 512MB vfat EFI bölümü (sda1) ve geri kalan ext4 (sda2)

    mkfs.vfat /dev/sda1
    mkfs.ext4 /dev/sda2

**Kurulum ve GRUB İşlemleri:**

.. code-block:: shell

    mkdir -p /hedef /hedef/boot
    mount /dev/sda2 /hedef
    mount /dev/sda1 /hedef/boot

    cp -prfv /kaynak/* /hedef
    sync

    chroot /hedef

    grub-install --removable --boot-directory=/boot --efi-directory=/boot /dev/sda
    grub-mkconfig -o /boot/grub/grub.cfg


.. raw:: pdf

   PageBreak

**3-UEFI Sistem Kurulumu**
==========================

Bu yöntem, UEFI destekli sistemlerde Ext4 dosya sistemi ve GRUB bootloader kullanarak kurulum yapılmasını sağlar.

**UEFI Tespiti:**

.. code-block:: shell

    [[ -d /sys/firmware/efi/ ]] && echo UEFI || echo Legacy

**Disk Bölümlendirme:**

.. code-block:: shell

    cfdisk /dev/sda
    # 512MB vfat EFI bölümü (sda1), geri kalan ext4 (sda2)

    mkfs.vfat /dev/sda1
    mkfs.ext4 /dev/sda2

**Kurulum ve GRUB İşlemleri:**

.. code-block:: shell

    mkdir -p /hedef /hedef/boot/efi
    mount /dev/sda2 /hedef
    mount /dev/sda1 /hedef/boot/efi

    cp -prfv /kaynak/* /hedef
    sync

    chroot /hedef

    mount -t efivarfs efivarfs /sys/firmware/efi/efivars
    grub-install --removable --boot-directory=/boot --efi-directory=/boot --target=x86_64-efi /dev/sda
    grub-mkconfig -o /boot/grub/grub.cfg


   
.. raw:: pdf

   PageBreak

.. _sistemkurulumu:
Sistem Kurulumu
===============

apt Paket Sistemi
+++++++++++++++++

apt paket sistemi debian tabanlı sistemlerde paket yönetimi için kullanılan bir uygulamadır.
Temel işlemler şunlardır.

Yerel Paket İndexini Güncelleme
-------------------------------

.. code-block:: shell

	sudo apt  update

Paket Yükleme
-------------

.. code-block:: shell

	sudo apt install paket_adi

Paket Silme
-----------

.. code-block:: shell

	sudo apt remove paket_adi

.. raw:: pdf

   PageBreak


Chroot Nedir?
+++++++++++++

chroot komutu çalışan sistem üzerinde belirli bir klasöre root yetkisi verip sadece o klasörü sanki linux sistemi gibi çalıştıran bir komuttur. Sağladığı avantajlar çok fazladır. Bunlar;

    - Sistem tasarlama
    - Sitem üzerinde yeni dağıtımlara müdahale etme ve sorun çözme
    - Kullanıcı kendine özel geliştirme ortamı oluşturabilir.
    - Yazılım bağımlıkları sorunlarına çözüm olabilir.
    - Kullanıcıya sadece kendisine verilen alanda sınırsız yetki verme vb.

.. image:: /_static/images/chroot-1.png
  :width: 600
  :height: 400


Yukarıdaki resimde user1 altında wrk dizini altına yeni bir sistem kurulmuş gibi yapılandırmayı gerçekleştirmiş.

**/home/etapadmin/test** dizinindeki sistem üzerinde sisteme erişmek için;

.. code-block:: shell

	# sisteme erişim yapıldı.
	sudo chroot /home/etapadmin/test 
	
**/home/etapadmin/test** dizinindeki sistem üzerinde sistemi silmek için;

.. code-block:: shell

	# sistem silindi
	sudo rm -rf /home/etapadmin/test

.. raw:: pdf

   PageBreak
   
Yeni sistem tasarlamak ve erişmek için temel komutları ve komut yorumlayıcının olması gerekmektedir. Bunun için bize gerekli olan komutları bu yapının içine koymamız gerekmektedir. Örneğin ls komutu için doğrudan çalışıp çalışmadığını ldd komutu ile kontrol edelim.

.. image:: /_static/images/chroot-2.png
  :width: 600

Görüldüğü gibi ls komutunun çalışması için bağımlı olduğu kütüphane dosyaları bulunmaktadır. Bağımlı olduğu dosyaları yeni oluşturduğumuz sistem dizinine aynı dizin yapısında kopyalamamız gerekmektedir. Bu dosyalar eksiksiz olursa ls komutu çalışacaktır. Fakat bu işlemi tek tek yapmamız çok zahmetli bir işlemdir. Bu işi yapacak script dosyası aşağıda verilmiştir.

Bağımlılık Scripti
------------------

lddscript.sh

.. code-block:: shell

	#!/bin/bash

	if [ ${#} != 2 ]
	then
	    echo "usage $0 PATH_TO_BINARY target_folder"
	    exit 1
	fi
	path_to_binary="$1"
	target_folder="$2"

	# if we cannot find the the binary we have to abort
	if [ ! -f "${path_to_binary}" ]
	then
	    echo "The file '${path_to_binary}' was not found. Aborting!"
	    exit 1
	fi

	echo "---> copy binary itself" # copy the binary itself
	cp --parents -v "${path_to_binary}" "${target_folder}"

	echo "---> copy libraries" # copy the library dependencies
	ldd "${path_to_binary}" | awk -F'[> ]' '{print $(NF-1)}' | while read -r lib
	do
	    [ -f "$lib" ] && cp -v --parents "$lib" "${target_folder}"
	done

Basit Sistem Oluşturma
----------------------

Bu örnekte kullanıcının(etapadmin) ev dizinine(/home/etapadmin) test dizini oluşturuldu ve işlemler yapıldı. 
ls, rmdir, mkdir ve bash komutlarından oluşan sistem hazırlama.

Sistem Dizinin Oluşturulması
----------------------------

.. code-block:: shell

	# ev dizinine test dizini oluşturuldu.
	mkdir /home/etapadmin/test/
	
/home/etapadmin/ dizinine **Bağımlılık Scripti** kodunu **lddscripts.sh** oluşturalım.

ls Komutu
----------

.. code-block:: shell

	# ls komutu ve bağımlılığı kopyalandı.
	bash lddscripts.sh /bin/ls /home/etapadmin/test/

.. image:: /_static/images/chroot-3.png
  :width: 600

Bu işlemi diğer komutlar içinde sırasıyla yapmamız gerekmektedir.

rmdir Komutu
------------

.. code-block:: shell

	# rmdir komutu ve bağımlılığı kopyalandı.
	bash lddscripts.sh /bin/rmdir /home/etapadmin/test/

.. image:: /_static/images/chroot-4.png
  :width: 600


.. raw:: pdf

   PageBreak
   
mkdir Komutu
------------

.. code-block:: shell

	# mkdir komutu ve bağımlılığı kopyalandı.
	bash lddscripts.sh /bin/mkdir /home/etapadmin/test/

.. image:: /_static/images/chroot-5.png
  :width: 600

bash Komutu
------------

.. code-block:: shell

	# bash komutu ve bağımlılığı kopyalandı.
	bash lddscripts.sh /bin/bash /home/etapadmin/test/

.. image:: /_static/images/chroot-6.png
  :width: 600


chroot Sistemde Çalışma
------------------------

.. code-block:: shell

	sudo chroot /home/etapadmin/test komutunu kullanmalıyız.

.. image:: /_static/images/chroot-7.png
  :width: 600

- **abc** dizini oluşturuldu, **abc** dizini silindi, **pwd** komutuyla konum öğrenildi, **ldd** komutu sistemimizde olmadığından hata verdi.
- Çıkış için ise **exit** komutu kullanılarak sistemden çıkıldı.

Kaynak:
https://stackoverflow.com/questions/64838052/how-to-delete-n-characters-appended-to-ldd-list
https://app.diagrams.net/

.. raw:: pdf

   PageBreak




**Kaynak Kod Derleme**
++++++++++++++++++++++

Bir uygulamanın kodları genellikle çalışmaz(python benzeri kodlar istisna). Bu kodlardan sistemlerin çalışması için çalışabilir dosyalar üretilir(linuxta ikili dosya, elf, windowsta exe, com vb.). Bu çalışabilir dosyaları koddan oluştururken iki faklı şekilde oluşturabiliriz.

1- **Paylaşımlı Derleme(dynamic):** Kendine lazım olan kütüphaneleri sistem üzerindeki başka uygulamalarla ortak kullanır. 
2- **Paylaşımsız, gömülü(static):** Kendisine lazım olan kütütphaneleri kendi içinde barındırır(porable uygulama gibi).

Şimdi aşağıdaki kaynak kodumuzu iki farklı yöntemle derleyelim.

.. code-block:: C

	//main.c dosyamız
	#include <stdio.h>
	void main(){
	    printf("Merhaba\n");
	}


**2-Paylaşımlı Derleme(dynamic):** 
--------------------------------

Derlenen uygulama  sistemde bulunan kütüphaneleri kullanacak şeklide derlenmesidir. Uygulama boyutu küçüktür, taşınabirliği sınırlanabilir.
Aşağıdaki gibi derlenir.

.. code-block:: shell

	gcc -o main main.c

main.c kodumuzu **main** adında ikili çalışabilir dosyaya dönüşütürdük. **ldd** komutuyla **main** dosyasının kullandığı kütüphaneler öğrenilir.

.. code-block:: shell

	unset LD_PRELOAD
	ldd ./main 
		linux-vdso.so.1 (0x00007ffdb3bb9000)
		libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007f2c53fe0000)
		/lib64/ld-linux-x86-64.so.2 (0x00007f2c541e7000)


Burada **libc.so.6** ve **ld-linux-x86_64.so.2** dosyaları **glibc** tarafından sağlanır. 
Derlenmiş dosyanın çalışması için tüm bağımlılıklarının sistemde bulunması gereklidir.Sadece gerekli olan kütüphaneleri görmek için   **readelf -d** komutu kullanılabilir. Aşağıda gerekli olan kütüphaneler listeleniyor.
 
.. code-block:: shell

	readelf -d ./main | grep -i needed 
		0x0000000000000001 (NEEDED)             Paylaşımlı kitaplık: [libc.so.6]
		
.. raw:: pdf

   PageBreak


**Bağımlı Olan Dosyaların İncelenmesi**
---------------------------------------

ldd çıktımızda görünen kütüphaneler(linux-vdso.so.1, libc.so.6,/lib64/ld-linux-x86-64.so.2)  **main** uygulamamızın çalışması için gerekli kütüphanelerdir. Bu dosyalara detaylandırarak inceleyelim.

**interpreter Kavramı**
.......................

libc.so.6 ve ld-linux-x86-64.so.2 glibc kütüphanesinde bulunan dosyalardır. Bu dosyalardan libc.so.6 temel C kütüphanesidir. ld-linux-x86-64.so.2 ise interpreter olup dosyanın ne şekilde çalıştırılacağını belirler. Bir dosyanın hangi interpreter ile çalıştığını bulmak için file komutuyla görebiliriz. Aşağıdaki file çıktısında **interpreter** **/lib64/ld-linux-x86-64.so.2** olduğunu görüyoruz. linux-vdso.so.1 ise kernel tarafından sağlanır ve herhangi bir dosya şeklinde bulunmaz.

.. code-block:: shell

	file ./main 
	./main: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, 		
	BuildID[sha1]=73d16d408e961200d876f1838a6b7645f64a29df, for GNU/Linux 3.2.0, not stripped

**LD_LIBRARY_PATH**
-------------------

Derlenmiş bir dosyanın bağımlılığı genellikle sistemde kurulu bulunmalıdır. Bazen farklı konumda özel bir kütüphane gerekebilir. Bu durumlarda LD_LIBRARY_PATH çevresel değişkenini kullanarak konum belirtilir.

.. code-block:: shell

	ldd main
	linux-vdso.so.1 (0x00007ffdb3bb9000)
	libmain.so => not found
	libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007f2c53fe0000)
	/lib64/ld-linux-x86-64.so.2 (0x00007f2c541e7000)

**libmain.so** dosyası sistemdeki yeri bilinmediğinden hata aldık. Şimdi **LD_LIBRARY_PATH** ile konumunu belirtelim, tekrar deneyelim.

.. code-block:: shell

	export LD_LIBRARY_PATH=/home/abc/main/libs/
	ldd main
	linux-vdso.so.1 (0x00007ffdb3bb9000)
	libmain.so => /home/abc/main/libs/libmain.so (0x00007f92ed6cb000)
	libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007f2c53fe0000)
	/lib64/ld-linux-x86-64.so.2 (0x00007f2c541e7000)

ldd çıktımızda tüm kütüphanelerin bulunduğu görülmektedir.

**ldconfig**
------------

Sistemdeki kütüpkhanelerin konumlarını **/etc/ld.so.conf** dosyasına bakarak belirler. 

.. code-block:: shell
	
	#/etc/ld.so.conf dosyası
	/usr/lib64
	/usr/lib
	/lib64
	/lib

Kütüphanelerde değişiklik yapılmışsa ve hemen bu değişikliği sistemin görmesini istersek **ldconfig** komutu kullanılmalıdır.

**2-Paylaşımsız, gömülü(static):**
--------------------------------

Derlenen uygulama sistemde  bulunan ve çalışması için gerekli olan kütüphaneleri uygulama içine dahil eden bir derleme yöntemidir. Uygulamamızı static derlemek için  **-static** parametresi ekleyerek derlenir.

.. code-block:: shell

	gcc -o main main.c -static

Paylaşımlı(dynamic) derleme işleminde bağımlı olduğu dosyaları **ldd** komutunu kullanarak öğrenmiştik. Şimdi paylaşımsız derlediğimiz **main** dosyasında bağımğımlı olduğu kütüphaneleri kontrol ediyoruz.

.. code-block:: shell

	ldd main
	    not a dynamic executable

Bağımlı kütüphaneler yerine **not a dynamic executable** mesajı gördük. Bunun anlamı çalışması için hiçbir kütüphaneye ihtiyaç duymaz. Bu bir avantaj ve taşınabirliği artırır. Devevantajı ise boyutu büyük olur. İhtiyaca göre paylaşımlı veya paylaşımsız derleme tercih edilir.


.. raw:: pdf

   PageBreak




Derleme Araçları
++++++++++++++++

Linux sistemlerinde kodlarımızı derlemek  kullanılan uygulamalara derleme araçları denir. Birden fazla araç olsada  en temel derleme araçları **make**, **cmake**, **meson**, **python**.




**1-make**
++++++++++

make, yazılım geliştirme süreçlerinde sıkça kullanılan bir araçtır. Özellikle C ve C++ gibi dillerde projelerin derlenmesi ve yönetilmesi için kullanılır.

Aşağıdaki C kodumuzu(merhaba.c dosyası) make ile nasıl derleyeceğimizi anlatalım;

.. code-block:: C
	
	#include <stdio.h>
	int main(){
	    puts("Merhaba");
	    return 0;
	}


Makefile Nedir?
---------------

Makefile, make aracının nasıl çalışacağını belirten bir dosyadır. İçinde hedefler, bağımlılıklar ve komutlar bulunur. Örneğin, bir C programını derlemek için aşağıdaki gibi basit bir Makefile oluşturabilirsiniz. Makefile ve merhaba.c dosyası aynı konumda olmalıdır.

.. code-block:: shell

	CC=gcc
	CFLAGS=-I.
	all: program
	program: merhaba.o 
		$(CC) -o program merhaba.o
	merhaba.o: merhaba.c
		$(CC) -c merhaba.c $(CFLAGS)
	clean:
		rm -f *.o program

merhaba dosyasından **program** adında bir ikili dosya oluşturmak için aşağıdaki komutlar Makefile ve merhaba.c dosyasının olduğu konumda çalıştırılır.

.. code-block:: shell

	make
	make install

Genellikle Makefile dosyası olmaz. Onun yerine **configure.ac** dosyası olur. **configure.ac** dosyasından **Makefile** dosyası elde etmek için, öncelikle **autoconf** ve **automake** araçlarının sisteminizde kurulu olması gerekmektedir. 

**autoreconf -fvi** komutu çalıştırılıarak configure dosyamızı üretir.Bu araçlar, yapılandırma dosyalarınızı işleyerek gerekli **Makefile** dosyalarını oluşturmanıza yardımcı olur.

**configure** komutunun devamında **--prefix** dışında başka parametreleride olabilir. Bu paramatreleri "Read.me" dosyası içerisinde bulunabilir veya **configure --help** komutu kaynak kodların olduğu konumda kullanılarak görülebilir. Bu kaynak kod aşağıdaki gibi derlenir.

.. code-block:: shell

	$ autoreconf -fvi
	$ ./configure --prefix=/usr
	$ make
	$ make install 
	
.. raw:: pdf

   PageBreak


**2-cmake**
+++++++++++

CMake, projelerin derlenmesi ve yapılandırılması için kullanılan bir araçtır. Bir paketi CMake ile derlemek için genellikle aşağıdaki adımları izleriz:

    İlk olarak, projenin kök dizininde bir CMakeLists.txt dosyası oluşturun.
    Ardından, CMake komutunu kullanarak projeyi yapılandırın ve derleyin. Örneğin:

.. code-block:: shell

	mkdir compile_packages
	cd compile_packages
	cmake ..
	make

    Bu adımları takip ederek, CMake ile paketinizi başarıyla derleyebilirsiniz.

CMake'in esnekliği ve kullanım kolaylığı sayesinde paketlerin derlenmesi ve yapılandırılması oldukça kolay hale gelir.


Bu kaynak kod aşağıdaki gibi derlenir:

.. code-block:: shell

	mkdir compile_packages
	cd compile_packages
	cmake ..
	make
	make install
	


**3-meson**
+++++++++++

Meson, modern bir yapılandırma betik dili ve Ninja ise hızlı bir derleyici aracıdır. Bir paketi derlemek için öncelikle Meson ile yapılandırma dosyalarını oluşturmanız gerekir. Ardından, Ninja derleyici aracını kullanarak bu yapılandırmayı derleyebilirsiniz.

İlk olarak, projenizin dizinine gidin ve Meson ile yapılandırma dosyalarını oluşturun:

.. code-block:: shell

	meson setup builddir --prefix=/usr

Sonra, oluşturulan builddir dizinine geçin ve Ninja ile derlemeyi başlatın:

.. code-block:: shell

	ninja -C builddir

Bu adımları takip ederek Meson ve Ninja kullanarak paketinizi başarılı bir şekilde derleyebilirsiniz.



Bu kaynak kod aşağıdaki gibi derlenir:

.. code-block:: shell
	
	# paketin yükleneceği konum
	INSTALL_ROOT=/
	meson setup builddir --prefix=/usr
	ninja -C builddir
	INSTALL_ROOT=$INSTALL_ROOT ninja -C builddir install
	
.. raw:: pdf

   PageBreak


**4-python**
++++++++++++

Python ile paket derlemek için genellikle **setuptools** ve **distutils** gibi kütüphaneler kullanılır. Öncelikle, projenizin kök dizininde bir **setup.py** dosyası oluşturmanız gerekir. Bu dosya, paketin yapılandırmasını ve gereksinimlerini tanımlar.

Örnek bir setup.py dosyası aşağıdaki gibi olabilir:

.. code-block:: shell

	from setuptools import setup

	setup(
	    name='paket_adi',
	    version='1.0',
	    packages=['paket'],
	    install_requires=[
		'bağımlılık_paketi',
	    ],
	)

Ardından, terminalde projenizin bulunduğu dizine giderek aşağıdaki komutu çalıştırarak paketi derleyebilirsiniz:

.. code-block:: shell
	# yükleme konumu
	INSTALL_ROOT=/
	python3 -m compile_packages
	python3 -m installer --destdir="$INSTALL_ROOT" dist/*.whl

Bu komut, paketi dist klasörüne derleyecektir. Artık paketiniz hazır ve dağıtıma uygun hale gelmiştir.

.. raw:: pdf

   PageBreak


**BusyBox**
+++++++++++

**BusyBox**, https://busybox.net/about.html adresteki bilgilere göre birçok temel Unix aracını tek bir ikili dosya içinde sunan, küçük ve esnek bir programdır. Çoğunlukla **initramfs** sistemlerinde ve gömülü Linux dağıtımlarında tercih edilir. BusyBox ile komutlar şu şekilde çalıştırılabilir:

.. code-block:: shell

   busybox [komut]

Bir komutu doğrudan çalıştırabilmek için BusyBox’u o komut adıyla sembolik bağlamak mümkündür. Örneğin, **tar** komutunu BusyBox üzerinden çalıştırmak için:

.. code-block:: shell

   ln -s /bin/busybox ./tar
   ./tar

Burada busybox içindeki gömülü olan tar kullanmayı gördük. Aslında aklımaza gelen her komutun busybox içinde gömülü hali vardır. Ama bu tüm komutlar için ve tüm parametreleri için geçerli değildir. Busybox içindeki tüm komutların kısayolunu(sembolik bağı) eklemek için aşağıdaki komut kullanılır.

.. code-block:: shell

   busybox --install -s /bin

Derleme
-------

Gömülü sistem tasarımı veya **initramfs** içinde kullanılacak busybox **paylaşımsız(static)** derlenir. Bu şekilde derlendiğinde glibc kütüphanelerine ihtiyaç duymadan çalışacaktır. 

Şimdi busybox derlemek için https://busybox.net/ adresinden **stable** başlığı altındaki kaynak kodlarını indiriniz.

.. code-block:: shell
	
   # kaynak kod indirilir
   wget https://busybox.net/downloads/busybox-1.36.1.tar.bz2
   
   # indirilen dosya açılır
   tar -xvjf busybox-1.36.1.tar.bz2
   
   # açılan kaynak dosyalarının bulunduğu dizine geçilir
   cd busybox-1.36.1/

Şimdi kodlarımızı indirdik. derlemek için aşağıdaki komutları çalıştıralım.

.. code-block:: shell

   # varsayılan yapılandırmayı uygula
   make defconfig
   
   # static derleme yapacaksak  sed ile .config dosyasını düzenliyoruz.
   sed -i "s|.*CONFIG_STATIC_LIBGCC .*|CONFIG_STATIC_LIBGCC=y|" .config
   sed -i "s|.*CONFIG_STATIC .*|CONFIG_STATIC=y|" .config
   
   # derliyoruz
   make
   
   # Static derleme sonucu aşağıdaki gibi görünür.
   ldd /bin/busybox 
   özdevimli bir çalıştırılabilir değil

Derleme tamamlandığında, oluşturulan **busybox** ikili dosyası kaynak dizininde bulunur.

.. raw:: pdf

   PageBreak



OpenRC
++++++

Openrc sistem açılışında çalışacak uygulamaları çalıştıran servis yöneticisidir.

**Çalıştırılması**
------------------

Openrc servis yönetiminin çalışması için boot parametrelerine yazılması gerekmektedir.  
**/boot/grub.cfg** içindeki  
**linux /vmlinuz init=/usr/sbin/openrc-init root=/dev/sdax**  
olan satırda  
**init=/usr/sbin/openrc-init**  
yazılması gerekmektedir. Artık sistem openrc servis yöneticisi tarafından uygulamalar çalıştırılacak ve sistem hazır hale getirilecek.

**openrc Kullanımı**
--------------------

Servis etkinleştirip devre dışı hale getirmek için **rc-update** komutu kullanılır.  
Aşağıda **udhcpc** internet servisi örnek olarak gösterilmiştir.  
**/etc/init.d/** konumunda **udhcpc** dosyamızın olması gerekmektedir.

.. code-block:: shell

    # servis etkinleştirmek için
    rc-update add udhcpc boot
    # servisi devre dışı yapmak için
    rc-update del udhcpc boot
    # Burada udhcpc servis adı, boot ise runlevel adıdır.

Elle **/etc/runlevels/** altında bulunan **boot**, **default**, **nonetwork**, **shutdown**, **sysinit** dizinlerine  
**/etc/init.d/** dizininin altındaki dosyaları **ln** komutuyla kısayol yaparsak  
**rc-update add** komutunun yaptığı görevi yapmış oluruz.  
Kısayolu silersek **rc-update del** komutunun görevini yapmış oluruz.

**/etc/runlevels/** altında bulunan **boot**, **default**, **nonetwork**, **shutdown**, **sysinit** dizinler servis dosyalarımızın hangi sırayla çalışacağını belirleyen dizinlerdir.  
Mesela **boot** dizini ilk açılış sırasında çalışacak olan servis dosyalarının konulacağı dizindir.

Servisleri başlatıp durdurmak için ise **rc-service** komutu kullanılır.

.. code-block:: shell

    rc-service udhcpc start
    # veya şu şekilde de çalıştırılabilir.
    /etc/init.d/udhcpc start

Servislerin durumunu öğrenmek için **rc-status** komutu kullanılır. Ayrıca  
sistemdeki servislerin sonraki açılışta hangisinin başlatılacağını öğrenmek için  
parametresiz olarak **rc-update** kullanabilirsiniz.

.. code-block:: shell

    # şu an hangi servislerin çalıştığını gösterir
    rc-status
    # sonraki açılışta hangi servislerin çalışacağını gösterir
    rc-update

Sistemi kapatmak veya yeniden başlatmak için **openrc-shutdown** komutunu kullanabilirsiniz.

.. code-block:: shell

    openrc-shutdown -p 0     # kapatmak için
    openrc-shutdown -r 0     # yeniden başlatmak için

.. raw:: pdf

   PageBreak

**Servis Dosyası**
------------------

Openrc servis dosyaları basit birer **bash** betiğidir. Bu betikler **openrc-run** komutu ile çalıştırılır ve çeşitli fonksiyonlardan oluşabilir.  
Servis dosyaları **/etc/init.d** içerisinde bulunur.  
Servisleri ayarlamak için ise **/etc/conf.d** içerisine aynı isimle ayar dosyası oluşturabiliriz.

Çalıştırılacak komut, komut parametreleri ve **pidfile** dosyamızı aşağıdaki gibi belirtebiliriz.

.. code-block:: shell

    description="Ornek servis"
    command=/usr/bin/ornek-servis
    command_args=--parametre
    pidfile=/run/ornek-servis.pid

Bununla birlikte **start**, **stop**, **status**, **reload**, **start_pre**, **stop_pre** gibi fonksiyonlar da yazabiliriz.

.. code-block:: shell

    start(){
        ebegin "Starting ${RC_SVCNAME}"
        start-stop-daemon --start --pidfile "/run/servis.pid" --exec /usr/bin/ornek-servis --parametre
    }

Servis bağımlılıklarını belirtmek için ise **depend** fonksiyonu kullanılır.

.. code-block:: shell

    depend() {
      need localmount
      after dbus
    }

.. raw:: pdf

   PageBreak



Qemu Kullanımı
++++++++++++++

qemu açık kaynaklı Virtual Box, Vmware benzeri sanallaştırma aracıdır. 

Sisteme Kurulum
---------------

.. code-block:: shell

    sudo apt update
    sudo apt install qemu-system-x86  qemu-utils

qemu Kullanımı
--------------
    
.. code-block:: shell

    # 30GB disk oluşturuldu.
    qemu-img create disk.img 30G
    qemu-system-x86_64 --enable-kvm -hda disk.img -m 2G -cdrom etahta.iso
    # qemu-system-x86_64 --enable-kvm -hda disk.img -m 2G #sadece disk ile çalıştırılıyor
    # qemu-system-x86_64 -m 2G -cdrom etahta.iso          #sadece iso dosyası ile çalıştırma

Sistem Hızlandırılması
----------------------

**--enable-kvm** eğer sistem disk ile çalıştırıldığında bu parametre eklenmezse yavaş çalışacaktır.

Boot Menu Açma
--------------

Sistemin diskten mi imajdan mı başlayacağını başlangıçta belirlemek için boot menu gelmesini istersek aşağıdaki gibi komut satırına seçenek eklemeliyiz.
    
.. code-block:: shell
    
    qemu-system-x86_64 --enable-kvm -cdrom distro.iso -hda disk.img -m 4G -boot menu=on  

Uefi kurulum için:
------------------

sudo apt-get install ovmf

qemu-system-x86_64 --enable-kvm -bios /usr/share/ovmf/OVMF.fd -cdrom distro.iso -hda disk.img -m 4G -boot menu=on   

qemu Host Erişimi:
------------------

İstemci bilgisayar ip'si:10.0.2.15 ve ana bilgisayar 10.0.0.2 olarak ayarlıyor.

vmlinuz ve initrd
-----------------
qemu ile vmlinuz ve initrd.img dosyaları iso olmadan test edilebilir.

.. code-block:: shell

    qemu-system-x86_64 --enable-kvm -kernel /boot/vmlinuz-5.17 -initrd /home/deneme/initrd.img -append "quiet" -m 512m

qemu Terminal Yönlendirmesi
----------------------------

.. code-block:: shell
    
    qemu-system-x86_64 --enable-kvm -kernel vmlinuz -initrd initrd.img -m 3G -serial stdio -append "console=ttyS0"

Diskteki Sistemin Açılışını Terminale Yönlendirme
-------------------------------------------------

.. code-block:: shell
    
    qemu-system-x86_64 -nographic -kernel boot/vmlinuz -hda disk.img -append console=ttyS0

Kaynak:
| https://www.ubuntubuzz.com/2021/04/how-to-boot-uefi-on-qemu.html  

.. raw:: pdf

   PageBreak


Live Sistem Oluşturma
+++++++++++++++++++++

Canlı sistem oluşturma veya RAM üzerinden çalışan sistem hazırlamak için SquashFS dosya sisteminde dağıtım sıkıştırılmalıdır.  
SquashFS, Linux işletim sistemlerinde sıkıştırılmış bir dosya sistemidir. Sistemimizi sıkıştırır ve ardından salt okunur bir dosya sistemine dönüştürür.

SquashFS Oluşturma
------------------

.. code-block:: shell

    # mksquashfs input_source output/filesystem.squashfs -comp xz -wildcards 
    mksquashfs initrd $HOME/distro/filesystem.squashfs -comp xz -wildcards


Cdrom Erişimi
-------------

Cd veya Dvd aygıtı Linux sistemlerinde /dev/sr0 aygıt dosyası olarak erişilir.  
Cd içeriği üzerinde okuma yapmak için aşağıdaki komutu kullanabiliriz.

.. code-block:: shell

    cat /dev/sr0

Cdrom Bağlama
-------------

.. code-block:: shell

    mkdir cdrom
    mount /dev/sr0 /cdrom

Bu işlem sonucunda cdrom bağlanmış olacaktır. ISO dosyamızın içerisine erişebiliriz.

Squashfs Dosyasını Bulma
------------------------

Genellikle isoların içine squashfs dosyası oluşturulur. Bu sayede live yükleme yapılabilir.  
Örneğin, /live/filesystem.squashfs imaj dosyalarında konumudur.

Squashfs Bağlama
----------------

Squashfs dosyasını bağlamadan önce loop modülünün yüklü olması gerekmektedir. Eğer yüklemediyseniz;

.. code-block:: shell

    # loop modülü yüklenir.
    modprobe loop 
    mkdir canli
    mount -t squashfs -o loop cdrom/live/filesystem.squashfs /canli

Squashfs Sistemine Geçiş
------------------------

Yukarıdaki adımlarda squashfs dosyamızı /canli adında dizine bağlamış olduk.  
Bu aşamadan sonra sistemimizin bir kopyası olan squashfs canlıdan erişilebilir veya sistemi buradan başlatabiliriz.

Squashfs dosya sistemimize bağlanmak için;

.. code-block:: shell

    chroot canli /bin/bash

Bu işlemin yerine exec komutuyla bağlanırsak sistemimiz id "1" değeriyle çalıştıracaktır.  
Eğer sistemin bu dosya sistemiyle açılmasını istiyorsak exec ile çalıştırıp id=1 olmasına dikkat etmeliyiz.

.. raw:: pdf

   PageBreak


**kmod Nedir?**
+++++++++++++++

Linux çekirdeği ile donanım arasındaki haberleşmeyi sağlayan kod parçalarıdır. Bu kod parçalarını kernele eklediğimizde kerneli tekrardan derlememiz gerekmektedir. Her eklenen koddan sonra kernel derleme, kod çıkarttığımzda kernel derlemek ciddi bir iş yükü ve karmaşa yaratacaktır.

Bu sorunların çözümü için modul vardır. moduller kernele istediğimiz kod parpalarını ekleme ya da çıkartma yapabiliyoruz. Bu işlemleri yaparken kenel derleme işlemi yapmamıza gerek yok.

Kernele modul yükleme kaldırma için kmod aracı kullanılmaktadır. kmaod aracı;

	.. code-block:: shell

		ln -s kmod /bin/depmod
		ln -s kmod /bin/insmod
		ln -s kmod /initrd/bin/lsmod
		ln -s kmod /bin/modinfo
		ln -s kmod /bin/modprobe
		ln -s kmod /bin/rmmod

şeklinde sembolik bağlarla yeni araçlar oluşturulmuştur.

**lsmod :** yüklü modulleri listeler

**insmod:** tek bir modul yükler

**rmmod:** tek bir modul siler

**modinfo:** modul hakkında bilgi alınır 

**modprobe:** insmod komutunun aynısı fakat daha işlevseldir. module ait bağımlı olduğu modülleride yüklemektedir. modprobe  modülü /lib/modules/ dizini altında aramaktadır.

**depmod:** /lib/modules dizinindeki modüllerin listesini günceller. Fakat başka bir dizinde ise basedir=konum şeklinde belirtmek gerekir. konum dizininde /lib/modules/** şeklinde kalsörler olmalıdır.

.. raw:: pdf

   PageBreak


**strip**
+++++++++

strip komutu, derlenmiş program veya paylaşılan kütüphanelerin dosya boyutunu küçültmek için kullanılır. Derleme sırasında eklenen gereksiz sembol ve hata ayıklama bilgilerini kaldırarak dosyayı küçültür.

strip komutunu kullanmak için terminalde şu komutu yazabilirsiniz:

.. code-block:: shell

    strip dosya_adı

Burada "dosya_adı", boyutu azaltılacak dosyanın adıdır. Örneğin:

.. code-block:: shell

    strip program

Bu komut, özellikle Linux ve Unix sistemlerinde yaygın kullanılır. Dosya boyutunu küçülterek disk alanı tasarrufu sağlar ve programların dağıtımı için uygundur.

Ancak, hata ayıklama veya sembol bilgilerine ihtiyaç duyduğunuz durumlarda strip komutunu kullanmamanız gerekir.

Özetle, strip komutu derlenmiş dosyaların gereksiz bilgilerini temizleyerek boyutlarını azaltan basit ve etkili bir Linux aracıdır.

.. raw:: pdf

   PageBreak


**Kullanıcı Ekleme**
++++++++++++++++++++

linux sistemlerine kullanıcı eklemek için iki farklı komut bulunur. Bu komutlar adduser ve useradd komutlarıdır.


**adduser:**
------------

Kullanıcı dostu bir arayüz sunar. Birçok aşamayı bizim adımıza yapar. Temelde useradd komutunu kullanarak yazılan bir script olarak düşünebiliriz.

.. code-block:: shell

	# adduser komutuyla kullanıcı oluşturma
	sudo adduser yeni_kullanici

**useradd:** 
------------

Kullanıcıdan tüm parametreleri girmesini ister.  Bu sebepten çok tercih edilmemektedir. Fakat özel bir şekilde kullanıcı oluşturulmak istenildiğinde tercih edilir. Bu dokümanda kurulum aşamalarında useradd komutu kullanıldı.


.. code-block:: shell

	# useradd komutuyla kullanıcı oluşturma
	sudo useradd -m -s /bin/bash yeni_kullanici -d /home/yeni_kullanici
	# -s/bin/bash : kullanıcının kullanacağı shell belirtiliyor.
	# -d /home/yeni_kullanici : home dizinine oluşturulacak kullanıcı dizini belirtiyoruz


.. raw:: pdf

   PageBreak

.. _githubbilgi:
**github**
++++++++++

GitHub üzerinde yeni bir depo açmak oldukça basit bir işlemdir. Aşağıdaki adımları takip ederek hızlıca kendi deponuzu oluşturabilirsiniz:

- **GitHub Hesabınıza Giriş Yapın:** GitHub ana sayfasına gidin ve hesabınıza giriş yapın. Eğer bir hesabınız yoksa, öncelikle bir hesap oluşturmalısınız.

- **Yeni Depo Oluşturma:** Sağ üst köşede bulunan "+" simgesine tıklayın ve "New repository" seçeneğini seçin.

- **Depo Bilgilerini Girin:** Açılan sayfada, depo adını (repository name) ve isteğe bağlı olarak bir açıklama (description) girin. Depo özel (private) veya herkese açık (public) olarak ayarlanabilir.

- **İlk Dosyayı Oluşturma:** "Initialize this repository with a README" seçeneğini işaretleyerek, depo oluşturulduğunda otomatik olarak bir README dosyası oluşturabilirsiniz.

- **Depoyu Oluşturma:** "Create repository" butonuna tıklayarak deponuzu oluşturun.

Artık GitHub üzerinde yeni bir deponuz var! Bu depoyu yerel bilgisayarınıza klonlayarak projelerinizi yönetmeye başlayabilirsiniz. Örneğin, terminalde şu komutu kullanarak deponuzu klonlayabilirsiniz:


.. code-block:: shell

	git clone https://github.com/kullaniciadi/depoadi.git

Bu adımları takip ederek GitHub üzerinde kolayca depo açabilirsiniz.

.. raw:: pdf

   PageBreak

**X11 Kullanıcısının Tespiti**
++++++++++++++++++++++++++++++

Linux ortamında masaütündeyken sudo ile script çalıştırıldığında masaütünü açtığımız kullanıcının tespiti aşağıdaki kodla yapılabilir.

.. code-block:: shell

	#!/bin/bash

	# Detect the name of the display in use
	display=":$(ls /tmp/.X11-unix/* | sed 's#/tmp/.X11-unix/X##' | head -n 1)"

	# Detect the user using such display
	user=$(who | grep '('$display')' | awk '{print $1}')

	# Detect the id of the user
	uid=$(id -u $user)

	echo $user $uid
	
	
.. raw:: pdf

   PageBreak



.. _yardimcikonular:
Yardımcı Konular
================

.. _kaynaklar:
**Kaynaklar**
=============================
.. toctree::
	:glob:

.. code-block:: shell

	- https://tr.wikipedia.org/wiki/Linux
	- https://chatgpt.com/
	- https://stackoverflow.com/questions/64838052/how-to-delete-n-characters-appended-to-ldd-list
	- https://app.diagrams.net/
	- https://www.ubuntubuzz.com/2021/04/how-to-boot-uefi-on-qemu.html
	- https://wiki.gentoo.org/wiki/OpenRC
	- https://busybox.net/
	- https://busybox.net/about.html
	- https://sulincix.gitlab.io/distro-kitabi/
	- https://gitlab.com/turkman/devel/doc/wiki/
	- https://turkman.gitlab.io/devel/doc/wiki/
	- 



**Not:** Metin düzenlemelerinde chatgpt kullanılmıştır.


.. raw:: pdf

   PageBreak

.. _gelistiricimesaji:
**Geliştiricilere Mesajımız**
=============================
.. toctree::
	:glob:


Gnu/Linux, açık kaynaklı bir işletim sistemidir. Kullanıcı ve geliştiriclere bir çok avantajlar sunmaktadır. Bunlar;

- Kodlarına erişilebilir(Açık Kaynak)
- Dağıtılabir
- Değiştirilebilir
- Virüsten etilenme azdır
- Özelleştirilebilir
- Güvenlik en önemli şarttır
- Düşük donanımlarda iyi performan verir
- Bağımlılığı azaltır

Bu özellikleri açısından Gnu/Linux tercih etmek çok avantajlıdır. Geliştirme aşamalarına destek vermek, öğrenmek bize, toplumumuza ve ülkemize sayısız faydalar saylayacaktır.

.. image:: /_static/images/contact.svg
	:width: 150
  		
- https://github.com/kendiliuxunuyap
- kendiliuxunuyap@gmail.com


.. raw:: pdf

   PageBreak

.. toctree::
	:glob:


Kendi Linux'unu Yap
===================

Bu dokumanda dağıtım hazırlamak için temel işlemler anlatılmaktadır.

Bu kitap, açık kaynak ve özgür yazılıma gönül vermiş kişilerin, Türkçe kaynak bulamama sıkıntısına bir çözüm olarak hayata geçirilmiş bir projedir. Açık kaynak dünyasında kendi dağıtımlarını yapmak isteyen kişilere bir rehber olacak şekilde hazırlanmıştır. Bu dokümanda anlatılan sıralamaya göre işlemleri uyguladığınızda kendi sisteminiz derleyip iso halinde son kullanıcını kullanabileceği gibi bir sistem ortaya çıkartabilirsiniz. 


Kaynak ve dokümanlarımız yansılarımız:

* Bu sitedeki bilgilerin pdf kitap hali için `tıklayınız. <https://kendilinuxunuyap.github.io/kitap/>`_


.. image:: /_static/logo.png
  :width: 600
  :align: center

.. raw:: pdf

   PageBreak

**Yazar**
+++++++++
- Bayram KARAHAN
- Celalettin AKARSU

**Paket Derleme**
+++++++++++++++++
- Bayram KARAHAN
- Celalettin AKARSU


**İletişim**
++++++++++++

- https://github.com/kendilinuxunuyap
- https://kendilinuxunuyap.github.io
- kendilinuxunuyap@gmail.com


.. raw:: pdf

   PageBreak

Ön Söz
======


Bu kitap, açık kaynak ve özgür yazılım dünyasına ilgi duyan herkes için hazırlanmıştır. Amacı, Türkçe kaynak eksikliğini gidermek ve kendi Linux dağıtımını oluşturmak isteyenlere yol göstermektir.

Bu serinin ilk kitabında, **Temel Linux Sistemi**'nin nasıl derlenip kullanılabilir hale getirileceği
anlatılmıştı. 

İkinci kitabında, oluşturduğumuz **Temel Linux Sistemi** üzerinde **X11 (grafik
ortamının)** nasıl derlenip çalıştırılacağı anlatıldı. 

Bu kitabımızda ise **X11 (grafik ortamının)** üzerine **LXDE** masaüstü ortmaının derlenmesi ve yüklenmesi anlatılmaktadır.

Bu kitap, LXDE masaüstü ortamının kaynaktan derlemek isteyen Linux kullanıcıları için kapsamlı bir rehber sunmayı amaçlamaktadır.  Ayrıca, bu süreç Linux sistemlerinin nasıl çalıştığını anlamak için harika bir öğrenme fırsatı sunar.

.. raw:: pdf

   PageBreak

İçindekiler
===========

.. list-table::
   :widths: 60 10

   * - 1- :ref:`temelkavramlar`
     - 5
   * - 2- :ref:`sistemhazirlanmasi`
     - 8
   * - 3- :ref:`paketderleme`
     - 18
   * - 4- :ref:`isohazirlama`
     - 100
   * - 5- :ref:`sistemcalistirma-inceleme`
     - 103
   * - 6- :ref:`xpenceresistemi`
     - 108
   * - 7- :ref:`yardimcikonular`
     - 110
   * - 8- :ref:`kaynaklar`
     - 147
   * - 9- :ref:`gelistiricimesaji`
     - 148
 
.. raw:: pdf

   PageBreak

.. footer:: ###Page###

.. toctree::

**Pencere Yöneticisi Nedir?**
=============================

Bir ``pencere yöneticisi`` (window manager), bir masaüstü sisteminde **kullanıcı ve uygulama pencereleri arasındaki etkileşimi yöneten** temel yazılımlardır. Kimi bağımsız çalışırken, kimileri tam masaüstü ortamlarının bir parçasıdır. Sistem kaynakları, kullanıcı deneyimi ve özelleştirme gereksinimlerine göre farklı türleri tercih edilebilir.

Temel Görevleri
---------------

1. **Pencere Oluşturma ve Kontrolü**
   - Uygulama pencerelerini oluşturur, kapatır, yeniden boyutlandırır ve taşır.
   - Pencerelerin hangi sırada ve hangi pencerenin önde olduğunu belirler (odak yönetimi).

2. **Çerçeve ve Dekorasyon Sağlama**
   - Pencerelere başlık çubuğu, kenarlık, simge durumuna küçültme, büyütme ve kapatma gibi kontroller ekler.
   - Bazı yöneticiler tema desteği ile görsel özelleştirme sunar.

3. **Düzenleme (Layout) Yönetimi**
   - Pencerelerin nasıl yerleşeceğini belirler:
   - **Stacking (Yığınlama):** Pencereler üst üste gelir (örnek: Openbox, XFWM).
   - **Tiling (Döşeme):** Pencereler ekranı böler, üst üste gelmez (örnek: i3, bspwm).
   - **Dynamic:** Hem stacking hem tiling yöntemlerini karıştırabilir (örnek: awesomewm).

4. **Fare ve Klavye Etkileşimi**
   - Pencereleri sürükleme, yeniden boyutlandırma gibi işlemleri fareyle yapmaya olanak tanır.
   - Kısayol tuşları ile pencere geçişi, kapatma, taşıma gibi işlemleri sağlar.

5. **Masaüstü Ortamı Entegrasyonu (isteğe bağlı)**
   - Bazı pencere yöneticileri bağımsız çalışırken (örneğin Fluxbox),bazıları masaüstü ortamlarının bir parçasıdır (örneğin GNOME → Mutter, KDE → KWin).

.. list-table:: Popüler Pencere Yöneticileri
   :header-rows: 1
   :widths: 15 15 40

   * - Adı
     - Türü
     - Açıklama
   * - Openbox
     - Stacking
     - Hafif ve özelleştirilebilir
   * - i3
     - Tiling
     - Klavye odaklı, minimal
   * - KWin
     - Stacking + efekt
     - KDE Plasma bileşeni
   * - Mutter
     - GNOME bileşeni
     - Modern kompozit WM
   * - XFWM4
     - XFCE bileşeni
     - Hafif ve geleneksel
   * - Fluxbox
     - Stacking
     - Minimalist, bağımsız


Kaynaklar
---------

- ArchWiki – Window Manager: https://wiki.archlinux.org/title/Window_manager
- Debian Wiki – WindowManagers: https://wiki.debian.org/WindowManager
- Gentoo Wiki – Window Managers: https://wiki.gentoo.org/wiki/Window_managers
- https://en.wikipedia.org/wiki/Window_manager

.. raw:: pdf

   PageBreak

**Linux Masaüstü Ortamları ve Pencere Yöneticileri**
====================================================

Bu belgede, yaygın olarak kullanılan bazı Linux masaüstü ortamları ve pencere yöneticileri tanıtılmaktadır.

***Openbox**
------------

``Openbox``, hafif ve son derece özelleştirilebilir bir *pencere yöneticisidir*. Kendi başına bir masaüstü ortamı değildir, ancak diğer bileşenlerle birlikte kullanılarak işlevsel bir masaüstü ortamı haline getirilebilir.

- Hafif yapısı ile düşük sistem kaynaklarında bile çalışır.
- Menü ve kısayol tuşları tamamen kullanıcı tarafından yapılandırılabilir.
- LXDE gibi hafif masaüstü ortamlarının bir parçası olarak da kullanılır.

**LXDE (Lightweight X11 Desktop Environment)**
----------------------------------------------

``LXDE``, düşük donanım kaynaklarına sahip sistemler için tasarlanmış hafif bir masaüstü ortamıdır.

- Ana pencere yöneticisi: ``Openbox``
- Hızlı ve düşük bellek kullanımı
- GTK2 üzerine inşa edilmiştir
- Geliştiricileri, daha modern bir yapı olan ``LXQt`` projesine yönelmiştir.

**XFCE**
--------

``XFCE``, hafifliği ve kullanıcı dostu arayüzüyle bilinen bir masaüstü ortamıdır.

- GTK tabanlıdır (GTK3)
- Panel, dosya yöneticisi (Thunar), ayarlar ve eklenti sistemi gibi bileşenlere sahiptir.
- Hem hafif hem de modern bir masaüstü deneyimi sunar.

**KDE Plasma**
--------------

``KDE``, tam özellikli ve görsel olarak zengin bir masaüstü ortamıdır. Günümüzde ``KDE Plasma`` olarak anılır.

- Qt kütüphanesi kullanılarak geliştirilmiştir.
- Geniş özelleştirme seçenekleri ve güçlü yerleşik uygulamalar (Dolphin, Konsole, KWin)
- Sistem kaynaklarını daha fazla kullanır, ancak son sürümler büyük ölçüde optimize edilmiştir.

**Cinnamon**
------------

``Cinnamon``, geleneksel masaüstü deneyimini korumayı hedefleyen modern bir ortamdır. ``Linux Mint`` tarafından geliştirilmiştir.

- GNOME 3'ün bir çatallanmasıdır, ancak klasik masaüstü düzenine sahiptir.
- GTK üzerine inşa edilmiştir.
- Windows benzeri menü ve panel yapısı sunar.

**GNOME**
---------

``GNOME``, modern ve basit bir masaüstü ortamıdır. Özellikle dokunmatik destekli ve geniş ekran cihazlar için optimize edilmiştir.

- GTK+ tabanlıdır.
- Minimalist tasarımıyla dikkat çeker (örneğin varsayılan olarak masaüstü simgeleri yoktur).
- Özellikle Ubuntu’nun varsayılan masaüstüdür.

Karşılaştırma Özeti
-------------------

.. list-table:: Popüler Linux Masaüstü Ortamları Karşılaştırması
   :header-rows: 1
   :widths: 15 15 15 15 10 10 10 10

   * - Ortam
     - Teknoloji
     - Hafiflik
     - Özellik
     - Panel
     - Menü
     - Tema
     - Uygulama
   * - Openbox
     - WM (X11)
     - Çok Hafif
     - Az
     - Hayır
     - Evet
     - Var
     - Yok
   * - LXDE
     - GTK2
     - Hafif
     - Orta
     - Evet
     - Evet
     - Var
     - Orta
   * - XFCE
     - GTK3
     - Orta
     - Orta
     - Evet
     - Evet
     - Var
     - Orta
   * - KDE Plasma
     - Qt
     - Ağır
     - Geniş
     - Evet
     - Evet
     - Çok
     - Geniş
   * - Cinnamon
     - GTK3
     - Orta-Ağır
     - Geniş
     - Evet
     - Evet
     - Çok
     - Geniş
   * - GNOME
     - GTK4
     - Ağır
     - Geniş
     - Hayır
     - Hayır
     - Az
     - Geniş

Kaynaklar
---------

- https://wiki.archlinux.org/title/Desktop_environment
- https://wiki.debian.org/DesktopEnvironment
- https://www.gnome.org/
- https://www.kde.org/
- https://www.linuxmint.com/

.. raw:: pdf

   PageBreak


.. _temelkavramlar:

**Temel Kavramlar**

Bir önceki kitabımızda **X Pencere Sistemini** oluşturmayı ve iso halinde kurulumu anlatmıştık.
Şimdi ise bu **X Pencere Sistemini** kurarak bu sistem üzerine **LXDE** araçları ve kütüphanelerini derleyerek **LXDE** masaüstü ortamının nasıl çalışacağı analatılacaktır. **X Pencere Sistemi** https://github.com/kendilinuxunuyap/kly-x11-distro/releases/download/current/kly-x11-distro.iso adresinde bulunmaktadır. İso indirip kurulum yapabilirsiniz.

**X Pencere Sistemi Kurulumu**
------------------------------

Sistemin kurulumu için resimlerde görünen sıraya göre seçimler yapmalıyız.

.. image:: /_static/images/iso-30.png
  :width: 600

.. image:: /_static/images/iso-31.png
  :width: 600

.. raw:: pdf

   PageBreak
   
Kurulum menüsünde kullanıcı adları ve parolaları, klayve varsayılan olarak;

- Kullanıcı: root	Parola: 1
- Kullanıcı: user1	Parola: 1
- Dil   	: tr_TR
- Klavye   	: trq

menüden değişiklik yapabilirsiniz. Değişiklik yapmadan sadece kurulum diskini ve disk bölümünü seçip Install(Yükle) işlemi yapabilirsiniz.


.. image:: /_static/images/iso-32.png
  :width: 600

.. image:: /_static/images/iso-33.png
  :width: 600


.. raw:: pdf

   PageBreak
   
**Sistemin Çalışması**
----------------------

Sistem kurulumu gerçekleştiğinde  sistem resimde görüldüğü gibi açılmalıdır.

.. image:: /_static/images/iso-40.png
  :width: 600

Sisteme **user1** (parola=1) kullanıcısı olarak giriş yapıldığı görülmektedir.

.. image:: /_static/images/x110.png
  :width: 600
  
**xinit** çalışınca **X Pencere Sistemine** geçiş yapılacak.

.. raw:: pdf

   PageBreak
   
**xinit** çalışınca **X Pencere Sistemi** aşağıdaki gibi açılacaktır.

.. image:: /_static/images/x111.png
  :width: 600
  
**X Pencere Sistemi** çalıştırılmış ve pencere yönetimini ve masaüstü ortamı için **openbox** çalıştırılıyor.

.. image:: /_static/images/x112.png
  :width: 600

**xcalc** uygulamasının çalıştırılması aşağıda gösterilmiştir.

.. image:: /_static/images/x113.png
  :width: 600

**X Pencere Sistemi** sistemi görüldüğü üzere çalışmaktadır. Artık **LXDE Masaüstü Ortamı** paketlerini ve bağımlılıklarını **kly Paket Sistemini** kullanarak derlenecek ve **X Pencere Sistemi** üzerine kurularak masaüstü ortamımızı çalışır hale getireceğiz.

.. raw:: pdf

   PageBreak

**Sistemin Internet Bağlantısı**
--------------------------------


**Temel Sistem** içerisinde bulunan **iproute2, dhclient, net-tools** paketleri derlendi ve açılışta **dhclient** aktif hale gelmektedir. Bu paket ile ağa dahil olunmaktadır.

Aşağıda atanan ip adresini görmekteyiz. Eğer ip adresi almamışsa terminalde **dhclient** komutunu çalıştırınız.

.. image:: /_static/images/internet.png
  :width: 600

.. raw:: pdf

   PageBreak

**Sisteme openssh ile Bağlanma**
--------------------------------

ssh terminal üzerinden uzak bilgisayarlara erişim yapan bir uygulamadır. **Temel Sistem** içerisinde ssh paketi derlendi ve açılışta aktif hale gelmektedir.

Aşağıda **ssh** ile erişimin nasıl yapıldığı görülmektedir.

.. image:: /_static/images/ssh.png
  :width: 600

Bu doküman boyunca paketleri **Debian** ortamında derleyeceğiz. Derlediğimiz paketleri **X Pencere Sistemi'ne** kopyalacağız. Kopyalama işlemini **ssh** paketi içinde gelen **sftp** veya **scp** ile yapacağız. Kopyalanan paketlerin **kurulması ve kaldırıması** gibi işlemleri **ssh** bağlantısı üzerinden gerçekleştireceğiz.

.. raw:: pdf

   PageBreak

**Sisteme sftp ile Bağlanma**
-----------------------------

**sftp** terminal veya pencere yöneticisi üzerinden uzak bilgisayarlara erişim yapan bir uygulamadır. **Temel Sistem** içerisinde **ssh** paketinin bir parçası olarak gelmektedir.

Aşağıda **sftp** ile erişimin nasıl yapıldığı görülmektedir.

.. image:: /_static/images/sftp1.png
  :width: 600

.. image:: /_static/images/sftp2.png
  :width: 600


.. raw:: pdf

   PageBreak

**Sisteme scp ile Dosya Kopyalama**
-----------------------------------

**scp** terminal üzerinden uzak bilgisayarlara dosya kopyalaması yapan bir uygulamadır. **Temel Sistem** içerisinde **ssh** paketinin bir parçası olarak gelmektedir.

Aşağıda **scp** ile **deneme** dosyasının nasıl kopyalandığı görülmektedir.

.. image:: /_static/images/scp.png
  :width: 600

.. raw:: pdf

   PageBreak

.. _sistemhazirlanmasi:
**X Pencere Sistemin Hazırlanması**
===================================

.. _giris:

**Ön Hazırlık**
---------------

Paket derleme işlemi öncesi aşağıdaki konuları bilmemiz gerekmektedir. Bunlar; 

1. Derleme(Dinamik/Static) 
2. chroot Kullanımı 
3. İso Oluşturma
4. ssh Kullanımı
5. sftp Kullanımı
6. scp Kullanımı
7. VirtualBox Kullanmı
8. cfdisk Kullanımı

Burada liste halinde verilen konu başlıkları bu dokümanın **Yardımcı Konular** bölümünde anlatılmaktadır. 

Bundan sonraki adımlarda kendi dağıtımımızın **LXDE masaüstü ortmaını** derleyerek **X Pencere Sistemi** üzerinde çalıştıracağız!


GNU Araçlarıyla **LXDE Masaüstü Ortamının** derleme işlemini **kly Paket Sistemi** kullanılarak derleyeceğiz. Derleme işlemini **kly -c** komutuyla yapacağız. Derlenen paketleri **scp** ve **sftp** kullanarak **Temel Sistem** üzerine kopyalayacağız. **kly -pi** komutumuzla kopyaladığımız paketi **X Pencere Sistemi** üzerine kuracağız. Oluşturduğumuz paketleri istersek github'a yükleyip. github üzerinden kururabiliriz.

.. raw:: pdf

   PageBreak


**LXDE Masaüstü Ortamı için Gerekli Paketler**
----------------------------------------------

.. list-table::
   :widths: 33 33 33

   * - 0- :ref:`giris`
     - 29- :ref:`libXfont`
     - 58- :ref:`cups`
   * - 1- :ref:`libfm`
     - 30- :ref:`libxkbcommon`
     - 59- :ref:`gdbm`
   * - 2- :ref:`menu-cache`
     - 31- :ref:`libxkbui`
     - 60- :ref:`mpdecimal`
   * - 3- :ref:`libfm-extra`
     - 32- :ref:`libxklavier`
     - 61- :ref:`libgusb`
   * - 4- :ref:`lxmenu-data`
     - 33- :ref:`libXpresent`
     - 62- :ref:`libisl`
   * - 5- :ref:`lxde-common`
     - 34- :ref:`libXres`
     - 63- :ref:`libmpc`
   * - 6- :ref:`lxappearance`
     - 35- :ref:`libxss`
     - 64- :ref:`duktape`
   * - 7- :ref:`lxinput`
     - 36- :ref:`libXtst`
     - 65- :ref:`atkmm`
   * - 8- :ref:`lxrandr`
     - 37- :ref:`libXv`
     - 66- :ref:`at-spi2-core`
   * - 9-  :ref:`lxsession`
     - 38- :ref:`libXvMC`
     - 67- :ref:`libtiff`
   * - 10- :ref:`lxpanel`
     - 39- :ref:`libXxf86dga`
     - 68- :ref:`libepoxy`
   * - 11- :ref:`lxtask`
     - 40- :ref:`libXxf86vm`
     - 69- :ref:`gobject-introspection`
   * - 12- :ref:`lxterminal`
     - 41- :ref:`tslib`
     - 70- :ref:`p11-kit`
   * - 13- :ref:`pcmanfm`
     - 42- :ref:`vte3`
     - 71- :ref:`nettle`
   * - 14- :ref:`lxlauncher`
     - 43- :ref:`xapp`
     - 72- :ref:`desktop-file-utils`
   * - 15- :ref:`lxhotkey`
     - 44- :ref:`xcb-util-cursor`
     - 73- :ref:`libidn2` 
   * - 16- :ref:`lxde-icon-theme`
     - 45- :ref:`xcb-util-errors`
     - 74- :ref:`locale-tr`
   * - 17- :ref:`libjpeg-turbo`
     - 46- :ref:`xcb-util-image`
     - 75- :ref:`hicolor-icon-theme`
   * - 18- :ref:`cairo`
     - 47- :ref:`xcb-util-keysyms`
     - 76- :ref:`polkit`
   * - 19- :ref:`gdk-pixbuf`
     - 48- :ref:`xcb-util-renderutil`
     - 77- :ref:`libjpeg62`
   * - 20- :ref:`gtksourceview4`
     - 49- :ref:`xcb-util-wm`
     - 78- :ref:`gpicview`
   * - 21- :ref:`hsakmt`
     - 50- :ref:`xtrans`
     - 79- :ref:`libdmx`
   * - 22- :ref:`libFS`
     - 51- :ref:`libkeybinder3`
     - 80- :ref:`lightdm`
   * - 23- :ref:`libnotify`
     - 52- :ref:`libexif`
     - 81- :ref:`lightdm-gtk-greeter`
   * - 24- :ref:`libvdpau`
     - 53- :ref:`gtk3`
     - 82- :ref:`libgpg-error`
   * - 25- :ref:`libwnck3`
     - 54- :ref:`shared-mime-info`
     - 83- :ref:`libgcrypt`
   * - 26- :ref:`libXaw3d`
     - 55- :ref:`lz4`
     - 84- 
   * - 27- :ref:`libXcomposite`
     - 56- :ref:`gnutls`
     - 85- 
   * - 28- :ref:`libXdamage`
     - 57- :ref:`lcms2`
     - 86- 


**Bağımlılık Zinciri**
----------------------

**LXDE** paketleri **gtk3** ile derlenecek. Bunun için ilk olarak **libfm** paketinin **gtk3** ile derlenmeli ve sonra mevcut sistemimize kurmalıyız. Sistemimize kurulduktan sonra **LXDE** paketlerini **gtk3** ile  derlenmeli. **libfm** ve **menu-cache** ilk kurulması gereken paketler. Paket derleme işlemine başlamadan önce, aşağıdaki temel araçları sisteminize kurmalısınız. ::

	sudo apt update
	sudo apt-get install debootstrap xorriso mtools make squashfs-tools gcc wget unzip xz-utils tar zstd fakeroot \
	autoconf automake autotools-dev make meson cmake ninja-build pkgconf patch libtool grub-pc grub-pc-bin
	
.. raw:: pdf

   PageBreak


.. _libfm:
**libfm**
===============

Menü tanımları ve veri dosyalarını içerir. Diğer bileşenlerin menü bilgilerini kullanabilmesi için öncelikle derlenmelidir.


**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="libfm"
	version="1.4.0"
	description="Library for file management"
	source="https://github.com/lxde/libfm/archive/${version}.tar.gz"
	depends="gtk3,pango,intltool,menu-cache"
	group="x11.libs"

	setup(){
		cd $SOURCEDIR

		autoreconf -fvi
		 ./configure --prefix=/usr \
		    --libdir=/usr/lib64/ \
		    --sysconfdir=/etc \
			--with-gtk=3 \
			--with-gnu-ld
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
	}


**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_

.. raw:: pdf

   PageBreak

.. _menu-cache:
**menu-cache**
==============

Menü tanımları ve veri dosyalarını içerir. Diğer bileşenlerin menü bilgilerini kullanabilmesi için öncelikle derlenmelidir.


**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="menu-cache"
	version="1.1.0"
	description="Caching mechanism for freedesktop.org compliant menus"
	source="https://github.com/lxde/menu-cache/archive/refs/tags/$version.tar.gz"
	depends="libfm-extra"
	group="lxde.base"

	setup(){
		mkdir -p /tmp/bps/build/patches
		cp ${dizin}/${paket}/patches/* /tmp/bps/build/patches/
		cd $SOURCEDIR
		patch -Np1 < ../patches/menu-cache-1.1.0-0001-Support-gcc10-compilation.patch
		autoreconf -fvi
		./configure --prefix=/usr \
		    --libdir=/usr/lib64/ 
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
	}

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_

.. raw:: pdf

   PageBreak

.. _libfm-extra:
**libfm-extra**
===============

Menü tanımları ve veri dosyalarını içerir. Diğer bileşenlerin menü bilgilerini kullanabilmesi için öncelikle derlenmelidir.


**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="libfm-extra"
	version="1.3.2"
	description="Library for file management"
	source="https://github.com/lxde/libfm/archive/refs/tags/${version}.tar.gz"
	depends="gtk3,pango,intltool,menu-cache"
	group="x11.libs"


	setup(){
		mkdir -p /tmp/bps/build/patches
		cp ${dizin}/${paket}/patches/* /tmp/bps/build/patches/
		cd $SOURCEDIR
		patch -Np1 -i ../patches/libfm-fixes.patch
		autoreconf -fvi
		 ./configure --prefix=/usr \
		    --libdir=/usr/lib64/ \
			  --with-gtk=3   \
			 --with-extra-only
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
	}

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_

.. raw:: pdf

   PageBreak

.. _lxmenu-data:
**lxmenu-data**
===============

Menü tanımları ve veri dosyalarını içerir. Diğer bileşenlerin menü bilgilerini kullanabilmesi için öncelikle derlenmelidir.


**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="lxmenu-data"
	version="0.1.5"
	description="Provides files needed for LXDE application menus"
	source="https://github.com/lxde/lxmenu-data/archive/refs/tags/$version.tar.gz"
	depends=""
	builddepend="intltool"
	group="lxde.base"


	setup(){
		cd $SOURCEDIR
		autoreconf -fvi
		./configure --prefix=/usr \
		    --sysconfdir=/etc
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
	}


**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _lxde-common:
**lxde-common**
===============

Ortak konfigürasyon dosyaları, tema ve temel altyapı öğelerini sağlar. LXDE'nin diğer bileşenleri için temel oluşturur.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="lxde-common"
	version="0.99.2"
	description="LXDE Session default configuration files and nuoveXT2 iconset "
	source="https://github.com/lxde/lxde-common/archive/refs/tags/$version.tar.gz"
	depends=""
	builddepend=""
	group="lxde.base"


	setup(){
		cd $SOURCEDIR
		autoreconf -fvi
		./configure --prefix=/usr \
		    --libdir=/usr/lib64/
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
	}


**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _lxappearance:
**lxappearance**
================

GTK temalarını ve simge setlerini yönetmek için kullanılan tema yapılandırma aracıdır.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="lxappearance"
	version="0.6.3"
	description="Feature-rich GTK+ theme switcher of the LXDE Desktop"
	source="https://downloads.sourceforge.net/lxde/$name-$version.tar.xz"
	depends="gtk3,dbus-glib"
	builddepend=""
	group="lxde.base"

	setup(){
		cp -prvf $PACKAGEDIR/00-gtk3-fix.patch /tmp/bps/build/
		cd $SOURCEDIR
		patch -Np1 -i ../00-gtk3-fix.patch
		./configure --prefix=/usr --enable-gtk3 \
		    --libdir=/usr/lib64/ \
		    --enable-dbus
		    
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
	}

Ek dosyaları indirmek için `tıklayınız. <https://kendilinuxunuyap.github.io/_static/files/lxappearance/files.tar>`_


**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


 
.. raw:: pdf

   PageBreak

.. _lxinput:
**lxinput**
===========

Fare ve klavye ayarlarının yapılandırılması için gerekli bileşendir.


**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="lxinput"
	version="0.3.5"
	description="LXDE keyboard and mouse configuration tool"
	source="https://downloads.sourceforge.net/lxde/lxinput-$version.tar.xz"
	depends="gtk3"
	builddepend="intltool"
	group="lxde.base"


	setup(){
		cd $SOURCEDIR
		autoreconf -fvi
		./configure --prefix=/usr \
		    --libdir=/usr/lib64/ \
		    --enable-gtk3 
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
	}


**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_

 
.. raw:: pdf

   PageBreak

.. _lxrandr:
**lxrandr**
===========


Ekran çözünürlüğü ve monitör yapılandırması için grafiksel arayüz sağlar. `xrandr` aracı üzerine kuruludur.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="lxrandr"
	version="0.3.2"
	description="Monitor configuration tool (part of LXDE)"
	source="https://downloads.sourceforge.net/lxde/lxrandr-$version.tar.xz"
	depends="gtk3,xrandr"
	builddepend="intltool"
	group="lxde.base"


	setup(){
		cd $SOURCEDIR
		autoreconf -fvi
		./configure --prefix=/usr \
			--enable-gtk3 \
			--enable-man \
		    --libdir=/usr/lib64/
	}

	build(){
		make DESTDIR=$DESTDIR
	}

	package(){
		make DESTDIR=$DESTDIR install
	}

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


 
.. raw:: pdf

   PageBreak

.. _lxsession:
**lxsession**
=============

LXDE oturum yöneticisi. Masaüstü oturumu başlatma ve yönetme işlevlerini üstlenir.


**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="lxsession"
	version="0.5.5"
	description="Lightweight X11 session manager"
	#source="https://downloads.sourceforge.net/lxde/lxsession-$version.tar.xz"
	source="https://salsa.debian.org/lxde-team/lxsession/-/archive/debian/$version-2/lxsession-debian-$version-2.tar.gz"
	depends="gtk3,polkit"
	builddepend="intltool,vala,docbook-xsl"
	group="lxde.base"


	setup(){
		cd $SOURCEDIR
		autoreconf -fvi
		./configure --prefix=/usr\
		    --sysconfdir=/etc \
		    --libexecdir=/usr/libexec \
		    --enable-gtk3 \
		    --enable-buildin-clipboard \
		    --libdir=/usr/lib64/ \
		    --enable-buildin-polkit
	}

	build(){
		make
	}

	package(){
		make  DESTDIR="$DESTDIR" install
		# Ignore package by AppStream to avoid duplicated IDs
		echo "X-AppStream-Ignore=true" >> "$DESTDIR/usr/share/applications/lxsession-default-apps.desktop"
		echo "X-AppStream-Ignore=true" >> "$DESTDIR/usr/share/applications/lxsession-edit.desktop"
	}

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


 
.. raw:: pdf

   PageBreak

.. _lxpanel:
**lxpanel**
===========

Görev çubuğu ve panel bileşeni. Menü, sistem tepsisi ve uygulama başlatıcıları gibi öğeleri yönetir.


**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="lxpanel"
	version="0.10.1"
	description="Lightweight X11 desktop panel for LXDE"
	source="https://downloads.sourceforge.net/lxde/lxpanel-$version.tar.xz"
	depends="libwnck3,wireless-tools,curl,alsa-lib,libwnck,"
	builddepend="intltool,docbook-xml,docbook-xsl,wireless_tools"
	group="lxde.base"


	setup(){
		cd $SOURCEDIR
		# Disable pager plugin as it breaks panel layout with GTK+ 3
		# https://sourceforge.net/p/lxde/bugs/773/
		sed -i "/pager.c/d" plugins/Makefile.am
		sed -i "/STATIC_PAGER/d" src/private.h
		sed -i "s/libwnck-3.0//" configure.ac
		sed -i "s/background=1/background=0/" data/default/panels/panel.in
		
		autoreconf -fvi
		./configure --prefix=/usr \
		    --libdir=/usr/lib64/ \
		    --enable-gtk3 \
		    --disable-silent-rules \
		    --with-plugins=all,-cpufreq
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
	}

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _lxtask:
**lxtask**
==========

Basit bir görev yöneticisidir. Sistem kaynaklarını ve çalışan işlemleri gösterir.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="lxtask"
	version="0.1.10"
	description="LXDE Task manager"
	source="https://github.com/lxde/lxtask/archive/refs/tags/$version.tar.gz"
	depends="gtk3"
	builddepend="intltool"
	group="lxde.base"


	setup(){
		cd $SOURCEDIR
		autoreconf -fvi
		./configure --prefix=/usr \
		    --libdir=/usr/lib64/ \
		    --enable-gtk3
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
	}

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _lxterminal:
**lxterminal**
==============

LXDE için terminal öykünücüsüdür. Terminal erişimi sağlar.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="lxterminal"
	version="0.4.0"
	description="Lightweight vte-based tabbed terminal emulator for LXDE"
	source="https://salsa.debian.org/lxde-team/lxterminal/-/archive/debian/$version-2/lxterminal-debian-$version-2.tar.gz"
	#source="https://downloads.sourceforge.net/lxde/lxterminal-$version.tar.xz"	
	depends="vte3,gtk3,dejavu"
	builddepend="intltool"
	group="lxde.base"


	setup(){
		cd $SOURCEDIR
		autoreconf -fvi
		./configure \
			--prefix=/usr \
		    --libdir=/usr/lib64/ \
		    --enable-gtk3 
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
	}

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _pcmanfm:
**pcmanfm**
===========

Dosya yöneticisi. Dosya gezintisi, masaüstü yönetimi ve simge gösterimi işlevlerini yerine getirir.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="pcmanfm"
	version="1.3.2"
	description="LXDE keyboard and mouse configuration tool"
	source="https://github.com/lxde/pcmanfm/archive/refs/tags/$version.tar.gz"
	depends="lxmenu-data,libfm,menu-cache,libkeybinder3"
	builddepend="intltool"
	group="lxde.base"


	setup(){
		cd $SOURCEDIR
		autoreconf -fvi
		./configure --prefix=/usr \
		    --libdir=/usr/lib64/ \
		    --with-gtk=3 
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
	}

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _lxlauncher:
**lxlauncher**
==============

Netbook tarzı uygulama başlatıcı. Menü verilerine dayanır.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="lxlauncher"
	version="0.2.5"
	description="Open source clone of the Asus launcher for EeePC"
	source="https://github.com/lxde/lxlauncher/archive/refs/tags/$version.tar.gz"
	depends="startup-notification,gtk3,menu-cache"
	builddepend="intltool"
	group="lxde.base"


	setup(){
		cd $SOURCEDIR
		autoreconf -fvi
		./configure --prefix=/usr \
		    --libdir=/usr/lib64/ \
		    --sysconfdir=/etc \
		    --enable-gtk3
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
	}

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


 
.. raw:: pdf

   PageBreak

.. _lxhotkey:
**lxhotkey**
============

Klavye kısayollarının yönetimi ve atanması için kullanılır.


**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="lxhotkey"
	version="0.1.1"
	description="LXDE hotkey"
	source="https://github.com/lxde/lxhotkey/archive/refs/tags/$version.tar.gz"
	depends="libfm"
	builddepend="libexif"
	group="lxde.base"


	setup(){
		cd $SOURCEDIR
		autoreconf -fvi
		./configure --prefix=/usr \
		    --libdir=/usr/lib64/ \
		    --with-gtk=3
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
	}

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


	 
.. raw:: pdf

   PageBreak

.. _lxde-icon-theme:
**lxde-icon-theme**
===================

Lxde ikon ve tema paketidir.


**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="lxde-icon-theme"
	version="0.5.1"
	description="LXDE default icon theme based on nuoveXT2"
	source="https://downloads.sourceforge.net/lxde/lxde-icon-theme-$version.tar.xz"
	depends=""
	builddepend=""
	group="lxde.base"


	setup(){
		cd $SOURCEDIR
		./configure --prefix=/usr \
		    --libdir=/usr/lib64/
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
	}

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


	 
.. raw:: pdf

   PageBreak

.. _libjpeg-turbo:
**libjpeg-turbo**
=================

JPEG görüntü kodek kütüphanesidir ve orijinal libjpeg kütüphanesinin hız odaklı bir çatalıdır. x86, x86-64, ARM ve PowerPC sistemlerde temel JPEG sıkıştırma ve açma işlemlerini hızlandırır.

**Paketi Derleme :**
--------------------

.. code-block:: bash

    #!/usr/bin/env bash
    name="libjpeg-turbo"
    version="3.0.3"
    description="MMX, SSE, and SSE2 SIMD accelerated JPEG library"
    source="https://github.com/libjpeg-turbo/libjpeg-turbo/archive/refs/tags/$version.tar.gz"
    depends=""
    group="media.libs"
    
    
    setup(){
        cd $SOURCEDIR
        mkdir build
        cd build
    
        cmake -DCMAKE_INSTALL_PREFIX=/usr \
            -DCMAKE_INSTALL_LIBDIR=/usr/lib64 \
            -DWITH_JPEG8=ON ..
    }
    
    build(){
        make
    }
    
    package(){
        make install DESTDIR=$DESTDIR
        mkdir -p $DESTDIR/lib64
        cd $DESTDIR/lib64
    ln -s ../usr/lib64/libjpeg.so.8 libjpeg.so.8.2.2
    }

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _cairo:
**cairo**
=========

2D vektör grafikleri çizimi için kullanılan açık kaynaklı bir kütüphanedir. Çizgiler, şekiller, metinler ve görüntüler gibi grafiksel öğeleri oluşturmak ve işlemek için platformdan bağımsız bir API sunar. Linux, Windows ve macOS gibi farklı platformlarda çalışır ve genellikle GTK+, Firefox gibi uygulamalarda kullanılır. Hafif, esnek ve yüksek kaliteli grafik çıktıları üretir.

**Paketi Derleme :**
--------------------

.. code-block:: bash

    #!/usr/bin/env bash
    name="cairo"
    version="1.18.0"
    description="A vector graphics library with cross-device output support"
    source="https://gitlab.freedesktop.org/cairo/cairo/-/archive/$version/cairo-$version.tar.gz"
    depends="pixman,libpng,glib,libpcre2,fontconfig,libX11"
    group="x11.libs"
    
    
    setup(){
    	cd $SOURCEDIR
    	meson setup $BUILDDIR --prefix=/usr \
            --libdir=/usr/lib64/ \
            -D b_lto=true \
            -D gtk_doc=false \
            -D spectre=disabled \
            -D symbol-lookup=disabled \
            -D tests=disabled
    }
    
    build(){
        ninja -C $BUILDDIR
    }
    
    package(){
        DESTDIR=$DESTDIR ninja -C $BUILDDIR install
    }

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _gdk-pixbuf:
**gdk-pixbuf**
==============

GTK+ kütüphanesinin bir parçası olan açık kaynaklı bir kütüphanedir ve 2D piksel tabanlı görüntü işleme için kullanılır. Görüntüleri yüklemek, kaydetmek, ölçeklendirmek, döndürmek ve manipüle etmek gibi işlemleri gerçekleştirir. PNG, JPEG, GIF gibi popüler görüntü formatlarını destekler.

**Paketi Derleme :**
--------------------

.. code-block:: bash

    #!/usr/bin/env bash
    name="gdk-pixbuf"
    version="2.42.10"
    description="gdk-pixbuf Image loading library for GTK+ "
    source="https://download.gnome.org/sources/gdk-pixbuf/${version%.*}/gdk-pixbuf-$version.tar.xz"
    depends="libjpeg-turbo,shared-mime-info,gi-docgen,libtiff,libpng,glib"
    group="x11.libs"
    
    
    setup(){
    	cd $SOURCEDIR
        meson setup $BUILDDIR --prefix=/usr \
            --libdir=/usr/lib64/ \
            -Db_lto=true \
            -D builtin_loaders=all \
            -Dman=false \
            -D installed_tests=false \
            -D tiff=enabled \
            -D introspection=enabled \
            -D tests=false
    
    }
    
    build(){
    	meson compile -C $BUILDDIR
        #ninja -C $BUILDDIR
    }
    
    package(){
    	DESTDIR="$DESTDIR" meson install -C $BUILDDIR
    
    }
    
Ek dosyaları indirmek için `tıklayınız. <https://kendilinuxunuyap.github.io/_static/files/gdk-pixbuf/files.tar>`_

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _gtksourceview4:
**gtksourceview4**
==================

GTK+ tabanlı uygulamalar için gelişmiş bir metin düzenleme bileşenidir. Kaynak kodu düzenleme, sözdizimi vurgulama, satır numaraları, otomatik girintileme gibi özellikler sunar. Programlama dilleri ve betik dosyaları için özelleştirilmiş düzenleme desteği sağlar. Hafif, esnek ve genellikle GNOME tabanlı editörlerde (ör. gedit) kullanılır.

**Paketi Derleme :**
--------------------

.. code-block:: bash

    #!/usr/bin/env bash
    name="gtksourceview4"
    version="4.8.4"
    description="A text widget adding syntax highlighting and more to GNOME"
    source="https://download.gnome.org/sources/gtksourceview/${version%.*}/gtksourceview-${version}.tar.xz"
    depends="gtk3,libxml2,gobject-introspection"
    group="x11.libs"
    
    
    setup(){
    	cd $SOURCEDIR
        meson setup $BUILDDIR --prefix=/usr \
            --libdir=/usr/lib64/ \
            -Db_lto=true \
            -Dgtk_doc=true
    }
    
    build(){
        ninja -C $BUILDDIR
    }
    
    package(){
        DESTDIR=$DESTDIR ninja -C $BUILDDIR install
    }

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_

    
.. raw:: pdf

   PageBreak

.. _hsakmt:
**hsakmt**
==========

AMD ROCm (Radeon Open Compute) platformunun parçası olan bir kütüphanedir. Kullanıcı modundan AMD HSA (Heterogeneous System Architecture) çekirdek sürücüsüyle (AMDKFD) iletişim kurmak için bir ara katman sağlar. GPU ve CPU arasındaki heterojen bilgi işlem işlemlerini destekler, özellikle Kaveri ve Carrizo APU'lar için optimize edilmiştir. Hafif ve açık kaynaklıdır.

**Paketi Derleme :**
--------------------

.. code-block:: bash

    #!/usr/bin/env bash
    name="hsakmt"
    version="1.0.0"
    description="Package hsakt"
    source="https://www.x.org/archive/individual/lib/hsakmt-$version.tar.gz"
    depends=""
    group="x11.libs"

    setup(){
        $SOURCEDIR/configure --prefix=/usr \
            --libdir=/usr/lib64/
    }
    
    build(){
        make
    }
    
    package(){
        make install DESTDIR=$DESTDIR
    }

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _libFS:
**libFS**
=========

X Window System'de yazı tipi sunucusu (font server) ile istemciler arasındaki iletişimi sağlayan bir kütüphanedir. X11 uygulamalarının uzak veya yerel yazı tipi sunucularından yazı tipi verilerine erişmesini sağlar. Hafif bir yapıya sahip olup, Xorg sistemlerinde yazı tipi yönetimini kolaylaştırır. Genellikle modern sistemlerde doğrudan kullanım yerine X sunucusuyla entegre çalışır.

**Paketi Derleme :**
--------------------

.. code-block:: bash

    #!/usr/bin/env bash
    name="libFS"
    version="1.0.9"
    description="X.Org FS library"
    source="https://www.x.org/archive/individual/lib/libFS-$version.tar.xz"
    depends="xorgproto"
    group="x11.libs"
    
    
    setup(){
        $SOURCEDIR/configure --prefix=/usr \
            --libdir=/usr/lib64/
    }
    
    build(){
        make
    }
    
    package(){
        make install DESTDIR=$DESTDIR
    }

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _libnotify:
**libnotify**
=============

Masaüstü bildirimlerini göstermek için kullanılan bir kütüphanedir. GNOME ve diğer masaüstü ortamlarında uygulamaların kullanıcıya geçici, pop-up tarzı bildirimler göndermesini sağlar. `Freedesktop.org'un bildirim şartnamesine <https://specifications.freedesktop.org/notification-spec/1.3/>`_ dayanır ve hafif, kullanımı kolay bir API sunar. Genellikle GTK+ uygulamalarıyla entegre çalışır.

**Paketi Derleme :**
--------------------

.. code-block:: bash

    #!/usr/bin/env bash
    name="libnotify"
    version="0.8.2"
    description="Library for sending desktop notifications"
    source="https://download.gnome.org/sources/libnotify/${version%.*}/libnotify-${version}.tar.xz"
    depends=""
    group="x11.libs"
    
    setup(){
    	cd $SOURCEDIR
        meson setup $BUILDDIR --prefix=/usr \
            --libdir=/usr/lib64/ \
            -Dgtk_doc=false     \
            -Dman=false \
    		-Ddefault_library=both
    }
    
    build(){
        ninja -C $BUILDDIR
    }
    
    package(){
        DESTDIR=$DESTDIR ninja -C $BUILDDIR install
    }

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _libvdpau:
**libvdpau**
============

NVIDIA'nın VDPAU (Video Decode and Presentation API for Unix) arayüzünü destekleyen bir kütüphanedir. Video oynatma ve kod çözme işlemlerini GPU üzerinden hızlandırmak için kullanılır. Linux sistemlerinde medya oynatıcılar ve uygulamalar tarafından donanım tabanlı video işleme için tercih edilir. Hafif ve açık kaynaklıdır, özellikle NVIDIA GPU'larla uyumludur.

**Paketi Derleme :**
--------------------

.. code-block:: bash

    #!/usr/bin/env bash
    name="libvdpau"
    version="1.5"
    description="VDPAU wrapper and trace libraries"
    source="https://gitlab.freedesktop.org/vdpau/libvdpau/-/archive/$version/libvdpau-$version.tar.gz"
    depends="libXext"
    group="x11.libs"
    
    
    setup(){
    	cd $SOURCEDIR
        meson setup $BUILDDIR --prefix=/usr \
            -Ddefault_library=both \
            --libdir=/usr/lib64 \
            -Ddri2=true
    }
    
    build(){
        ninja -C $BUILDDIR
    }
    
    package(){
        DESTDIR=$DESTDIR ninja -C $BUILDDIR install
    }

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _libwnck3:
**libwnck3**
============

GNOME masaüstü ortamı için kullanılan bir kütüphanedir. Uygulamaların açık pencereleri, çalışma alanlarını ve masaüstü görevlerini yönetmesini sağlar Pencere listeleme, değiştirme, simge durumuna küçültme gibi işlevler sunar. Hafif ve GTK+ tabanlı uygulamalarda sıkça kullanılır.

**Paketi Derleme :**
--------------------

.. code-block:: bash

    #!/usr/bin/env bash
    name="libwnck3"
    version="43.0"
    description="A window navigation construction kit "
    source="https://gitlab.gnome.org/GNOME/libwnck/-/archive/43.0/libwnck-43.0.tar.gz"
    depends="startup-notification"
    group="x11.libs"
    
    
    setup(){
    	cd $SOURCEDIR
    	meson setup $BUILDDIR --prefix=/usr \
            --libdir=/usr/lib64/ 
    }
    
    build(){
        ninja -C $BUILDDIR
    }
    
    package(){
        DESTDIR=$DESTDIR ninja -C $BUILDDIR install
    }

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _libXaw3d:
**libXaw3d**
============

X Window System (X11) için geliştirilmiş bir grafik kullanıcı arayüzü (GUI) kitaplığı olan X Athena Widgets (Xaw) kütüphanesinin 3 boyutlu (3D) görünümlü bir türevidir.

**Paketi Derleme :**
--------------------

.. code-block:: bash

    #!/usr/bin/env bash
    name="libXaw3d"
    version="1.6.4"
    description="X.Org Xaw3d library"
    source="https://www.x.org/archive/individual/lib/libXaw3d-$version.tar.gz"
    depends="libX11,libXt,libXmu,libXext"
    group="x11.libs"
    
    
    setup(){
        $SOURCEDIR/configure --prefix=/usr \
            --libdir=/usr/lib64/
    }
    
    build(){
        make
    }
    
    package(){
        make install DESTDIR=$DESTDIR
    }

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _libXcomposite:
**libXcomposite**
=================

X11 sisteminde pencere kompozisyonunu desteklemek için kullanılan bir yazılım kütüphanesidir. Pencerelerin içeriklerini ayrı ayrı bellek tamponlarında tutarak, bu pencerelerin birleşiminin yapılmasını sağlar. Şeffaflık, gölgeler, geçiş efektleri gibi gelişmiş görüntü özelliklerinin sağlanmasını mümkün kılar.

**Paketi Derleme :**
--------------------

.. code-block:: bash

    #!/usr/bin/env bash
    name="libXcomposite"
    version="0.4.6"
    description="X.Org Xcomposite library"
    source="https://gitlab.freedesktop.org/xorg/lib/libxcomposite/-/archive/libXcomposite-$version/libxcomposite-libXcomposite-$version.tar.gz"
    depends=""
    group="x11.libs"
    
    setup(){
    	cd $SOURCEDIR
    	autoreconf -fvi
        ./configure --prefix=/usr \
            --libdir=/usr/lib64/
    }
    
    build(){
        make
    }
    
    package(){
        make install DESTDIR=$DESTDIR
    }

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _libXdamage:
**libXdamage**
==============

Bir pencerenin hangi kısımlarının değiştiğini takip etmek kullanılır. Yani, bir pencere üzerinde sadece değişen (güncellenen) alanları bildirir. Bu sayede:

- Ekran kaydı (screen recording),
- Uzaktan masaüstü paylaşımı (VNC vs.),
- Compositing window manager'lar,
- GPU optimizasyonları,

gibi uygulamalarda sadece değişen pikselleri işleyerek performans kazancı sağlar.

**Paketi Derleme :**
--------------------

.. code-block:: bash

    #!/usr/bin/env bash
    name="libXdamage"
    version="1.1.6"
    description="X.Org Xdamage library"
    source="https://www.x.org/archive/individual/lib/libXdamage-$version.tar.xz"
    depends="libXfixes,libX11"
    group="x11.libs"
    
    
    setup(){
        $SOURCEDIR/configure --prefix=/usr \
            --libdir=/usr/lib64/
    }
    
    build(){
        make
    }
    
    package(){
        make install DESTDIR=$DESTDIR
    }

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _libXfont:
**libXfont**
============

X sunucusunun font (bitmap veya outline tabanlı) dosyalarını yüklemesini, analiz etmesini ve istemcilere sunmasını sağlar.X sunucusu ile istemciler arasındaki yazı tipi işlemlerini destekler, ancak doğrudan uygulamalar tarafından kullanılmaz. Genellikle X sunucusunun içinde veya onunla birlikte çalışan font sunucularında kullanılır.

**Paketi Derleme :**
--------------------

.. code-block:: bash

    #!/usr/bin/env bash
    name="libXfont"
    version="1.5.4"
    description="X.Org Xfixes library"
    source="https://www.x.org/archive/individual/lib/libXfont-$version.tar.gz"
    depends="libfontenc,freetype"
    group="x11.libs"
    
    
    setup(){
        $SOURCEDIR/configure --prefix=/usr \
            --libdir=/usr/lib64/
    }
    
    build(){
        make
    }
    
    package(){
        make install DESTDIR=$DESTDIR
    }

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _libxkbcommon:
**libxkbcommon**
================

Klavye tuşlarının hangi karaktere veya işlevlere karşılık geldiğini belirler. xkb (X Keyboard Extension) sistemini kullanarak klavye haritalarını işler. Klavye düzenlerinin yorumlanmasını ve yönetilmesini sağlar (örn. QWERTY, Dvorak, Türkçe Q, Türkçe F). Uygulamaların hangi tuşa hangi karakterin karşılık geldiğini anlamasına yardımcı olur.

Nerelerde Kullanılır:
---------------------

- Wayland tabanlı sistemlerde (örneğin GNOME Shell, KDE Plasma Wayland oturumları)
- Modern X11 uygulamalarında
- Toolkit'lerde: GTK, Qt, WLRoots, Weston
- Terminal emülatörleri ve kompozit pencere yöneticileri

**Paketi Derleme :**
--------------------

.. code-block:: bash

    #!/usr/bin/env bash
    name="libxkbcommon"
    version="1.7.0"
    description="keymap handling library for toolkits and window systems"
    source="https://github.com/xkbcommon/libxkbcommon/archive/refs/tags/xkbcommon-$version.tar.gz"
    depends="libxml2,libxcb,xkeyboard-config,wayland-protocols,wayland"
    makedepend="bison,wayland-protocols,wayland"
    group="x11.libs"
    
    setup(){
    cd $SOURCEDIR
        meson setup $BUILDDIR \
            --prefix=/usr \
            --libdir=/usr/lib64/ \
            --libexecdir=/usr/lib64/ \
            -Denable-docs=false \
            -Denable-wayland=true
    }
    
    build(){
        ninja -C $BUILDDIR 
    }
    
    package(){
        DESTDIR=$DESTDIR ninja -C $BUILDDIR install
    }

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _libxkbui:
**libxkbui**
============

X Keyboard Extension (XKB) kullanıcı arayüzü bileşenlerini sağlayan bir kütüphanedir.X11 sistemlerinde klavye düzeni ve davranışlarını kontrol eden bir sistemdir. **libxkbui**, bu sistemin bir parçası olan grafik kullanıcısı arayüzü öğelerini içerir. Özellikle XKB yapılandırma araçlarının GUI bileşenlerini sağlar (örneğin: xkbcomp, xkbutils, xkbselect, vs.).

**Paketi Derleme :**
--------------------

.. code-block:: bash

    #!/usr/bin/env bash
    name="libxkbui"
    version="1.0.2"
    description="Package libxkbui"
    source="https://www.x.org/archive/individual/lib/libxkbui-$version.tar.gz"
    depends="libX11,libXt,libxkbfile"
    group="x11.libs"
    
    
    setup(){
        $SOURCEDIR/configure --prefix=/usr \
            --libdir=/usr/lib64/
    }
    
    build(){
        make
    }
    
    package(){
        make install DESTDIR=$DESTDIR
    }

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _libxklavier:
**libxklavier**
===============

X11 sistemlerinde çalışan uygulamaların, sistemdeki klavye düzenlerini (keyboard layouts) ve XKB (X Keyboard Extension) yapılandırmalarını okumasına ve değiştirmesine imkan tanıyan bir kütüphanedir.

- Klavye düzenlerini (örneğin: Türkçe Q, ABD, Dvorak) listelemek, okumak, değiştirmek için bir API sunar.
- XKB altyapısını kullanır (X Keyboard Extension).
- GNOME ve diğer masaüstü ortamlarında klavye düzeni değiştirici araçlar tarafından kullanılır (örneğin: gnome-control-center, gsd-keyboard, lxde keyboard switcher).



**Paketi Derleme :**
--------------------

.. code-block:: bash

    #!/usr/bin/env bash
    name="libxklavier"
    version="5.4"
    description="High-level API for X Keyboard Extension"
    source="https://people.freedesktop.org/~svu/libxklavier-${version}.tar.bz2"
    depends="glib,iso-codes,libxml2"
    group="x11.libs"
    
    
    setup(){
    cd  $SOURCEDIR
    	autoreconf -fvi
        $SOURCEDIR/configure --prefix=/usr \
            --libdir=/usr/lib64/ \
    		--with-xkb-bin-base=/usr/bin \
          	--with-xkb-base=/usr/share/X11/xkb \
    		--enable-gtk-doc
    }
    
    build(){
        make
    }
    
    package(){
    #mkdir -p $DESTDIR/usr/share/X11/xkb
        make install DESTDIR=$DESTDIR $jobs
        mkdir -p $DESTDIR/usr/lib64/pkgconfig
        install $SOURCEDIR/libxklavier.pc $DESTDIR/usr/lib64/pkgconfig/libxklavier.pc
    
    }

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _libXpresent:
**libXpresent**
===============

X Present Extension'ın istemci tarafı API’sini sağlar. Bu eklenti, daha düzgün, yırtılmasız (tearing-free) grafik güncellemeleri için ekran sunumlarını (presentation) kontrol etmeye yarar.

Uygulamaların (özellikle oyunlar, video oynatıcılar, pencere yöneticileri) tam ekran veya pencere içi çizimlerini ekranla senkronize bir şekilde sunmalarını sağlar.

Bu, klasik X11 sistemlerinde sık görülen ekran yırtılması (tearing) sorununu azaltmaya yardımcı olur.

VSync benzeri işlevler için altyapı sağlar.

**Paketi Derleme :**
--------------------

.. code-block:: bash

    #!/usr/bin/env bash
    name="libXpresent"
    version="1.0.1"
    description="X Present Extension C Library"
    source="https://www.x.org/archive/individual/lib/libXpresent-$version.tar.xz"
    depends="libX11,xorgproto,libXext,libXfixes,libXrandr"
    group="x11.libs"
    
    
    setup(){
        $SOURCEDIR/configure --prefix=/usr \
            --libdir=/usr/lib64/
    }
    
    build(){
        make
    }
    
    package(){
        make install DESTDIR=$DESTDIR
    }

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _libXres:
**libXres**
===========

X sunucusundaki kaynak (resource) kullanımını izlemek için kullanılır.

Özellikle her X11 istemcisinin, ne kadar grafik kaynağı kullanıyor, kaç pencere kaç grafik nesnesi oluşturuyor, hangi istemci ne kadar kaynak tüketiyor öğrenmeyi sağlar.

**Paketi Derleme :**
--------------------

.. code-block:: bash

    #!/usr/bin/env bash
    name="libXres"
    version="1.2.2"
    description="X.Org XRes library"
    source="https://www.x.org/archive/individual/lib/libXres-$version.tar.xz"
    depends="libX11,libXext,xorgproto"
    group="x11.libs"
    
    
    setup(){
        $SOURCEDIR/configure --prefix=/usr \
            --libdir=/usr/lib64/
    }
    
    build(){
        make
    }
    
    package(){
        make install DESTDIR=$DESTDIR
    }

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _libxss:
**libxss**
==========

X11 (X Window System) için geliştirilmiş, ekran koruyucu (screen saver) durumunu izlemeye ve kontrol etmeye yarayan bir kütüphanedir.

**Paketi Derleme :**
--------------------

.. code-block:: bash

    #!/usr/bin/env bash
    name="libxss"
    version="1.2.4"
    description="X11 Screen Saver extension library"
    source="https://xorg.freedesktop.org/releases/individual/lib/libXScrnSaver-${version}.tar.xz"
    depends="libXext,util-macros,xorgproto"
    group="x11.libs"
    
    
    
    setup(){
        autoreconf -fvi
        $SOURCEDIR/configure --prefix=/usr \
            --libdir=/usr/lib64/
    }
    
    build(){
        make
    }
    
    package(){
        make install DESTDIR=$DESTDIR
    }

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _libXtst:
**libXtst**
===========

Klavye ve fare girdilerini simüle etmek için kullanılır. Programların veya test otomasyonlarının, gerçek kullanıcı girişi olmadan fare hareketi, tıklama veya tuş vuruşu gibi eylemleri taklit etmesini sağlar. Ekran kayıt, otomasyon, uzaktan kumanda yazılımları tarafından yaygın kullanılır.

**Paketi Derleme :**
--------------------

.. code-block:: bash

    #!/usr/bin/env bash
    name="libXtst"
    version="1.2.4"
    description="X.Org Xlib-based client API for the XTEST & RECORD extensions library"
    source="https://www.x.org/archive/individual/lib/libXtst-$version.tar.xz"
    depends="libX11,libXext,xorgproto,libXi"
    group="x11.libs"
    
    
    setup(){
    	$SOURCEDIR/configure --prefix=/usr \
    		--libdir=/usr/lib64/
    }
    
    build(){
        make
    }
    
    package(){
        make install DESTDIR=$DESTDIR
    }

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _libXv:
**libXv**
=========

Video görüntüsünü donanım hızlandırmalı olarak X11 pencerelerine hızlıca çizmek için kullanılır. Video oynatıcılar veya medya uygulamalarının, video karelerini CPU yerine GPU ile doğrudan X11 penceresine aktarmasını sağlar. Böylece daha az CPU kullanımı, daha akıcı video oynatma ve daha düşük gecikme elde edilir.

**Paketi Derleme :**
--------------------

.. code-block:: bash

    #!/usr/bin/env bash
    name="libXv"
    version="1.0.12"
    description="X.Org Xv library"
    source="https://www.x.org/archive/individual/lib/libXv-$version.tar.xz"
    depends=""
    group="x11.libs"
    
    
    setup(){
        $SOURCEDIR/configure --prefix=/usr \
            --libdir=/usr/lib64/
    }
    
    build(){
        make
    }
    
    package(){
        make install DESTDIR=$DESTDIR
    }

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _libXvMC:
**libXvMC**
===========

Video oynatma sırasında video kod çözme işlemlerini donanım hızlandırmalı olarak yapmayı mümkün kılar. Bu, özellikle MPEG video kodeklerinde CPU yükünü azaltmak ve akıcı video oynatımı sağlamak için kullanılır. Yani, video oynatıcıların sadece görüntüyü göstermekle kalmayıp, kod çözme sürecinde GPU desteği almasını sağlar.

**Paketi Derleme :**
--------------------

.. code-block:: bash

    #!/usr/bin/env bash
    name="libXvMC"
    version="1.0.13"
    description="X.Org XvMC library"
    source="https://www.x.org/archive/individual/lib/libXvMC-$version.tar.xz"
    depends="libX11,libXext,libXv,xorgproto"
    group="x11.libs"
    
    
    setup(){
        $SOURCEDIR/configure --prefix=/usr \
            --libdir=/usr/lib64/
    }
    
    build(){
        make
    }
    
    package(){
        make install DESTDIR=$DESTDIR
    }

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _libXxf86dga:
**libXxf86dga**
===============

Uygulamaların, X sunucusunu atlayarak doğrudan grafik donanımına erişmesini sağlar. Bu sayede özellikle tam ekran uygulamalarda daha hızlı ve düşük gecikmeli grafik çizimi mümkün olur. CPU ve GPU arasında daha hızlı veri aktarımı sağlar.

**Paketi Derleme :**
--------------------

.. code-block:: bash

    #!/usr/bin/env bash
    name="libXxf86dga"
    version="1.1.6"
    description="X.Org Xxf86dga library"
    source="https://www.x.org/archive/individual/lib/libXxf86dga-$version.tar.gz"
    depends=""
    group="x11.libs"
    
    
    setup(){
        $SOURCEDIR/configure --prefix=/usr \
            --libdir=/usr/lib64/
    }
    
    build(){
        make
    }
    
    package(){
        make install DESTDIR=$DESTDIR
    }

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _libXxf86vm:
**libXxf86vm**
==============

X sunucusuna bağlı olarak çalışan uygulamaların, ekran çözünürlüğü, yenileme hızı, renk derinliği gibi video modlarını değiştirmesini sağlar. Tam ekran uygulamaların (özellikle oyunlar) dinamik olarak ekran modlarını değiştirmesi için kullanılır.  
Kullanıcı etkileşimi olmadan ekran çözünürlüğünü programlı değiştirebilir.

**Paketi Derleme :**
--------------------

.. code-block:: bash

    #!/usr/bin/env bash
    name="libXxf86vm"
    version="1.1.5"
    description="X.Org Xxf86vm library"
    source="https://www.x.org/archive/individual/lib/libXxf86vm-$version.tar.xz"
    depends=""
    group="x11.libs"
    
    
    setup(){
        $SOURCEDIR/configure --prefix=/usr \
            --libdir=/usr/lib64/
    }
    
    build(){
        make
    }
    
    package(){
        make install DESTDIR=$DESTDIR
    }

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _tslib:
**tslib**
=========

tslib paketi, özellikle TypeScript projelerinde kullanılan bir yardımcı (utility) kütüphanedir. TypeScript derleyicisinin (tsc) ürettiği JavaScript kodlarında kullanılan bazı yardımcı fonksiyonları içerir.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="tslib"
	version="1.22"
	description="Touchscreen Access Library"
	source="https://github.com/libts/tslib/releases/download/${version}/tslib-${version}.tar.xz"
	depends=""
	group="x11.libs"


	setup () {
		autoreconf -fvi
		$SOURCEDIR/configure --prefix=/usr \
			--libdir=/usr/lib64/
	}

	build () {
		make
	}

	package () {
		make DESTDIR="$DESTDIR" install $jobs
	}

 
**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _vte3:
**vte3**
========

vte3, GNOME Terminal gibi terminal emülatörlerinde kullanılan bir terminal widget'ıdır. GTK+ tabanlı uygulamalarda terminal öykünmesi sağlamak için kullanılır.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="vte3"
	version="0.76.2"
	description="vte Library providing a virtual terminal emulator widget"
	source="https://gitlab.gnome.org/GNOME/vte/-/archive/${version}/vte-${version}.tar.gz"
	depends="cairo,fribidi,gcc,gdk-pixbuf2,glib,glibc,gnutls,icu,lz4,pango,pcre2"
	builddepend="at-spi2-core,gi-docgen,git,gobject-introspection,gperf,gtk3,meson,vala"
	group="x11.libs"

	setup(){
	cd $SOURCEDIR
		meson setup $BUILDDIR --prefix=/usr \
			--libdir=/usr/lib64/ \
			-Db_lto=false \
			-Ddocs=false \
			-Dgtk3=true \
			-Dgtk4=false \
			-D_systemd=false 
	}

	build(){
		ninja -C $BUILDDIR
	}

	package(){
		DESTDIR=$DESTDIR ninja -C $BUILDDIR install
	}


**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _xapp:
**xapp**
========

xapp, Linux Mint tarafından geliştirilen ve GTK tabanlı uygulamalarda ortak işlevleri kolaylaştırmak için kullanılan bir yardımcı kütüphanedir.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="xapp"
	version="2.8.0"
	description="Common library for X-Apps project"
	source="https://github.com/linuxmint/xapp/archive/$version/xapp-${version}.tar.gz"
	depends="libdbusmenu,libgnomekbd,vala,py3-pygobject,make,gobject-introspection"
	group="x11.libs"


	setup(){
		cd $SOURCEDIR
		meson setup $BUILDDIR --prefix=/usr \
		    	--libdir=/usr/lib64/
	}


	build(){
		ninja -C $BUILDDIR
	}

	package(){
		DESTDIR=$DESTDIR ninja -C $BUILDDIR install
	}


**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _xcb-util-cursor:
**xcb-util-cursor**
===================

xcb-util-cursor, X11 pencere sistemi için kullanılan XCB (X C Binding) kütüphanesinin bir uzantısıdır. Özellikle fare (cursor) simgeleriyle çalışmak için geliştirilmiştir.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="xcb-util-cursor"
	version="0.1.4"
	description="X C-language Bindings sample implementations"
	source="https://www.x.org/releases/individual/xcb/xcb-util-cursor-${version}.tar.xz"
	depends="libxcb,xcb-util-image,xcb-util-renderutil,xorgproto"
	group="x11.libs"


	setup(){
		$SOURCEDIR/configure --prefix=/usr \
			--libdir=/usr/lib64 \
			--enable-shared \
			--enable-static \
			--disable-devel-docs \
			--without-doxygen
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
	}

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _xcb-util-errors:
**xcb-util-errors**
===================

XCB (X C Binding) kütüphanesi için geliştirilen bir yardımcı (utility) kütüphanedir ve X11 hatalarını (error) daha okunabilir şekilde raporlamak için kullanılır.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="xcb-util-errors"
	version="1.0.1"
	description="Package xcb-util-errors"
	source="https://www.x.org/archive/individual/lib/xcb-util-errors-$version.tar.xz"
	depends=""
	group="x11.libs"


	setup(){
		$SOURCEDIR/configure --prefix=/usr \
		    --libdir=/usr/lib64/
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
	}


**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


 
.. raw:: pdf

   PageBreak

.. _xcb-util-image:
**xcb-util-image**
==================

XCB (X C Binding) kütüphanesi için geliştirilmiş bir yardımcı modüldür ve X11 üzerinde görüntü (image) işleme işlerini kolaylaştırmak için kullanılır.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="xcb-util-image"
	version="0.4.1"
	description="X C-language Bindings sample implementations"
	source="https://www.x.org/releases/individual/xcb/xcb-util-image-${version}.tar.xz"
	depends="libxcb,xcb-util,xorgproto,util-macros"
	group="x11.libs"


	setup(){
		$SOURCEDIR/configure --prefix=/usr \
		    --libdir=/usr/lib64 \
		--enable-shared \
		--enable-static \
		--disable-devel-docs \
		--without-doxygen
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
	}

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _xcb-util-keysyms:
**xcb-util-keysyms**
====================

XCB (X C Binding) kütüphanesi için geliştirilen bir yardımcı modüldür ve klavye tuş kodları ile tuş sembolleri (keysyms) arasında çeviri yapmayı kolaylaştırır.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="xcb-util-keysyms"
	version="0.4.1"
	description="X C-language Bindings sample implementations"
	source="https://www.x.org/archive/individual/lib/xcb-util-keysyms-$version.tar.xz"
	depends=""
	group="x11.libs"


	setup(){
		$SOURCEDIR/configure --prefix=/usr \
			--libdir=/usr/lib64/
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
	}


**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


 
.. raw:: pdf

   PageBreak

.. _xcb-util-renderutil:
**xcb-util-renderutil**
=======================

xcb-util-renderutil, X11 sisteminde kullanılan bir yardımcı kütüphanedir ve XCB (X C Binding) adı verilen düşük seviyeli, modern bir X protokolü arayüzünün bir parçasıdır. Daha spesifik olarak, xcb-util-renderutil kütüphanesi, X11'in Render Extension (Render uzantısı) ile çalışmayı kolaylaştırmak için bazı yardımcı işlevler sağlar.

**Paketi Derleme :**
--------------------


.. code-block:: bash

	#!/usr/bin/env bash
	name="xcb-util-renderutil"
	version="0.3.10"
	description="X C-language Bindings sample implementations"
	source="https://www.x.org/releases/individual/xcb/xcb-util-renderutil-${version}.tar.xz"
	depends="libxcb,util-macros,xorgproto"
	group="x11.libs"


	setup(){
		$SOURCEDIR/configure --prefix=/usr \
		    --libdir=/usr/lib64 \
			--enable-shared \
			--enable-static \
			--disable-devel-docs \
			--without-doxygen
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
	}

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _xcb-util-wm:
**xcb-util-wm**
===============

XCB (X C Binding) için geliştirilen bir yardımcı kütüphanedir ve X11 pencere yöneticisi protokolleriyle çalışmayı kolaylaştırır.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="xcb-util-wm"
	version="0.4.2"
	description="X C-language Bindings sample implementations"
	source="https://www.x.org/archive/individual/lib/xcb-util-wm-$version.tar.xz"
	depends=""
	group="x11.libs"


	setup(){
		$SOURCEDIR/configure --prefix=/usr \
		    --libdir=/usr/lib64/
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
	}

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _xtrans:
**xtrans**
==========

xcb-util-wm, XCB tabanlı pencere yöneticileri ve X11 istemcileri için, ICC ve EWMH gibi pencere yöneticisi protokollerini uygulamayı kolaylaştıran bir yardımcı kütüphanedir.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="xtrans"
	version="1.5.0"
	description="X.Org xtrans library"
	source="https://www.x.org/archive//individual/lib/xtrans-$version.tar.gz"
	depends=""
	group="x11.libs"


	setup(){

		$SOURCEDIR/configure --prefix=/usr \
		    --libdir=/usr/lib64/
	}

	build(){
		make
	}

	package(){
		make DESTDIR=$DESTDIR install
	}


**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


 
.. raw:: pdf

   PageBreak

.. _libkeybinder3:
**libkeybinder3**
=================

Linux masaüstü ortamlarında global klavye kısayollarını yakalamak ve yönetmek için kullanılan bir kütüphanedir.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="libkeybinder3"
	version="0.3.2"
	description="Musical key detection library for digital audio"
	source="https://github.com/kupferlauncher/keybinder/releases/download/keybinder-3.0-v$version/keybinder-3.0-$version.tar.gz"
	depends="gtk3"
	builddepend="gtk-doc,gobject-introspection"
	group="dev.libs"


	setup(){
		cd $SOURCEDIR
		autoreconf -fvi
		./configure --prefix=/usr \
		    --libdir=/usr/lib64/ \
		    --with-gtk=3
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
	}


**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _libexif:
**libexif**
===========

JPEG ve TIFF formatındaki fotoğrafların EXIF (Exchangeable Image File Format) meta verilerini okumak ve yazmak için kullanılan açık kaynaklı bir kütüphanedir.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="libexif"
	version="0.6.25"
	description="Library to parse an EXIF file and read the data from those tags"
	source="https://github.com/libexif/libexif/archive/refs/tags/v${version}.tar.gz"
	depends=""
	group="media.libs"


	setup(){
		cd $SOURCEDIR
		autoreconf -fvi
		./configure --prefix=/usr \
		    --libdir=/usr/lib64/
	}

	build(){
		make
	}

	package(){
		make DESTDIR="$DESTDIR" install
	}

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


 
.. raw:: pdf

   PageBreak

.. _gtk3:
**gtk3**
========

GTK3, C dilinde yazılmış, açık kaynaklı bir görsel kullanıcı arayüzü (GUI) toolkit'idir. GNOME masaüstü ortamının temelini oluşturan bu kütüphane, masaüstü uygulamaları geliştirmek için kullanılır.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="gtk3"
	version="3.24.49"
	description="Gimp Toolkit"
	source="https://gitlab.gnome.org/GNOME/gtk/-/archive/${version}/gtk-${version}.tar.gz"
	depends="cairo,libXi,libXext,libXfixes,libXcursor,libXdamage,librsvg,at-spi2-core,shared-mime-info,\
	gdk-pixbuf,libxkbcommon,libepoxy,colord,libcloudproviders,dconf,cantarell-fonts,libpng,\
	libXcomposite,libXinerama,glib,libXrandr,pango,wayland"
	builddepend="sassc,libsass"
	group="gui.libs"

	setup(){
		CFLAGS="$CFLAGS -O2" \
		CXXFLAGS="$CXXFLAGS -O2" \

		XDG_DATA_DIRS=/usr/share/ 
		cp -r ${dizin}/${paket}/files/ /tmp/kly/build/
		cd $SOURCEDIR
		patch -Np1 -i ../files/0001-Allow-disabling-legacy-Tracker-search.patch

		meson setup $BUILDDIR --prefix=/usr \
		--libdir=/usr/lib64/ \
		-Db_lto=true \
		-Dman=true \
		-Dgtk_doc=true \
		-Dbroadway_backend=true \
		-Dtests=false \
		-Dwayland_backend=false
	  
	}

	build(){
	   ninja -C $BUILDDIR
	   #meson compile -C build
	}

	package(){
		DESTDIR=$DESTDIR ninja -C $BUILDDIR install

		install -Dm644 /dev/stdin "$DESTDIR/usr/share/gtk-3.0/settings.ini" <<END
		[Settings]
		gtk-icon-theme-name = Adwaita
		gtk-theme-name = Adwaita
		gtk-font-name = Cantarell 11
		END

		#DESTDIR="$DESTDIR" meson install -C build
		#mkdir -p ${DESTDIR}/etc/sysconf.d
		mkdir -p ${DESTDIR}/etc/profile.d
		echo "export GTK_OVERLAY_SCROLLING=0" > ${DESTDIR}/etc/profile.d/gtk3.sh
		echo "export GDK_CORE_DEVICE_EVENTS=1" >> ${DESTDIR}/etc/profile.d/gtk3.sh

	}

Ek dosyaları indirmek için `tıklayınız. <https://kendilinuxunuyap.github.io/_static/files/gtk3/files.tar>`_

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _shared-mime-info:
**shared-mime-info**
====================

Linux ve Unix sistemlerinde MIME türlerini tanımlamak için kullanılan bir veritabanıdır. MIME (Multipurpose Internet Mail Extensions), internetteki çeşitli dosya türlerini tanımlamak için kullanılan bir standarttır.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="shared-mime-info"
	version="2.4"
	description="The Shared MIME-info Database specification"
	source="https://gitlab.freedesktop.org/xdg/shared-mime-info/-/archive/${version}/shared-mime-info-${version}.tar.gz"
	depends="libxml2"
	group="x11.misc"

	setup(){
		
		cd $SOURCEDIR
		meson setup $BUILDDIR --prefix=/usr \
		    --libdir=/usr/lib64/
	}

	build(){
		ninja -C $BUILDDIR
	}

	package(){
		DESTDIR=$DESTDIR ninja -C $BUILDDIR install
	}

Ek dosyaları indirmek için `tıklayınız. <https://kendilinuxunuyap.github.io/_static/files/shared-mime-info/files.tar>`_

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


	 
.. raw:: pdf

   PageBreak

.. _lz4:
**lz4**
=======

lz4, veriyi hızlı bir şekilde sıkıştırmak ve açmak için kullanılan bir hızlı ve verimli sıkıştırma algoritması ve kütüphanesidir. Özellikle yüksek hız ve düşük gecikme gereksinimleri olan durumlar için uygundur.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="lz4"
	version="1.9.4"
	description="Extremely fast compression algorithm"
	source="https://github.com/lz4/lz4/archive/refs/tags/v1.9.4.tar.gz"
	depends=""
	builddepend=""
	group="app.arch"

	setup(){
		echo ""
	}

	build(){
		cd $SOURCEDIR
		make PREFIX=/usr
	}

	package(){
		make install DESTDIR=$DESTDIR PREFIX=/usr
		mv ${DESTDIR}/usr/{lib,lib64}
	}


**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


 
.. raw:: pdf

   PageBreak

.. _gnutls:
**gnutls**
==========

GnuTLS, SSL/TLS (Secure Sockets Layer / Transport Layer Security) protokollerini ve kripto işlemleri uygulamak için kullanılan açık kaynaklı bir kütüphanedir. Güvenli internet iletişimini sağlamak için yaygın olarak kullanılır.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="gnutls"
	version="3.8.0"
	url="https://www.gnupg.org/ftp/gcrypt/gnutls"
	description="The GnuTLS Transport Layer Security Library"
	source="https://www.gnupg.org/ftp/gcrypt/gnutls/v${version%.*}/gnutls-${version}.tar.xz"
	depends="nettle,p11-kit,unbound"
	group="net.libs"
	uses_extra="zstd brotli libidn2"


	setup(){
	cd $SOURCEDIR
		./configure --prefix=/usr \
		--libdir=/usr/lib64 \
		--disable-guile \
		--enable-ssl3-support \
		--enable-openssl-compatibility \
		--with-included-unistring \
		--with-included-libtasn1\
		--with-zstd \
		--with-brotli \
		--with-libidn2
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
	}

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


 
.. raw:: pdf

   PageBreak

.. _lcms2:
**lcms2**
=========

lcms2 (Little CMS 2), görüntü işleme ve renk yönetimi için kullanılan açık kaynaklı bir kütüphanedir. Görüntülerin renk profilini yönetmek, dönüştürmek ve renk doğruluğunu sağlamak için kullanılır.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="lcms2"
	version="2.16"
	url="https://netix.dl.sourceforge.net/project/lcms/lcms/2.14/lcms2-2.14.tar.gz"
	description="Small-footprint color management engine, version 2"
	source="https://netix.dl.sourceforge.net/project/lcms/lcms/${version}/lcms2-${version}.tar.gz"
	depends="libtiff"
	group="media.libs"

	setup(){

		$SOURCEDIR/configure --prefix=/usr \
		    --libdir=/usr/lib64/
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
	}


**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _cups:
**cups**
========

CUPS, Unix ve Unix benzeri işletim sistemlerinde (Linux, macOS, BSD gibi) kullanılan, yazıcıların yönetimi ve baskı işlemlerini yöneten açık kaynaklı bir yazıcı sunucu sistemidir. CUPS, yazıcılar arası iletişimi yönetmek için Internet Printing Protocol (IPP) kullanır ve baskı kuyruklarını, yazıcı yönetimini sağlar.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="cups"
	version="2.4.7"
	description="The Common Unix Printing System "
	source="https://github.com/OpenPrinting/cups/releases/download/v${version}/cups-${version}-source.tar.gz"
	depends="openssl"
	group="net.print"


	setup(){
		cp -prvf $PACKAGEDIR/files/ /tmp/kly/build/
		cd $SOURCEDIR
		./configure --prefix=/usr \
		    --libdir=/usr/lib64/ \
			--sysconfdir=/etc \
			--localstatedir=/var \
			--with-menudir=/usr/share/applications \
			--with-icondir=/usr/share/icons \
			--with-logdir=/var/log/cups \
			--with-docdir=/usr/share/cups \
			--with-rundir=/run/cups \
			--with-cupsd-file-perm=0755 \
			--with-cups-user=lp \
			--with-cups-group=lp \
			--with-system-groups=lpadmin \
			--with-domainsocket=/run/cups/cups.sock \
			--enable-libusb \
			--without-rcdir \
			--without-php \
			--disable-pam \
			--enable-raw-printing \
			--enable-dbus \
			--with-dbusdir=/usr/share/dbus-1 \
			--enable-libpaper \
			--enable-ssl=yes \
			--enable-gnutls \
			--disable-launchd \
			--disable-systemd
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
		mkdir -p "$DESTDIR"/etc/{passwd,group,init}.d
		install ../files/cups.groups "$DESTDIR"/etc/group.d/cups
		install ../files/cups.users "$DESTDIR"/etc/passwd.d/cups
		install ../files/cupsd.initd "$DESTDIR"/etc/init.d/cupsd
		
		mv $DESTDIR/usr/lib/* $DESTDIR/usr/lib64/
		rm -rf $DESTDIR/usr/lib
	}

Ek dosyaları indirmek için `tıklayınız. <https://kendilinuxunuyap.github.io/_static/files/cups/files.tar>`_

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


 
.. raw:: pdf

   PageBreak

.. _gdbm:
**gdbm**
========

GDBM, GNU Database Manager'ın kısaltmasıdır ve verileri anahtar-değer çiftleri (key-value pairs) olarak depolayan bir veritabanı yönetim sistemidir. C dilinde yazılmıştır ve düşük seviyeli, hızlı ve taşınabilir bir veritabanı çözümü sunar.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="gdbm"
	version="1.23"
	description="GNU dbm is a set of database routines that use extensible hashing"
	source="https://ftp.gnu.org/gnu/gdbm/gdbm-$version.tar.gz"
	depends=""
	builddepend=""
	group="dev.libs"

	setup(){
		cd $SOURCEDIR
		./configure --prefix=/usr \
			--libdir=/usr/lib64 \
			--enable-libgdbm-compat \
			--disable-largefile \
			--disable-dependency-tracking \
			--enable-fast-install
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
	}


**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


 
.. raw:: pdf

   PageBreak

.. _mpdecimal:
**mpdecimal**
=============

MPDecimal, çok hassas sayısal hesaplamalar yapmak için kullanılan, yüksek hassasiyetli aritmetik sağlayan bir kütüphanedir. Özellikle ondalık sayı işlemlerine odaklanarak, kayıpları minimize eder ve kullanıcıya gelişmiş hassasiyet sunar.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="mpdecimal"
	version="4.0.0"
	url="https://www.bytereef.org/mpdecimal/index.html"
	description="Package for correctly-rounded arbitrary precision decimal floating point arithmetic"
	source="https://www.bytereef.org/software/$name/releases/$name-$version.tar.gz"
	depends=""
	builddepend=""
	group="net.db"

	setup(){
		cd $SOURCEDIR
		./configure --prefix=/usr \
		    --libdir=/usr/lib64
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
	}


**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


 
.. raw:: pdf

   PageBreak

.. _libgusb:
**libgusb**
===========

libgusb, USB cihazlarıyla etkileşim kurmak için kullanılan bir C kütüphanesidir. GUSB (GNOME USB) olarak da bilinir ve özellikle GNOME masaüstü ortamı ile entegre çalışmak için geliştirilmiştir. USB cihazlarını yönetmek ve onlarla iletişim kurmak için düşük seviyeli API'ler sağlar.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="libgusb"
	version="0.4.9"
	url="https://github.com/hughsie/libgusb"
	description=" GObject wrapper for libusb "
	source="https://github.com/hughsie/libgusb/archive/refs/tags/$version.tar.gz"
	depends="vala,gi-docgen,mesa,libusb,json-glib"
	group="dev.libs"

	setup(){
	cd $SOURCEDIR
		meson setup $BUILDDIR --prefix=/usr \
		    --libdir=/usr/lib64/
	}

	build(){
		ninja -C $BUILDDIR
	}

	package(){
	   DESTDIR=$DESTDIR ninja -C $BUILDDIR install
	}

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_



 
.. raw:: pdf

   PageBreak

.. _libisl:
**libisl**
==========

libisl, Integer Set Library'nin kısaltmasıdır ve tam sayı kümeleri üzerinde işlem yapmak için kullanılan bir kütüphanedir. Genellikle doğrusal optimizasyon ve matematiksel modelleme problemleri çözmek için kullanılır.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="libisl"
	version="0.26"
	description="An Integer Set Library for the Polyhedral Model"
	source="https://libisl.sourceforge.io/isl-${version}.tar.bz2"
	depends="gmp"
	builddepend=""
	group="dev.libs"

	setup(){
		cd $SOURCEDIR

		./configure --prefix=/usr \
			--mandir=/usr/share/man \
			--infodir=/usr/share/info \
			--localstatedir=/var
	}

	build(){
		make
	}

	package(){
		make DESTDIR=$DESTDIR install
		install -dm755 "${DESTDIR}"/usr/share/gdb/python/auto-load/usr/lib
		mv "$DESTDIR"/usr/lib/*-gdb.py "$DESTDIR"/usr/share/gdb/python/auto-load/usr/lib/
	}

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _libmpc:
**libmpc**
==========

libmpc, Multiple Precision Complex (Çok Hassas Karmaşık Sayılar) kütüphanesidir. Bu kütüphane, yüksek doğruluklu karmaşık sayılarla çalışmayı sağlayan bir matematiksel araçtır. Özellikle karmaşık sayılar üzerinde yapılan hesaplamaların çok hassas ve yüksek doğruluk gerektirdiği durumlarda kullanılır.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	version="1.3.1"
	name="libmpc"
	depends="glibc,mpfr"
	description="Library for the arithmetic of complex numbers with arbitrarily high precision"
	source="https://ftp.gnu.org/gnu/mpc/mpc-$version.tar.gz"
	groups="dev.libs"

	setup()
	{
		cd $SOURCEDIR
		./configure --prefix=/usr \
		    --libdir=/usr/lib64
	}
	build()
	{
		make
	}
	package()
	{
		make install DESTDIR=${DESTDIR}
	}

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


 
.. raw:: pdf

   PageBreak

.. _duktape:
**duktape**
===========

Duktape, C dilinde yazılmış ve gömülü sistemler için optimize edilmiş bir JavaScript motorudur. Hafif, taşınabilir ve kolayca entegre edilebilen bir JavaScript çalışma zamanı sağlar. Genellikle, JavaScript'i düşük seviyeli uygulamalara eklemek isteyen geliştiriciler tarafından kullanılır.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="duktape"
	version="2.7.0"
	url="https://duktape.org"
	description="Embeddable Javascript engine"
	source="https://duktape.org/$name-$version.tar.xz"
	group="dev.lang"


	_make(){
		make -f Makefile.sharedlibrary INSTALL_PREFIX=/usr "$@"
	}
	setup()
	{
	cd $SOURCEDIR
		# tools/configure.py needs Python 2
		sed -i 's/^#undef DUK_USE_FASTINT$/#define DUK_USE_FASTINT/' src/duk_config.h

		# Add missing NEEDED on libm.so
		sed -i 's/duktape\.c/& -lm/' Makefile.sharedlibrary

	}
	build(){
		_make
	}

	package(){
		_make DESTDIR="$DESTDIR" install
		install -Dt "$DESTDIR/usr/share/licenses/$name" -m644 LICENSE.txt
	}


**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


 
.. raw:: pdf

   PageBreak

.. _atkmm:
**atkmm**
=========

atkmm, C++ için ATK (Accessibility Toolkit) bağlayıcısıdır. ATK, GNOME ve diğer Linux masaüstü ortamlarında erişilebilirlik (accessibility) desteği sağlamak için kullanılan bir araçtır. atkmm, C++ dilinde yazılmış uygulamaların ATK ile etkileşime girmesini sağlayan bir kütüphanedir.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="atkmm"
	version="2.28.3"
	url="https://www.gtkmm.org"
	description="Atkmm is the official C++ interface for the ATK accessibility toolkit library."
	source="https://download.gnome.org/sources/atkmm/${version%.*}/atkmm-${version}.tar.xz"
	depends="at-spi2-core,glibmm"
	group="dev.cpp"

	setup () {
	cd $SOURCEDIR
		meson setup $BUILDDIR --prefix=/usr \
		--libdir=/usr/lib64/
	}

	build () {
		ninja -C $BUILDDIR
	}

	package () {
		DESTDIR=${DESTDIR} ninja -C $BUILDDIR install
	}

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


 
.. raw:: pdf

   PageBreak

.. _at-spi2-core:
**at-spi2-core**
================

at-spi2-core, GNOME masaüstü ortamında kullanılan AT-SPI2 (Assistive Technology Service Provider Interface 2) framework'ünün çekirdek bileşenidir. Bu framework, erişilebilirlik (accessibility) araçları ve yazılımları ile masaüstü uygulamaları arasındaki iletişimi sağlar. AT-SPI2, özellikle görme engelli kullanıcılar için ekran okuyucuları ve diğer yardımcı teknolojilerle etkileşimde bulunabilmesini sağlar.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="at-spi2-core"

	version="2.50.1"
	url="https://gitlab.gnome.org/GNOME/at-spi2-core"
	description="GTK+ & GNOME Accessibility Toolkit"

	source="https://gitlab.gnome.org/GNOME/at-spi2-core/-/archive/AT_SPI2_CORE_${version//./_}/at-spi2-core-AT_SPI2_CORE_${version//./_}.tar.gz"
	depends="glib,libffi,libpcre2,libXtst"

	setup(){
	cd $SOURCEDIR
		meson setup $BUILDDIR --prefix=/usr \
		    --libdir=/usr/lib64/ 

	}

	build(){
		ninja -C $BUILDDIR
	}

	package(){
	   DESTDIR=$DESTDIR ninja -C $BUILDDIR install
	}


**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _libtiff:
**libtiff**
===========

libtiff, TIFF (Tagged Image File Format) dosyalarını işlemek için kullanılan açık kaynaklı bir kütüphanedir. TIFF, genellikle yüksek kaliteli görüntülerin saklanmasında kullanılan bir dosya formatıdır ve genellikle dijital fotoğrafçılık, tarama ve grafik tasarım gibi alanlarda yaygın olarak kullanılır

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="libtiff"
	version="4.6.0"
	description="Tag Image File Format (TIFF) library"
	source="https://gitlab.com/libtiff/libtiff/-/archive/v$version/libtiff-v$version.tar.gz"
	depends=""
	group="media.libs"

	setup(){
		cd $SOURCEDIR
		autoreconf -fvi
		./configure --prefix=/usr \
		    --libdir=/usr/lib64/ \
		    --disable-docs
	}

	build(){
		make
	}

	package(){
		make DESTDIR="${DESTDIR}" install
	}

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


 
.. raw:: pdf

   PageBreak

.. _libepoxy:
**libepoxy**
===========

libepoxy, OpenGL ve OpenGL ES gibi grafik API'leri için platformlar arası uyumluluk sağlamak amacıyla kullanılan bir C kütüphanesidir. Bu kütüphane, özellikle OpenGL sürüm uyuşmazlıklarını çözer ve dinamik sürücü yükleme gibi işlemleri kolaylaştırır. Yani, farklı sistemlerde ve platformlarda OpenGL ile çalışan uygulamalar için bir uyumluluk katmanı sağlar.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="libepoxy"
	version="1.5.10"
	description="Library for handling OpenGL function pointer management"
	source="https://github.com/anholt/libepoxy/archive/refs/tags/$version.tar.gz"
	depends="libX11,mesa"
	group="media.libs"


	setup(){
		cd $SOURCEDIR
		meson setup $BUILDDIR --prefix=/usr \
		    --libdir=/usr/lib64/
	}

	build(){
		ninja -C $BUILDDIR 
	}

	package(){
		DESTDIR=$DESTDIR ninja -C $BUILDDIR install
	}


**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _gobject-introspection:
**gobject-introspection**
=========================

gobject-introspection, GObject tabanlı kütüphanelerin, çalışma zamanında yansıma (reflection) bilgilerini sağlamasına olanak tanıyan bir mekanizmadır. Bu, C dilinde yazılmış kütüphanelerin, farklı programlama dillerinde kullanılabilmesini sağlayan bir altyapıdır. GObject, GNOME platformu ve GTK+ gibi araçlar için temel bir nesne modelidir. gobject-introspection, bu kütüphanelerin diğer dillerde de kullanılmasını mümkün kılar.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="gobject-introspection"
	version="1.72.0"
	description="Introspection system for GObject-based libraries"
	source="https://gitlab.gnome.org/GNOME/gobject-introspection/-/archive/${version}/gobject-introspection-${version}.tar.gz"
	depends="cairo,libtool,python,py3-setuptools"
	builddepend="bison,flex,libffi,meson"
	group="dev.libs"

	setup(){
		cd $SOURCEDIR
		meson setup $BUILDDIR --prefix=/usr \
		    --libdir=/usr/lib64/ \
		    --wrap-mode=nodownload
	}

	build(){
		ninja -C $BUILDDIR
	}

	package(){
		DESTDIR=$DESTDIR ninja -C $BUILDDIR install
	}


**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


 
.. raw:: pdf

   PageBreak

.. _p11-kit:
**p11-kit**
===========

p11-kit, PKCS#11 tabanlı kriptografik modülleri (özellikle donanım güvenlik modülleri ve akıllı kartlar gibi) yönetmek için kullanılan bir kütüphanedir. PKCS#11, kripto işlemciler veya akıllı kartlar gibi güvenli donanımları yazılımlarına bağlamaya yarayan bir API'dir. p11-kit, bu modülleri daha kolay kullanabilmek ve yönetebilmek için bir araç seti sunar.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="p11-kit"
	version="0.25.5"
	url="https://github.com/p11-glue/p11-kit"
	description="Library for loading and sharing PKCS#11 modules"
	source="https://github.com/p11-glue/p11-kit/releases/download/${version}/p11-kit-${version}.tar.xz"
	depends="libtasn1,elfutils,libffi"
	group="app.crypt"

	setup(){
		cd $SOURCEDIR
		autoreconf -fvi
		./configure --prefix=/usr \
		    --libdir=/usr/lib64 \
		    --with-libffi \
			--without-systemd \
			--with-trust-paths=/etc/ssl/certs/ca-certificates.crt
	}

	build(){
		make
	}

	package(){
	   make install DESTDIR=$DESTDIR
	}


**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


 
.. raw:: pdf

   PageBreak

.. _nettle:
**nettle**
==========

Nettle, kriptografik algoritmalar için bir açık kaynak kütüphanesidir. Linux sistemlerinde genellikle güvenlik ve şifreleme işlemleri için kullanılır. AES, SHA, RSA gibi yaygın kriptografik algoritmaları sağlar ve bunların hızlı bir şekilde uygulanabilmesini sağlar. Bu paket, birçok kriptografi tabanlı uygulama ve yazılımda temel bir bileşen olarak yer alır. Nettle, C dilinde yazılmıştır ve GNU Genel Kamu Lisansı (GPL) altında dağıtılmaktadır. Kısacası, güvenli veri iletimi ve şifreleme için kritik bir araçtır.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="nettle"
	version="3.9"
	url="https://www.lysator.liu.se/~nisse/nettle"
	description="A low-level cryptographic library"
	source="https://ftp.gnu.org/gnu/nettle/nettle-${version}.tar.gz"
	depends="glibc"
	group="dev.libs"


	setup(){
		cd $SOURCEDIR
		./configure --prefix=/usr \
		    --libdir=/usr/lib64
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
	}


**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


 
.. raw:: pdf

   PageBreak

.. _desktop-file-utils:
**desktop-file-utils**
======================

desktop-file-utils, Linux sistemlerinde masaüstü ortamlarıyla ilgili dosya işlemleri yapan bir yazılım paketidir. Bu araç, .desktop dosyalarını işlemek ve doğrulamak için kullanılır. .desktop dosyaları, bir uygulamanın masaüstü ortamında nasıl görüntüleneceği ve çalıştırılacağına dair bilgi içeren metin dosyalarıdır. Bu dosyalar, bir uygulamanın menülerde nasıl görüneceğini, hangi simgeyi kullanacağını, çalıştırılacak komutları ve diğer önemli bilgileri belirler.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="desktop-file-utils"
	version="0.27"
	description="Command line utilities for working with desktop entries"
	source="https://www.freedesktop.org/software/desktop-file-utils/releases/desktop-file-utils-${version}.tar.xz"
	depends="glib"
	builddepend="git,meson"
	group="dev.util"


	setup(){
		cd $SOURCEDIR
		meson setup $BUILDDIR --prefix=/usr \
		    --libdir=/usr/lib64/
	}

	build(){
		ninja -C build
	}

	package(){
		DESTDIR=$DESTDIR ninja -C $BUILDDIR install
	}


**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _libidn2:
**libidn2**
===========

libidn2, Internationalized Domain Names (IDN) yani Uluslararasılaştırılmış Alan Adları için kullanılan bir kütüphanedir. Bu kütüphane, DNS (Domain Name System) üzerinde yer alan, ASCII dışındaki karakter setlerini (örneğin, Türkçe, Arapça, Çince gibi dillerdeki karakterler) destekleyen alan adlarını doğru şekilde işleyebilmek için kullanılır.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="libidn2"
	version="2.3.8"
	description="Free software implementation of IDNA2008, Punycode and TR46"
	source="https://ftp.gnu.org/gnu/libidn/libidn2-${version}.tar.gz"
	depends="libunistring"
	group="net.dns"

	setup(){
		cd $SOURCEDIR
		./configure --prefix=/usr \
		    --libdir=/usr/lib64 \
		    --disable-static \
		    --disable-nls
	}
	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
	}


**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _locale-tr:
**locale-tr**
=============

locale-tr, Türkçe dil ve yerel ayarları sistemde uygun şekilde sağlamak için kullanılan bir yerelleştirme dosyası ya da paketi olup, sistemdeki tarih, saat, dil, para birimi gibi birçok yerel ayarın Türkçe’ye uyumlu olmasını sağlar.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="locale-tr"
	version="1.0"
	description="loacale türkçeleştirme ayarı"
	source=""
	depends="glibc,tzdata"
	group="sys.apps"


	setup(){
		echo ""
	}

	build(){
		echo ""
	}

	package(){
	umask 022
	mkdir -p ${DESTDIR}/lib64
	mkdir -p ${DESTDIR}/lib64/locale

	mkdir -p ${DESTDIR}/etc
	mkdir -p ${DESTDIR}/etc/profile.d
	cp -prfv $PACKAGEDIR/files/locale.sh  ${DESTDIR}/etc/profile.d/locale.sh
	cp -prfv $PACKAGEDIR/files/keyboard.sh  ${DESTDIR}/etc/profile.d/keyboard.sh
	cp -prfv $PACKAGEDIR/files/locale.gen  ${DESTDIR}/etc/locale.gen
	cp -prfv $PACKAGEDIR/files/profile  ${DESTDIR}/etc/profile
	}

Ek dosyaları indirmek için `tıklayınız. <https://kendilinuxunuyap.github.io/_static/files/locale-tr/files.tar>`_

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


 
.. raw:: pdf

   PageBreak

.. _hicolor-icon-theme:
**hicolor-icon-theme**
======================

hicolor-icon-theme, Linux ve Unix tabanlı sistemlerde, masaüstü ortamları ve uygulamalar için simge seti sağlayan bir temadır. Bu tema, "hicolor" adıyla bilinir ve genellikle uygulamaların simgelerini bir standarda oturtmak amacıyla kullanılır.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="hicolor-icon-theme"
	version="0.17"
	description="Freedesktop.org Hicolor icon theme"
	source="http://icon-theme.freedesktop.org/releases/hicolor-icon-theme-$version.tar.xz"
	depends=""
	group="x11.themes"


	setup(){
		cd $SOURCEDIR
		./configure --prefix=/usr \
		    --libdir=/usr/lib64/
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
	}


**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _polkit:
**polkit**
==========

Polkit, Linux ve diğer Unix tabanlı sistemlerde, yönetici yetkisi gerektiren işlemleri güvenli bir şekilde yetkilendirmek için kullanılan bir araçtır. Kullanıcılar, sistemdeki kritik işlemleri gerçekleştirirken Polkit sayesinde yalnızca gerekli izinlere sahip olduklarında işlem yapabilir. Bu, hem güvenliği arttırır hem de sistem yöneticilerine daha ayrıntılı izin yönetimi sunar.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="polkit"
	version="123"
	url="https://gitlab.freedesktop.org/polkit/polkit"
	description="Application development toolkit for controlling system-wide privileges"
	source="https://gitlab.freedesktop.org/polkit/polkit/-/archive/$version/polkit-$version.tar.gz"
	depends="duktape,expat,glib,pam,elogind"
	builddepend="gobject-introspection,gtk-doc,meson"
	group="sys.auth"

	setup(){
	cp -prfv $PACKAGEDIR/files /tmp/kly/build/
	cd $SOURCEDIR

		meson setup $BUILDDIR --prefix=/usr \
		    --libdir=/usr/lib64/ \
		    -Db_lto=true \
		    -Dsession_tracking="libelogind" \
		    -Dsystemdsystemunitdir=/trash \
			-Dpam_prefix=/etc/pam.d \
			-Dpolkitd_user=polkitd

	}

	build(){
		ninja -C $BUILDDIR $jobs
	}

	package(){
		DESTDIR=$DESTDIR ninja -C $BUILDDIR install $jobs
		DESTDIR="$BUILDDIR/elogind/dest" meson install --no-rebuild -C elogind
		
		chown -R polkitd:polkitd $DESTDIR/etc/polkit-1/rules.d $DESTDIR/usr/share/polkit-1/rules.d
		chmod -R 700 $DESTDIR/etc/polkit-1/rules.d $DESTDIR/usr/share/polkit-1/rules.d
		chmod 4755 $DESTDIR/usr/lib/polkit-1/polkit-agent-helper-1
		chmod 4755 $DESTDIR/usr/bin/pkexec

		rm -rf $DESTDIR/garbage
		install -d $DESTDIR/etc/init.d

		install -Dm755 ../files/polkit.initd $DESTDIR/etc/init.d/polkit
		mkdir -p $DESTDIR/var
		mkdir -p $DESTDIR/var/empty
	}

Ek dosyaları indirmek için `tıklayınız. <https://kendilinuxunuyap.github.io/_static/files/polkit/files.tar>`_

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak

.. _libjpeg62:
**libjpeg62**
=============

libjpeg62, JPEG formatındaki resimlerin sıkıştırılması, çözülmesi ve işlenmesi için kullanılan bir kütüphanedir. Genellikle görüntü işleme uygulamalarında, web servislerinde ve fotoğraf düzenleme yazılımlarında kullanılır. Daha yeni sürümler olsa da, libjpeg62 eski sistemler ve uygulamalar için hala önemli bir kütüphanedir.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="libjpeg62"
	version="0"
	description="MMX, SSE, and SSE2 SIMD accelerated JPEG library"
	source="http://ftp.de.debian.org/debian/pool/main/libj/libjpeg6b/libjpeg6b_6b2.orig.tar.gz"
	depends=""
	group="media.libs"

	setup(){
		cd $SOURCEDIR 
		autoreconf -fvi    
		./configure --prefix=/lib64/libjpeg62
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
		mkdir -p $DESTDIR/lib64
		cd $DESTDIR/lib64
		ln -s libjpeg62/lib/libjpeg.so.62 libjpeg.so.62
	}


**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


 
.. raw:: pdf

   PageBreak

.. _gpicview:
**gpicview**
============

gpicview, GNOME masaüstü ortamı için hafif, hızlı ve basit bir resim görüntüleyicisidir. Kullanıcı dostu arayüzü ve temel görüntüleme özellikleriyle, sistem kaynaklarını verimli kullanırken kullanıcıya hızlı bir şekilde resimlere göz atma imkanı sunar. 

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="gpicview"
	version="0.3.1"
	description="Lightweight image viewer"
	source="https://github.com/lxde/gpicview/archive/refs/tags/$version.tar.gz"
	depends="gtk3"
	builddepend="intltool"
	group="lxde.apps"


	setup(){
		cd $SOURCEDIR
		autoreconf -fvi
		./configure --prefix=/usr \
			--enable-gtk3 \
		    --libdir=/usr/lib64/
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
	}

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_

 
.. raw:: pdf

   PageBreak

.. _libdmx:
**libdmx**
==========

libdmx, DMX (Distributed Multihead X) protokolünü destekleyen bir kütüphanedir. DMX, X Window System üzerinde birden fazla ekranı (multihead) birleştirerek dağıtık bir masaüstü ortamı oluşturmanıza olanak tanır. DMX, temel olarak, birden fazla X sunucusunun birleşik bir şekilde çalışmasını sağlar, böylece birden fazla monitörü tek bir büyük masaüstü ortamı olarak kullanabilirsiniz.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="libdmx"
	version="1.1.4"
	description="X.Org dmx library"
	source="https://www.x.org/archive/individual/lib/libdmx-$version.tar.gz"
	depends=""
	group="x11.libs"


	setup(){
		$SOURCEDIR/configure --prefix=/usr \
		    --libdir=/usr/lib64/
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
	}


**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


 
.. raw:: pdf

   PageBreak

.. _lightdm:
**lightdm**
===========

LightDM, Linux sistemlerinde kullanılan bir giriş yöneticisidir (display manager).
Görevi:

- Bilgisayar açıldığında grafiksel giriş ekranını (login screen) sağlar.
- Kullanıcıların kullanıcı adı ve şifreyle oturum açmasını sağlar.
- Açılacak masaüstü ortamını/seansı seçmeye imkân verir.

**Paketi Derleme :**
--------------------

Debian'da paketi derlemek için aşağıdaki paketlerin kurulu olması gerekir.

.. code-block:: bash

    sudo apt install libgcrypt20-dev, libxklavier-dev

.. code-block:: bash

	#!/usr/bin/env bash
	name="lightdm"
	version="1.32.0"
	description="A lightweight display manager"
	source="https://salsa.debian.org/xfce-extras-team/lightdm/-/archive/debian/$version-1/lightdm-debian-$version-1.tar.gz"
	depends="libX11,pam,libxklavier,xorg-server,libxcb,glib,libgcrypt,libXdmcp,xmodmap,xrdb,libXi"
	group="x11.misc"


	setup(){
		cp -prvf $PACKAGEDIR/files/ /tmp/kly/build/
		cd $SOURCEDIR
	   	./autogen.sh
		./configure --prefix=/usr --sysconfdir=/etc --libdir=/usr/lib64/ --localstatedir=/var \
		        --disable-tests --disable-gtk-doc --enable-yelp-tools --enable-qt5-base \
		        --with-greeter-user=lightdm --with-greeter-session=lightdm-gtk-greeter
	}

	build(){
		make
	}

	package(){
		make install DESTDIR=$DESTDIR
		# create user and group
		# install service
		mkdir -p $DESTDIR/etc/init.d
		install ../files/lightdm.initd $DESTDIR/etc/init.d/zlightdm
		mkdir -p $DESTDIR/usr/bin/
		# generate lightdm-session file
		#echo "#!/bin/sh" > $DESTDIR/usr/bin/lightdm-session
		#echo 'exec /etc/X11/xinit/Xsession $@' >> $DESTDIR/usr/bin/lightdm-session
		install -Dm755 ../files/lightdm-session $DESTDIR/usr/bin/lightdm-session
		# fix pam config
		sed -i "s/systemd/elogind/g" $DESTDIR/etc/pam.d/*
		
		 for level in boot default nonetwork shutdown sysinit ; do
		mkdir -p ${DESTDIR}/etc/runlevels/$level
		done
	install ${DESTDIR}/etc/init.d/zlightdm ${DESTDIR}/etc/runlevels/default/zlightdm
	}

Ek dosyaları indirmek için `tıklayınız. <https://kendilinuxunuyap.github.io/_static/files/lightdm/files.tar>`_

**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


 
.. raw:: pdf

   PageBreak

.. _lightdm-gtk-greeter:
**lightdm-gtk-greeter**
=======================

lightdm-gtk-greeter, LightDM için kullanılan bir greeter (karşılama arayüzü) paketidir. LightDM sadece oturum yönetimini yapar, ama kendi başına grafiksel giriş ekranı göstermez. Bu ekranı sağlamak için bir greeter gerekir. lightdm-gtk-greeter, GTK+ kütüphanesi ile yazılmış hafif, sade ve özelleştirilebilir bir giriş ekranı sağlar.

**Paketi Derleme :**
--------------------

Debian'da paketi derlemek için aşağıdaki paketlerin kurulu olması gerekir.

.. code-block:: bash

    sudo apt install liblightdm-gobject-dev, xfce4-dev-tools

.. code-block:: bash

	#!/usr/bin/env bash
	name="lightdm-gtk-greeter"
	version="2.0.8"
	description="Gtk based greeter for lightdm."
	source="https://github.com/Xubuntu/lightdm-gtk-greeter/releases/download/lightdm-gtk-greeter-$version/lightdm-gtk-greeter-$version.tar.gz"
	depends="gtk3,lightdm"
	builddepend="exo,xfce4-dev-tools"
	group="x11.misc"

	setup () {
		cd $SOURCEDIR
		autoreconf -fvi
		./configure --prefix=/usr \
			--libdir=/usr/lib64/ \
			--sysconfdir=/etc \
			--sbindir=/usr/bin \
			--with-libxklavier \
			--enable-kill-on-sigterm \
			--disable-libido \
			--disable-libindicator
	}

	build(){
		make
	}

	package(){
		make DESTDIR=$DESTDIR install
	}


**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


 
.. raw:: pdf

   PageBreak

.. _libgpg-error:
**libgpg-error**
================

libgpg-error, GnuPG ve libgcrypt gibi kütüphanelerde kullanılan hata kodlarını ve açıklamalarını sağlayan yardımcı kütüphanedir.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="libgpg-error"
	version="1.47"
	url="https://www.gnupg.org/"
	description="Support library for libgcrypt"

	source="https://www.gnupg.org/ftp/gcrypt/libgpg-error/${name}-${version}.tar.bz2"
	depends="glibc"
	group="dev.libs"

	setup(){
	cd $SOURCEDIR
		autoreconf -vfi
		./configure --prefix=/usr \
		    --libdir=/usr/lib64/
	}

	build(){
		make
	}

	package(){
		make DESTDIR=$DESTDIR install
	}


**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


 
.. raw:: pdf

   PageBreak

.. _libgcrypt:
**libgcrypt**
=============

libgcrypt, GnuPG’nin de kullandığı, şifreleme, imzalama, hash ve rastgele sayı üretimi gibi kriptografik işlemler sağlayan bir kütüphanedir.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="libgcrypt"
	version="1.10.3"
	url="https://www.gnupg.org"
	description="General purpose cryptographic library based on the code from GnuPG"
	source="https://gnupg.org/ftp/gcrypt/libgcrypt/libgcrypt-1.10.3.tar.gz"
	depends="libgpg-error"


	setup(){
	cd $SOURCEDIR
	sed -i "s:t-secmem::" tests/Makefile.am
	sed -i "s:t-sexp::" tests/Makefile.am

		autoreconf -fvi
		./configure --prefix=/usr \
		    --libdir=/usr/lib64/ \
		    --disable-padlock-support
	}

	build(){
		make $jobs
	}

	package(){
		make DESTDIR=${DESTDIR} install $jobs
	}


**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


 
.. raw:: pdf

   PageBreak

.. _paketderleme:
**GNU Araçlarıyla Pencere Yöneticisi Derleme**
==============================================

Kendi Linux'unu Yap
===================

Bu dokumanda dağıtım hazırlamak için temel işlemler anlatılmaktadır.

Bu kitap, açık kaynak ve özgür yazılıma gönül vermiş kişilerin, Türkçe kaynak bulamama sıkıntısına bir çözüm olarak hayata geçirilmiş bir projedir. Açık kaynak dünyasında kendi dağıtımlarını yapmak isteyen kişilere bir rehber olacak şekilde hazırlanmıştır. Bu dokümanda anlatılan sıralamaya göre işlemleri uyguladığınızda kendi sisteminiz derleyip iso halinde son kullanıcını kullanabileceği gibi bir sistem ortaya çıkartabilirsiniz. 


Kaynak ve dokümanlarımız yansılarımız:

* Bu sitedeki bilgilerin pdf kitap hali için `tıklayınız. <https://kendilinuxunuyap.github.io/kitap/>`_


Dağıtıma özgü ISO oluşturmak için o dağıtımın paket sistemi kullanılır.  
Bu dokümanda anlatılan **kly** paket sistemi, önceki bölümde detaylıca açıklanmıştır.

Bu bölümde, **kly** paket sistemini kullanarak ISO oluşturma adımları basit ve anlaşılır şekilde verilecektir. Aşağıda payşlaşılan script ile hazırlanan iso **/tmp/distro/distro.iso** konumunda olacaktır. Sistemi oluşturan paketleri;

- **github.com/kendilinuxunuyap/kly-base-packages**
- **github.com/kendilinuxunuyap/kly-x11-packages**
- **github.com/kendilinuxunuyap/kly-lxde-packages** konumlarından indirerek oluşturmaktadır.

**Not:** Anlatılan yöntem genel Linux dağıtımlarının ISO oluşturma mantığına dayanır. Araçlar, dizinler ve komutlarda küçük farklılıklar olabilir, ancak iş akışı aynıdır.

Aşağıdaki scriptle oluşturulmuş iso https://github.com/kendilinuxunuyap/kly-lxde-distro/releases/download/current/kly-x11-distro.iso adresinde bulunmaktadır. 

   
**kly Paket Sistemiyle ISO Oluşturma Scripti**
----------------------------------------------

.. code-block:: shell

	#--------------------------------------------------------------------------------------------------------------------
	#!/bin/bash
	set -x
	if which apt &>/dev/null && [[ -d /var/lib/dpkg && -d /etc/apt ]] ; then
		apt-get update
		echo "işlem başladı....."
		apt install xorriso grub-pc-bin grub-efi mtools make python3 dosfstools e2fsprogs squashfs-tools \
		python3-yaml gcc wget curl unzip xz-utils debootstrap git erofs-utils zstd -y
	fi
	apt-get install git devscripts equivs -y
	#--------------------------------------------------------------------------------------------------------------------
	rootfs="/tmp/distro/rootfs"
	distro="/tmp/distro"
	rm -rf $distro/iso
	#rm -rf $rootfs
	mkdir -p /tmp/distro/rootfs
	mkdir -p $rootfs/bin
	#mkdir -p distro/rootfs
	#export PATH=/bbin:$PATH
	cp busybox $rootfs/bin/busybox
	cp kly $rootfs/bin/kly
	cd $rootfs/bin/
	ln -s busybox cpio
	#busybox --install -s ./
	cd $rootfs/
	#cd distro/rootfs/
	mkdir  -p var run dev sys proc etc tmp/kly/kur
	bash -c "echo '127.0.0.1 kly' >> $rootfs/etc/hosts"
	bash -c "echo 'kly' > $rootfs/etc/hostname"
	bash -c "echo 'nameserver 8.8.8.8' > $rootfs/etc/resolv.conf"

	### system chroot  bind/mount
	for i in dev dev/pts proc sys; do mount -o bind /$i $rootfs/$i; done
	### manuel kly-tools install
	$rootfs/bin/busybox wget -O $rootfs/tmp/base-file-1.0.kly https://github.com/bpslinux/\
	kly-temel-paketler/raw/refs/heads/master/base-file/base-file-1.0.kly 1>$rootfs/dev/null 2>$rootfs/dev/null
	$rootfs/bin/busybox tar -xf $rootfs/tmp/base-file-1.0.kly -C $rootfs/tmp/kly/kur
	$rootfs/bin/busybox tar -xf $rootfs/tmp/kly/kur/rootfs.tar.xz -C $rootfs

	#paket adresi ekleniyor
	$rootfs/bin/busybox mkdir -p $rootfs/etc/kly
	echo "kendilinuxunuyap/kly-base-packages">$rootfs/etc/kly/sources.list
	echo "kendilinuxunuyap/kly-x11-packages">>$rootfs/etc/kly/sources.list
	echo "kendilinuxunuyap/kly-lxde-packages">>$rootfs/etc/kly/sources.list
	
	### installing kly package in rootfs
	$rootfs/bin/kly -u $rootfs
	#**********************************************************************
	echo root:x:0:0:root:/root:/bin/sh > $rootfs/etc/passwd 
	chmod 755 $rootfs/etc/passwd
	#**********************************************************************

	for paket in glibc readline ncurses bash openssl acl attr libcap libpcre2 gmp coreutils sqlite  \
	util-linux grep sed mpfr gawk findutils libgcc libcap-ng gzip xz-utils zstd bzip2 elfutils libselinux tar zlib \
	brotli curl
	do
	$rootfs/bin/kly -ri $paket $rootfs
	#chroot $rootfs /bin/kly -ri $paket; 
	done

	for paket in shadow file eudev cpio libsepol kmod audit libxcrypt libnsl libbsd libtirpc \
	e2fsprogs dosfstools initramfs-tools libxml2 expat libmd libaio lvm2 popt icu iproute2 \
	net-tools dhcp openrc rsync kbd kernel dialog live-boot live-config parted busybox nano grub \
	efibootmgr efivar libssh openssh pam 
	do
	#$rootfs/bin/kly -i $paket $rootfs
	chroot $rootfs /bin/kly -ri $paket; 
	done

	# burası x11 için olan paketlerdi. arasınsa ek paket varmı kontrol etmedim. edeceğim
	for paket in xorg-server pixman libpciaccess libXau libXdmcp libXfont2 libxshmfence libdrm libxcvt libfontenc \
	freetype libpng harfbuzz glib xterm libXft fontconfig libXext libXaw libXmu libXinerama libXpm libXt libX11 libICE \
	libXrender libxcb libSM xf86-input-libinput xf86-input-vmmouse xf86-video-amdgpu xf86-video-ast xf86-video-ati \
	xf86-video-dummy xf86-video-fbdev xf86-video-intel xf86-video-mga xf86-video-nouveau xf86-video-qxl xf86-video-r128 \
	xf86-video-siliconmotion xf86-video-vboxvideo xf86-video-vesa xkbcomp libxkbfile libglvnd mesa xkeyboard-config \
	libinput mtdev libevdev libwacom libgudev libffi xinit xcalc libXi openbox libXcursor libXfixes pango libXrandr \
	fribidi xcb-util libthai libdatrie startup-notification dejavu libunwind dbus polkit elogind
	do
	chroot $rootfs /bin/kly -ri $paket; 
	done


.. raw:: pdf

   PageBreak
   	
.. code-block:: shell

	#--------------------------------------------------------------------------------------------------------------------
	# scriptin devamı   
	# aşağıdaki paketleri kurunca lxsession açılıyor
	for paket in libjpeg-turbo  cairo gdk-pixbuf gtksourceview4 hsakmt libdmx libfm libFS libnotify libvdpau libwnck3 \
	libXaw3d libXcomposite libXdamage libXfont libxkbcommon libxkbui libxklavier libXpresent libXres libxss libXtst \
	libXv libXvMC	libXxf86dga libXxf86vm tslib vte3 xapp xcb-util-cursor xcb-util-errors xcb-util-image \
	xcb-util-keysyms xcb-util-renderutil xcb-util-wm xtrans
	do
	chroot $rootfs /bin/kly -ri $paket; 
	done

	for paket in libfm-extra menu-cache lxappearance lxde-common lxde-icon-theme lxhotkey lxinput lxlauncher \
	lxmenu-data lxpanel lxrandr lxsession lxtask lxterminal pcmanfm libkeybinder3 libexif gtk3 shared-mime-info \
	lz4 gnutls lcms2 cups gdbm mpdecimal libgusb libisl libmpc duktape locale-tr 
	do
	chroot $rootfs /bin/kly -ri $paket; 
	done

	for paket in atkmm at-spi2-core libtiff libepoxy gobject-introspection hicolor-icon-theme p11-kit nettle \
	desktop-file-utils libidn2
	do
	chroot $rootfs /bin/kly -ri $paket; 
	done

	### user add and passwd
	chroot $rootfs echo -e "1\n1\n"|chroot $rootfs passwd root
	chroot $rootfs useradd live -m -s /bin/sh -d /home/live
	chroot $rootfs echo -e "live\nlive\n"|chroot $rootfs passwd live
	for grp in users tty wheel cdrom audio dip video plugdev netdev; do
	chroot $rootfs usermod -aG $grp live || true
	done

	### update-initrd
	fname=$(basename $rootfs/boot/config*)
	kversion=${fname:7}
	mv $rootfs/boot/config* $rootfs/boot/config-$kversion
	cp $rootfs/boot/config-$kversion $rootfs/etc/kernel-config
	chroot $rootfs update-initramfs -u -k $kversion

	#### system chroot umount
	for dir in dev dev/pts proc sys ; do    while umount -lf -R $rootfs/$dir 2>/dev/null ; do true; done done

	#************************iso *********************************
	mkdir -p $distro/iso
	mkdir -p $distro/iso/boot
	mkdir -p $distro/iso/boot/grub
	mkdir -p $distro/iso/live || true

	#### Copy kernel and initramfs (Debian/Devuan)
	cp -pf $rootfs/boot/initrd.img-* $distro/iso/boot/initrd.img
	cp -pf $rootfs/boot/vmlinuz-* $distro/iso/boot/vmlinuz
	rm -rf $rootfs/boot
	#### Create squashfs
	mksquashfs $rootfs $distro/filesystem.squashfs -comp xz -wildcards
	mv $distro/filesystem.squashfs $distro/iso/live/filesystem.squashfs

	# grub.cfg dosyasını yaz
	cat << EOF > "$distro/iso/boot/grub/grub.cfg"
	set timeout=6; set default=1; terminal_input console;
	menuentry "Canli(live) GNU/Linux 64-bit" --class liveiso {
	linux /boot/vmlinuz boot=live init=/sbin/openrc-init net.ifnames=0 \
	biosdevname=0
	initrd /boot/initrd.img
	}
	menuentry "Kur GNU/Linux 64-bit" --class liveiso {
	linux /boot/vmlinuz boot=live init=/bin/kur quiet
	initrd /boot/initrd.img
	}
	EOF
	#iso oluşturuluyor
	grub-mkrescue $distro/iso/ -o $distro/distro.iso

Kaynaklar::

	- https://www.subrat.info/build-kernel-and-userspace/ - 08/07/2025
	- https://medium.com/@chienhaotan/compiling-and-running-a-minimal-kernel-with-busybox-bfc45a991017 - 08/07/2025
	- https://wiki.archlinux.org/title/GRUB_(T%C3%BCrk%C3%A7e)  - 08/07/2025
	- https://chatgpt.com/share/6875084c-6050-8012-9229-a37b47351aa2 - 14/07/2025

.. raw:: pdf

   PageBreak




.. _isohazirlama:
**ISO Hazırlama**
=================

Bu dokümanda anlatılan paketlerin **kly Paket Sistemiyle** hazırlanmış **LXDE Masaüstü Ortamı** isosu hazırlandı. İsoyu https://github.com/kendilinuxunuyap/kly-lxde-distro/releases/download/current/kly-lxde-distro.iso adresinden indirebilirsiniz.

Şimdi hazırlanan ISO’yu **QEMU** veya **VirtualBox** kullanarak çalıştıralım. Ekran görüntüleri aşağıda verilmiştir.

**Canlı(live) Sistem Kullanımı**
--------------------------------

.. image:: /_static/images/iso-20.png
  :width: 600
  :height: 200

.. image:: /_static/images/iso-21.png
  :width: 600
  :height: 450

Canlı(live) sistem çalıştırıldığında overlay live bir sistemin açıldığını görmekteyiz. Canlı(live) sistemde kullanıcı adları ve parolaları;

- Kullanıcı: root	Parola: 1
- Kullanıcı: live	Parola: live

.. raw:: pdf

   PageBreak
   
**Sistem Kurulumu**
-------------------

Sistemin kurulumu için resimlerde görünen sıraya göre seçimler yapmalıyız.

.. image:: /_static/images/iso-30.png
  :width: 600

.. image:: /_static/images/iso-31.png
  :width: 600

Kurulum menüsünde kullanıcı adları ve parolaları, klayve varsayılan olarak;

- Kullanıcı: root	Parola: 1
- Kullanıcı: user1	Parola: 1
- Dil   	: tr_TR
- Klavye   	: trq

menüden değişiklik yapabilirsiniz. Değişiklik yapmadan sadece kurulum diskini ve disk bölümünü seçip Install(Yükle) işlemi yapabilirsiniz.


.. image:: /_static/images/iso-32.png
  :width: 600

.. image:: /_static/images/iso-33.png
  :width: 600


.. raw:: pdf

   PageBreak
   
**Sistemin Çalışması**
----------------------

Sistem kurulumu gerçekleştiğinde  sistem resimde görüldüğü gibi açılmalıdır.

.. image:: /_static/images/iso-40.png
  :width: 600

Sisteme **user1** (parola=1) kullanıcısı olarak giriş yapıldığı görülmektedir.

.. image:: /_static/images/lxde0.png
  :width: 600
  
**xinit** çalışınca **X Pencere Sistemine** geçiş yapılacak.

.. raw:: pdf

   PageBreak
   
**xinit** çalışınca **X Pencere Sistemi** aşağıdaki gibi açılacaktır.

.. image:: /_static/images/lxde1.png
  :width: 600
  
**X Pencere Sistemi** çalışınca aşağı ve pencere yönetimini ve masaüstü ortamı için **exec lxsession** çalıştırılıyor.

.. image:: /_static/images/lxde2.png
  :width: 600

Artık LXDE Masaüstü ortamındayız. LXDE araçlarının çalıştırılmış hali aşağıda görülmektedir.

.. image:: /_static/images/lxde3.png
  :width: 600

LXDE, sade sistem isteyen kullanıcılar için mükemmel bir tercihtir. Ancak görsellik, modernlik veya geniş özellik seti beklentiniz varsa daha güncel alternatifler (XFCE, Cinnamon) tercih edilebilir.

.. raw:: pdf

   PageBreak

.. _sistemcalistirma-inceleme:
Oluşan Sistemin Çalıştırılması İncelenmesi
==========================================

**LXDE'yi xinit veya startx'le Çalıştırma**
--------------------------------------------

**xinit ve startx** X Pencere Sistemi'ni başlatmak için kullanılan komutlardır. ``xinit`` ve ``startx``, X sunucusunu kullanıcı girişinden sonra manuel olarak başlatmak için kullanılır.

**xinit** X sunucusunu başlatır ve ardından belirtilen tek bir uygulamayı çalıştırır. **startx** ``xinit`` için bir kabuk (wrapper) komutudur. ``~/.xinitrc`` betiğini çalıştırır, yoksa sistem varsayılanını kullanır.

Eğer belirli bir pencere yöneticisi veya masaüstü ortamı ile başlatmak istiyorsanız, ~/.xinitrc dosyasını düzenlemeniz gerekebilir. Dosyanın içeriği şöyle olmalıdır:

**openbox Masaüstü Ortamını Kullanma**
--------------------------------------

.. code-block:: shell

	exec openbox-session

**lxde Masaüstü Ortamını Kullanma**
--------------------------------------

.. code-block:: shell

	exec lxsession



.. code-block:: shell
	
		#startx
		# veya
		xinit


.. raw:: pdf

   PageBreak
   	
**Lightdm**
-----------

**xinit** veya **startx** ile masaüstü ortamının açılışını sağlanacağını bu bölümde gördük. Fakat bu şekilde bir açılış süreci yorucu ve mevcut dağıtımların açılışından farklı olacaktır. Bu durum son kullanıcı için çok çekici veya kullanıcı dostu gelmeyebilir. Bundan dolayı **lightdm** kullanabilirsiniz. LightDM bir Display Manager (giriş yöneticisi)’dir.

**Görevi nedir?**::

	- Grafik arayüzlü giriş ekranını (login screen, greeter) sağlar.
	- Kullanıcı adı/şifre sorar ve oturumu başlatır.
	- Xorg veya Wayland oturumunu hazırlar.
	- Kullanıcıya masaüstü ortamını (LXDE, XFCE, MATE vb.) seçme imkânı verebilir.
	- Sistem açıldığında otomatik giriş (autologin) desteği vardır.
	- Yani, LightDM = kullanıcı ile X sunucusu arasındaki köprüdür.

Mevcut sistemimize ek olarak derlediğimiz paketleri aşağıdaki komutlarla sisteminize kurabilirsiniz. ::

	kly -ri lightdm
	kly -ri libgcrypt
	kly -ri libgpg-error
	kly -ri lightdm-gtk-greeter

Bu paketler kurulduğunda aşağıda görüldüğü gibi açılışta ekran karşılayacak ve giriş yapılabilecektir.

.. image:: /_static/images/lightdm1.png
  :width: 600
  :height: 150

Listeye gelen kullanıcılardan birini seçerek porala doğrulamasından sonra masaüstü ortamı açılacaktır.
 
.. image:: /_static/images/lightdm2.png
  :width: 600
  :height: 250

.. raw:: pdf

   PageBreak

.. _xpenceresistemi:
**Lxde Masaüstü Ortamı Çalıştırma**
===================================

**apt Paket Sistemi**
+++++++++++++++++++++

apt paket sistemi debian tabanlı sistemlerde paket yönetimi için kullanılan bir uygulamadır.
Temel işlemler şunlardır.

Yerel Paket İndexini Güncelleme
-------------------------------

.. code-block:: shell

	sudo apt  update

Paket Yükleme
-------------

.. code-block:: shell

	sudo apt install paket_adi

Paket Silme
-----------

.. code-block:: shell

	sudo apt remove paket_adi

.. raw:: pdf

   PageBreak


Paket sistemi, sisteme paket **(kurma, kaldırma, index güncelleme)** gibi temel işlemlerin yapılmasını sağlar. **Temel Sistem** kitabımımızda **Paket Sistemi(kly)** tasarımı anlatılmıştı. Bu kitapta ise paketleri derlerken kly paket sistemi kullanılarak derleyeceğiz. Paket sistemi paketleri tekrar tekrar derlemek yerine paket olarak hazırlamakta ve istediğimiz zaman oluşturulan sisteme yüklenmekte veya kaldırılmatadır. Bir sorun olduğu farkedildiğinde ise tekrar derlenerek sadece bu paket günecelenebilmektedir. Bu tür avantajlardan dolayı paket sistemini kullanacağız.

Burada paket sisteminin nasıl kullanılacağı anlatılacaktır. Paket sistemimiz **Temel Sistem** üzerinde **base-file** paketiyle sisteme yüklendi. 
Aşağıda **kly Temel Sistem** üzerinde hazır gelen paket sistemi uygulamalarımız görülmektedir.

.. image:: /_static/images/kly-paket-sistemi.png
  :width: 600

**kly:** *klypaketle, klykur, klykadir, klyupdate* scritplerimizin hepsini tek scriptte toplanmış halidir. Ayrıca paketlerin kurulumu ve kaldırılması sırasında bağımlılıklarınıda paketle birlikte kurmakta veya kaldırmakta. Bu dokümanda paketlerin derlenmesi, kurulması, kaldırılması vb. işlemler **kly** scripti kullanılarak yapılacaktır.  **klypaketle, klypaketle, klykur, klykaldir, klyupdate** scripleri bir öğretici olması nedeniyle bulunmaktadır. Daha kapsamlı işlemler için yetersiz kalacaktır.

**kly Paket Siteminin Debian'a Kurulumu**
------------------------------------------

kly paket sistemi **Temel Sistem** üzerinde kurulu olarak gelmektedir. Üstte verilen resimde görülmektedir. Kullanımı ve parametrelerini unutmanız durumunda **kly --help** komutuyla kullanımı öğrenebilirsiniz. 

Debian üzerinde kullanmak için kly scriptimizi indirip **/bin** konumuna kopyalayalım. Aşağıda verilen komutları sırasıyla çalıştırınız. **kly** paket sisteminin sorunsuz çalışması için **busybox** paketinin kurulu olması gerekektedir. Sorunsuz çalışmışsa **Debian** sistemimize **kly** paket sistemimiz kurulmuştur.

.. code-block:: bash

	wget https://kendilinuxunuyap.github.io/_static/files/base-file/kly
	sudo mv kly /bin/kly
	sudo chown root:root /bin/kly
	sudo chmod 755 /bin/kly
	sudo apt update
	sudo apt install busybox-static -y

.. raw:: pdf

   PageBreak

.. _klypaketyap:
**kly Paket Sistemiyle Paket Yapma**
------------------------------------

kly paket sistemi ile paket yapma işlemini Debian ortamında yapacağız. Debian üzerinde paket sistemimizi oluşturan scriptimiz **/bin/kly** konumunda olması gerekmektedir.

Şimdi **bash** paketinin **kly Paket Sistemi**'ni kullanarak derlemesini yapalım. Paket için aşağıda görüldüğü gibi masaüstüne **kly-paket** dizini oluşturuldu. **kly-paket**  dizini içine **bash** dizini oluşturuldu. **bash** dizini içine **klybuild** dosyası oluşturuldu.

.. image:: /_static/images/kly-paket-yap1.png
  :width: 600
 
**klybuild** dosyasının içerine aşağıdaki kodu ekleyiniz.

.. code-block:: bash

	#!/usr/bin/env bash
	version="5.2.21"
	name="bash"
	depends="glibc,readline,ncurses"
	description="GNU/Linux dağıtımında ön tanımlı kabuk"
	source="https://ftp.gnu.org/pub/gnu/bash/${name}-${version}.tar.gz"
	groups="app.shell"
	setup()	{
		cd $SOURCEDIR
		./configure --prefix=/usr --libdir=/usr/lib64 	--bindir=/bin \
			--with-curses --enable-readline	--without-bash-malloc
	}
	build()	{
		make 
	}
	package()	{
		make install DESTDIR=$DESTDIR
		cd $DESTDIR/bin
		ln -s bash sh
	}
**klybild dosyalarında Kullanılan Değişkenler**
-----------------------------------------------

- **ROOTBUILDDIR:** /home/$user/distro/build → Derleme dizini
- **BUILDDIR:** /home/$user/distro/build/build-${name}-${version} → Paket derleme dizini
- **DESTDIR:** /home/$user/distro/rootfs → Yükleme dizini
- **PACKAGEDIR:** $(pwd) → Derleme scriptinin bulunduğu dizin
- **SOURCEDIR:** /home/$user/distro/build/${name}-${version} → Kaynak dizin

Değişkenleri dereleme scripleri içinde kullanılmaktadır. Örneğin, kaynak dizinde işlem yapmak için sadece **$SOURCEDIR** kullanmanız yeterlidir. Bu yapılar tüm paketlerde geçerli olacak.


**Not:** Bazı paketlerin ek dosyaları olabilir. Derleme scripti altında **Ek dosya için tıklayınız** bağlantısını(link) kullanarak ek dosyaları indirin ve paketin dizini içine çıkartınız. **bash** paketinin ek dosyaları olsaydı **bash** dizini içine indiğimiz dosyayı  arşivde çıkartacaktık. 

.. raw:: pdf

   PageBreak
   
**kly-paket** dizini konumunda aşağıdaki gibi terminal açınız. 

.. image:: /_static/images/kly-paket-yap2.png
  :width: 600

Açılan terminalde aşağıda görüldüğü gibi komutu çalıştırınız. komut hangi konumda çalıştırılmışsa **.kly** uzantılı pakeyimiz orada oluşacaktır. Siz istediğiniz yerde çalıştırabilirsiniz. Önemli olan paket için oluştuduğunuz **klybuild** dosyanınızın konumunu doğru vermeniz.

.. image:: /_static/images/kly-paket-yap3.png
  :width: 600
  
.. raw:: pdf

   PageBreak

Aşağıda **bash** dizinini parametre olarak vererek **bash** paketimizin derlemesini başlatıyoruz.

.. image:: /_static/images/kly-paket-yap4.png
  :width: 600

Derleme işlemi paketin büyüklüğüne bağlı olarak zaman alacaktır. Paket derlemesi bittikten sonra aşağıda görüldüğü gibi termina çıktısı almalısınız. Sorun çıkması durumunda terminalde hata mesajları alırsınız.

.. image:: /_static/images/kly-paket-yap5.png
  :width: 600
  
Derleme işlemi bittikten sonra **kly-paket/bash** dizini komununda  aşağıda görüldüğü gibi **bash-5.2.21.kly** paketimizi oluşturacaktır.

.. image:: /_static/images/kly-paket-yap6.png
  :width: 600
  
.. raw:: pdf

   PageBreak

**kly ile Paket Kur**
---------------------

kly Paket Sistemi ile paket oluşturma konusunda **bash** paketi derlenmişti. Şimdi ise bu paketi **Temel Sistem** üzerine kopyalamayı ve kurma işlemini yapalım. **bash** paketimiz masaüstümüzde **kly-paket/bash/bash-5.2.21.kly** konumunda bulunmaktadır. Bu konumdaki dosyamızı **Temel Sistem** üzerine **scp** veya **sftp** kullanarak kopyalayabiliriz. **scp** terminal üzerinden kopyalar. **sftp** terminal veya pencere yöneticisi üzerinden kopyalar. Burada tercih size kalmıştır. **sftp** ile pencere yöneticisini kullanmak daha kolay olabilir. **scp ve sftp** kullanımı **Yardımcı Konular** bölümünde detaylıca anlatılmıştır. Ayrıca **Temel Sistemin Hazırlanması** bölümünde de **scp** ve **sftp** **Temel Sistem** ile nasıl kullanılacağı anlatıldı.

Aşağıda **sftp** ile  nasıl bağlantı yapılacağı görülmektedir. 

.. image:: /_static/images/kly-paket-kur1.png
  :width: 600
  
Aşağıda **sftp** ile **bash-5.2.21.kly** paketini kopyalanma öncesi **Temel Sistemde** olup olmadığını **ls -la** komutuyla kontrol ediyoruz.

.. image:: /_static/images/kly-paket-kur2.png
  :width: 600


.. raw:: pdf

   PageBreak
   
Kopyalama işleminden sonra **bash-5.2.21.kly** paketinin **Temel Sistemde** olup olmadığını **ls -la** komutuyla görüyoruz.

.. image:: /_static/images/kly-paket-kur3.png
  :width: 600
  
kly paket sistemini kullanarak yerelde bulunan paketin kurulumunu **kly -pi bash-5.2.21.kly /** komutuyla yapıyoruz.

.. image:: /_static/images/kly-paket-kur4.png
  :width: 600
  

.. raw:: pdf

   PageBreak

**kly ile Paket Kaldir**
------------------------

**kly Paket Sistemiyle** sistemde yüklü olan bir paketi **kly -r paketadı** şeklide komut kullanılarak kaldırılabilir. Daha önce paket oluşturma ve paket kurulum işlemlerinde **bash** paketini kullanmıştık. Şimdi **bash** paketini kaldırmamız durumunda sistemde terminali kulanamaz duruma getirecektir. Bazı temel paketleri kaldırmak sistemimizin bozulmasına sebep olabilir. Paket kaldırırken dikkatli olmak gerekir.

Aşağıda **bash** paketinin nasıl kaldırılacağı görülmektedir.

.. image:: /_static/images/kly-paket-kaldir1.png
  :width: 600
  
Bazı paketleri **(glibc, ncurses, readline, bash)** tasarladığımız **kly** paket sisteminde kaldırılmasını engelledik. Bu paketler kalması durumunda sistem kullanılamaz hale gelir. Eğer değişiklik gerekiyorsa sadece yeniden kurulum yapılabilir. Aşağıda paketin kaldırılamadığı mesajı görülmektedir.

.. image:: /_static/images/kly-paket-kaldir2.png
  :width: 600

**glibc, ncurses, readline, bash** dışında başka paketler olsaydı paket kaldırılması gerçekleşecekti.
 
.. raw:: pdf

   PageBreak

**kly Paketlerini Githuba Yükleme ve İndexleme**
++++++++++++++++++++++++++++++++++++++++++++++++

Depo, paketlerimizin olduğu alandır. Depoda ne kadar paket varsa bunların isimleri sürüm numaraları gibi bilgiler ile adreslerini liste halinde oluşturma işlemine **depo indexleme** denir.
Depo indexlenirken genellikle bilgiler **paket derleme talimatı(klybuild)** dosyasından alınır.
Paketlerin listesi, paketler kurulurken, silinirken ve güncellenirken kullanılmaktadır.

**kly github Depo Yapma**
-------------------------

Bu doküman kullanılarak hazırlanan paketleri bilgisayarınızda bir dizinde tutabiliriz. Fakat bu çok kısıtlı bir sistem olmasına sebep olacaktır. Paketleri bir internet ortamında bir yerde saklayarak, kurmak istediğimizde internet(uzak) üzerinden kurulması daha doğru bir yöntemdir. Bu dağıtımda paketlerimizi github.com üzerinde oluşturulan bir repository üzerinden çekilmektedir. İnternetteki paketlerimizin listesi her yeni paketi yükleme sırasında güncellenmektedir. Bu işlem github hesabı üzerinden yapılmaktadır. github hakkında temel işlemler için :ref:`githubbilgi` konusunu okuyunuz.


**github Sitesi Açılır**
........................

Singup seçeneği seçilerek bir hesap oluşturulur. Biz bu dokumanda kullandığımız kendilinuxunuyap hesabını açtık.

.. image:: /_static/images/github0.png
  :width: 600
  
**github Üzerinden Hesaba Giriş Yapılır**
.........................................

github hesabı açılır(kendilinuxunuyap) ve sağ tarafta bulunan menüden **Your repostrores** seçilir.

.. image:: /_static/images/github1.png
  :width: 600

.. raw:: pdf

   PageBreak
   
**Yeni Depo Alanı Oluşturulur**
...............................

Karşımıza gelen ekrandan **New** Seçeneği seçilir. 

.. image:: /_static/images/github2.png
  :width: 600

github repository oluşturulur(kly-binary-packages)

.. image:: /_static/images/github3.png
  :width: 600

.. raw:: pdf

   PageBreak

**kly-binary-packages Depomuz Yerele(Bilgisayara) Kopyalanır(Clone)**
.....................................................................

**kly-binary-packages** adresi kopayanır.

.. image:: /_static/images/github5.png
  :width: 600

Yerelde(bilgisayarda) istediğiniz yere(masaüstünü tercih ettim) indirilir(klonlanır/download).

.. image:: /_static/images/github6.png
  :width: 600


.. raw:: pdf

   PageBreak

**Paketimiz kly-binary-packages Dizinine Kopyalanır**
.....................................................


.. image:: /_static/images/github7.png
  :width: 600

**bash** paketi aşağıdaki gibi taşınır.

.. image:: /_static/images/github71.png
  :width: 600


.. raw:: pdf

   PageBreak
   
**index Dosyası Oluşturulur**
.............................


Aşağıdaki script kly paket dosyalarımızı olduğu dizinde tek tek açarak içerisinden **klybuild** dosyalarını çıkartır. Paketle ilgili bilgileri alıp **index.lst** dosyası oluşturmaktadır. İstersek paketler local ortamdada index oluşturabiliriz. Bu dokümanda github üzerinde oluşturacak şekilde anlatılmıştır. Paket indeksi oluşturan **index.lst** dosyası aşağıdaki gibi olacaktır. Listede name, version ve depends(bağımlı olduğu paketler) bilgileri bulunmaktadır. Bilgilerin arasında **|** karekteri kullanılmıştır.


.. image:: /_static/images/github80.png
  :width: 600
  
Yukarıda gösterildiği gibi **kly-binary-packages** dizininde aşağıda verilen **index** dosyasını oluşturunuz. Aşağıdaki script kodlarını **index** dosyasının içerisine ekleyin.

.. code-block:: shell

	#-------------------------------------------------------------------------------------------------------------------------------
	#!/bin/sh
	#set -ex
	mkdir /output -p
	mkdir -p /klysource
	>index.lst
	find * -type f -name *.kly |
			while IFS= read file_name; do
				dosya="$(dirname $file_name)/klybuild"
				version=$(cat $dosya|grep version=)
				name=$(cat $dosya|grep name=)
				depends=$(cat $dosya|grep depends=)
				echo "$name|$version|$depends|$(dirname $file_name)">>index.lst
			done
	cp -rf index.lst /output

	# *****************************source files******************************
	cp -prfv ./* /klysource/

	find /klysource/* -type f -name *.kly |
			while IFS= read file_name; do
			rm -rf "$file_name"
			done
	tar -cf /output/klysourcepackage.tar /klysource/
	rm -rf /klysource

.. raw:: pdf

   PageBreak
   
**main.yml Dosyası Oluşturulur**
................................

github'a dosya gönderdiğimizde **index** bash scriptimizi çalıştırması için aşağıda gösterilen şekilde **kly-binary-packages** dizinine  **.github/workflows** dizinini oluşturun. **.github/workflows** dizini içine **main.yml** dosyasını oluşturunuz.

.. image:: /_static/images/github8.png
  :width: 600

**main.yml** dosyasısdaki **sh index** satırı **index** scriptimizi her githuba paket gönderdiğimizde(commit) çalışacak ve **index.lst** dosyasını oluşturacaktır. **main.yml** içeriğine aşağıdaki kodları ekleyiniz.


.. code-block:: shell

	#-------------------------------------------------------------------------------------------------------------------------------
	name: CI

	on:
	  push:
		branches: [ master ]
	  schedule:
		- cron: "0 0 1 2 6"

	jobs:
		compile:
		    name: depoindex
		    runs-on: ubuntu-latest
		    steps:
		      - name: Check out the repo
		        uses: actions/checkout@v2
		      - name: Run the build process with Docker
		        uses: addnab/docker-run-action@v3
		        with:
		            image: debian:testing
		            options: -v ${{ github.workspace }}:/root -v /output:/output
		            run: |
		                cd /root
		                sh index
		      - uses: "marvinpinto/action-automatic-releases@latest"
		        with:
		            repo_token: "${{ secrets.GITHUB_TOKEN }}"
		            automatic_release_tag: "current"
		            prerelease: false
		            title: "Latest release"
		            files: |
		              /output/*

**Not:** Burada **main.yml** dosyasında **[ master ]** ifadesi **master** dalında çılışıldığını ifade eder. Eğer faklı dalla açılışıyorsak buradaki **[ master ]** yerine kullandığınız dalı yazınız.

.. raw:: pdf

   PageBreak

**github Dosya oluşturma İzni Verin**
.....................................

İnternet üzerinden **kly-binary-packages** reposunda settings->action->general->Workflow permissions->Read and write permissions  işaretlenmelidir.

.. image:: /_static/images/github4.png
  :width: 600
  
**github'a  kly-binary-packages Dizinini Yükleyelim(Uplod/Commit)**
...................................................................

Yerelde **kly-binary-packages** dizini içeriğini github üzerine aşağıdakı gibi gönderilir.

.. image:: /_static/images/github9.png
  :width: 600



.. raw:: pdf

   PageBreak
   
**github  kly-binary-packages Depo Kontrolü**
.............................................

Depomuza gönderdikten sonra aşağıdaki gibi gözükecektir.

.. image:: /_static/images/github10.png
  :width: 600



**index.lst İçeriği**
---------------------

https://github.com/kendilinuxunuyap/kly-binary-packages/releases/download/current/index.lst adresinde bulunan dosya aşağıdaki gibi liste oluşturacaktır.


.. image:: /_static/images/github11.png
  :width: 600


**index.lst** içeriği aşağıdaki gibidir. Tek paket olduğu için(sadece bash) bu şekilde gözüküyor.

.. code-block:: shell

	name="bash"|version="5.2.21"|depends="glibc,readline,ncurses"|bash

Birden fazla paketin olması durumunda aşağıdaki gibi gözükecektir.

.. code-block:: shell

	name="acl"|version="2.3.1"|depends="attr"|acl
	name="attr"|version="2.5.1"|depends=""|attr
	name="audit"|version='3.1.1'|depends=""|audit
	name="bash"|version="5.2.21"|depends="glibc,readline,ncurses"|bash



.. raw:: pdf

   PageBreak


**kly ile Paket Listelerini Güncelleme**
----------------------------------------

**kly Paket Sistemi** yerelde **.kly** paketlerini **kly -pi paket.kly** şeklinde kurulabilir. Ama bütün paketlerin yerelde olması bu sistemi kullanacak kişi sayısını sınırlandıracak ve birkaç  kişiyi geçmeyecektir. Paketleri internet ortamında tutmak sistemi kullanacak kişilerin sayısnı artıracak ve istenilen zaman ve konumda paketlere erişim imkanı sunacaktır. 


kly paketleri github üzerinde tutulmaktadır. Bu paketlerin listesini tutan index dosyası github ortamında **https://github.com/kendilinuxunuyap/kly-binary-packages/releases/download/current/index.lst** adresinde tutulmaktadır. Bu adresi sisteme kaydetmeliyizki güncelleme sırasında bu adreslerden güncel **index.lst** dosyasını yerele indirebilmeli. Adreslerin listesini tutan dosyamız **/etc/kly/sources.list** konumunda turulmaktadır. Debianda da benzer(/etc/apt/sources.list) durum bulunmaktadır.

.. image:: /_static/images/kly-paket-guncelle1.png
  :width: 600


Yerelde **(Temel Sistem)** ise **/var/lib/kly/index.lst** dosyamızda paketlerin listesi tutulur. Mevcut sisteme yeni bir paket yaptık ve github'a yüklediğimizi varsayalım. Bu durumda yerelde **(Temel Sistem)** ise **/var/lib/kly/index.lst** konumundaki dosyanında https://github.com/kendilinuxunuyap/kly-binary-packages/releases/download/current/index.lst adresindeki dosyayla aynı olması gerekir. Bu senaryo tüm linux dağıtımlarında aynıdır. Bu sebeplerden dolayı bir paket kurulum öncesi genelde **güncelleme** işlemi yapılır.
Aşağıda güncelleme işleminin yapıldığını göstermektedir.

.. image:: /_static/images/kly-paket-guncelle2.png
  :width: 600


Aşağıda  **/var/lib/kly/index.lst** konumundaki dosyanın içeriğini görmekteyiz.

.. image:: /_static/images/kly-paket-guncelle3.png
  :width: 600


.. raw:: pdf

   PageBreak

.. _klypaketsistemikullanimi:
**kly Paket Sistemi Kullanımı**
===============================

**VirtualBox**
++++++++++++++

VirtualBox, Oracle tarafından geliştirilen bir açık kaynaklı sanallaştırma yazılımıdır. Bilgisayarınızda çalışan bir işletim sisteminin (örneğin Windows, Linux, macOS) içinde başka bir işletim sistemi çalıştırmanıza izin verir. Bu çalıştırdığınız ikinci işletim sistemi (konuk/guest) kendi sanal donanımına sahipmiş gibi davranır. 

.. code-block:: shell

	sudo apt update				# index güncellenir
	sudo apt install virtualbox-7.0  	# Sisteme virtualbox kurulur
		
.. image:: /_static/images/vb1.png
  :width: 600
  :height: 350
  
Ekle seçeneğini seçin. Aşağıdaki gibi bir ekran gelecektir.
   
.. image:: /_static/images/vb2.png
  :width: 600
  :height: 350
  
.. raw:: pdf

   PageBreak

Aşağıdaki gibi seçenekleri doldurunuz.
   
.. image:: /_static/images/vb3.png
  :width: 600
  :height: 400

**İleri** seçeneği seçilir ve aşağıdaki gibi ekrana gelirsiniz. Bellek miktarını aşağıdaki gibi belirleyiniz. **İleri** seçeneği seçilir.

.. image:: /_static/images/vb4.png
  :width: 600
  :height: 400
  
.. raw:: pdf

   PageBreak

Disk boyutu belirlenir. 8GB bu sistem için yeterli. **İleri** seçeneği seçilir.
   
.. image:: /_static/images/vb5.png
  :width: 600
  :height: 400

Tüm işlemler bitince aşağıdaki gibi pencere gelir. Bitir'i seçerek işlem tamamlanır.

.. image:: /_static/images/vb6.png
  :width: 600
  :height: 400
  
.. raw:: pdf

   PageBreak

Bitir işlemi seçildikten sonra aşağıdaki gibi görünecektir.

.. image:: /_static/images/vb7.png
  :width: 600
  :height: 400

Ayarlar bölümünde aşağıdaki gibi **Ağ** ayarında değişiklik yapılır.

.. image:: /_static/images/vb8.png
  :width: 600
  :height: 400
  
.. raw:: pdf

   PageBreak

Başlat seçilerek sistem çalıştırılır.

.. image:: /_static/images/vb9.png
  :width: 600
  :height: 400  

**İso** açıldığıda aşağıdaki gibi ekran gelecektir. Burada seçili olan iso **Temel Sistem** isosudur.
 
.. image:: /_static/images/vb10.png
  :width: 600
  :height: 400
  
.. raw:: pdf

   PageBreak


**Kaynak Kod Derleme**
++++++++++++++++++++++

Bir uygulamanın kodları genellikle çalışmaz(python benzeri kodlar istisna). Bu kodlardan sistemlerin çalışması için çalışabilir dosyalar üretilir(linuxta ikili dosya, elf, windowsta exe, com vb.). Bu çalışabilir dosyaları koddan oluştururken iki faklı şekilde oluşturabiliriz.

1- **Paylaşımlı Derleme(dynamic):** Kendine lazım olan kütüphaneleri sistem üzerindeki başka uygulamalarla ortak kullanır. 
2- **Paylaşımsız, gömülü(static):** Kendisine lazım olan kütütphaneleri kendi içinde barındırır(porable uygulama gibi).

Şimdi aşağıdaki kaynak kodumuzu iki farklı yöntemle derleyelim.

.. code-block:: C

	//main.c dosyamız
	#include <stdio.h>
	void main(){
	    printf("Merhaba\n");
	}


**2-Paylaşımlı Derleme(dynamic):** 
--------------------------------

Derlenen uygulama  sistemde bulunan kütüphaneleri kullanacak şeklide derlenmesidir. Uygulama boyutu küçüktür, taşınabirliği sınırlanabilir.
Aşağıdaki gibi derlenir.

.. code-block:: shell

	gcc -o main main.c

main.c kodumuzu **main** adında ikili çalışabilir dosyaya dönüşütürdük. **ldd** komutuyla **main** dosyasının kullandığı kütüphaneler öğrenilir.

.. code-block:: shell

	unset LD_PRELOAD
	ldd ./main 
		linux-vdso.so.1 (0x00007ffdb3bb9000)
		libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007f2c53fe0000)
		/lib64/ld-linux-x86-64.so.2 (0x00007f2c541e7000)


Burada **libc.so.6** ve **ld-linux-x86_64.so.2** dosyaları **glibc** tarafından sağlanır. 
Derlenmiş dosyanın çalışması için tüm bağımlılıklarının sistemde bulunması gereklidir.Sadece gerekli olan kütüphaneleri görmek için   **readelf -d** komutu kullanılabilir. Aşağıda gerekli olan kütüphaneler listeleniyor.
 
.. code-block:: shell

	readelf -d ./main | grep -i needed 
		0x0000000000000001 (NEEDED)             Paylaşımlı kitaplık: [libc.so.6]
		


**ldconfig**
------------

Sistemdeki kütüpkhanelerin konumlarını **/etc/ld.so.conf** dosyasına bakarak belirler. 

.. code-block:: shell
	
	#/etc/ld.so.conf dosyası
	/usr/lib64
	/usr/lib
	/lib64
	/lib

Kütüphanelerde değişiklik yapılmışsa ve hemen bu değişikliği sistemin görmesini istersek **ldconfig** komutu kullanılmalıdır.

.. raw:: pdf

   PageBreak

**2-Paylaşımsız, gömülü(static):**
--------------------------------

Derlenen uygulama sistemde  bulunan ve çalışması için gerekli olan kütüphaneleri uygulama içine dahil eden bir derleme yöntemidir. Uygulamamızı static derlemek için  **-static** parametresi ekleyerek derlenir.

.. code-block:: shell

	gcc -o main main.c -static

Paylaşımlı(dynamic) derleme işleminde bağımlı olduğu dosyaları **ldd** komutunu kullanarak öğrenmiştik. Şimdi paylaşımsız derlediğimiz **main** dosyasında bağımğımlı olduğu kütüphaneleri kontrol ediyoruz.

.. code-block:: shell

	ldd main
	    not a dynamic executable

Bağımlı kütüphaneler yerine **not a dynamic executable** mesajı gördük. Bunun anlamı çalışması için hiçbir kütüphaneye ihtiyaç duymaz. Bu bir avantaj ve taşınabirliği artırır. Devevantajı ise boyutu büyük olur. İhtiyaca göre paylaşımlı veya paylaşımsız derleme tercih edilir.


.. raw:: pdf

   PageBreak




**Derleme Araçları**
++++++++++++++++++++

Linux sistemlerinde kodlarımızı derlemek  kullanılan uygulamalara derleme araçları denir. Birden fazla araç olsada  en temel derleme araçları **make**, **cmake**, **meson**, **python**.




**1-make**
++++++++++

make, yazılım geliştirme süreçlerinde sıkça kullanılan bir araçtır. Özellikle C ve C++ gibi dillerde projelerin derlenmesi ve yönetilmesi için kullanılır.

Aşağıdaki C kodumuzu(merhaba.c dosyası) make ile nasıl derleyeceğimizi anlatalım;

.. code-block:: C
	
	#include <stdio.h>
	int main(){
	    puts("Merhaba");
	    return 0;
	}


Makefile Nedir?
---------------

Makefile, make aracının nasıl çalışacağını belirten bir dosyadır. İçinde hedefler, bağımlılıklar ve komutlar bulunur. Örneğin, bir C programını derlemek için aşağıdaki gibi basit bir Makefile oluşturabilirsiniz. Makefile ve merhaba.c dosyası aynı konumda olmalıdır.

.. code-block:: shell

	CC=gcc
	CFLAGS=-I.
	all: program
	program: merhaba.o 
		$(CC) -o program merhaba.o
	merhaba.o: merhaba.c
		$(CC) -c merhaba.c $(CFLAGS)
	clean:
		rm -f *.o program

merhaba dosyasından **program** adında bir ikili dosya oluşturmak için aşağıdaki komutlar Makefile ve merhaba.c dosyasının olduğu konumda çalıştırılır.

.. code-block:: shell

	make
	make install

Genellikle Makefile dosyası olmaz. Onun yerine **configure.ac** dosyası olur. **configure.ac** dosyasından **Makefile** dosyası elde etmek için, öncelikle **autoconf** ve **automake** araçlarının sisteminizde kurulu olması gerekmektedir. 

**autoreconf -fvi** komutu çalıştırılıarak configure dosyamızı üretir.Bu araçlar, yapılandırma dosyalarınızı işleyerek gerekli **Makefile** dosyalarını oluşturmanıza yardımcı olur.

**configure** komutunun devamında **--prefix** dışında başka parametreleride olabilir. Bu paramatreleri "Read.me" dosyası içerisinde bulunabilir veya **configure --help** komutu kaynak kodların olduğu konumda kullanılarak görülebilir. Bu kaynak kod aşağıdaki gibi derlenir.

.. code-block:: shell

	$ autoreconf -fvi
	$ ./configure --prefix=/usr
	$ make
	$ make install 
	
.. raw:: pdf

   PageBreak


**2-cmake**
+++++++++++

CMake, projelerin derlenmesi ve yapılandırılması için kullanılan bir araçtır. Bir paketi CMake ile derlemek için genellikle aşağıdaki adımları izleriz:

    İlk olarak, projenin kök dizininde bir CMakeLists.txt dosyası oluşturun.
    Ardından, CMake komutunu kullanarak projeyi yapılandırın ve derleyin. Örneğin:

.. code-block:: shell

	mkdir compile_packages
	cd compile_packages
	cmake ..
	make

    Bu adımları takip ederek, CMake ile paketinizi başarıyla derleyebilirsiniz.

CMake'in esnekliği ve kullanım kolaylığı sayesinde paketlerin derlenmesi ve yapılandırılması oldukça kolay hale gelir.


Bu kaynak kod aşağıdaki gibi derlenir:

.. code-block:: shell

	mkdir compile_packages
	cd compile_packages
	cmake ..
	make
	make install
	


**3-meson**
+++++++++++

Meson, modern bir yapılandırma betik dili ve Ninja ise hızlı bir derleyici aracıdır. Bir paketi derlemek için öncelikle Meson ile yapılandırma dosyalarını oluşturmanız gerekir. Ardından, Ninja derleyici aracını kullanarak bu yapılandırmayı derleyebilirsiniz.

İlk olarak, projenizin dizinine gidin ve Meson ile yapılandırma dosyalarını oluşturun:

.. code-block:: shell

	meson setup builddir --prefix=/usr

Sonra, oluşturulan builddir dizinine geçin ve Ninja ile derlemeyi başlatın:

.. code-block:: shell

	ninja -C builddir

Bu adımları takip ederek Meson ve Ninja kullanarak paketinizi başarılı bir şekilde derleyebilirsiniz.



Bu kaynak kod aşağıdaki gibi derlenir:

.. code-block:: shell
	
	# paketin yükleneceği konum
	INSTALL_ROOT=/
	meson setup builddir --prefix=/usr
	ninja -C builddir
	INSTALL_ROOT=$INSTALL_ROOT ninja -C builddir install
	
.. raw:: pdf

   PageBreak


**4-python**
++++++++++++

Python ile paket derlemek için genellikle **setuptools** ve **distutils** gibi kütüphaneler kullanılır. Öncelikle, projenizin kök dizininde bir **setup.py** dosyası oluşturmanız gerekir. Bu dosya, paketin yapılandırmasını ve gereksinimlerini tanımlar.

Örnek bir setup.py dosyası aşağıdaki gibi olabilir:

.. code-block:: shell

	from setuptools import setup

	setup(
	    name='paket_adi',
	    version='1.0',
	    packages=['paket'],
	    install_requires=[
		'bağımlılık_paketi',
	    ],
	)

Ardından, terminalde projenizin bulunduğu dizine giderek aşağıdaki komutu çalıştırarak paketi derleyebilirsiniz:

.. code-block:: shell
	# yükleme konumu
	INSTALL_ROOT=/
	python3 -m compile_packages
	python3 -m installer --destdir="$INSTALL_ROOT" dist/*.whl

Bu komut, paketi dist klasörüne derleyecektir. Artık paketiniz hazır ve dağıtıma uygun hale gelmiştir.

.. raw:: pdf

   PageBreak


**OpenRC**
++++++++++

Openrc sistem açılışında çalışacak uygulamaları çalıştıran servis yöneticisidir.

**Çalıştırılması**
------------------

Openrc servis yönetiminin çalışması için boot parametrelerine yazılması gerekmektedir.  
**/boot/grub.cfg** içindeki  
**linux /vmlinuz init=/usr/sbin/openrc-init root=/dev/sdax**  
olan satırda  
**init=/usr/sbin/openrc-init**  
yazılması gerekmektedir. Artık sistem openrc servis yöneticisi tarafından uygulamalar çalıştırılacak ve sistem hazır hale getirilecek.

**openrc Kullanımı**
--------------------

Servis etkinleştirip devre dışı hale getirmek için **rc-update** komutu kullanılır.  
Aşağıda **udhcpc** internet servisi örnek olarak gösterilmiştir.  
**/etc/init.d/** konumunda **udhcpc** dosyamızın olması gerekmektedir.

.. code-block:: shell

    # servis etkinleştirmek için
    rc-update add udhcpc boot
    # servisi devre dışı yapmak için
    rc-update del udhcpc boot
    # Burada udhcpc servis adı, boot ise runlevel adıdır.

Elle **/etc/runlevels/** altında bulunan **boot**, **default**, **nonetwork**, **shutdown**, **sysinit** dizinlerine  
**/etc/init.d/** dizininin altındaki dosyaları **ln** komutuyla kısayol yaparsak  
**rc-update add** komutunun yaptığı görevi yapmış oluruz.  
Kısayolu silersek **rc-update del** komutunun görevini yapmış oluruz.

**/etc/runlevels/** altında bulunan **boot**, **default**, **nonetwork**, **shutdown**, **sysinit** dizinler servis dosyalarımızın hangi sırayla çalışacağını belirleyen dizinlerdir.  
Mesela **boot** dizini ilk açılış sırasında çalışacak olan servis dosyalarının konulacağı dizindir.

Servisleri başlatıp durdurmak için ise **rc-service** komutu kullanılır.

.. code-block:: shell

    rc-service udhcpc start
    # veya şu şekilde de çalıştırılabilir.
    /etc/init.d/udhcpc start

Servislerin durumunu öğrenmek için **rc-status** komutu kullanılır. Ayrıca  
sistemdeki servislerin sonraki açılışta hangisinin başlatılacağını öğrenmek için  
parametresiz olarak **rc-update** kullanabilirsiniz.

.. code-block:: shell

    # şu an hangi servislerin çalıştığını gösterir
    rc-status
    # sonraki açılışta hangi servislerin çalışacağını gösterir
    rc-update

Sistemi kapatmak veya yeniden başlatmak için **openrc-shutdown** komutunu kullanabilirsiniz.

.. code-block:: shell

    openrc-shutdown -p 0     # kapatmak için
    openrc-shutdown -r 0     # yeniden başlatmak için

.. raw:: pdf

   PageBreak

**Servis Dosyası**
------------------

Openrc servis dosyaları basit birer **bash** betiğidir. Bu betikler **openrc-run** komutu ile çalıştırılır ve çeşitli fonksiyonlardan oluşabilir.  
Servis dosyaları **/etc/init.d** içerisinde bulunur.  
Servisleri ayarlamak için ise **/etc/conf.d** içerisine aynı isimle ayar dosyası oluşturabiliriz.

Çalıştırılacak komut, komut parametreleri ve **pidfile** dosyamızı aşağıdaki gibi belirtebiliriz.

.. code-block:: shell

    description="Ornek servis"
    command=/usr/bin/ornek-servis
    command_args=--parametre
    pidfile=/run/ornek-servis.pid

Bununla birlikte **start**, **stop**, **status**, **reload**, **start_pre**, **stop_pre** gibi fonksiyonlar da yazabiliriz.

.. code-block:: shell

    start(){
        ebegin "Starting ${RC_SVCNAME}"
        start-stop-daemon --start --pidfile "/run/servis.pid" --exec /usr/bin/ornek-servis --parametre
    }

Servis bağımlılıklarını belirtmek için ise **depend** fonksiyonu kullanılır.

.. code-block:: shell

    depend() {
      need localmount
      after dbus
    }

.. raw:: pdf

   PageBreak



**Qemu Kullanımı**
++++++++++++++++++

qemu açık kaynaklı Virtual Box, Vmware benzeri sanallaştırma aracıdır. 

Sisteme Kurulum
---------------

.. code-block:: shell

    sudo apt update
    sudo apt install qemu-system-x86  qemu-utils

qemu Kullanımı
--------------
    
.. code-block:: shell

    # 30GB disk oluşturuldu.
    qemu-img create disk.img 30G
    qemu-system-x86_64 --enable-kvm -hda disk.img -m 2G -cdrom etahta.iso
    # qemu-system-x86_64 --enable-kvm -hda disk.img -m 2G #sadece disk ile çalıştırılıyor
    # qemu-system-x86_64 -m 2G -cdrom etahta.iso          #sadece iso dosyası ile çalıştırma

Sistem Hızlandırılması
----------------------

**--enable-kvm** eğer sistem disk ile çalıştırıldığında bu parametre eklenmezse yavaş çalışacaktır.

Boot Menu Açma
--------------

Sistemin diskten mi imajdan mı başlayacağını başlangıçta belirlemek için boot menu gelmesini istersek aşağıdaki gibi komut satırına seçenek eklemeliyiz.
    
.. code-block:: shell
    
    qemu-system-x86_64 --enable-kvm -cdrom distro.iso -hda disk.img -m 4G -boot menu=on  

Uefi kurulum için:
------------------

sudo apt-get install ovmf

qemu-system-x86_64 --enable-kvm -bios /usr/share/ovmf/OVMF.fd -cdrom distro.iso -hda disk.img -m 4G -boot menu=on   

qemu Host Erişimi:
------------------

İstemci bilgisayar ip'si:10.0.2.15 ve ana bilgisayar 10.0.0.2 olarak ayarlıyor.

vmlinuz ve initrd
-----------------
qemu ile vmlinuz ve initrd.img dosyaları iso olmadan test edilebilir.

.. code-block:: shell

    qemu-system-x86_64 --enable-kvm -kernel /boot/vmlinuz-5.17 -initrd /home/deneme/initrd.img -append "quiet" -m 512m

qemu Terminal Yönlendirmesi
----------------------------

.. code-block:: shell
    
    qemu-system-x86_64 --enable-kvm -kernel vmlinuz -initrd initrd.img -m 3G -serial stdio -append "console=ttyS0"

Diskteki Sistemin Açılışını Terminale Yönlendirme
-------------------------------------------------

.. code-block:: shell
    
    qemu-system-x86_64 -nographic -kernel boot/vmlinuz -hda disk.img -append console=ttyS0

Kaynak:
| https://www.ubuntubuzz.com/2021/04/how-to-boot-uefi-on-qemu.html  

.. raw:: pdf

   PageBreak


.. _githubbilgi:
**github**
++++++++++

GitHub üzerinde yeni bir depo açmak oldukça basit bir işlemdir. Aşağıdaki adımları takip ederek hızlıca kendi deponuzu oluşturabilirsiniz:


  
**GitHub Hesabınıza Giriş Yapın**
---------------------------------

GitHub ana sayfasına gidin ve hesabınıza giriş yapın. Eğer bir hesabınız yoksa, öncelikle bir hesap oluşturmalısınız.

.. image:: /_static/images/github0.png
  :width: 600
  
.. image:: /_static/images/github1.png
  :width: 600
  
  
**Yeni Depo Oluşturma**
-----------------------

 Sağ üst köşede bulunan "+" simgesine tıklayın ve "New repository" seçeneğini seçin.

.. image:: /_static/images/github2.png
  :width: 600

.. raw:: pdf

   PageBreak
   
  
**Depo Bilgilerini Girin**
--------------------------

 Açılan sayfada, depo adını (repository name) ve isteğe bağlı olarak bir açıklama (description) girin. Depo özel (private) veya herkese açık (public) olarak ayarlanabilir.

.. image:: /_static/images/github3.png
  :width: 600
 

 
**İlk Dosyayı Oluşturma**
-------------------------

 "Initialize this repository with a README" seçeneğini işaretleyerek, depo oluşturulduğunda otomatik olarak bir README dosyası oluşturabilirsiniz.

 .. image:: /_static/images/github5.png
  :width: 600
 
.. raw:: pdf

   PageBreak
   
**github Varsayılan Dal Ayarı:**
--------------------------------

githubda varsayılan olarak eskilede master, yeni sürümlerde main kullanılmaktadır. Projelermizde ve burad kullanılan yapılarda **master** kullanıldığı için aşağıda görülduğü gibi varsalılan dalı  **master** yapıyoruz.

.. image:: /_static/images/github-master.png
  :width: 600
  

**github komut Kullanımı**
--------------------------

.. image:: /_static/images/github-command.png
  :width: 600
  
github'ın çalışma mantığı yukarıda verilen resimde görüldüğü gibidir. Komutları kullanırken resimdeki gibi işlemleri yapmalıyız.

github'a göndermek için; **add --> commit --> push** kullanmalıyız.

github'dan indirmek için; **clone veya pull**  kullanmalıyız.

.. raw:: pdf

   PageBreak
   

**Sık Kullanılan github Komutları**
+++++++++++++++++++++++++++++++++++

**Depoyu Yerele indirme(Clone)**
--------------------------------

.. code-block:: shell

	git clone https://github.com/kullaniciadi/depoadi.git

- **Yerel Depoda Dosya Ekleme:**

.. code-block:: shell

	git add .

- **Yerel Depoda Değişiklik Etiketi Yapma:**

.. code-block:: shell

	git commit -m "ilk adım"

- **Yerel Depodaki Bilgileri Guthuba Gönderme:**

.. code-block:: shell

	git push origin master

- **Yerel Depodaki Bilgileri Guthuba Gönderme Reddedilirse:**

.. code-block:: shell

	git push origin master --force

- **Yerelde github'daki Depoyu clone Yapmadan Oluşturma:**

.. code-block:: shell

	cd proje
	git init
	git config --global user.name "name"
	git config --global user.email "name@gmail.com"
	git add README.md
	git add .
	git commit -m "first commit"
	git remote -v      # push ve pull yapılacak adresleri görmek için kullanılır
	git remote add origin https://github.com/userName/repoName.git
	git push -u origin master

**Dal(Branch):**
----------------

Dal projenin birden fazla kişi ile yapılmasında veya yeni özellikler eklenmek istediğinde projenin bir kopyası ile çalışma gerektirir. Aşağıda dal işlemleri içinkomutlar verilmiştir.

**Yeni Dal Oluşturmak, Seçmek ve Yeni Dalı github'a Göndermek:**

.. code-block:: shell

    # Dalları Görmek kullanılır Seçili olan dalın rengi farklı olur ve önünde * olur
    git branch
    # Dal oluşturmak
    git checkout yeni
    # Yeni dalı uzak adrese göndermek
    git push --force origin master komutu  yerine
    # Uzak adresimizde master dalı dışında yeni dalımızda oluşacaktır...
    git push --force origin yeni komutunu veriyoruz.


.. raw:: pdf

   PageBreak
   
**github token Oluşturma Kullanma**
-----------------------------------

github kullanırken dosya gondermek(**commit**) için kullanıcı adı ve parola ister. Burada hesap parolası yerine **token** kullanılır. Yeni bir **token** için aşağıdaki işlem adımlarını yapmalıyız.

**Settings Seçilir;**

.. image:: /_static/images/github-token1.png
  :width: 600

**Developper Settings Seçilir;**

.. image:: /_static/images/github-token2.png
  :width: 600

**Generate New Token Seçilir;**

.. image:: /_static/images/github-token5.png
  :width: 600

.. raw:: pdf

   PageBreak
   
**Erişim yapabileceği alanlar Seçilir;**
 
.. image:: /_static/images/github-token6.png
  :width: 600

**token Kullanmak üzere kullanmak üzere saklanır. Bu ekrandan sonra sadece silebiliriz. Göremeyiz kopyalayamayız.**

.. image:: /_static/images/github-token7.png
  :width: 600



.. raw:: pdf

   PageBreak

**elogind Yapılandırması**
==========================

Bu belge, **systemd kullanmayan** sistemlerde (OpenRC tabanlı) 
elogind login manager'ın kurulumu, yapılandırılması ve gerekli 
kullanıcı/PAM/agetty ayarlarını anlatır.

**1. Gerekli Kullanıcı ve Grup Tanımları**
------------------------------------------

elogind servisi için sistemde gerekli kullanıcı ve gruplar oluşturulur:

.. code-block:: bash

   groupadd -g 190 systemd-journal
   groupadd -g 191 elogind
   useradd -r -s /sbin/nologin -g elogind -u 191 elogind

Açıklama:
.........

- `systemd-journal` grubu, journal log erişimi için kullanılır.
- `elogind` kullanıcı ve grubu, servis için ayrılmıştır.
- `/sbin/nologin` ile bu kullanıcıyla doğrudan login engellenir.
- `-r` parametresi sistemi kullanıcı oluşturur, yani normal login için kullanılmaz.

**2. OpenRC Hizmet Dosyası (/etc/init.d/elogind)**
--------------------------------------------------

OpenRC ile `elogind` servisini yönetmek için basit bir init script örneği:

.. code-block:: bash

   #!/sbin/openrc-run
   description="elogind login manager"
   command=/usr/lib/elogind/elogind
   pidfile=/run/elogind.pid

   depend() {
       need dbus
       after dbus
   }

Açıklama:
.........

- `command`: elogind daemonunu başlatır.
- `pidfile`: servis PID bilgisini saklar.
- `depend()`: servis başlatılmadan önce D-Bus’ın aktif olmasını garanti eder.


.. raw:: pdf

   PageBreak
   
**3. Başlatma ve OpenRC’ye Ekleme**
-----------------------------------

.. code-block:: bash

   rc-update add elogind default
   rc-service elogind start

Açıklama:
.........

- `rc-update add`: Servisi boot sırasında otomatik başlatmaya ekler.
- `rc-service start`: Servisi hemen başlatır.

- **Önemli Kontrol:** elogind’in çalışıp çalışmadığını kontrol etmek için:

.. code-block:: bash

   loginctl list-sessions

- Eğer aktif oturumlar listeleniyorsa, elogind başarıyla çalışıyor demektir.

**4. PAM, Passwd ve Group Ayarları**
------------------------------------

**/etc/nsswitch.conf Örneği:**

.. code-block:: none

   passwd:      files
   group:       files
   shadow:      files

Açıklama:
........

- Kullanıcı ve grup bilgileri `files` (yerel /etc/passwd ve /etc/group) üzerinden çözülür.

**/etc/pam.d/system-auth Örneği:**

.. code-block:: none

   auth       required     pam_unix.so
   account    required     pam_unix.so
   password   required     pam_unix.so
   session    required     pam_unix.so
   session    include      elogind-user

.. note::

   **`session include elogind-user` satırı mutlaka ekli olmalıdır.**  
   Bu satır, kullanıcı oturumlarının elogind ile doğru şekilde yönetilmesini sağlar.  
   Eğer yoksa manuel olarak eklenmelidir:

   .. code-block:: bash

      sed -i "/elogind-user/d" /etc/pam.d/system-auth
      echo -e "\nsession    include    elogind-user" >> /etc/pam.d/system-auth


.. raw:: pdf

   PageBreak
   
**5. OpenRC Agetty Ayarı**
--------------------------

Bazı durumlarda `agetty`, varsayılan olarak `/bin/login` kullanmaz
ve bu nedenle elogind kullanıcı oturumunu başlatamaz.

**Ayar:**

.. code-block:: bash

   sed -i "/agetty_options/d" /etc/conf.d/agetty
   echo -e "\nagetty_options=\"-l /usr/bin/login\"" >> /etc/conf.d/agetty

Açıklama:
.........

- `-l /usr/bin/login` ile agetty doğru login programını çağırır.
- Bu ayar, sanal konsollardan kullanıcı girişlerinin doğru şekilde yapılmasını garanti eder.

**6. Diğer Öneriler ve Notlar**
-------------------------------

- `elogind`, sistemde `/run/systemd` gibi dizinler yaratır; böylece bazı uygulamalar systemd’ye ihtiyaç duymadan çalışabilir.
- Polkit yetkilendirme sorunları genellikle kullanıcıların `wheel` grubuna dahil olmamasıyla ilişkilidir.
- OpenRC + elogind ile systemd’ye gerek kalmadan oturum yönetimi sağlanabilir.

**Kaynaklar**::

- elogind resmi dokümanı: https://www.freedesktop.org/wiki/Software/systemd/elogind/  
- OpenRC belgeleri: https://wiki.gentoo.org/wiki/OpenRC  
- PAM belgeleri: https://www.linux-pam.org/  
- Polkit belgeleri: https://www.freedesktop.org/wiki/Software/polkit/

.. raw:: pdf

   PageBreak


**D-Bus Yapılandırması**
========================

Bu belge, **systemd kullanmayan** sistemlerde (OpenRC tabanlı) 
D-Bus servisinin kurulumu, yapılandırılması ve başlatılmasını anlatır. 
D-Bus, Linux ortamında uygulamalar arasında mesajlaşma sağlayan
bir IPC (Inter-Process Communication) sistemidir.

**Adım 1: Kullanıcı ve Grup Oluşturma**
---------------------------------------

.. code-block:: bash

    echo "messagebus:x:109:" >> /etc/group
    echo "messagebus:x:103:109::/nonexistent:/usr/sbin/nologin" >> /etc/passwd

**Adım 2: Sistem UUID ve machine-id Ayarı**
-------------------------------------------

.. code-block:: bash

    if [ ! -f /etc/machine-id ] ; then
        dbus-uuidgen --ensure=/etc/machine-id
    fi

**Açıklama**::

- `/etc/machine-id` dosyası sistemin benzersiz kimliğini tutar.
- `dbus-uuidgen --ensure` komutu, dosya yoksa oluşturur, varsa korur.
- Bu kimlik, D-Bus servislerinin ve bazı uygulamaların doğru çalışması için zorunludur.

**Adım 3: dbus-daemon-launch-helper İzin Kontrolü**
---------------------------------------------------

.. code-block:: bash

    if busybox ls /bin/su -la | grep "^...s" >/dev/null ; then
        chmod 4755 /usr/libexec/dbus-daemon-launch-helper
    fi

**Açıklama**::

- `dbus-daemon-launch-helper`, kullanıcı bazlı D-Bus daemonlarını başlatır.
- SUID bitinin (4) set edilmesi, root yetkisi ile çalışmasını sağlar.

**Adım 4: D-Bus Yapılandırma Yenileme**
---------------------------------------

.. code-block:: bash

    dbus-send --system --type=method_call --dest=org.freedesktop.DBus / \
        org.freedesktop.DBus.ReloadConfig >/dev/null 2>&1 || :

**Açıklama**::

- Bu komut, D-Bus sistem servisine yeni yapılandırmaları yüklemesini söyler.
- `--system` parametresi sistem bus’ını hedef alır.
- Hata oluşursa komut sessizce geçer (`|| :`).

.. raw:: pdf

   PageBreak
 
**Adım 5: D-Bus Servisini Başlatma (OpenRC)**
---------------------------------------------

D-Bus için OpenRC init script’i `/etc/init.d/dbus` şu mantıkla çalışır:

.. code-block:: bash

    #!/sbin/openrc-run
    #----------------------------------------------------------------------------------------------
    name="System Message Bus"
    description="An IPC message bus daemon"

    extra_started_commands="reload"

    supervisor=supervise-daemon
    command="/usr/bin/dbus-daemon"
    command_args="--system --nofork --nopidfile --syslog-only ${command_args:-}"
    command_background="yes"
    pidfile="/run/$RC_SVCNAME.pid"

    depend() {
        need localmount
        after bootmisc
    }

    start_pre() {
        mkdir -p /run/dbus
        /usr/bin/dbus-uuidgen --ensure=/etc/machine-id
    }

    stop_post() {
        [ ! -S /run/dbus/system_bus_socket ] || rm -f /run/dbus/system_bus_socket
    }

    reload() {
        ebegin "Reloading $name configuration"
        /usr/bin/dbus-send --print-reply --system --type=method_call \
                --dest=org.freedesktop.DBus \
                / org.freedesktop.DBus.ReloadConfig > /dev/null
        eend $?
    }

**Açıklama**::

- `supervise-daemon`: OpenRC’nin daemon’u denetlemesini sağlar.
- `command` ve `command_args`: D-Bus daemonunu sistem bus modunda başlatır.
- `start_pre()`: Servis başlamadan önce gerekli dizini oluşturur ve machine-id’yi doğrular.
- `stop_post()`: Servis durduğunda socket dosyasını temizler.
- `reload()`: Yapılandırma değişikliklerini uygulamak için D-Bus’a mesaj yollar.
- `depend()`: Servisin başlatılması için gerekli bağımlılıklar (localmount, bootmisc) belirtilir.
- `pidfile`: Servisin PID bilgisini tutar.

**Servis Dosyasının Yaptıklar**::

- D-Bus için sistem kullanıcı ve grup oluşturulur.
- machine-id ve gerekli izinler ayarlanır.
- OpenRC init script’i `/etc/init.d/dbus`, servisin başlatılmasını, durdurulmasını ve yeniden yüklenmesini yönetir.
- `rc-service dbus start` ile sistemde mesajlaşma servisi aktif olur.

**Kaynaklar**::

- D-Bus resmi sitesi:https://www.freedesktop.org/wiki/Software/dbus/  
- D-Bus belgeleri:https://dbus.freedesktop.org/doc/dbus/  
- OpenRC belgeleri:https://wiki.gentoo.org/wiki/OpenRC  
- dbus-daemon ve dbus-send man sayfaları:https://manpages.debian.org/dbus-user-session

.. raw:: pdf

   PageBreak


**polkit Yetkilendirme**
========================

Bu kılavuz, lxsession-logout penceresinde "Kapat" ve "Yeniden Başlat" 
işlemlerinin parola doğrulaması açılmasına rağmen başarısız olması sorununu 
çözer. Amaç: *wheel* grubundaki kullanıcıların GUI'den **poweroff/reboot** 
yapabilmesini sağlamak.

**Temel Ayar Kontrolü**
-----------------------

1) Elogind çalışıyor mu?
   ::
      rc-status | grep -E 'elogind|dbus'
      rc-service elogind status

2) Polkit aracı (agent) çalışıyor mu?
   ::
      pgrep -fa lxpolkit || pgrep -fa polkit-gnome-authentication-agent-1

3) Kullanıcı gerçekten *wheel* grubunda mı?
   ::
      id $USER


**Çözüm 1 — *wheel* Grubunu “Yönetici” Olarak Tanımlama**
-----------------------------------------------------------------------

Polkit’e *wheel* grubunun “yönetici kimliği (AdminIdentity)” olduğunu söyleyin. 
Bu, yönetici doğrulaması gerektiren işlemlerde *wheel* üyesinin **kendi parolasıyla** 
yetki almasını sağlar.

1) Dosyayı oluşturun: ``/etc/polkit-1/rules.d/40-wheel-admin.rules``
   ::
      /* Mark wheel group as administrators (use own password) */
      polkit.addAdminRule(function(action, subject) {
          if (subject.isInGroup("wheel")) {
              return ["unix-group:wheel"];
          }
      });

2) Dosya izinleri:
   ::
      chown root:root /etc/polkit-1/rules.d/40-wheel-admin.rules
      chmod 0644 /etc/polkit-1/rules.d/40-wheel-admin.rules

3) Tekrar oturum açın ve ``lxsession-logout`` üzerinden deneyin.


.. raw:: pdf

   PageBreak
   
**Çözüm 2 — Sadece Güç Eylemlerine *wheel* için “YES” Ver**
------------------------------------------------------------

Sistemde “admin” kavramını genişletmek istemiyorsanız, yalnızca poweroff/reboot
eylemlerine *wheel* için açıkça izin verin.

1) Dosyayı oluşturun: ``/etc/polkit-1/rules.d/49-login1-power-wheel.rules``
   ::
      /* Allow wheel to poweroff/reboot (elogind login1 actions) */
      polkit.addRule(function(action, subject) {
          if (!subject.isInGroup("wheel"))
              return;

          var a = action.id;
          if (a == "org.freedesktop.login1.power-off" ||
              a == "org.freedesktop.login1.power-off-multiple-sessions" ||
              a == "org.freedesktop.login1.reboot" ||
              a == "org.freedesktop.login1.reboot-multiple-sessions") {
              return polkit.Result.YES;
          }
      });

2) İzinler:
   ::
      chown root:root /etc/polkit-1/rules.d/49-login1-power-wheel.rules
      chmod 0644 /etc/polkit-1/rules.d/49-login1-power-wheel.rules

3) Tekrar oturum açın ve ``lxsession-logout`` üzerinden deneyin.


**Önemli Not:**
---------------

Sisteminizde polkit kullanıyorsanız ve masaüstü ortamı **LXDE** ise **lxpolkit** devre dışı bırakılmalıdır. Kaldırma işlemini **lxsession** otomatik başlatma seçeneklerinden **lxpolkit** kaldırılarak yapılır. Kaldırılmaması durumunda birden fazla yetkilendirme çalışıyor uyarısı alırız. 


**Kaynaklar**::

	- OpenRC Resmi Belgeler:	https://wiki.gentoo.org/wiki/OpenRC
	- Polkit Resmi Dokümantasyon:	https://www.freedesktop.org/software/polkit/docs/latest/
	- Arch Wiki — Polkit:	https://wiki.archlinux.org/title/Polkit
	- Arch Wiki — Elogind:	https://wiki.archlinux.org/title/Elogind
	- LXDE Resmi Wiki:	https://wiki.lxde.org/en/Main_Page
	- Debian Wiki — Polkit:	https://wiki.debian.org/PolicyKit
	- Polkit kural örnekleri (wheel group):	https://wiki.archlinux.org/title/Polkit#Bypass_password_prompt

.. raw:: pdf

   PageBreak


**pkexec, /etc/shells ve Polkit İlişkisi**
=========================================

Bu belge, ``pkexec`` komutunun çalışması için gerekli olan ``/etc/shells`` 
bağlantısını, Polkit ile olan ilişkisini ve doğru yapılandırma adımlarını açıklar.

**1 — Temel İlişki**
-------------------

- **pkexec**, bir komutu yönetici yetkileri ile çalıştırmak için kullanılır.
- Arka planda **Polkit** (PolicyKit) kullanarak yetkilendirme yapar.
- Yetkilendirme sırasında **PAM (Pluggable Authentication Modules)** kullanılır.
- Birçok PAM yapılandırması, kullanıcının giriş kabuğunun **/etc/shells** içinde listelenmiş olmasını zorunlu kılar.

.. note::

   Eğer kullandığınız kabuk (örn. ``/bin/bash``, ``/bin/zsh``, ``/usr/bin/fish``) 
   ``/etc/shells`` içinde yoksa ``pkexec`` ile kimlik doğrulama başarısız olabilir.

**2 — /etc/shells Dosyasını Kontrol Etme**
------------------------------------------

Geçerli kabuğunuz:
::

   echo $SHELL

Kabuğun ``/etc/shells`` içinde olup olmadığını kontrol edin:
::

   grep "$(basename $SHELL)" /etc/shells

**Eksikse ekleyin**:
::

   sudo sh -c 'echo /bin/bash >> /etc/shells'

.. warning::

   Güvenlik sebebiyle yalnızca gerçek kabuk programlarının yolunu ekleyin.  
   Rastgele betikler veya çalıştırılabilir dosyalar eklenmemelidir.

**3 — Polkit ile Bağlantı**
---------------------------

- ``pkexec`` çalışırken **Polkit** üzerinden yetki ister.
- Polkit kuralları ile hangi kullanıcı veya grubun yetki alabileceğini belirleyebilirsiniz.
- Eğer kullanıcı grubunuz Polkit tarafından **admin** olarak tanınmıyorsa, ``pkexec`` ile çalıştırma yetkiniz olmayabilir.

**4 — Wheel Grubunu Yönetici Olarak Tanımlama**
-----------------------------------------------

1) Dosya oluşturun:
::

   /etc/polkit-1/rules.d/40-wheel-admin.rules

İçeriği:
::

   /* Mark wheel group as administrators (use own password) */
   polkit.addAdminRule(function(action, subject) {
       if (subject.isInGroup("wheel")) {
           return ["unix-group:wheel"];
       }
   });

2) Dosya izinlerini ayarlayın:
::

   sudo chown root:root /etc/polkit-1/rules.d/40-wheel-admin.rules
   sudo chmod 0644 /etc/polkit-1/rules.d/40-wheel-admin.rules

3) Kullanıcınızı ``wheel`` grubuna ekleyin:
::

   sudo usermod -aG wheel $USER

4) Oturumu kapatıp tekrar açın.

**5 — Test**
------------

1) ``pkexec`` komutunu çalıştırın:
::

   pkexec env DISPLAY=$DISPLAY XAUTHORITY=$XAUTHORITY xterm

2) Parola soruluyorsa ve yetkilendirme başarılı oluyorsa ayarlarınız tamamdır.

**6 — Özet**
------------

- ``pkexec`` → Polkit kullanarak yetkilendirme yapar.
- Polkit → PAM üzerinden kimlik doğrular.
- PAM → Kullanıcı kabuğunun ``/etc/shells`` içinde olmasını bekler.
- ``/etc/shells`` → Geçerli kabuğunuz burada yoksa ``pkexec`` başarısız olur.
- Polkit kuralları ile hangi kullanıcı/grupların yetki alacağı belirlenir.

**Kaynaklar**::

- Polkit Dokümantasyonu: https://www.freedesktop.org/software/polkit/docs/latest/
- Arch Wiki — Polkit: https://wiki.archlinux.org/title/Polkit
- Arch Wiki — Sudo: https://wiki.archlinux.org/title/Sudo
- PAM /etc/shells: https://linux.die.net/man/5/shells


.. raw:: pdf

   PageBreak


**glib-compile-schemas Kullanımı**
==================================

``glib-compile-schemas`` komutu, GLib kütüphanesinin ``GSettings``
yapılandırma sisteminde kullanılan ``*.gschema.xml`` dosyalarını
ikili (binary) biçime derlemek için kullanılır.

Derleme işlemi sonunda ``gschemas.compiled`` adlı tek bir dosya oluşur.
Bu dosya, uygulamaların GSettings üzerinden yapılandırma okuma/yazma
işlemlerini hızlı ve verimli şekilde yapmasını sağlar.

**Temel Görev**
---------------

- ``*.gschema.xml`` → ``gschemas.compiled`` dönüşümünü yapmak.
- GSettings yapılandırma şemalarının sistem tarafından tanınmasını sağlamak.
- XML dosyalarının doğrudan okunması yerine, önceden derlenmiş ikili dosyadan hızlı erişim imkânı sunmak.

**Ne Zaman Kullanılır?**
------------------------

1. **Yeni bir GSettings şeması eklendiğinde:** Sisteme yeni bir paket veya uygulama kurulduğunda ve bu uygulama kendi ``*.gschema.xml`` dosyalarıyla birlikte geliyorsa, bu dosyaların derlenmesi gerekir.

2. **Mevcut bir şema değiştirildiğinde** 

3. **Sistem yükleme veya imaj oluşturma sürecinde:** Özel bir Linux imajı hazırlanırken (ör. distro yapımı) şemalar eklendikten sonra çalıştırılmalıdır.

4. **Manuel şema kurulumu yapıldığında:** Paket yöneticisi dışında, elle ``/usr/share/glib-2.0/schemas/`` dizinine XML dosyası kopyalandığında.

**Kullanım Şekli**
------------------

.. code-block:: bash

    sudo glib-compile-schemas /usr/share/glib-2.0/schemas/

**Açıklama:**

- ``/usr/share/glib-2.0/schemas/``  
  GLib tarafından kullanılan ana şema dizinidir. Burada tüm paketlere ait ``*.gschema.xml`` dosyaları bulunur.

- Komut, bu dizindeki tüm XML şemalarını tarar ve tek bir ``gschemas.compiled`` dosyası üretir.

**Dikkat Edilmesi Gerekenler**
------------------------------

- Komutun, şemaların bulunduğu dizin üzerinde yazma iznine sahip bir kullanıcı (genellikle ``root``) tarafından çalıştırılması gerekir.
- ``*.gschema.xml`` dosyalarında sözdizimi hatası varsa derleme başarısız olur.
- Derleme sonrası ``gschemas.compiled`` dosyasının mevcut ve güncel olduğundan emin olun.

**Kaynaklar**::

- GLib GSettings belgeleri:	https://developer.gnome.org/gio/stable/GSettings.html
- glib-compile-schemas kılavuz sayfası:	https://manpages.debian.org/glib-compile-schemas

.. raw:: pdf

   PageBreak


**gdk-pixbuf-query-loaders Kullanımı**
======================================

``gdk-pixbuf-query-loaders`` komutu, ``gdk-pixbuf`` kütüphanesinin kullanabileceği tüm resim yükleyicilerini (image loaders) tarar ve bunların bilgilerini derleyerek bir yapılandırma dosyası (``loaders.cache``) oluşturur.

Bu komut, özellikle GNOME ve GTK tabanlı uygulamaların farklı resim formatlarını (PNG, JPEG, SVG, GIF vb.) tanıyabilmesi için gereklidir.

**Temel Görev**
----------------

- Sistem üzerinde kurulu **gdk-pixbuf loader modüllerini** bulur.
- Bu modüllerin yeteneklerini (desteklenen dosya türleri, MIME tipleri vb.) listeler.
- Bilgileri ikili önbellek dosyası olan ``loaders.cache`` içine yazar.
- Böylece uygulamalar, her çalıştırıldığında modül taraması yapmak yerine
  bu önbellekten hızlıca bilgi alır.

**Ne Zaman Kullanılır?**
------------------------

1. **Yeni image loader eklendiğinde:** Örneğin, SVG desteği için ``librsvg`` kurulduğunda veya başka bir formatı destekleyen eklenti eklendiğinde.

2. **gdk-pixbuf güncellendiğinde:** Kütüphane sürümü değiştiğinde, modül yolları değişebileceği için ``loaders.cache`` dosyasının yeniden oluşturulması gerekir.

3. **Sistem imajı hazırlanırken:** Özel bir Linux dağıtımı yapılırken, kök dosya sisteminde tüm loader'ların kayıtlı olduğundan emin olmak için.

4. **Elle modül kurulumu yapıldığında:** Paket yöneticisi dışında manuel olarak bir loader modülü kopyalandığında veya derlendiğinde.

**Kullanım Şekli**
------------------

.. code-block:: bash

    sudo gdk-pixbuf-query-loaders --update-cache

**Açıklama**::

- ``--update-cache`` Otomatik olarak tüm loader'ları tarar ve sonuçları ``loaders.cache`` dosyasına yazar.
- Varsayılan cache dosyası konumu: ``/usr/lib/x86_64-linux-gnu/gdk-pixbuf-2.0/2.10.0/loaders.cache`` (Konum, mimari ve dağıtıma göre değişebilir.)
- ``gdk-pixbuf-query-loaders`` komutu **stdout** çıktısı verir; eğer ``--update-cache`` kullanılmazsa bu çıktı elle bir dosyaya yönlendirilmelidir:

.. code-block:: bash

	gdk-pixbuf-query-loaders > /usr/lib/.../loaders.cache

**Dikkat Edilmesi Gerekenler**
------------------------------

- Komutun, cache dosyasının bulunduğu dizine yazma izni olan kullanıcı (genellikle ``root``) tarafından çalıştırılması gerekir.
- Modüller doğru yüklenmiyorsa veya bazı formatlar açılamıyorsa, cache dosyasının güncel olduğundan emin olun.
- Yanlış mimarideki (32-bit/64-bit) loader modülleri eklenirse hatalar oluşabilir.

**Kaynaklar**::

- GDK-Pixbuf Belgeleri:	https://developer.gnome.org/gdk-pixbuf/stable/
- gdk-pixbuf-query-loaders kılavuz sayfası:	https://manpages.debian.org/gdk-pixbuf-query-loaders

.. raw:: pdf

   PageBreak


**user-dirs**
++++++++++++

user-dirs, Linux işletim sistemlerinde kullanıcıların özel klasörlerini içeren bir sistemdir. Bu klasörler genellikle "Masaüstü", "Belgeler", "İndirilenler" gibi isimlerle tanımlanır ve kullanıcıların dosyalarını düzenlemelerini kolaylaştırır.

user-dirs klasörünü kaldırmak için aşağıdaki adımları izleyebilirsiniz:

    Terminali açın ve aşağıdaki komutu girin:

.. code-block:: shell

	nano ~/.config/user-dirs.dirs

Bu komut, user-dirs.dirs dosyasını açacaktır. Bu dosya, kullanıcı klasörlerinin yolunu ve adını içerir.
Dosyayı düzenlemek için, kaldırmak istediğiniz klasörün satırını bulun ve "#" işaretiyle başlayan bir yorum satırı yapın. Örneğin, "Masaüstü" klasörünü kaldırmak istiyorsanız, satırı aşağıdaki gibi düzenleyin:

.. code-block:: shell

	#XDG_DESKTOP_DIR="$HOME/Masaüstü"

Dosyayı kaydetmek ve kapatmak için "Ctrl + X" tuşlarına basın, ardından "Y" tuşuna basın ve Enter tuşuna basın.
Değişikliklerin etkili olması için oturumu kapatıp tekrar açın veya aşağıdaki komutu girin:

.. code-block:: shell

	xdg-user-dirs-update

Bu adımları takip ederek user-dirs klasörünü Linux sisteminizden kaldırabilirsiniz. Ancak, dikkatli olun ve yanlışlıkla önemli dosyaları silmemeye özen gösterin.

Yeni oluşturulacak kullanıcılarda oluşturulmamasını istiyorsak **/etc/skel/.config/user-dirs.dirs** dosyasını silmeliyiz.


.. raw:: pdf

   PageBreak

**Sistem Dili Değiştirme**
++++++++++++++++++++++++++

Dil kodlarına /usr/share/i18n/locales içerisinden ulaşabilirsiniz.

Karakter kodlamalara /usr/share/i18n/charmaps içinden ulaşabilirsiniz.

Sistem dilini ayarlamak için öncelikle /etc/locale.gen dosyamızı aşağıdaki gibi düzenleyelim.::

	tr_TR.UTF-8 UTF-8

**Not:** En altta boş bir satır bulunmalıdır.

Ardından /lib64/locale dizini yoksa oluşturalım.::

	mkdir -p /lib64/locale/

Şimdi de çevresel değişkenlerimizi ayarlamak için /etc/profile.d/locale.sh dosyamızı düzenleyelim.::

	#!/bin/sh
	# Language settings
	export LANG="tr_TR.UTF-8"
	export LC_ALL="tr_TR.UTF-8"

Not: Türkçe büyük küçük harf dönüşümü (i -> İ ve ı -> I) ascii standartına uyumsuz olduğu için LC_ALL kısmını türkçe ayarlamayı önermiyoruz. Bunun yerine C.UTF-8 veya en_US.UTF-8 olarak ayarlayabilirsiniz.

Son olarak locale-gen komutunu çalıştıralım.::

	locale-gen

Eğer /lib64/locale/ dizine okuma iznimiz yoksa verelim.::

	chmod 755 -R /lib64/locale/

**Çevresel Değişken Ayarlama Yöntemleri**
-----------------------------------------

**1. Yöntem**
.............

/etc/default/locale dosyasını root olarak bir metin editörü ile açın.

- **Türkçe için :** LANG=tr_TR.UTF-8
- **İngilizce için :** LANG=en_US.UTF-8

Sistemi yeniden başlattığınızda seçtiğiniz dil aktif olacaktır.


**2. Yöntem**
.............

/etc/profile.d/locale.sh dosyanı oluşturun içeriğini aşağıdaki gibi ayarlayın.

.. code-block:: shell

	# Language settings
	export LANG="tr_TR.UTF-8"
	export LC_ALL="tr_TR.UTF-8"

**/etc/profile.d/**  dizin erişim iznini 755 yapın.

**3.Yöntem**
............

ayarlarını değiştirmek istediğimiz kullanıcı dizinideki **~/.profile** dosyasının içeriğine aşağıdaki kod satırını eklemeliyiz.

.. code-block:: shell
	
	export LANG="tr_TR.UTF-8"
	export LC_ALL="tr_TR.UTF-8"


**Profile Dosyası**
--------------------

**/etc/profile** dosyası, Linux sistemlerinde kullanıcıların oturum açtıklarında çalıştırılan bir betik dosyasıdır. Bu dosya, tüm kullanıcılar için ortak kabuk ayarlarını ve ortam değişkenlerini tanımlar. 

Kullanıcı oturumu başlatıldığında, **/etc/profile** dosyası sistem genelindeki ayarları yükler ve kullanıcı oturumuna uygular. Bu dosya, kullanıcıların kabuk ortamlarını yapılandırmak ve özelleştirmek için kullanılır.

Örneğin, PATH değişkenini tanımlamak veya diğer kabuk ayarlarını yapılandırmak için /etc/profile dosyası düzenlenebilir. Bu dosya, sistem genelinde tutarlı bir kabuk ortamı sağlamak için önemlidir.

.. code-block:: shell

	/etc/profile
	/etc/profile.d/*
	/etc/environment
	~/.profile, veya ~/.bash_profile veya ~/.login veya ~/.zprofile giriş kabuğunuza bağlı olarak
	~/.pam_environment
	(yalnızca terminalde çalışan kabuklar için) /etc/bash.bashrc, /etc/zshrc, ~/.bashrc, ~/.zshrc vb.


**Not:** /etc/profile.d/ dizinine root dışında kullanıcılar erişim sağlaması için 755 yapmalısınız.
 
**profile**
-----------

**/etc/profile** dosyanının içerisinde aşağıdaki betik olmalıdır. Bu betik **/etc/profile.d** içerisinde betikler varsa tüm kullanıcılar için çalıştırılmasını sağlar.

.. code-block:: shell

	if [ -d /etc/profile.d ]; then
	  for i in /etc/profile.d/*.sh; do
		if [ -r $i ]; then
		  . $i
		fi
	  done
	  unset i
	fi

.. raw:: pdf

   PageBreak


**Kullanıcı Ekleme**
++++++++++++++++++++

linux sistemlerine kullanıcı eklemek için iki farklı komut bulunur. Bu komutlar adduser ve useradd komutlarıdır.


**adduser:**
------------

Kullanıcı dostu bir arayüz sunar. Birçok aşamayı bizim adımıza yapar. Temelde useradd komutunu kullanarak yazılan bir script olarak düşünebiliriz.

.. code-block:: shell

	# adduser komutuyla kullanıcı oluşturma
	sudo adduser yeni_kullanici

**useradd:** 
------------

Kullanıcıdan tüm parametreleri girmesini ister.  Bu sebepten çok tercih edilmemektedir. Fakat özel bir şekilde kullanıcı oluşturulmak istenildiğinde tercih edilir. Bu dokümanda kurulum aşamalarında useradd komutu kullanıldı.


.. code-block:: shell

	# useradd komutuyla kullanıcı oluşturma
	sudo useradd -m -s /bin/bash yeni_kullanici -d /home/yeni_kullanici
	# -s/bin/bash : kullanıcının kullanacağı shell belirtiliyor.
	# -d /home/yeni_kullanici : home dizinine oluşturulacak kullanıcı dizini belirtiyoruz


.. raw:: pdf

   PageBreak

**cgroup**
++++++++++

Cgroup, Linux sistemlerinde kaynak yönetimi için güçlü bir araçtır. Özellikle sunucu ve konteyner ortamlarında, kaynakları etkili bir şekilde yönetmek ve izlemek için vazgeçilmezdir. Yukarıda bahsedilen adımları takip ederek, cgroup ile kaynak yönetimi yapmaya başlayabilirsiniz. Unutmayın, her zaman sistem kaynaklarınızı izlemek ve gerektiğinde ayarlamalar yapmak önemlidir.

**Cgroup'un Temel Özellikleri**
-------------------------------

- **Kaynak Sınırlama:** Cgroup, belirli bir grup süreç için CPU, bellek, disk ve ağ gibi kaynakları sınırlamanıza olanak tanır. Örneğin, bir uygulamanın bellek kullanımını 512 MB ile sınırlamak istiyorsanız, cgroup kullanarak bunu kolayca yapabilirsiniz.

- **Kaynak İzleme:** Cgroup, süreçlerin kaynak kullanımını izlemek için de kullanılabilir. Bu, sistem yöneticilerinin hangi süreçlerin ne kadar kaynak kullandığını görmesine yardımcı olur.

- **Hiyerarşi:** Cgroup, hiyerarşik bir yapıya sahiptir.

- **Güvenlik:** Belirli süreçlerin diğer süreçlerin kaynaklarına erişimini kısıtlayarak güvenliği artırır.

**Cgroup Kullanımı**
--------------------

Cgroup kullanmaya başlamak için öncelikle sisteminizde cgroup'un etkin olduğundan emin olmalısınız. Genellikle modern Linux dağıtımlarında cgroup varsayılan olarak aktiftir. Cgroup ile çalışmak için aşağıdaki adımları izleyebilirsiniz:

**1. Cgroup Oluşturma**

Öncelikle, bir cgroup oluşturmalısınız. Bunun için terminalde aşağıdaki komutu kullanabilirsiniz:


.. code-block:: shell

	sudo mkdir /sys/fs/cgroup/memory/my_cgroup

Bu komut, "my_cgroup" adında bir bellek cgroup'u oluşturur.

**2. Kaynak Sınırlama**

Oluşturduğunuz cgroup'a bellek sınırı eklemek için şu komutu kullanabilirsiniz:


.. code-block:: shell

	echo 512M | sudo tee /sys/fs/cgroup/memory/my_cgroup/memory.limit_in_bytes

Bu komut, "my_cgroup" için bellek sınırını 512 MB olarak ayarlar.

**3. Süreç Ekleme**

Artık bir cgroup oluşturduğunuza göre, bu cgroup'a süreç ekleyebilirsiniz. Bunun için, eklemek istediğiniz sürecin PID'sini öğrenin ve aşağıdaki komutu kullanın:


.. code-block:: shell

	echo <PID> | sudo tee /sys/fs/cgroup/memory/my_cgroup/cgroup.procs

Burada <PID> kısmını eklemek istediğiniz sürecin PID'si ile değiştirin.

**4. İzleme**

Cgroup'un kaynak kullanımını izlemek için aşağıdaki komutu kullanabilirsiniz:


.. code-block:: shell

	cat /sys/fs/cgroup/memory/my_cgroup/memory.usage_in_bytes

Bu komut, "my_cgroup" içindeki süreçlerin toplam bellek kullanımını gösterir.

	
.. raw:: pdf

   PageBreak

.. _yardimcikonular:
Yardımcı Konular
================

.. _kaynaklar:
**Kaynaklar**
=============================
.. toctree::
	:glob:

.. code-block:: shell

	- https://tr.wikipedia.org/wiki/Linux - 02/07/2025
	- https://www.subrat.info/build-kernel-and-userspace/ - 08/07/2025
	- https://medium.com/@chienhaotan/compiling-and-running-a-minimal-kernel-with-busybox-bfc45a991017 - 08/07/2025
	- https://stackoverflow.com/questions/64838052/how-to-delete-n-characters-appended-to-ldd-list - 20/06/2025
	- https://gist.github.com/bluedragon1221/a58b0e1ed4492b44aa530f4db0ffef85 - 09/07/2025	
	- https://app.diagrams.net/
	- https://www.ubuntubuzz.com/2021/04/how-to-boot-uefi-on-qemu.html - 20/06/2024
	- https://wiki.gentoo.org/wiki/OpenRC - 30/06/2025
	- https://busybox.net/  - 01/07/2025
	- https://busybox.net/about.html - 01/07/2025
	- https://sulincix.gitlab.io/distro-kitabi/ - 05/07/2025
	- https://gitlab.com/turkman/devel/doc/wiki/ - 05/07/2025
	- https://turkman.gitlab.io/devel/doc/wiki/ - 05/07/2025
	- https://grok.com/share/c2hhcmQtMw%3D%3D_5c049e44-be57-4652-872f-55def669d917 - 09/07/2025
	- https://www.linuxfromscratch.org/lfs/
	- https://wiki.archlinux.org/title/GRUB_(T%C3%BCrk%C3%A7e)#UEFI_sistemler - 08/07/2025
	- https://tldp.org/HOWTO/html_single/SquashFS-HOWTO/ - 09/07/2025
	- https://askubuntu.com/questions/437880/extract-a-squashfs-to-an-existing-directory - 11/07/2025
	- https://grok.com/share/c2hhcmQtMw%3D%3D_2ad2ac6b-d067-40b0-9b55-46db0c2c98dc - 10/07/2025
	- https://chatgpt.com/
	

**Not:** Metin düzenlemelerinde chatgpt kullanılmıştır.

.. raw:: pdf

   PageBreak

.. _gelistiricimesaji:
**Geliştiricilere Mesajımız**
=============================
.. toctree::
	:glob:

Gnu/Linux, açık kaynaklı bir işletim sistemidir. Kullanıcı ve geliştiriclere bir çok avantajlar sunmaktadır. Bunlar;

- Kodlarına erişilebilir(Açık Kaynak)
- Dağıtılabir 
- Değiştirilebilir
- Virüsten etilenme azdır
- Özelleştirilebilir 
- Bağımlılığı azaltır
- Güvenlik en önemli şarttır 
- Düşük donanımlarda iyi performan verir

Bu özellikleri açısından Gnu/Linux tercih etmek çok avantajlıdır. Geliştirme aşamalarına destek vermek, öğrenmek bize, toplumumuza ve ülkemize sayısız faydalar saylayacaktır.


.. raw:: pdf

   PageBreak

.. _lisans:
===========================
**Lisans Bilgileri**
===========================

Bu proje iki farklı lisans altında dağıtılmaktadır:

1. **Kaynak Kodlar (Source Code)**:
   
   Bu dokümandaki kaynak kodların tamamı Free Software Foundation tarafından yayınlanan GNU Genel Kamu Lisansı'nın (GPL) 3. versiyonu ile lisanslıdır.

   Lisansın bir kopyasını şu adresten edinebilirsiniz:
   https://www.gnu.org/licenses/gpl-3.0.html

2. **Dokümantasyon ve Medya (Documentation and Media)**:
   
   Bu doküman içerisindeki tüm grafikler, görseller ve metinler aşağıdaki lisans altında dağıtılmaktadır:

   Copyright (C) <2025> <İSİM / KURUM>


**İletişim**
++++++++++++

- https://github.com/kendilinuxunuyap
- https://kendilinuxunuyap.github.io
- kendilinuxunuyap@gmail.com



.. raw:: pdf

   PageBreak

.. toctree::
	:glob:


