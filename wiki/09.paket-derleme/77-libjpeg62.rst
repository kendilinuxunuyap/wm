.. _libjpeg62:
**libjpeg62**
=============

JPEG formatındaki resimler için kullanılan bir kütüphanedir.

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
