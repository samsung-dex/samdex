# GLOSSARY — kamus listrik bahasa manusia

Dikelompokkan per tema. Analogi utama: ledeng (air) dan rumah tangga.
Ketemu istilah asing di runbook? Cari di sini dulu.

## Konsep dasar
- **Tegangan (volt, V)** — tekanan air; kekuatan dorong listrik.
- **Arus (ampere, A)** — deras aliran airnya.
- **Daya (watt, W)** — tekanan x deras; total kerja per detik; "tagihan" sebenarnya.
- **Hambatan (ohm, Ω)** — penyempitan pipa; pembatas aliran.
- **Polaritas** — arah aliran; DC satu arah; ketuker +/− = barang rusak.
- **Short / korslet** — + dan − ketemu tanpa hambatan; air muncrat tanpa kran; arus ngamuk.
- **Kontinuitas / beep** — mode meter buat ngecek dua titik nyambung atau tidak.
- **Impedansi** — hambatan versi umum; di project ini baca saja "hambatan".
- **Node** — titik temu beberapa kaki/kabel yang secara listrik sama.
- **Paralel vs seri** — paralel: kepala sama kepala, ekor sama ekor (kapasitas nambah,
  tegangan tetap); seri: berantai (tegangan nambah). Cap bank = paralel.
- **OL (over limit)** — bacaan meter "di luar jangkauan" = biasanya jalur putus/terbuka.
- **Center-positive** — pin tengah barrel adaptor = kutub +; standar umum, tapi tetap verifikasi.

## Komponen
- **Resistor** — pembatas arus; mengubah listrik jadi panas secukupnya.
- **Resistor kapur** — resistor semen 10W; dummy load (beban palsu) buat test.
- **Kapasitor (cap)** — toren setrum; nyimpan dan melepas cepat.
- **Elco** — kapasitor elektrolit kaleng; ada polaritas (strip minus).
- **Polymer / solid cap** — elco versi isi polymer; ESR rendah, tahan spike.
- **MLCC** — kapasitor keramik SMD kecil; cepet banget, tapi bikin build looks tambalan.
- **Monolithic ceramic** — keramik radial blob biru berkaki; pengganti MLCC yang ramah solder pemula.
- **ESR** — hambatan dalam cap; low-ESR = keran toren lebar; yang kita cari.
- **Inductor** — kumparan di dalam modul; bagian dari mesin penurun tegangan; jangan diutak-atik.
- **Trimpot / potensio** — sekrup biru pemutar setpoint tegangan output modul.
- **Resistor FB** — resistor pabrik penentu tegangan bawaan; target mod seller; bukan target lo.
- **NTC / thermistor** — sensor suhu baterai; sebagian hp nolak boot tanpa ini di pin T.
- **Fuse + holder** — sekering; putus duluan biar yang mahal nggak ikut mati.
- **Heatsink** — sirip aluminium penyebar panas.
- **Thermal tape / paste** — tape konduktif buat nempel; paste buat ngisi celah IC-heatsink (bukan lem).
- **Flex** — pita kabel oranye tipis; jalur konektor baterai.
- **Pad** — titik logam tempat nyolder di flex/PCB.
- **Barrel jack / DC female** — colokan adaptor; female jack pigtail = versi berkabel buat disolder.
- **Bus wire** — kabel pendek pengumpul node (mis. node + cap bank).
- **AWG** — ukuran kabel; angka kecil = gemuk. 20AWG cukup buat rail ini.

## Modul & sistem
- **Buck / step-down** — penurun tegangan; XL4015 lo itu.
- **Rail** — seluruh jalur satu tegangan; "rail 4.2V" = semua kabel bertegangan 4.2V.
- **VBAT** — pin jalur baterai di board hp; tujuan akhir eliminator.
- **PMIC** — IC manajer listrik dalam hp; yang bagi-bagi setrum ke komponen.
- **SoC** — prosesor hp; sumber panas yang dikipas.
- **CC/CV** — mode arus tetap / tegangan tetap; relevan kalau modul punya dua trimpot.
- **Current limit** — proteksi pembatas arus modul; ngerem sebelum ngamuk.
- **Thermal shutdown** — proteksi mati sendiri saat kepanasan.
- **Headroom** — cadangan kapasitas; modul 5A narik 3A = headroom 2A.
- **Spike / transient / load step** — permintaan arus mendadak; lima kran kebuka bareng.
- **Droop** — tegangan kecemplung sesaat karena suplai ketinggalan; penyebab reboot misterius.
- **Cap bank** — beberapa cap paralel mepet konektor; toren + ember penanggung spike.
- **Dummy load** — beban palsu (resistor kapur) buat test tanpa melibatkan hp.
- **Burn-in** — uji nyala berjam-jam buat nyari cacat dini.

## Solder & tools
- **Cold joint** — solderan kelihatan nempel tapi nggak ngantar; kusam berbintil.
- **Reflow** — manasin ulang solderan biar ngalir dan ngantar bener.
- **Tinning** — ngasih lapisan timah tipis dulu di pad/kabel sebelum nyolder beneran.
- **Flux** — pembersih oksida; bikin timah mau ngalir; penyelamat pemula.
- **Solder sucker / wick** — penyedot / sumur timah; tombol undo.
- **Strain relief** — pengunci kabel (hot glue) biar solderan nggak ketarik.
- **Helping hands** — stand bercapit penahan benda kerja; tangan ketiga lo.
- **IPA** — alkohol isopropil; pembersih flux dan kotoran pad.
- **DCV / ohm / beep / capacitance** — mode-mode multimeter: tegangan DC, hambatan,
  kontinuitas, kapasitas. Project ini hidup di DCV + beep; capacitance bonus.

## Cara pakai file ini
Ketemu kata asing di runbook → grep file ini → lanjut kerja.
Nemu istilah baru yang belum ada? Tambahin sendiri; repo lo, kamus lo.
