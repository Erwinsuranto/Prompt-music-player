# Prompt-music-player


# 
```


```
# 
```


```
# 
```


```
# 
```


```
# 
```


```
# 
```


```
# 
```


```
# 
```


```
# 
```


```
# 
```


```
# 
```


```
# 
```


```
# 
```
Tambahkan fitur Lyrics pada project Audiva Music (/root/YT-Music-Mod).

TUJUAN:
Buat tab "Lyrics" pada halaman Now Playing benar-benar berfungsi, bukan hanya tombol UI.

ATURAN PENTING:
- Jangan mengubah atau merusak layout Search / All Songs yang sudah diperbaiki.
- Jangan mengubah player, queue, related, favorite, atau fungsi playback yang sudah berjalan kecuali benar-benar diperlukan untuk integrasi lyrics.
- Jangan membuat ulang arsitektur aplikasi.
- Pertahankan style UI Audiva yang sekarang.
- Kerjakan langsung pada repository yang ada dan gunakan struktur/kode yang sudah tersedia.
- Sebelum coding, inspect terlebih dahulu bagaimana data lagu, metadata, audio URL, Now Playing modal/page, dan routing saat ini bekerja.

FITUR LYRICS:
1. Pada Now Playing yang saat ini memiliki tab:
   Song | Lyrics | Queue | Related
   buat tab "Lyrics" menampilkan panel lirik ketika dipilih.

2. Cari sumber data lyrics yang SUDAH tersedia di project/API yang digunakan Audiva.
   - Periksa apakah metadata lagu/API response sudah memiliki lyrics atau synchronized lyrics.
   - Jika sudah ada, gunakan data tersebut.
   - Jangan menambahkan provider/API eksternal berbayar hanya untuk fitur ini.
   - Jangan hardcode lirik lagu tertentu.

3. Dukung dua jenis lirik:
   A. Plain lyrics
      - Tampilkan teks lirik dengan rapi.
      - Gunakan line wrapping yang baik.
      - Bisa discroll secara vertikal.
   B. Timestamped/synchronized lyrics
      - Parse timestamp per baris.
      - Tandai baris yang sedang aktif berdasarkan currentTime audio.
      - Saat lagu berjalan, highlight baris aktif.
      - Auto-scroll perlahan agar baris aktif tetap terlihat.
      - Jangan membuat auto-scroll mengganggu user ketika user sedang scroll manual.

4. Sinkronisasi:
   - Gunakan current playback time dari player yang sudah ada.
   - Jangan membuat audio player kedua.
   - Ketika pause, sinkronisasi berhenti.
   - Ketika seek/forward/backward, posisi lirik harus langsung menyesuaikan.
   - Ketika lagu berganti, lyrics harus reset dan memuat lyrics lagu baru.

5. STATE:
   - Loading: tampilkan indikator/loading sederhana.
   - Lyrics tersedia: tampilkan lyrics.
   - Lyrics tidak tersedia: tampilkan pesan "Lirik tidak tersedia untuk lagu ini."
   - Error API: jangan membuat player error; tampilkan fallback yang aman.
   - Jangan membuat layout bergeser/overflow horizontal.

6. DESAIN MOBILE:
   - Lyrics harus nyaman dibaca di layar HP.
   - Panel lyrics menggunakan ruang yang tersedia pada Now Playing.
   - Judul lagu/artist tetap jelas.
   - Jangan membuat teks terlalu kecil.
   - Jangan membuat lirik memenuhi seluruh layar jika struktur Now Playing saat ini memang menggunakan tab.
   - Gunakan spacing dan typography yang konsisten dengan Audiva.
   - Pastikan tidak tertutup oleh mini player atau bottom navigation.
   - Tidak boleh ada horizontal overflow.

7. DESKTOP:
   - Pertahankan layout Now Playing desktop yang sudah ada.
   - Lyrics panel harus memiliki max-width yang nyaman dibaca.
   - Jangan membuat artwork atau komponen Song menjadi membesar hanya karena Lyrics.

8. PERFORMANCE:
   - Jangan request lyrics berulang setiap audio timeupdate.
   - Lyrics cukup dimuat ketika lagu berubah atau ketika data lyrics memang belum tersedia.
   - Gunakan cache sederhana selama sesi jika diperlukan.

9. KOMPATIBILITAS:
   - Jangan menghapus API/function existing.
   - Jangan mengubah kontrak endpoint existing jika tidak diperlukan.
   - Jika endpoint backend perlu diperbaiki untuk mengambil lyrics, lakukan secara modular dan tetap backward-compatible.

10. VERIFIKASI:
   Setelah implementasi:
   - jalankan syntax/build check yang sesuai project;
   - pastikan tidak ada JavaScript error;
   - test lagu dengan lyrics;
   - test lagu tanpa lyrics;
   - test play/pause;
   - test seek;
   - test pindah lagu;
   - test tab Song ↔ Lyrics ↔ Queue ↔ Related;
   - test mobile dan desktop;
   - pastikan Search / All Songs tetap seperti sebelumnya.

JANGAN BERHENTI hanya setelah membuat UI tab Lyrics.
Pastikan tab Lyrics benar-benar terhubung ke data lyrics dan playback time yang sudah ada.

Setelah selesai, berikan ringkasan:
- file yang diubah;
- sumber data lyrics yang digunakan;
- apakah synchronized lyrics berhasil didukung;
- hasil build/test;
- git commit hash.

Lalu commit perubahan dengan pesan:
"Add synchronized lyrics to now playing"
dan push ke origin main.

```
# 
```
Kita akan membuat repository terpisah bernama `ssh-setup`, khusus untuk mengaktifkan SSH password login pada VPS baru dengan cara sesederhana mungkin, idealnya satu kali menjalankan script.

Ini adalah PROMPT 1 — AUDIT & DESAIN SAJA.

Tugas:
1. Audit environment VPS saat ini:
   - OS dan versinya
   - systemd/init system
   - lokasi konfigurasi sshd
   - versi OpenSSH server
   - nama service SSH (`ssh`/`sshd`)
   - apakah root login saat ini diizinkan
   - apakah password authentication saat ini diizinkan
   - apakah ada konfigurasi di `/etc/ssh/sshd_config.d/`
   - apakah cloud-init atau konfigurasi provider berpotensi menimpa setting SSH

2. Cari semua konfigurasi SSH yang efektif dan konflik, terutama:
   - `PermitRootLogin`
   - `PasswordAuthentication`
   - `KbdInteractiveAuthentication`
   - `PubkeyAuthentication`
   - `AuthenticationMethods`

3. Jangan mengubah konfigurasi sistem.
   Jangan restart/reload SSH.
   Jangan mengubah password.
   Jangan membuat file repository.
   Jangan install package apa pun.

4. Berdasarkan hasil audit, desain script `enable-password.sh` yang nantinya:
   - aman dijalankan pada VPS baru
   - idempotent
   - membuat konfigurasi SSH khusus tanpa merusak konfigurasi bawaan
   - memvalidasi `sshd` sebelum restart
   - mendukung Ubuntu/Debian sebisa mungkin
   - menghindari lockout SSH
   - dapat dijalankan ulang tanpa menghasilkan konfigurasi duplikat
   - memberikan output/status yang jelas
   - memungkinkan root login menggunakan password

5. Periksa juga apakah ada perbedaan antara konfigurasi yang tertulis di file dan konfigurasi efektif hasil `sshd -T`.

6. Berikan laporan:
   - kondisi VPS saat ini
   - konfigurasi SSH efektif
   - potensi masalah/konflik
   - desain struktur repository
   - desain alur `enable-password.sh`
   - rekomendasi keamanan

PENTING:
- Ini hanya audit.
- Jangan melakukan perubahan apa pun pada sistem.
- Jangan commit atau push.
- Berhenti setelah laporan audit selesai.

```
# 
```
Prompt: Phase 8B — Real Picture-in-Picture Player

Di /root/music-player lanjutkan dari hasil diagnosis Phase 8.

Tujuan:
Membuat Music Player dapat dibuka sebagai floating Picture-in-Picture player ketika user keluar dari halaman, jika browser mendukung.

PENTING:
- Jangan mengubah YouTubeProvider.
- Jangan membuat YT.Player kedua.
- Jangan mengambil direct audio YouTube.
- Jangan bypass DRM/iklan.
- Jangan menggunakan scraper.
- Jangan menambahkan storage/Telegram/downloader.
- Gunakan player YouTube yang sudah ada.
- Jika browser tidak mendukung PiP, fallback ke popup player existing.

Audit kode existing terlebih dahulu.

Diketahui project sudah memiliki:
- startSystemPip()
- openPipWidget()
- Media Session
- popup player

Tugas:

1. Audit implementasi PiP existing.
2. Deteksi:
   - documentPictureInPicture
   - Picture-in-Picture API
   - Media Session enterpictureinpicture
   - browser support

3. Gunakan Document Picture-in-Picture jika tersedia untuk membuat floating player HTML.

4. Floating player minimal menampilkan:
   - cover
   - title
   - artist
   - play/pause
   - previous
   - next
   - progress
   - close

5. Semua kontrol harus menggunakan:
   PlaybackManager → YouTubeProvider

6. Jangan membuat player YouTube baru di jendela PiP.
   PiP hanya menjadi UI/controller.

7. Sinkronkan:
   - current song
   - play/pause
   - progress
   - next/previous
   - queue
   - metadata

8. Ketika PiP ditutup:
   - playback tetap berjalan jika browser mengizinkan
   - popup player existing tetap tersedia
   - tidak membuat YT.Player baru

9. Ketika kembali ke halaman:
   - PiP ditutup sesuai behavior browser
   - UI utama kembali sinkron

10. Tambahkan fallback:
   Jika Document PiP tidak tersedia:
   → gunakan popup player existing.
   Jangan tampilkan error fatal.

11. Mobile Android:
   Uji semampunya:
   - Chrome Android
   - Home
   - pindah aplikasi
   - PiP muncul/tidak
   - kontrol play/pause
   - next
   - kembali ke browser

12. Desktop:
   - Chrome
   - background tab
   - PiP
   - close PiP
   - kembali ke tab

13. Jangan mengklaim background audio berhasil jika belum dites pada perangkat nyata.

14. Test:
   - PiP supported
   - PiP unsupported fallback
   - metadata sync
   - play/pause
   - next/previous
   - progress
   - close PiP
   - one YT.Player
   - popup fallback
   - existing 226+ regression tests

15. Jika ada perubahan dan semua test PASS:
   git add .
   git commit -m "feat: add picture-in-picture player"
   git push origin main

Jika PiP tidak dapat digunakan untuk YouTube IFrame karena keterbatasan browser:
- jangan membuat workaround ilegal;
- laporkan limitation dengan jelas;
- jangan commit perubahan yang tidak perlu.

Tampilkan hasil real-device test secara terpisah dari unit test.

```
# 
```
Prompt: Investigate Chrome Android Background Playback

Di /root/music-player lakukan investigasi terakhir untuk masalah background playback.

JANGAN mengubah code.
JANGAN commit/push.

Kondisi:
- YouTube IFrame adalah playback provider.
- Media Session sudah diimplementasikan.
- Unit test lulus.
- Android Chrome real-device background playback masih gagal.
- Target: setelah user menekan Home, musik tetap berjalan.

Audit:

1. Periksa versi Chrome Android yang digunakan.
2. Periksa apakah project sudah memiliki:
   - manifest.json
   - service worker
   - PWA installability
   - display: standalone
   - Media Session API

3. Tentukan apakah menjadikan Music Player sebagai PWA secara resmi dapat membantu background playback ketika sumber audio tetap YouTube IFrame.

4. Bedakan:
   - background tab
   - installed PWA
   - Picture-in-Picture
   - screen lock
   - Android notification/media control

5. Jangan menyarankan direct audio URL YouTube.
6. Jangan menyarankan scraper.
7. Jangan bypass DRM/iklan.
8. Jangan membuat audio proxy YouTube.

6. Berikan hasil dengan kategori:

A. Bisa diperbaiki di aplikasi
B. Bisa dengan PWA tetapi perlu pengujian
C. Dibatasi Chrome Android
D. Dibatasi YouTube IFrame

7. Jika ada solusi PWA yang resmi dan masuk akal, jelaskan perubahan yang diperlukan tetapi jangan implementasikan.

8. Lakukan pengecekan apakah ada kode kita sendiri yang memanggil pause(), destroy(), reload(), atau menghentikan playback ketika document hidden/pagehide.

9. Jangan mengubah file.

Tampilkan diagnosis akhir dan rekomendasi.

```
# 
```
Prompt: Real Android Background Playback Diagnosis

Di /root/music-player, jangan ubah code dan jangan commit/push.

Kita sudah mengetahui unit test Media Session PASS, tetapi Android Chrome background playback masih NOT TESTED.

Tujuan:
Cari tahu penyebab sebenarnya mengapa YouTube IFrame belum terbukti tetap berjalan ketika browser keluar dari foreground.

Lakukan audit dan diagnosis saja.

1. Audit YouTubeProvider dan Media Session.
2. Pastikan Media Session benar-benar dipanggil dari top-level page.
3. Pastikan metadata dan action handler terdaftar.
4. Pastikan playbackState mengikuti state YT.Player.
5. Audit visibilitychange/pagehide/pageshow.
6. Pastikan aplikasi TIDAK memanggil pause ketika document menjadi hidden.
7. Pastikan tidak ada reload/destroy YT.Player ketika halaman menjadi background.
8. Audit apakah service worker/PWA diperlukan atau justru tidak relevan.
9. Jangan membuat direct audio stream.
10. Jangan bypass YouTube/DRM/iklan.
11. Jangan membuat YT.Player kedua.

Berikan diagnosis:
A. Bug aplikasi yang bisa diperbaiki,
B. keterbatasan browser,
C. keterbatasan YouTube IFrame,
atau
D. belum dapat dipastikan tanpa real-device test.

Jika memang bisa diperbaiki secara resmi, jelaskan perubahan yang diperlukan tetapi JANGAN implementasikan dulu.

Jalankan test yang aman dan tampilkan hasilnya.
Jangan commit/push.

```
# Prompt: Phase 8 — Background Playback & Media Session
```

Prompt: Phase 8 — Background Playback & Media Session

Di repository /root/music-player, lanjutkan pengembangan Music Player.

TUJUAN:
Membuat playback sebisa mungkin tetap berjalan ketika user:
- keluar dari halaman web
- membuka aplikasi lain
- meminimalkan browser
- mengunci layar

dan menyediakan kontrol media native jika browser mendukung.

PENTING:
- Tetap menggunakan PlaybackManager → YouTubeProvider.
- Tetap menggunakan YouTube IFrame Player.
- Jangan membuat direct audio stream YouTube.
- Jangan bypass iklan/DRM.
- Jangan menggunakan scraper.
- Jangan membuat YT.Player kedua.
- Jangan mengubah sumber katalog.
- Jangan menambahkan Telegram/storage/downloader.
- Jangan menjanjikan background playback jika browser/YouTube memang membatasi.
- Fallback harus tetap playback normal di foreground.

TAHAP 1 — AUDIT

Audit:
1. public/player/playback-manager.js
2. public/player/youtube-provider.js
3. public/app.js
4. public/index.html
5. lifecycle YT.Player
6. browser visibilitychange/pagehide/pageshow
7. existing audio/media handling
8. PWA/service worker jika ada

Tentukan apakah project sudah memiliki:
- Media Session API
- navigator.mediaSession
- MediaMetadata
- media session action handlers
- PWA manifest
- service worker
- Wake Lock
- visibility handling

Jangan menambahkan service worker hanya untuk memaksa audio YouTube tetap berjalan.

TAHAP 2 — MEDIA SESSION

Jika browser mendukung Media Session API, implementasikan integrasi dengan PlaybackManager.

Set metadata:
- title
- artist
- album
- artwork

Action handlers:
- play
- pause
- previoustrack
- nexttrack
- seekbackward
- seekforward
- seekto

Semua action harus diteruskan ke PlaybackManager → YouTubeProvider.

Jangan membuat player baru.

Update:
navigator.mediaSession.playbackState

menjadi:
- playing
- paused
- none

sesuai state player sebenarnya.

TAHAP 3 — BACKGROUND/LOCK SCREEN

Audit dan implementasikan lifecycle yang aman untuk:
- visibilitychange
- pagehide
- pageshow
- freeze/resume jika browser mendukung

Jangan memanggil pause hanya karena document.visibilityState berubah menjadi hidden.

Jika browser mengizinkan YouTube IFrame tetap berjalan di background:
- biarkan playback berjalan.

Jika browser menghentikannya:
- jangan mencoba bypass restriction.
- tampilkan fallback/error state yang jelas bila diperlukan.

TAHAP 4 — ANDROID

Optimalkan untuk:
- Android Chrome
- Android browser berbasis Chromium

Target:
1. Play lagu.
2. Tekan Home.
3. Buka aplikasi lain.
4. Kembali ke browser.
5. Playback state tetap sinkron.
6. Jika browser menyediakan media notification/control, kontrol harus bekerja.
7. Lock screen test jika browser mengizinkan.

Jangan menganggap semua browser Android memiliki behavior yang sama.

TAHAP 5 — DESKTOP

Pastikan background tab tidak menyebabkan:
- duplicate player
- reload player
- reset queue
- reset current track
- reset progress
- playback state salah

TAHAP 6 — MOBILE UI

Pastikan ketika user kembali ke web:
- popup player tetap sinkron
- progress benar
- play/pause benar
- current song benar
- queue tetap benar

TAHAP 7 — TEST

Buat test untuk:

1. Media Session tersedia
2. Media Session tidak tersedia → fallback aman
3. metadata update
4. play action
5. pause action
6. next action
7. previous action
8. seek action
9. playbackState update
10. visibility hidden
11. visibility visible
12. pagehide/pageshow
13. satu YT.Player tetap digunakan
14. queue tidak berubah
15. popup player tetap sinkron
16. no-song state
17. error state

Jalankan semua regression test sebelumnya.

Target:
Semua test PASS.

TAHAP 8 — REAL DEVICE TEST

Jika environment memungkinkan, dokumentasikan hasil:
- Android Chrome foreground
- Android Chrome background
- Android Chrome lock screen
- desktop background tab

Bedakan dengan jelas:
PASS = browser benar-benar mempertahankan playback
LIMITATION = browser/YouTube menghentikan playback
NOT TESTED = tidak dapat diuji

Jangan mengklaim background playback berhasil jika hanya lolos unit test.

TAHAP 9 — GIT

Jika ada perubahan dan semua regression test PASS:

git add .
git commit -m "feat: improve background playback support"
git push origin main

Jika browser limitation membuat sebagian behavior tidak dapat dijamin, jangan membuat workaround ilegal. Laporkan limitation tersebut.

Tampilkan:
- file berubah
- Media Session support
- background playback result
- lock screen result
- Android result
- desktop result
- total test
- commit SHA
- git status
```
# Prompt: Jalankan Music Player
```
Di repository /root/music-player, jalankan Music Player sekarang.

Tugas:
1. Pastikan berada di:
   /root/music-player

2. Jangan mengubah source code.
3. Jangan membuat commit.
4. Jangan push.
5. Cek apakah ada proses Music Player yang sedang berjalan.
6. Jika belum berjalan, jalankan server menggunakan:
   npm start

7. Jalankan sebagai proses background yang tetap hidup setelah terminal/AI selesai, gunakan metode yang sudah tersedia di server (misalnya nohup jika sesuai).

8. Pastikan server listen pada port yang tersedia. Jangan mengambil port yang sedang digunakan service lain.

9. Setelah server berjalan, lakukan test:
   curl -I http://127.0.0.1:PORT/
   curl http://127.0.0.1:PORT/api/home

10. Tampilkan:
   - PID server
   - port yang digunakan
   - status server
   - hasil HTTP test
   - URL yang bisa dibuka dari luar VPS berdasarkan IP VPS

11. Jangan mematikan service lain yang tidak berkaitan.

Jika port default project sudah dikonfigurasi, gunakan port tersebut. Jika port sedang dipakai service lain, cari port kosong dan jelaskan port yang dipilih.

```
# Prompt: Persistent Popup Player on Back
```
Di repository /root/music-player, tambahkan fitur Persistent Popup/Mini Player.

Tujuan:
Ketika user menekan Back/kembali dari halaman Now Playing atau berpindah kembali ke halaman sebelumnya, lagu yang sedang diputar tetap berjalan dan player berubah menjadi popup/mini player yang selalu terlihat.

PENTING:
- Jangan mengubah arsitektur PlaybackManager.
- Jangan mengubah YouTubeProvider.
- Jangan membuat instance YT.Player kedua.
- Gunakan player instance yang sudah aktif.
- Jangan menghentikan playback ketika navigasi/back.
- Jangan menambahkan DirectProvider.
- Jangan menambahkan Telegram, storage, downloader, atau database.
- Pertahankan semua fitur existing.

BEHAVIOR:

1. Jika tidak ada lagu yang sedang diputar:
   - popup player tidak ditampilkan.

2. Jika ada lagu sedang diputar:
   - mini/popup player tetap tersedia ketika user kembali dari Now Playing.
   - playback tetap berjalan.

3. Popup player menampilkan:
   - cover
   - judul lagu
   - artist
   - play/pause
   - next
   - progress bar
   - tombol untuk membuka Now Playing
   - tombol close/hide jika memang sesuai dengan UI existing

4. Ketika popup player diklik:
   - buka kembali Now Playing.
   - jangan membuat YT.Player baru.

5. Ketika user menekan Back dari Now Playing:
   - kembali ke halaman sebelumnya.
   - player tetap aktif.
   - popup player muncul.

6. Ketika berpindah:
   Home → Search → Album → Artist → Playlist
   popup player tetap tersedia selama ada lagu aktif.

7. Ketika lagu berubah:
   - popup otomatis memperbarui cover, title, artist, duration, dan progress.

8. Ketika play/pause dilakukan dari popup:
   - state harus langsung sinkron dengan YouTubeProvider dan PlaybackManager.

9. Ketika next dilakukan:
   - gunakan queue existing.
   - jangan membuat player baru.

10. Ketika lagu selesai:
   - ikuti behavior existing untuk repeat/autoplay/radio/queue.

RESPONSIVE:

Mobile:
- popup/mini player berada di atas bottom navigation jika ada.
- tidak menutupi tombol navigasi.
- tinggi compact.
- tombol mudah ditekan.

Desktop:
- gunakan mini player/popup yang rapi.
- jangan menutupi konten utama.
- tetap terlihat ketika user berpindah halaman.

NAVIGATION:

Audit cara routing/navigation existing terlebih dahulu.

Jangan menggunakan location.reload() untuk membuat fitur ini.

Pastikan state player tidak hilang ketika:
- browser back
- tombol Back UI
- pindah halaman internal
- membuka/menutup Now Playing

LIFECYCLE:

Pastikan:
- hanya ada satu YT.Player
- popup hanya menjadi UI/controller tambahan
- event listener tidak duplicate
- tidak ada memory leak
- destroy/re-init tidak terjadi hanya karena membuka/menutup popup

TEST:

Tambahkan/regression test untuk:

1. tidak ada lagu → popup hidden
2. lagu aktif → popup visible
3. Now Playing → Back → popup visible
4. popup → Now Playing
5. play/pause dari popup
6. next dari popup
7. perubahan lagu memperbarui popup
8. queue tetap sama
9. YT.Player tetap satu instance
10. playback tidak berhenti ketika Back
11. mobile viewport
12. desktop viewport
13. refresh behavior sesuai state existing

Jalankan:
- node --check semua JS
- semua unit test existing
- semua frontend test existing
- semua regression test existing
- test baru popup player
- endpoint baseline

Jangan melakukan perubahan yang tidak berkaitan.

Jika semua test PASS:
git add .
git commit -m "feat: add persistent popup player"
git push origin main

Setelah selesai tampilkan:
- file yang berubah
- behavior popup
- hasil test
- konfirmasi bahwa hanya satu YT.Player digunakan
- commit SHA
- status git

```
# Prompt: Phase 7 — Final YouTube Production Audit
```
Prompt: Phase 7 — Final YouTube Production Audit

Di repository /root/music-player, lakukan final production audit untuk versi YouTube Music.

TUJUAN:
Memastikan versi YouTube benar-benar stabil ketika digunakan melalui browser nyata, mobile, desktop, dan jaringan berbeda.

PENTING:
- Jangan menambahkan fitur baru.
- Jangan implement DirectProvider.
- Jangan mengubah sumber katalog.
- Jangan membuat direct audio stream YouTube.
- Jangan bypass iklan/DRM.
- Jangan menambahkan Telegram, storage, downloader, database, atau authentication.
- YouTubeProvider tetap playback utama.
- Perbaiki hanya bug nyata yang ditemukan dalam audit.

1. BASELINE
Pastikan:
- git status bersih sebelum mulai
- semua test Phase 6 masih PASS
- server dapat dijalankan
- endpoint utama tetap normal

2. REAL BROWSER AUDIT

Gunakan browser/HTTP verification yang tersedia untuk menguji:

Desktop:
- Chrome/Chromium
- viewport normal desktop
- search
- play
- pause
- next/previous
- queue
- shuffle
- repeat
- seek
- volume
- quality
- lyrics
- album
- artist
- playlist

Mobile:
- viewport sekitar 390px
- touch interaction
- mini player
- Now Playing
- queue
- search
- scrolling
- orientation/responsive layout

3. YOUTUBE PLAYBACK

Verifikasi:
- YT.Player hanya satu instance
- onReady bekerja
- onStateChange bekerja
- ENDED → next bekerja
- BUFFERING tidak membuat state macet
- error player ditangani
- next/previous cepat tidak menyebabkan race
- reload halaman tidak meninggalkan state rusak
- membuka/menutup Now Playing tidak membuat player baru

4. YOUTUBE PREMIUM

Jika tersedia akun/session Premium untuk pengujian browser:
- verifikasi player tetap berfungsi ketika user memiliki YouTube Premium
- jangan meminta atau menyimpan credential
- jangan mencoba mengotomatisasi login
- jangan memalsukan status Premium
- jangan mengubah mekanisme iklan YouTube

Jika akun Premium tidak tersedia, cukup dokumentasikan bahwa pengujian Premium tidak dapat dilakukan.

5. NETWORK

Simulasikan bila tooling memungkinkan:
- normal
- koneksi lambat
- request timeout
- API gagal
- browser offline lalu online kembali

Pastikan:
- tidak blank screen
- error state jelas
- player tidak crash
- recovery dapat dilakukan

6. CONSOLE

Audit browser console:
- uncaught exception
- unhandled promise rejection
- duplicate event listener
- failed API request
- failed asset
- CORS error
- iframe error

Bedakan error aplikasi sendiri dengan warning/error yang berasal dari YouTube IFrame pihak ketiga.

7. PERFORMANCE

Audit:
- memory leak
- duplicate player
- excessive API request
- excessive DOM render
- unnecessary reload
- localStorage abuse
- event listener leak

Jangan menambahkan dependency besar.

8. EXISTING FEATURES

Regression check:
- Home
- Search
- Suggestions
- Charts
- Moods
- Album
- Artist
- Playlist
- Related
- Radio/autoplay
- Queue
- Favorites
- History
- Local playlist
- Lyrics
- SponsorBlock
- Sleep timer
- Playback speed
- Quality
- Mini Player
- Now Playing
- responsive UI
- light/dark theme

9. SECURITY/BASIC CONFIG

Audit secara ringan:
- tidak ada API key/secret hardcoded
- tidak ada credential browser
- tidak ada debug endpoint yang tidak diperlukan
- input query ditangani dengan aman
- tidak ada file rahasia yang ikut git

Jangan melakukan security redesign besar.

10. PERBAIKAN

Jika menemukan bug:
- perbaiki hanya bug yang benar-benar terverifikasi
- jangan mengubah behavior yang sudah benar
- setelah setiap perbaikan jalankan regression test

11. FINAL TEST

Jalankan:
- node --check semua JS
- JSON validation
- seluruh unit test
- seluruh frontend test
- seluruh regression test
- endpoint live test
- browser/UI test
- playback test

Target:
SEMUA PASS.

12. FINAL REPORT

Tampilkan:
- browser test
- mobile test
- desktop test
- playback test
- API test
- console result
- performance result
- security/basic config result
- bug ditemukan
- bug diperbaiki
- file berubah
- total test PASS/FAIL
- status YouTube playback

13. GIT

Jika ada perubahan dan SEMUA test PASS:

git add .
git commit -m "test: finalize YouTube Music production audit"
git push origin main

Jika tidak ada perubahan:
- jangan membuat empty commit
- cukup laporkan working tree clean

Setelah selesai, jangan mengerjakan Phase DirectProvider/Telegram/storage.

```

# Prompt: Phase 6 — Complete YouTube Music Features
```
Prompt: Phase 6 — Complete YouTube Music Features

Di repository /root/music-player, lanjutkan Phase 6.

TUJUAN:
Selesaikan dan poles seluruh fitur yang menggunakan YouTube Music/YouTube asli sampai production-ready.

SCOPE WAJIB:
Hanya YouTube Music + YouTube IFrame playback.

JANGAN:
- implement DirectProvider
- implement direct audio YouTube
- bypass iklan/DRM
- Telegram
- Google Drive
- R2
- downloader baru
- database baru
- authentication baru
- mengganti sumber katalog
- redesign besar UI

DEFAULT:
PlaybackManager → YouTubeProvider tetap menjadi playback utama.

TAHAP 1 — AUDIT FITUR EXISTING

Audit seluruh fitur berikut:

1. Home
2. Search
3. Search suggestions
4. Songs
5. Videos
6. Albums
7. Artists
8. Playlists
9. Charts
10. Moods/Genres
11. Album detail
12. Artist detail
13. Playlist detail
14. Related music
15. Radio/autoplay
16. Queue
17. Play next
18. Shuffle
19. Repeat
20. Lyrics
21. History
22. Favorites
23. Local playlists
24. Saved albums/artists/playlists
25. Statistics
26. SponsorBlock
27. Playback quality
28. Playback speed
29. Sleep timer
30. Picture-in-picture jika existing
31. Mini player
32. Now Playing
33. Theme
34. Mobile responsive
35. Desktop responsive

TAHAP 2 — API

Audit semua endpoint yang digunakan frontend.

Untuk setiap endpoint:
- pastikan response konsisten
- validasi parameter
- handle empty result
- handle YouTube API error
- handle timeout/network failure
- jangan membuat frontend crash

Pastikan endpoint existing tetap backward compatible.

TAHAP 3 — SEARCH

Pastikan:
- search normal
- filter Songs/Videos/Albums/Artists/Playlists
- suggestions
- empty result
- error state
- hasil duplicate tidak berlebihan
- thumbnail dan metadata benar
- videoId/browseId benar

TAHAP 4 — ALBUM/ARTIST/PLAYLIST

Pastikan:
- detail berhasil dibuka
- metadata benar
- track list benar
- play all
- shuffle
- add to queue
- save
- thumbnail
- navigation back
- pagination/continuation jika memang digunakan

TAHAP 5 — PLAYBACK

Audit secara menyeluruh:
- play
- pause
- resume
- next
- previous
- seek
- volume
- speed
- quality
- queue
- shuffle
- repeat
- autoplay/radio

Pastikan hanya ada satu instance YT.Player.

Pastikan tidak terjadi race condition ketika:
- user menekan next cepat
- user mengganti lagu saat buffering
- lagu selesai
- player error
- user berpindah halaman
- Now Playing dibuka/ditutup

TAHAP 6 — LYRICS

Pastikan lyrics:
- mengambil data berdasarkan lagu yang benar
- tidak menampilkan lyrics lagu sebelumnya
- synced lyrics tetap sinkron
- fallback plain lyrics tetap bekerja
- error lyrics tidak mengganggu playback

TAHAP 7 — LIBRARY

Pastikan:
- favorite
- history
- playlist
- saved items
- statistics

tidak hilang atau corrupt.

Pastikan localStorage error tidak menyebabkan aplikasi crash.

TAHAP 8 — SPONSORBLOCK

Audit integrasi SponsorBlock.

Pastikan:
- tidak mengganggu lagu normal
- error SponsorBlock tidak menghentikan playback
- segment salah tidak menyebabkan seek loop
- state reset ketika lagu berubah

TAHAP 9 — ERROR HANDLING

Tambahkan/fix handling untuk:
- YouTube unavailable
- video removed
- playback error
- API timeout
- API response kosong
- thumbnail gagal
- lyrics gagal
- network offline
- player initialization gagal

Error harus user-friendly dan tidak menyebabkan blank screen.

TAHAP 10 — PERFORMANCE

Audit:
- duplicate API request
- duplicate event listener
- unnecessary render
- unnecessary player reload
- memory leak
- localStorage access berlebihan
- cache yang tidak perlu

Jangan menambahkan dependency besar.

TAHAP 11 — TEST

Jalankan seluruh test yang sudah ada.

Tambahkan test hanya jika memang diperlukan untuk bug/regression yang ditemukan.

Wajib:
- node --check semua JS
- JSON validation
- PlaybackManager tests
- YouTubeProvider tests
- frontend load tests
- endpoint tests
- search tests
- album/artist/playlist tests
- queue tests
- race-condition tests
- lyrics tests
- library tests

Target:
SEMUA test harus PASS.

TAHAP 12 — MANUAL/HTTP VERIFICATION

Test endpoint real:
- /api/home
- /api/search?q=test
- /api/charts
- /api/moods
- /api/next
- /api/related
- /api/browse
- /api/suggest
- /api/lyrics
- /api/sponsorblock
- /api/resolve
- endpoint lain yang benar-benar digunakan frontend

Pastikan HTTP 200 atau error response yang memang expected.

TAHAP 13 — REGRESSION

Pastikan:
- YouTube Music catalog tetap berfungsi
- YouTube IFrame tetap berfungsi
- PlaybackManager tetap default YouTubeProvider
- UI mobile tetap berfungsi
- UI desktop tetap berfungsi
- tidak ada DirectProvider implementation
- tidak ada Telegram/Storage/Downloader baru

Jika menemukan bug, perbaiki hanya dalam scope Phase 6.

SEBELUM COMMIT:

Tampilkan:
1. daftar file berubah
2. fitur yang diperbaiki
3. bug yang ditemukan
4. hasil seluruh test
5. hasil endpoint test
6. status YouTube playback
7. status working tree

Jika SEMUA test PASS:
git add .
git commit -m "feat: complete YouTube Music features"
git push origin main

Jika tidak ada perubahan yang diperlukan:
jangan membuat empty commit.

JANGAN melakukan perubahan di luar scope.

```

# Prompt: Phase 5 — UI/UX Music Player
```

Di repository /root/music-player, lanjutkan Phase 5: UI/UX Music Player.

Tujuan:
Merapikan dan meningkatkan pengalaman penggunaan Music Player di mobile dan desktop, tanpa merusak fitur atau arsitektur playback yang sudah stabil.

PENTING:
- Jangan mengubah YouTubeProvider secara arsitektural.
- Jangan implement DirectProvider.
- Jangan menambahkan Telegram, downloader, storage, database, atau authentication.
- Jangan mengubah sumber katalog YouTube Music.
- Playback harus tetap menggunakan PlaybackManager → YouTubeProvider.
- Pertahankan semua fitur existing.

Sebelum coding:
1. Audit UI existing di public/index.html, public/app.js, dan public/styles.css.
2. Jalankan baseline test terlebih dahulu.
3. Identifikasi bagian UI yang benar-benar perlu diperbaiki.
4. Jangan melakukan redesign total jika tidak diperlukan.

Target UI:

1. Mobile-first
   - nyaman pada layar Android
   - tidak ada horizontal overflow
   - tombol player mudah ditekan
   - bottom navigation/player tidak menutupi konten
   - Now Playing nyaman digunakan dengan satu tangan

2. Desktop
   - layout tetap rapi pada layar besar
   - sidebar dan content tidak bertabrakan
   - player tetap mudah diakses

3. Mini Player
   - tampil saat ada lagu aktif
   - cover, judul, artist
   - play/pause
   - next
   - klik untuk membuka Now Playing

4. Now Playing
   - cover besar
   - judul + artist
   - progress bar
   - elapsed/duration
   - play/pause
   - previous/next
   - shuffle
   - repeat
   - volume
   - quality
   - lyrics
   - queue

5. Queue
   - lagu aktif terlihat jelas
   - reorder/remove tetap berfungsi
   - queue tidak hilang ketika UI berpindah halaman

6. Search
   - search bar nyaman di mobile
   - loading state
   - empty state
   - error state
   - hasil search tetap memakai API existing

7. Album / Artist / Playlist
   - card/list responsive
   - thumbnail tidak pecah
   - informasi tetap terbaca pada layar kecil

8. Loading/Error
   - tambahkan state yang jelas jika API YouTube Music gagal
   - jangan membuat error JS ketika data kosong
   - jangan menampilkan blank screen tanpa informasi

9. Accessibility dasar
   - tombol memiliki title/aria-label yang sesuai
   - keyboard navigation desktop tetap memungkinkan
   - kontras teks/tombol tetap terbaca

10. Performance
   - jangan menambahkan library frontend besar tanpa alasan
   - hindari event listener duplicate
   - hindari render berulang yang tidak diperlukan
   - jangan mengganggu lifecycle YT.Player

Testing wajib:
- node --check seluruh JS
- validasi JSON
- existing unit tests
- frontend load test
- endpoint baseline
- test mobile viewport
- test desktop viewport
- test mini player
- test Now Playing
- test queue
- test search
- test theme light/dark jika fitur existing tetap digunakan
- pastikan YouTube playback tetap normal

Jika menemukan bug:
- perbaiki hanya bug yang berkaitan dengan scope Phase 5.
- jangan melakukan perubahan backend yang tidak diperlukan.

Setelah selesai tampilkan:
- file yang berubah
- perubahan UI utama
- hasil seluruh test
- masalah yang ditemukan dan diperbaiki
- status YouTube playback

Jika semua test lulus:
git add .
git commit -m "feat: improve music player UI"
git push origin main

Jika tidak ada perubahan yang diperlukan, jangan membuat empty commit.
```

# Prompt: Fix Facebook OAuth Domain Configuration
```
Prompt: Phase 4 — YouTube Playback Optimization

Di repository /root/music-player, lanjutkan Phase 4.

Tujuan:
Mengoptimalkan playback YouTube yang sekarang tanpa membuat bypass iklan atau direct-stream YouTube.

PENTING:
- YouTubeProvider tetap menjadi provider utama/default.
- Jangan menggunakan scraper, DRM bypass, circumvention, atau metode untuk menghindari sistem iklan YouTube.
- Jangan mengambil direct audio URL dari YouTube.
- Jangan menghapus YouTube IFrame Player.
- Jangan implement DirectProvider.
- Jangan menambahkan Telegram, storage, downloader, atau database.
- Pertahankan semua fitur existing.

Tugas:

1. Audit seluruh YouTubeProvider dan PlaybackManager.

2. Audit lifecycle YT.Player:
   - onReady
   - onStateChange
   - onError
   - onPlaybackQualityChange
   - loadVideoById
   - cueVideoById
   - play/pause
   - seek
   - volume
   - playback rate

3. Pastikan tidak terjadi:
   - duplicate YT.Player
   - duplicate event listener
   - race condition saat next/previous
   - playback state tidak sinkron dengan UI
   - queue melompat ke lagu yang salah
   - autoplay gagal setelah track selesai
   - player stuck pada BUFFERING
   - lyrics/history salah track

4. Audit kualitas playback:
   - default YouTube Music audio mode
   - quality/max mode yang sudah ada
   - mobile browser
   - Android Chrome
   - iOS Safari
   - desktop browser

5. Audit kompatibilitas ketika user memiliki YouTube Premium.
   Jangan mengubah atau memalsukan authentication.
   Jangan membuat klaim bahwa embedded player pasti bebas iklan.
   Pastikan aplikasi tidak mengganggu session/account YouTube pengguna.

6. Audit SponsorBlock agar tidak mengganggu playback normal.

7. Audit error handling:
   - video unavailable
   - playback error
   - network error
   - player initialization error
   - API error

8. Audit performa:
   - unnecessary reloadVideo
   - unnecessary player recreation
   - excessive API calls
   - memory leak
   - event listener leak

9. Buat perbaikan hanya jika benar-benar diperlukan dan tetap mempertahankan behavior existing.

10. Jalankan semua test:
   - node --check semua JS
   - existing unit tests
   - frontend load test
   - endpoint baseline
   - YouTube IFrame initialization test
   - PlaybackManager/YouTubeProvider test

11. Jangan mengubah DirectProvider selain jika diperlukan untuk menjaga interface compatibility.

12. Tampilkan laporan:
   - masalah yang ditemukan
   - perbaikan yang dilakukan
   - file yang berubah
   - hasil semua test
   - status YouTube playback

13. Jika semua test lulus:
   git add .
   git commit -m "fix: optimize YouTube playback"
   git push origin main

Jika tidak ada masalah yang perlu diperbaiki:
- jangan membuat perubahan hanya demi membuat commit;
- cukup laporkan bahwa baseline sudah optimal dan working tree tetap clean.

```
