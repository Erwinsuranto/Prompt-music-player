# Prompt-music-player


# 
```


```

# 
```


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
