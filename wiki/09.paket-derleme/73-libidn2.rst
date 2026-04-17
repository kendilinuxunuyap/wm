.. _libidn2:
**libidn2**
===========

Alan Adları için kullanılan bir kütüphanedir.

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
