**pkexec, /etc/shells ve Polkit İlişkisi**
=========================================

Bu belge, ``pkexec`` komutunun çalışması için gerekli olan ``/etc/shells`` 
bağlantısını, Polkit ile olan ilişkisini ve doğru yapılandırma adımlarını açıklar.

**1 — Temel İlişki**
-------------------

- **pkexec**, bir komutu yönetici yetkileri ile çalıştırmak için kullanılır.
- Arka planda **Polkit** (PolicyKit) kullanarak yetkilendirme yapar.
- Yetkilendirme sırasında **PAM (Pluggable Authentication Modules)** kullanılır.
- Birçok PAM yapılandırması, kullanıcının giriş kabuğunun **/etc/shells** içinde listelenmiş olmasını zorunlu kılar.

.. note::

   Eğer kullandığınız kabuk (örn. ``/bin/bash``, ``/bin/zsh``, ``/usr/bin/fish``) 
   ``/etc/shells`` içinde yoksa ``pkexec`` ile kimlik doğrulama başarısız olabilir.

**2 — /etc/shells Dosyasını Kontrol Etme**
------------------------------------------

Geçerli kabuğunuz:
::

   echo $SHELL

Kabuğun ``/etc/shells`` içinde olup olmadığını kontrol edin:
::

   grep "$(basename $SHELL)" /etc/shells

**Eksikse ekleyin**:
::

   sudo sh -c 'echo /bin/bash >> /etc/shells'

.. warning::

   Güvenlik sebebiyle yalnızca gerçek kabuk programlarının yolunu ekleyin.  
   Rastgele betikler veya çalıştırılabilir dosyalar eklenmemelidir.

**3 — Polkit ile Bağlantı**
---------------------------

- ``pkexec`` çalışırken **Polkit** üzerinden yetki ister.
- Polkit kuralları ile hangi kullanıcı veya grubun yetki alabileceğini belirleyebilirsiniz.
- Eğer kullanıcı grubunuz Polkit tarafından **admin** olarak tanınmıyorsa, ``pkexec`` ile çalıştırma yetkiniz olmayabilir.

**4 — Wheel Grubunu Yönetici Olarak Tanımlama**
-----------------------------------------------

1) Dosya oluşturun:
::

   /etc/polkit-1/rules.d/40-wheel-admin.rules

İçeriği:
::

   /* Mark wheel group as administrators (use own password) */
   polkit.addAdminRule(function(action, subject) {
       if (subject.isInGroup("wheel")) {
           return ["unix-group:wheel"];
       }
   });

2) Dosya izinlerini ayarlayın:
::

   sudo chown root:root /etc/polkit-1/rules.d/40-wheel-admin.rules
   sudo chmod 0644 /etc/polkit-1/rules.d/40-wheel-admin.rules

3) Kullanıcınızı ``wheel`` grubuna ekleyin:
::

   sudo usermod -aG wheel $USER

4) Oturumu kapatıp tekrar açın.

**5 — Test**
------------

1) ``pkexec`` komutunu çalıştırın:
::

   pkexec env DISPLAY=$DISPLAY XAUTHORITY=$XAUTHORITY xterm

2) Parola soruluyorsa ve yetkilendirme başarılı oluyorsa ayarlarınız tamamdır.

**6 — Özet**
------------

- ``pkexec`` → Polkit kullanarak yetkilendirme yapar.
- Polkit → PAM üzerinden kimlik doğrular.
- PAM → Kullanıcı kabuğunun ``/etc/shells`` içinde olmasını bekler.
- ``/etc/shells`` → Geçerli kabuğunuz burada yoksa ``pkexec`` başarısız olur.
- Polkit kuralları ile hangi kullanıcı/grupların yetki alacağı belirlenir.

**Kaynaklar**::

- Polkit Dokümantasyonu: https://www.freedesktop.org/software/polkit/docs/latest/
- Arch Wiki — Polkit: https://wiki.archlinux.org/title/Polkit
- Arch Wiki — Sudo: https://wiki.archlinux.org/title/Sudo
- PAM /etc/shells: https://linux.die.net/man/5/shells


.. raw:: pdf

   PageBreak

