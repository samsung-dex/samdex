# RUNBOOK — dex-eliminator

Aturan main: tiap step punya kriteria PASS. Gagal = berhenti, debug, jangan
loncat. Semua angka dicatat ke `measurements.md`. Istilah asing ada di
`glossary.md`.

## Fase 0 — Inspeksi kedatangan (tanpa daya)
- [ ] XL4015: solderan mengkilap bentuk kubah (kusam/berbintil = cold joint,
      reflow ulang dulu), kaki komponen utuh, trimpot tidak pecah.
- [ ] Adaptor: label 12V >=2A. Cek polaritas barrel pakai meter DCV: probe
      merah ke pin tengah, hitam ke selongsong → angka positif = center-positive. Catat.
- [ ] Fan: label 12V, baling diputar tangan halus tidak seret.
- [ ] Elco: badan tidak kembung, strip minus terbaca.
- [ ] Foto semua → `photos/00-unboxing/`.

## Fase 1 — Set bench (hp TIDAK terlibat)
- [ ] Rakit input: DC female jack → fuse inline 3A di jalur + → IN+ modul;
      jalur − → IN− modul.
      PASS: meter di pad IN nunjuk +11..13V, bukan minus.
- [ ] Nyala tanpa beban. Meter DCV20 di kabel OUT. Puter trimpot ke 4.20
      (multi-turn, 10-25 putaran; sabar).
      PASS: 4.18-4.22 stabil 1 menit.
- [ ] Dummy load: tempel resistor kapur 2.2R ke kabel OUT (twist + isolasi),
      probe meter tetap di titik sama. Burn-in 30-60 menit.
      PASS: bacaan 4.15-4.25; drift <0.05V; modul hangat bukan menyengat.
      WARNING: permukaan resistor >100C. Taruh di keramik, jangan dipegang.
- [ ] Matikan, lepas resistor. Log: V noload, V load, durasi, suhu modul (rasa tangan).

## Fase 2 — Prep flex donor
- [ ] Panen flex dari baterai bekas: isolasi sel dulu (tape kedua terminal),
      jangan tusuk/bengkokkan sel. Sel kembung = buang selnya proper, flex tetap aman dipakai.
- [ ] Petakan pin. Sel masih bertegangan: mode DCV, cari pasangan pad yang
      nunjukin 3.0-4.2V → pad kena probe merah = +, tandai spidol.
      Sel mati: mode ohm → pad vs − yang nunjuk orde kOhm = pin T (sensor suhu).
      PASS: tiga pin tertandai: +, −, T.
- [ ] Bersihkan pad, tin tipis-tipis.

## Fase 3 — Blok cap bank
- [ ] Paralel 2x elco 1000uF + 1x monolithic 22uF: semua kaki + jadi satu node,
      semua − jadi satu node. Strip minus elco = sisi −. Monolithic bebas.
- [ ] Bungkus hot glue/heat shrink jadi satu blok rapi; dua bus wire keluar
      (merah dari node +, hitam dari node −), panjang <5cm.
      PASS: beep test bus merah vs hitam = diam, atau blip singkat sekali lalu
      diam (itu cap keisi, normal). Beep terus-terusan = short, bongkar.

## Fase 4 — Integrasi & verify (hp masih BELUM konek)
- [ ] Solder OUT modul: merah → pad + flex, hitam → pad − flex.
- [ ] Solder bus cap bank paralel di titik yang sama (mepet konektor).
- [ ] Strain relief: hot glue kunci semua kabel di badan flex.
      PASS: beep test pad + vs − = diam / blip singkat sekali.
- [ ] Nyala tanpa hp. Meter di pad flex.
      PASS: 4.15-4.25. Meleset = matikan, re-set trimpot, ulang. (Boleh puter
      trimpot SELAMA hp belum konek.)
- [ ] Pasang fan paralel di rail input; arah blower ke area SoC + menyapu modul.

## Fase 5 — First boot & load bertahap
- [ ] Hp MATI total. Dudukkan flex ke konektor sampai mentok.
- [ ] Nyala adaptor → boot.
      PASS: masuk OS tanpa error baterai/temperatur.
      Gagal boot / error temp → matikan, ke tabel troubleshooting (NTC).
- [ ] Idle 10 menit. PASS: 4.1-4.3V di flex, tanpa reboot.
- [ ] DeX ringan 30 menit (browser/video). PASS: sama.
- [ ] DeX heavy 30-60 menit (game/benchmark). PASS: tanpa reboot; log V min/max.
- [ ] Lulus semua = production ready. Foto final → `photos/99-final/`.

## Fase 6 — Maintenance
- [ ] Bulan pertama: sesi 4 jam seminggu, log ke measurements.
- [ ] Bulanan: inspeksi solderan + glue + debu fan.
- [ ] Reboot muncul kemudian = curigai solderan cap bank dulu, lalu ukur V di flex saat load.

## Troubleshooting
| Gejala | Tersangka pertama | Aksi |
|---|---|---|
| Gagal boot / error temperatur | pin T kosong | ukur NTC sel bekas (orde kOhm), pasang resistor nilai sama di pad T |
| Reboot cuma saat heavy | droop: solderan cap bank / kabel kurus | reflow, tambah cap, ukur V di flex saat load |
| Modul panas menyengat | ventilasi / beban | reposition fan, heatsink kecil di IC, cek arus real |
| Output 0V | fuse putus / polaritas input | cek kontinuitas fuse, cek polaritas |
| Bacaan meter lompat-lompat | probe kendor / cold joint | wiggle test, reflow solderan dicurigai |

## STOP CONDITIONS (kena salah satu = CABUT ADAPTOR DULU)
Asap/bau hangus • >4.3V di flex • beep terus saat test + vs − • percikan •
permukaan panas sampai nggak bisa disentuh.

## Aturan emas
1. Trimpot cuma boleh diputer saat hp BELUM konek.
2. Cabut adaptor dulu, mikir kemudian.
3. Semua angka masuk measurements.md — itu CI lo.
4. Ragu = berhenti, foto, tanya.
