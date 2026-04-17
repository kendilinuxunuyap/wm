.. _gpicview:
**gpicview**
============

gpicview, GNOME masaüstü ortamı için resim görüntüleyicisidir.

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
