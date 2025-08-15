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

