**gdk-pixbuf-query-loaders Kullanımı**
======================================

``gdk-pixbuf-query-loaders`` komutu, ``gdk-pixbuf`` kütüphanesinin kullanabileceği tüm resim yükleyicilerini (image loaders) tarar ve bunların bilgilerini derleyerek bir yapılandırma dosyası (``loaders.cache``) oluşturur.

Bu komut, özellikle GNOME ve GTK tabanlı uygulamaların farklı resim formatlarını (PNG, JPEG, SVG, GIF vb.) tanıyabilmesi için gereklidir.

**Temel Görev**
----------------

- Sistem üzerinde kurulu **gdk-pixbuf loader modüllerini** bulur.
- Bu modüllerin yeteneklerini (desteklenen dosya türleri, MIME tipleri vb.) listeler.
- Bilgileri ikili önbellek dosyası olan ``loaders.cache`` içine yazar.
- Böylece uygulamalar, her çalıştırıldığında modül taraması yapmak yerine
  bu önbellekten hızlıca bilgi alır.

**Ne Zaman Kullanılır?**
------------------------

1. **Yeni image loader eklendiğinde:** Örneğin, SVG desteği için ``librsvg`` kurulduğunda veya başka bir formatı destekleyen eklenti eklendiğinde.

2. **gdk-pixbuf güncellendiğinde:** Kütüphane sürümü değiştiğinde, modül yolları değişebileceği için ``loaders.cache`` dosyasının yeniden oluşturulması gerekir.

3. **Sistem imajı hazırlanırken:** Özel bir Linux dağıtımı yapılırken, kök dosya sisteminde tüm loader'ların kayıtlı olduğundan emin olmak için.

4. **Elle modül kurulumu yapıldığında:** Paket yöneticisi dışında manuel olarak bir loader modülü kopyalandığında veya derlendiğinde.

**Kullanım Şekli**
------------------

.. code-block:: bash

    sudo gdk-pixbuf-query-loaders --update-cache

**Açıklama**::

- ``--update-cache`` Otomatik olarak tüm loader'ları tarar ve sonuçları ``loaders.cache`` dosyasına yazar.
- Varsayılan cache dosyası konumu: ``/usr/lib/x86_64-linux-gnu/gdk-pixbuf-2.0/2.10.0/loaders.cache`` (Konum, mimari ve dağıtıma göre değişebilir.)
- ``gdk-pixbuf-query-loaders`` komutu **stdout** çıktısı verir; eğer ``--update-cache`` kullanılmazsa bu çıktı elle bir dosyaya yönlendirilmelidir:

.. code-block:: bash

	gdk-pixbuf-query-loaders > /usr/lib/.../loaders.cache

**Dikkat Edilmesi Gerekenler**
------------------------------

- Komutun, cache dosyasının bulunduğu dizine yazma izni olan kullanıcı (genellikle ``root``) tarafından çalıştırılması gerekir.
- Modüller doğru yüklenmiyorsa veya bazı formatlar açılamıyorsa, cache dosyasının güncel olduğundan emin olun.
- Yanlış mimarideki (32-bit/64-bit) loader modülleri eklenirse hatalar oluşabilir.

**Kaynaklar**::

- GDK-Pixbuf Belgeleri:	https://developer.gnome.org/gdk-pixbuf/stable/
- gdk-pixbuf-query-loaders kılavuz sayfası:	https://manpages.debian.org/gdk-pixbuf-query-loaders

.. raw:: pdf

   PageBreak

