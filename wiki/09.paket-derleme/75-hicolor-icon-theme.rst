.. _hicolor-icon-theme:
**hicolor-icon-theme**
======================

Masaüstü ortamları ve uygulamalar için bir temadır. 

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
