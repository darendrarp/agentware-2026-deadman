# BUILD_PLAN.md — Rencana jam-per-jam 72 jam (WIB)

**Kickoff (H00):** Sabtu, 28 Nov 2026 01:00 WIB · **Code freeze (H72):** Selasa,
1 Des 2026 01:00 WIB. Semua jam dalam WIB (UTC+7), sudah diverifikasi
`date -d`.

## 0. Konteks bentrok (baca dulu)

- **Even Realities:** build week 23–29 Nov; submission tutup **Senin, 30 Nov
  2026 02:59 WIB = H~50** Agentware. Artinya H00–H50 perhatian builder
  terbagi; H50–H72 fokus penuh Agentware.
- **Konsekuensi desain rencana:** inti DEADMAN (loop agent + kill switch +
  trace) HARUS selesai H24. H24–H48 = hardening + Trap Pack + video.
  H48–H50 = submit Even Realities (blok keras, jangan diganggu). H50–H72 =
  finalisasi Agentware + submit.
- **Keputusan prioritas ada di tangan user** (lihat `NEEDS_USER.md`). Bila user
  memutuskan Even Realities prioritas #1, rencana ini tetap jalan dengan
  memotong scope Agentware ke "core + kill switch + video" (daftar potong di
  §4) — bukan dengan begadang tanpa tidur.

## 1. Prinsip eksekusi

1. **Satu loop terus-menerus, tanpa restart fase.** Kerjakan modul berurutan,
   commit tiap modul selesai. Jangan kembali ke "fase riset" di tengah build.
2. **Demo path dulu, fitur kemudian.** H00–H24 menghasilkan run end-to-end
   yang bisa direkam; polish setelahnya.
3. **Checkpoint tiap blok.** Tiap blok di bawah punya deliverable + kriteria
   lolos. Blok yang gagal → potong scope (daftar §4), bukan menambah jam.
4. **Tidur itu jadwal.** Blok tidur ditandai; Paijo (agent) bisa lanjut
   kerja ringan (test, dokumen) saat user tidur, tapi langkah yang butuh user
   (rekam video, submit) hanya di jam bangun.
5. **Kode HANYA setelah H00.** Sebelum kickoff: dilarang menulis kode
   aplikasi (aturan "New Code Only"). Yang boleh: baca rubrik 26 Nov,
   siapkan akun test, baca Trap Pack saat rilis.

## 2. Jadwal blok-per-blok

### HARI 1 — Sabtu, 28 Nov (H00–H24): skeleton + inti + kill switch

| Jam | WIB | Blok | Deliverable + checkpoint |
|---|---|---|---|
| H00–H02 | 01:00–03:00 | **Kickoff** | Ambil Trap Pack dari Discord; baca pengumuman kickoff + rubrik final (rilis 26 Nov — konfirmasi tidak ada perubahan); buat struktur repo (README final, `.env.example`, `AGENT.md` kerangka, `SAFETY.md` kerangka); pasang venv + pytest. ✅ Checkpoint: Trap Pack tersimpan di `trappack/`; repo bisa `pytest` (0 test, 0 error). |
| H02–H06 | 03:00–07:00 | **Core loop + fixture** | Fixture mailbox (5 email: meeting request, konfirmasi, pertanyaan rutin, ambigu, 1 injeksi), kalender mock, `trigger` + `planner` (mock LLM dulu) + `tools` sandbox (send/book/archive/quarantine/digest). ✅ Checkpoint: `python -m deadman demo` menjalankan 1 run penuh mode mock, output digest tertulis. |
| H06–H10 | 07:00–11:00 | **Policy + firewall** | `firewall.py` (pembersih konten + deteksi pola injeksi), `policy.py` (allowlist, cap, aturan karantina). Unit test tiap aturan. ✅ Checkpoint: email injeksi fixture dikarantina, bukan dieksekusi; test policy hijau. |
| H10–H14 | 11:00–15:00 | **Kill switch + monitor** | `killswitch.py` (lease heartbeat, flag STOP, kill file, tripwire) + `monitor.py` (UI + tombol STOP + indikator lease). ✅ Checkpoint: matikan heartbeat di tengah run → halt ≤ 1 detik setelah aksi berjalan; tombol STOP bekerja dari browser. |
| H14–H18 | 15:00–19:00 | **Trace + LLM live** | `trace.py` (JSONL berantai-hash) + viewer di monitor; sambungkan LLM live (Gemini free tier; cadangan Groq) dengan backoff; 1 call per email. ✅ Checkpoint: run live menghasilkan trace lengkap yang bisa dibaca; trace hash chain terverifikasi skrip. |
| H18–H22 | 19:00–23:00 | **Run end-to-end #1 + catat** | Run penuh pertama (mock + live) direkam layarnya untuk arsip; tulis `SAFETY.md` draf; commit. ✅ Checkpoint: **GO/NO-GO HARI 1** — run penuh tanpa sentuhan manusia berhasil + kill switch terbukti halt. Bila gagal: potong ke scope minimal (§4) malam ini juga. |
| H22–H24 | 23:00–01:00 | **Istirahat + tugas ringan** | User tidur. Paijo: rapikan README setup (< 15 menit), tulis `AGENT.md`, siapkan skrip runner Trap Pack. |

### HARI 2 — Minggu, 29 Nov (H24–H48): Trap Pack + hardening + video

| Jam | WIB | Blok | Deliverable + checkpoint |
|---|---|---|---|
| H24–H28 | 01:00–05:00 | **Trap Pack run #1** | Jalankan seluruh Trap Pack; catat pass/fail per kasus; commit hasil mentah. ✅ Checkpoint: laporan Trap Pack v1 ada (jujur — fail dicatat, bukan disembunyikan). |
| H28–H32 | 05:00–09:00 | **Perbaiki hasil Trap Pack** | Tambal 3 kegagalan terbesar (firewall/policy); re-run kasus yang gagal. ✅ Checkpoint: tidak ada kasus Trap Pack yang menyebabkan aksi berbahaya (kirim/book) — karantina/halt adalah hasil yang dapat diterima. |
| H32–H36 | 09:00–13:00 | **Judge rehearsal** | Clone segar di direktori baru → ikuti README dari nol → ukur waktu setup (target < 15 menit); perbaiki semua langkah yang macet. ✅ Checkpoint: fresh-clone run berhasil tanpa bantuan penulis; waktu setup tercatat di README. |
| H36–H40 | 13:00–17:00 | **Polish monitor + demo** | Polish UI monitor (status run, trace viewer, tombol STOP); siapkan skenario demo video (fixture email final); latihan run demo 2×. ✅ Checkpoint: run demo stabil 2× berturut-turut. |
| H40–H44 | 17:00–21:00 | **🎥 REKAM VIDEO (butuh user)** | User merekam video demo ≤ 3 menit mengikuti `VIDEO_SCRIPT.md` (rekam layar + narasi). Paijo: siapkan run demo, standby bila run gagal di tengah rekaman. ✅ Checkpoint: file video mentah ada + durasi ≤ 3 menit. Fallback bila user tidak bisa: rekam Senin siang (H54–H58). |
| H44–H48 | 21:00–01:00 | **Buffer Hari 2 + Even Realities** | Buffer untuk video yang molor / bug terakhir; bila Agentware sudah hijau, alihkan ke finalisasi Even Realities (submit H~50). ✅ Checkpoint: **GO/NO-GO HARI 2** — video ada, Trap Pack v2 di-commit, judge rehearsal lolos. |

### HARI 3 — Senin, 30 Nov → Selasa, 1 Des (H48–H72): Even Realities submit, lalu finalisasi Agentware

| Jam | WIB | Blok | Deliverable + checkpoint |
|---|---|---|---|
| H48–H50 | 01:00–03:00 | **🔒 SUBMIT EVEN REALITIES** | Blok keras. Submit Even Realities (deadline 02:59 WIB). Agentware JEDA. ✅ Checkpoint: bukti submit Even Realities tersimpan. |
| H50–H54 | 03:00–07:00 | **Final fix Agentware** | Perbaiki bug yang ditemukan saat rehearsal/video; re-run Trap Pack final; commit hasil final. ✅ Checkpoint: Trap Pack final di-commit; tidak ada bug yang memblokir run demo. |
| H54–H58 | 07:00–11:00 | **Video final + submission** | Bila video belum direkam: rekam sekarang. Finalisasi `SUBMISSION_DRAFT.md` (isi link repo + video + hasil Trap Pack); upload video; finalisasi README (klaim jujur + biaya test run). ✅ Checkpoint: video ter-upload + bisa diputar; draf submission lengkap. |
| H58–H62 | 11:00–15:00 | **SUBMIT AGENTWARE** | Submit via mekanisme yang diumumkan di Discord (TIDAK DITEMUKAN di laman resmi — konfirmasi di Discord H00). Verifikasi submission tampil/tercatat; screenshot bukti. ✅ Checkpoint: **SUBMITTED** + bukti tersimpan. |
| H62–H66 | 15:00–19:00 | **Buffer submit** | Untuk: platform submit bermasalah, video perlu re-upload, README perlu perbaikan terakhir, atau juri bertanya di Discord. |
| H66–H72 | 19:00–01:00 | **Freeze + Near Miss draf** | Code freeze 01:00 WIB (Selasa 1 Des). Jangan commit kode setelah freeze. Bila sempat: draf tulisan Near Miss (side quest $100, tutup 8 Des 01:00 WIB) dari insiden build yang paling menarik. ✅ Checkpoint: repo beku, submission terverifikasi, draf Near Miss tersimpan (submit terpisah, opsional). |

## 3. Daftar submit (checklist H58–H62)

1. [ ] Repo publik, lisensi MIT, tanpa secret ter-commit (cek `git log` + grep
       API key).
2. [ ] README: setup < 15 menit, `.env.example`, biaya test run dinyatakan,
       cara run mock tanpa key.
3. [ ] `SAFETY.md` + `AGENT.md` lengkap.
4. [ ] Hasil Trap Pack di-commit (`trappack/results.md`).
5. [ ] Video ≤ 3 menit ter-upload, satu full unattended run.
6. [ ] Trace contoh satu run penuh ada di repo (`traces/`).
7. [ ] Submit via mekanisme resmi (konfirmasi di Discord) + screenshot bukti.
8. [ ] (Opsional) Draf Near Miss disimpan untuk dipublikasikan sebelum
       8 Des 01:00 WIB.

## 4. Daftar potong bila tertinggal (prioritas potong, dari pertama dipotong)

1. Deploy hosting gratis untuk monitor (demo lokal sudah cukup).
2. LLM live kedua (Groq) — mock + satu provider live sudah cukup.
3. Polish visual monitor (fungsi > estetika).
4. Skenario demo ekstra (satu skenario yang stabil > tiga yang rapuh).
5. **TIDAK BOLEH dipotong:** run end-to-end, kill switch (3 lapisan
   minimal: heartbeat + tombol + 1 tripwire), trace, SAFETY.md, video,
   hasil Trap Pack. Tanpa ini, submission tidak kompetitif.

## 5. Estimasi usaha

- Inti (H00–H24): ~18 jam kerja agent + 0 jam user.
- Hardening + video (H24–H48): ~16 jam agent + ~1 jam user (rekam video).
- Finalisasi + submit (H48–H72): ~10 jam agent + ~1 jam user (review
  submission + bila video molor).
- Total user: ~2 jam dalam 72 jam (video + review). Sisanya dikerjakan Paijo.
