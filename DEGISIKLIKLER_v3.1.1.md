# Güvenli Okul v3.1.1 — Değişiklik kaydı

## Özellikle korunanlar
- `app.py`, `stil.py`, `i18n.py` ve diğer mevcut sayfaların arayüz akışı/dekorasyonu değiştirilmedi.
- Mevcut logo, modüller, içerikler ve özellikler silinmedi.
- Veritabanı dosyası ZIP'e eklenmedi; yerel kayıtların üzerine yazılmaz.
- Otomatik veri silme/retention mekanizması eklenmedi.

## Yapılan düzeltmeler ve eklemeler
1. **PDF yazı tipleri:** Türkçe ve Latin dilleri için DejaVu Sans, Arapça için Noto Sans Arabic dosyaları eklendi. PDF artık yazı tipi bulunamadığında bozuk varsayılan fontla devam etmek yerine açıklayıcı hata verir.
2. **Arapça PDF desteği:** `arabic-reshaper` ve `python-bidi` kullanılarak harf birleştirme ve sağdan sola metin sıralaması desteklenir. Bu iki paket `requirements.txt` içinde zaten tanımlı.
3. **Daha güvenilir sayım:** PDF tüm bildirim kayıtlarını belleğe çekmek yerine SQL toplu istatistiklerini kullanır. Böylece eski 100.000 satırlık liste sınırı rapor sayımlarını etkilemez.
4. **PDF altbilgisi:** Sayfa numarası ve rapor oluşturulma zamanı eklendi. Tekil bildirim açıklamaları ve takip kodları rapora dahil edilmez.
5. **Eksik kurulum örneği:** README'nin tarif ettiği `.streamlit/secrets.toml.example` eklendi. İçinde gerçek parola bulunmaz; yönetici parolası kullanıcının kendi bilgisayarında üretilmelidir.
6. **Git güvenliği:** Mevcut `gitignore.txt` silinmedi; GitHub'ın tanıdığı `.gitignore` dosyası ayrıca eklendi. Yerel veritabanı ve gerçek `secrets.toml` bu dosyada yok sayılır.
7. **Regresyon testleri:** PDF'nin altı Latin tabanlı dilde üretimi, kişisel bildirim metninin dışarıda kalması ve kayıt listesi sınırından bağımsız toplu sayım testleri eklendi. Arapça testi, bağımlılıkların kurulu olduğu ortamda çalışır.

## Kontrol sonucu
- Python sözdizimi derlemesi: başarılı.
- Otomatik test: 8 başarılı, 1 atlandı.
- Türkçe, İngilizce, Almanca, Fransızca, İspanyolca ve Azerbaycanca PDF dosyaları oluşturuldu ve PDF okuyucusuyla açıldı.
- Arapça test bu kontrol ortamında `arabic-reshaper` ve `python-bidi` yüklü olmadığından çalıştırılamadı. Uygulama bilgisayarında `py -m pip install -r requirements.txt` komutu bu gereksinimleri kurar.
- Streamlit arayüzü bu kontrol ortamında başlatılmadı; arayüz dosyaları değiştirilmedi.
