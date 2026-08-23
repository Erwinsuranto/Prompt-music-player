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
