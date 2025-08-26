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
