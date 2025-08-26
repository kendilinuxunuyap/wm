.. _giris:

**Ön Hazırlık**
---------------

Paket derleme işlemi öncesi aşağıdaki konuları bilmemiz gerekmektedir. Bunlar; 

1. Derleme(Dinamik/Static) 
2. chroot Kullanımı 
3. İso Oluşturma
4. ssh Kullanımı
5. sftp Kullanımı
6. scp Kullanımı
7. VirtualBox Kullanmı
8. cfdisk Kullanımı

Burada liste halinde verilen konu başlıkları bu dokümanın **Yardımcı Konular** bölümünde anlatılmaktadır. 

Bundan sonraki adımlarda kendi dağıtımımızın **LXDE masaüstü ortmaını** derleyerek **X Pencere Sistemi** üzerinde çalıştıracağız!


GNU Araçlarıyla **LXDE Masaüstü Ortamının** derleme işlemini **kly Paket Sistemi** kullanılarak derleyeceğiz. Derleme işlemini **kly -c** komutuyla yapacağız. Derlenen paketleri **scp** ve **sftp** kullanarak **Temel Sistem** üzerine kopyalayacağız. **kly -pi** komutumuzla kopyaladığımız paketi **X Pencere Sistemi** üzerine kuracağız. Oluşturduğumuz paketleri istersek github'a yükleyip. github üzerinden kururabiliriz.

.. raw:: pdf

   PageBreak


**LXDE Masaüstü Ortamı için Gerekli Paketler**
----------------------------------------------

.. list-table::
   :widths: 33 33 33

   * - 0- :ref:`giris`
     - 29- :ref:`libXfont`
     - 58- :ref:`cups`
   * - 1- :ref:`libfm`
     - 30- :ref:`libxkbcommon`
     - 59- :ref:`gdbm`
   * - 2- :ref:`menu-cache`
     - 31- :ref:`libxkbui`
     - 60- :ref:`mpdecimal`
   * - 3- :ref:`libfm-extra`
     - 32- :ref:`libxklavier`
     - 61- :ref:`libgusb`
   * - 4- :ref:`lxmenu-data`
     - 33- :ref:`libXpresent`
     - 62- :ref:`libisl`
   * - 5- :ref:`lxde-common`
     - 34- :ref:`libXres`
     - 63- :ref:`libmpc`
   * - 6- :ref:`lxappearance`
     - 35- :ref:`libxss`
     - 64- :ref:`duktape`
   * - 7- :ref:`lxinput`
     - 36- :ref:`libXtst`
     - 65- :ref:`atkmm`
   * - 8- :ref:`lxrandr`
     - 37- :ref:`libXv`
     - 66- :ref:`at-spi2-core`
   * - 9-  :ref:`lxsession`
     - 38- :ref:`libXvMC`
     - 67- :ref:`libtiff`
   * - 10- :ref:`lxpanel`
     - 39- :ref:`libXxf86dga`
     - 68- :ref:`libepoxy`
   * - 11- :ref:`lxtask`
     - 40- :ref:`libXxf86vm`
     - 69- :ref:`gobject-introspection`
   * - 12- :ref:`lxterminal`
     - 41- :ref:`tslib`
     - 70- :ref:`p11-kit`
   * - 13- :ref:`pcmanfm`
     - 42- :ref:`vte3`
     - 71- :ref:`nettle`
   * - 14- :ref:`lxlauncher`
     - 43- :ref:`xapp`
     - 72- :ref:`desktop-file-utils`
   * - 15- :ref:`lxhotkey`
     - 44- :ref:`xcb-util-cursor`
     - 73- :ref:`libidn2` 
   * - 16- :ref:`lxde-icon-theme`
     - 45- :ref:`xcb-util-errors`
     - 74- :ref:`locale-tr`
   * - 17- :ref:`libjpeg-turbo`
     - 46- :ref:`xcb-util-image`
     - 75- :ref:`hicolor-icon-theme`
   * - 18- :ref:`cairo`
     - 47- :ref:`xcb-util-keysyms`
     - 76- :ref:`polkit`
   * - 19- :ref:`gdk-pixbuf`
     - 48- :ref:`xcb-util-renderutil`
     - 77- :ref:`libjpeg62`
   * - 20- :ref:`gtksourceview4`
     - 49- :ref:`xcb-util-wm`
     - 78- :ref:`gpicview`
   * - 21- :ref:`hsakmt`
     - 50- :ref:`xtrans`
     - 79- :ref:`libdmx`
   * - 22- :ref:`libFS`
     - 51- :ref:`libkeybinder3`
     - 80- :ref:`lightdm`
   * - 23- :ref:`libnotify`
     - 52- :ref:`libexif`
     - 81- :ref:`lightdm-gtk-greeter`
   * - 24- :ref:`libvdpau`
     - 53- :ref:`gtk3`
     - 82- :ref:`libgpg-error`
   * - 25- :ref:`libwnck3`
     - 54- :ref:`shared-mime-info`
     - 83- :ref:`libgcrypt`
   * - 26- :ref:`libXaw3d`
     - 55- :ref:`lz4`
     - 84- 
   * - 27- :ref:`libXcomposite`
     - 56- :ref:`gnutls`
     - 85- 
   * - 28- :ref:`libXdamage`
     - 57- :ref:`lcms2`
     - 86- 


**Bağımlılık Zinciri**
----------------------

**LXDE** paketleri **gtk3** ile derlenecek. Bunun için ilk olarak **libfm** paketinin **gtk3** ile derlenmeli ve sonra mevcut sistemimize kurmalıyız. Sistemimize kurulduktan sonra **LXDE** paketlerini **gtk3** ile  derlenmeli. **libfm** ve **menu-cache** ilk kurulması gereken paketler. Paket derleme işlemine başlamadan önce, aşağıdaki temel araçları sisteminize kurmalısınız. ::

	sudo apt update
	sudo apt-get install debootstrap xorriso mtools make squashfs-tools gcc wget unzip xz-utils tar zstd fakeroot \
	autoconf automake autotools-dev make meson cmake ninja-build pkgconf patch libtool grub-pc grub-pc-bin
	
.. raw:: pdf

   PageBreak

