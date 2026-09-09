# MEASUREMENTS — logbook

File ini CI-nya build lo. Semua angka masuk sini, termasuk yang gagal.
Kegagalan = data, bukan aib. Baris gagal justru yang paling berharga buat
debug bulan depan.

## Kriteria PASS rujukan (dari runbook)
| Item | PASS |
|---|---|
| Polaritas barrel adaptor | angka positif, +11..13V |
| OUT modul tanpa beban | 4.18-4.22V |
| OUT modul + dummy 2A, 60 menit | 4.15-4.25V, drift <0.05V |
| Pad flex sebelum colok hp | 4.15-4.25V |
| Flex saat idle | 4.1-4.3V |
| Flex saat DeX heavy (V min) | >=4.0V; bawah itu = droop, curigai cap bank |
| NTC sel bekas | catat nilai kOhm-nya, berapa pun |

## Template sesi (copy per session)
### Session N — YYYY-MM-DD — <judul>
| Tanggal | Fase-step | Titik ukur | Mode meter | Bacaan | PASS? | Catatan |
|---|---|---|---|---|---|---|
|  |  |  |  |  |  |  |

## Log
### Session 1 — EXAMPLE (hapus baris contoh ini saat pakai)
| 2026-XX-XX | F0 | barrel adaptor | DCV | +12.1V | PASS | center-positive |
| 2026-XX-XX | F1-2 | OUT noload | DCV | 4.20V | PASS | trimpot ~14 putaran |
| 2026-XX-XX | F1-3 | OUT dummy 60' | DCV | 4.18V | PASS | modul hangat, resistor panas wajar |

## Maintenance log
| Tanggal | Inspeksi | Hasil | Aksi |
|---|---|---|---|
|  | solderan, glue, debu fan |  |  |
