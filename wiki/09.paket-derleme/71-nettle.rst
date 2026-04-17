.. _nettle:
**nettle**
==========

Güvenlik ve şifreleme işlemleri için kullanılır.Güvenli veri iletimi ve şifreleme aracıdır.

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
