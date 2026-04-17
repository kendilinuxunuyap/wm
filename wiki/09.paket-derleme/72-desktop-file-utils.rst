.. _desktop-file-utils:
**desktop-file-utils**
======================

Masaüstü ortamlarıyla ilgili dosya işlemleri yapan yazılım paketidir.

**Paketi Derleme :**
--------------------

.. code-block:: bash

	#!/usr/bin/env bash
	name="desktop-file-utils"
	version="0.27"
	description="Command line utilities for working with desktop entries"
	source="https://www.freedesktop.org/software/desktop-file-utils/releases/desktop-file-utils-${version}.tar.xz"
	depends="glib"
	builddepend="git,meson"
	group="dev.util"


	setup(){
		cd $SOURCEDIR
		meson setup $BUILDDIR --prefix=/usr \
		    --libdir=/usr/lib64/
	}

	build(){
		ninja -C build
	}

	package(){
		DESTDIR=$DESTDIR ninja -C $BUILDDIR install
	}


**Not:** Burada verilen derleme talimatı(script) **kly Paket Sistemi**'ni kullanarak paketi derler ve oluştur. Oluşan paket(**.kly uzantılı dosya**)  **kly Paket Sistemi** kullanılarak siteme yüklenebilir. **kly Paket Sistemiyle Paket Yapma** konusunu okumak için `tıklayınız. <#klypaketyap>`_


.. raw:: pdf

   PageBreak
