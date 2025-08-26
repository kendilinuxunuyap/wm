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
