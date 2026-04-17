.. _libgpg-error:
**libgpg-error**
================

GnuPG ve libgcrypt için yardımcı kütüphanedir.

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
