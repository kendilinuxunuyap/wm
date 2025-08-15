**glib-compile-schemas Kullanımı**
==================================

``glib-compile-schemas`` komutu, GLib kütüphanesinin ``GSettings``
yapılandırma sisteminde kullanılan ``*.gschema.xml`` dosyalarını
ikili (binary) biçime derlemek için kullanılır.

Derleme işlemi sonunda ``gschemas.compiled`` adlı tek bir dosya oluşur.
Bu dosya, uygulamaların GSettings üzerinden yapılandırma okuma/yazma
işlemlerini hızlı ve verimli şekilde yapmasını sağlar.

**Temel Görev**
---------------

- ``*.gschema.xml`` → ``gschemas.compiled`` dönüşümünü yapmak.
- GSettings yapılandırma şemalarının sistem tarafından tanınmasını sağlamak.
- XML dosyalarının doğrudan okunması yerine, önceden derlenmiş ikili dosyadan hızlı erişim imkânı sunmak.

**Ne Zaman Kullanılır?**
------------------------

1. **Yeni bir GSettings şeması eklendiğinde:** Sisteme yeni bir paket veya uygulama kurulduğunda ve bu uygulama kendi ``*.gschema.xml`` dosyalarıyla birlikte geliyorsa, bu dosyaların derlenmesi gerekir.

2. **Mevcut bir şema değiştirildiğinde** 

3. **Sistem yükleme veya imaj oluşturma sürecinde:** Özel bir Linux imajı hazırlanırken (ör. distro yapımı) şemalar eklendikten sonra çalıştırılmalıdır.

4. **Manuel şema kurulumu yapıldığında:** Paket yöneticisi dışında, elle ``/usr/share/glib-2.0/schemas/`` dizinine XML dosyası kopyalandığında.

**Kullanım Şekli**
------------------

.. code-block:: bash

    sudo glib-compile-schemas /usr/share/glib-2.0/schemas/

**Açıklama:**

- ``/usr/share/glib-2.0/schemas/``  
  GLib tarafından kullanılan ana şema dizinidir. Burada tüm paketlere ait ``*.gschema.xml`` dosyaları bulunur.

- Komut, bu dizindeki tüm XML şemalarını tarar ve tek bir ``gschemas.compiled`` dosyası üretir.

**Dikkat Edilmesi Gerekenler**
------------------------------

- Komutun, şemaların bulunduğu dizin üzerinde yazma iznine sahip bir kullanıcı (genellikle ``root``) tarafından çalıştırılması gerekir.
- ``*.gschema.xml`` dosyalarında sözdizimi hatası varsa derleme başarısız olur.
- Derleme sonrası ``gschemas.compiled`` dosyasının mevcut ve güncel olduğundan emin olun.

**Kaynaklar**::

- GLib GSettings belgeleri:	https://developer.gnome.org/gio/stable/GSettings.html
- glib-compile-schemas kılavuz sayfası:	https://manpages.debian.org/glib-compile-schemas

.. raw:: pdf

   PageBreak

