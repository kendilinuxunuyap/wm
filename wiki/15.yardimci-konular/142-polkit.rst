**polkit Yetkilendirme**
========================

Bu kılavuz, lxsession-logout penceresinde "Kapat" ve "Yeniden Başlat" 
işlemlerinin parola doğrulaması açılmasına rağmen başarısız olması sorununu 
çözer. Amaç: *wheel* grubundaki kullanıcıların GUI'den **poweroff/reboot** 
yapabilmesini sağlamak.

**Temel Ayar Kontrolü**
-----------------------

1) Elogind çalışıyor mu?
   ::
      rc-status | grep -E 'elogind|dbus'
      rc-service elogind status

2) Polkit aracı (agent) çalışıyor mu?
   ::
      pgrep -fa lxpolkit || pgrep -fa polkit-gnome-authentication-agent-1

3) Kullanıcı gerçekten *wheel* grubunda mı?
   ::
      id $USER


**Çözüm 1 — *wheel* Grubunu “Yönetici” Olarak Tanımlama**
-----------------------------------------------------------------------

Polkit’e *wheel* grubunun “yönetici kimliği (AdminIdentity)” olduğunu söyleyin. 
Bu, yönetici doğrulaması gerektiren işlemlerde *wheel* üyesinin **kendi parolasıyla** 
yetki almasını sağlar.

1) Dosyayı oluşturun: ``/etc/polkit-1/rules.d/40-wheel-admin.rules``
   ::
      /* Mark wheel group as administrators (use own password) */
      polkit.addAdminRule(function(action, subject) {
          if (subject.isInGroup("wheel")) {
              return ["unix-group:wheel"];
          }
      });

2) Dosya izinleri:
   ::
      chown root:root /etc/polkit-1/rules.d/40-wheel-admin.rules
      chmod 0644 /etc/polkit-1/rules.d/40-wheel-admin.rules

3) Tekrar oturum açın ve ``lxsession-logout`` üzerinden deneyin.


.. raw:: pdf

   PageBreak
   
**Çözüm 2 — Sadece Güç Eylemlerine *wheel* için “YES” Ver**
------------------------------------------------------------

Sistemde “admin” kavramını genişletmek istemiyorsanız, yalnızca poweroff/reboot
eylemlerine *wheel* için açıkça izin verin.

1) Dosyayı oluşturun: ``/etc/polkit-1/rules.d/49-login1-power-wheel.rules``
   ::
      /* Allow wheel to poweroff/reboot (elogind login1 actions) */
      polkit.addRule(function(action, subject) {
          if (!subject.isInGroup("wheel"))
              return;

          var a = action.id;
          if (a == "org.freedesktop.login1.power-off" ||
              a == "org.freedesktop.login1.power-off-multiple-sessions" ||
              a == "org.freedesktop.login1.reboot" ||
              a == "org.freedesktop.login1.reboot-multiple-sessions") {
              return polkit.Result.YES;
          }
      });

2) İzinler:
   ::
      chown root:root /etc/polkit-1/rules.d/49-login1-power-wheel.rules
      chmod 0644 /etc/polkit-1/rules.d/49-login1-power-wheel.rules

3) Tekrar oturum açın ve ``lxsession-logout`` üzerinden deneyin.


**Önemli Not:**
---------------

Sisteminizde polkit kullanıyorsanız ve masaüstü ortamı **LXDE** ise **lxpolkit** devre dışı bırakılmalıdır. Kaldırma işlemini **lxsession** otomatik başlatma seçeneklerinden **lxpolkit** kaldırılarak yapılır. Kaldırılmaması durumunda birden fazla yetkilendirme çalışıyor uyarısı alırız. 


**Kaynaklar**::

	- OpenRC Resmi Belgeler:	https://wiki.gentoo.org/wiki/OpenRC
	- Polkit Resmi Dokümantasyon:	https://www.freedesktop.org/software/polkit/docs/latest/
	- Arch Wiki — Polkit:	https://wiki.archlinux.org/title/Polkit
	- Arch Wiki — Elogind:	https://wiki.archlinux.org/title/Elogind
	- LXDE Resmi Wiki:	https://wiki.lxde.org/en/Main_Page
	- Debian Wiki — Polkit:	https://wiki.debian.org/PolicyKit
	- Polkit kural örnekleri (wheel group):	https://wiki.archlinux.org/title/Polkit#Bypass_password_prompt

.. raw:: pdf

   PageBreak

