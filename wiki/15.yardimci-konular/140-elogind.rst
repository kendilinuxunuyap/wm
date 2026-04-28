**elogind Yapılandırması**
==========================

Bu belge, **systemd kullanmayan** sistemlerde (OpenRC tabanlı) 
elogind login manager'ın kurulumu, yapılandırılması ve gerekli 
kullanıcı/PAM/agetty ayarlarını anlatır.

**1. Gerekli Kullanıcı ve Grup Tanımları**
------------------------------------------

elogind servisi için sistemde gerekli kullanıcı ve gruplar oluşturulur:

.. code-block:: bash

   groupadd -g 190 systemd-journal
   groupadd -g 191 elogind
   useradd -r -s /sbin/nologin -g elogind -u 191 elogind

Açıklama:
.........

- `systemd-journal` grubu, journal log erişimi için kullanılır.
- `elogind` kullanıcı ve grubu, servis için ayrılmıştır.
- `/sbin/nologin` ile bu kullanıcıyla doğrudan login engellenir.
- `-r` parametresi sistemi kullanıcı oluşturur, yani normal login için kullanılmaz.

**2. OpenRC Hizmet Dosyası (/etc/init.d/elogind)**
--------------------------------------------------

OpenRC ile `elogind` servisini yönetmek için basit bir init script örneği:

.. code-block:: bash

   #!/sbin/openrc-run
   description="elogind login manager"
   command=/usr/lib/elogind/elogind
   pidfile=/run/elogind.pid

   depend() {
       need dbus
       after dbus
   }

Açıklama:
.........

- `command`: elogind daemonunu başlatır.
- `pidfile`: servis PID bilgisini saklar.
- `depend()`: servis başlatılmadan önce D-Bus’ın aktif olmasını garanti eder.


.. raw:: pdf

   PageBreak
   
**3. Başlatma ve OpenRC’ye Ekleme**
-----------------------------------

.. code-block:: bash

   rc-update add elogind default
   rc-service elogind start

Açıklama:
.........

- `rc-update add`: Servisi boot sırasında otomatik başlatmaya ekler.
- `rc-service start`: Servisi hemen başlatır.

- **Önemli Kontrol:** elogind’in çalışıp çalışmadığını kontrol etmek için:

.. code-block:: bash

   loginctl list-sessions

- Eğer aktif oturumlar listeleniyorsa, elogind başarıyla çalışıyor demektir.

**4. PAM, Passwd ve Group Ayarları**
------------------------------------

**/etc/nsswitch.conf Örneği:**

.. code-block:: none

   passwd:      files
   group:       files
   shadow:      files

Açıklama:
.........

- Kullanıcı ve grup bilgileri `files` (yerel /etc/passwd ve /etc/group) üzerinden çözülür.

**/etc/pam.d/system-auth Örneği:**

.. code-block:: none

   auth       required     pam_unix.so
   account    required     pam_unix.so
   password   required     pam_unix.so
   session    required     pam_unix.so
   session    include      elogind-user

.. note::

   **`session include elogind-user` satırı mutlaka ekli olmalıdır.**  
   Bu satır, kullanıcı oturumlarının elogind ile doğru şekilde yönetilmesini sağlar.  
   Eğer yoksa manuel olarak eklenmelidir:

   .. code-block:: bash

      sed -i "/elogind-user/d" /etc/pam.d/system-auth
      echo -e "\nsession    include    elogind-user" >> /etc/pam.d/system-auth


.. raw:: pdf

   PageBreak
   
**5. OpenRC Agetty Ayarı**
--------------------------

Bazı durumlarda `agetty`, varsayılan olarak `/bin/login` kullanmaz
ve bu nedenle elogind kullanıcı oturumunu başlatamaz.

**Ayar:**

.. code-block:: bash

   sed -i "/agetty_options/d" /etc/conf.d/agetty
   echo -e "\nagetty_options=\"-l /usr/bin/login\"" >> /etc/conf.d/agetty

Açıklama:
.........

- `-l /usr/bin/login` ile agetty doğru login programını çağırır.
- Bu ayar, sanal konsollardan kullanıcı girişlerinin doğru şekilde yapılmasını garanti eder.

**6. Diğer Öneriler ve Notlar**
-------------------------------

- `elogind`, sistemde `/run/systemd` gibi dizinler oluşturur; böylece bazı uygulamalar systemd’ye ihtiyaç duymadan çalışabilir.
- Polkit yetkilendirme sorunları genellikle kullanıcıların `wheel` grubuna dahil olmamasıyla ilişkilidir.
- OpenRC + elogind ile systemd’ye gerek kalmadan oturum yönetimi sağlanabilir.

**Kaynaklar**::

- elogind resmi dokümanı: https://www.freedesktop.org/wiki/Software/systemd/elogind/  
- OpenRC belgeleri: https://wiki.gentoo.org/wiki/OpenRC  
- PAM belgeleri: https://www.linux-pam.org/  
- Polkit belgeleri: https://www.freedesktop.org/wiki/Software/polkit/

.. raw:: pdf

   PageBreak

