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
