# Scheduling

## Definisi

Scheduling menentukan prioritas proses yang perlu dilayani oleh CPU terlebih dahulu

## Short CPU Burst

Proses ketika CPU mengeksekusi barisan program yang sedikit, sehingga terjadi traffic sedikit. Termasuk dalam kategori `IO Bound`

## Long CPU Burst

Proses ketika CPU mengeksekusi barisan program yang panjang, sehingga terjadi traffic banyak. Termasuk dalam kategori `CPU Bound`

## Scheduling Algorithm Goals

- Fairness

Memastikan setiap proses membatahkan jatahnya secara adil

- Batch System

Penentuan kapan sebuah proses dapat dimulai dan perlu diakhiri

- Interactive Systems

Menentukan kapan proses dimulai berdasarkan `human perception`

- Real-time Systems

Menentukan apakah deadline termasuk `critical` atau tidak.

## Scheduling Batch Systems

- First-come first-served

Keuntungan: Mudah untuk diimplementasikan

Kelemahan: Tidak optimal

- Shortest job first

Keuntungan: Mendekati optimal

Kelemahan: Harus mengetahui run-time tiap proses

- Shortest remaining time next