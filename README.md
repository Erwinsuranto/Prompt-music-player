# Prompt-music-player


# 
```


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
