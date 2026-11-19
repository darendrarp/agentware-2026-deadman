# NEEDS_USER.md — Kebutuhan user untuk Agentware Hackathon 2026

**Total waktu user selama 72 jam event: ~2 jam** (rekam video + review
submission). Sisanya dikerjakan Paijo. Tapi 4 hal di bawah ini HANYA bisa
dilakukan/diputuskan user — jangan sampai terlewat.

---

## 1. KEPUTUSAN: prioritas vs Even Realities (paling lambat 27 Nov)

Kickoff Agentware (Sab 28 Nov 01:00 WIB) bentrok dengan 2 hari terakhir
build week Even Realities (23–29 Nov), dan submission Even Realities tutup
Senin 30 Nov 02:59 WIB — tepat di tengah jendela 72 jam Agentware (H~50).

**Pilih satu:**

- **A. Even Realities dulu, Agentware jalan dengan scope inti.**
  BUILD_PLAN.md sudah dirancang untuk ini: inti DEADMAN selesai H24, lalu
  H50–H72 fokus penuh Agentware setelah Even Realities tersubmit.
  (Rekomendasi default — hadiah Even Realities $10K vs Agentware $1,8K.)
- **B. Agentware prioritas penuh 28–30 Nov.**
  Even Realities harus sudah 95% selesai sebelum 28 Nov 01:00 WIB, atau
  disubmit apa adanya di H48–H50.
- **C. Skip Agentware bila Even Realities belum siap 27 Nov malam.**
  Keputusan mundur paling lambat Jumat 27 Nov 20:00 WIB (5 jam sebelum
  kickoff) — jangan mulai 72 jam dengan dua proyek setengah jalan.

## 2. Gabung Discord Hackathon Raptors + registrasi (sebelum 26 Nov)

- **Discord:** https://discord.gg/xfYPDZYqeh (dari tombol laman resmi).
- Registrasi event dibuka sejak 26 Okt — lakukan via Discord (cara submit
  TIDAK DITEMUKAN di laman resmi; konfirmasi di Discord saat registrasi).
- Di Discord, tanyakan/konfirmasi: **(a)** cara submit resmi, **(b)** metode
  payout hadiah (TIDAK DITEMUKAN di laman), **(c)** kode perk sponsor
  (Solari, Keenable, akta.pro, Treg — dibagikan di Discord sebelum kickoff).
- Team formation tutup 23 Nov — tidak relevan (solo).

## 3. Cek rubrik 26 Nov (5 menit, Paijo yang kerjakan — user cukup baca ringkasan)

Full brief + rubrik penilaian rilis **26 Nov 2026** (jam pasti TIDAK
DITEMUKAN). Paijo akan cek ulang dan menyesuaikan prioritas build bila
bobot kriteria ternyata berbeda dari asumsi. User hanya perlu membaca
ringkasan perubahan (bila ada) sebelum kickoff.

## 4. Rekam video demo ≤ 3 menit (butuh user, ~1 jam)

- **Jadwal utama:** Minggu 29 Nov 17:00–21:00 WIB (H40–H44).
  **Fallback:** Senin 30 Nov 07:00–11:00 WIB (H54–H58).
- Naskah lengkap: `VIDEO_SCRIPT.md`. Rekam layar + narasi (atau teks layar
  bila tidak mau bersuara). Tanpa face cam — tidak diwajibkan.
- Paijo menyiapkan run demo + standby bila run gagal di tengah rekaman.

## 5. Review + gas submission (30 menit, Senin 30 Nov siang)

- Review draf submission (`SUBMISSION_DRAFT.md` yang sudah diisi link video
  + hasil Trap Pack), lalu gas submit di H58–H62.
- Submit dilakukan Paijo via mekanisme resmi (setelah dikonfirmasi di
  Discord); user memverifikasi bukti submit.

## 6. Opsional (tidak wajib, tapi bernilai)

- **The Near Miss (side quest, 3 × $100):** tulis pengalaman build
  (insiden nyaris-rogue / Trap Pack yang lolos / guardrail jam ke-60) dan
  publikasikan di X / LinkedIn / Dev.to / blog sebelum **Selasa 8 Des 2026
  01:00 WIB**. Draf disiapkan Paijo di H66–H72; user yang mempublikasikan
  (akun user). Dinilai dari insight, bukan follower.
- **Akun API gratis (opsional — mock mode sudah cukup):** bila ingin jalur
  LLM live, siapkan API key Gemini (Google AI Studio, gratis tanpa kartu)
  dan/atau Groq (gratis tanpa kartu). Key disimpan di `.env` lokal, TIDAK
  PERNAH di-commit. Bila tidak mau repot: lewati — juri bisa run penuh mode
  mock tanpa key apa pun.
- **FreeLLMAPI (opsional, dev-time saja):** router LLM self-hosted sudah
  terinstal di VM (`~/workspace/freellmapi`, server 127.0.0.1:3001) tapi
  first-run setup belum selesai (akun admin + provider keys belum dibuat).
  Bila mau dipakai sebagai failover LLM selama build, selesaikan setup
  sebelum kickoff. Bukan dependensi juri.

## 7. Yang TIDAK dibutuhkan dari user

- Tidak ada biaya / fee pendaftaran (event gratis).
- Tidak ada KYC / atestasi identitas yang disebut di laman resmi.
- Tidak ada syarat mahasiswa / domisili.
- Tidak ada akun baru yang wajib dibuat selain Discord (dan itu pun untuk
  registrasi/pengumuman).
