# dex-eliminator

Battery eliminator (dummy battery) 4.2V untuk board Samsung Galaxy Note 10/10+,
tujuan: Samsung DeX heavy mode tanpa baterai, stationary rig.

> Status: WIP — fase komisioning
> Risiko: SEDANG. Lo kerja langsung di rail baterai hp. Ikuti runbook, jangan improvisasi saat live.

## Apa ini?
Suplai permanen pengganti baterai:
- **Input:** adaptor 12V (satu-satunya sumber, >=2A, disarankan 3A)
- **Converter:** modul buck XL4015, diset 4.20V via trimpot
- **Output:** ke pad VBAT+ / GND di flex baterai donor
- **Buffer:** cap bank (polymer 1000uF x2 + monolithic 22uF) di sisi flex
- **Cooling:** fan + heatsink 12V ngeblower SoC, paralel di rail input
- **Proteksi:** fuse inline 3A di jalur 12V+, current limit + thermal shutdown bawaan XL4015

## Kenapa tanpa baterai?
Baterai li-ion tua = kembung, drop, throttling. Rig stationary nggak butuh
energi portabel; butuh suplai stabil yang nggak menua. Eliminator = baterai
yang nggak pernah habis dan nggak pernah kembung.

## Arsitektur (block diagram)

    ADAPTOR 12V (+) --[FUSE 3A]--+--> IN+ XL4015
                                 +--> fan merah (12V, 0.1A)
    ADAPTOR 12V (-) -------------+--> IN- XL4015
                                 +--> fan hitam

    OUT+ XL4015 --> pad VBAT+ flex  <== cap bank paralel di titik ini
    OUT- XL4015 --> pad GND   flex  <== (mepet konektor, bukan mepet modul)

## Angka kunci
| Parameter | Nilai | Catatan |
|---|---|---|
| Setpoint output | 4.18-4.22V | diukur di titik flex, saat dummy load |
| Langit-langit absolut | 4.40V | dari label sel; lewat = zona mati |
| Beban rata-rata hp | 1.5-2.5A | DeX heavy |
| Spike transient | ditanggung cap bank | orde milidetik |
| Arus input adaptor | 1.2-1.7A @12V | daya ~13-20W |
| Fan | 12V 0.1A | paralel rail input |

## Isi repo
- `README.md` — file ini
- `bom.md` — daftar belanja + link + harga + status
- `runbook.md` — prosedur komisioning & test; BACA SEBELUM MENYENTUH APAPUN
- `glossary.md` — kamus istilah listrik bahasa manusia
- `measurements.md` — log tegangan/arus tiap tahap (ini "CI" lo)
- `diagram.md` — block diagram & catatan skema
- `photos/` — dokumentasi build per tahap

## Golden rules
1. Set tegangan SEBELUM konek ke hp. Jangan pernah puter trimpot saat hp live.
2. Beep test (+ vs - di flex) wajib lolos sebelum colok.
3. Cap bank hidup di sisi flex, sedekat mungkin ke konektor.
4. Stop condition kena = cabut adaptor dulu, mikir kemudian.
5. Repo ini dokumentasi, bukan pengganti kewaspadaan.

## Stop conditions
- Asap / bau hangus
- Meter >4.3V di titik flex
- Beep saat test kontinuitas + vs -
- Hp error temperatur / gagal boot berulang
- Modul panas sampai nggak bisa disentuh

## Disclaimer
Mod sendiri = risiko sendiri. Dokumen ini build log + panduan, bukan garansi.
Kalau ragu di satu step: berhenti, foto, tanya lagi.

## Changelog
- v0.1 — repo init; BOM terkumpul; XL4015 (pre-soldered) di tangan
