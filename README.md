# Praktikum Bersama Dosen: Data Layer Provinsi pada Google My Maps

Peta titik provinsi di Indonesia menggunakan **Google My Maps**, dibagi menjadi 5 layer berdasarkan wilayah pulau besar.

- **Nama / NIM:** Eko Muchamad Haryono / 0110223079
- **Program Studi:** Teknik Informatika, STT Terpadu Nurul Fikri
- **Mata Kuliah:** Sistem Informasi Geografis
- **Dosen Pengampu:** Dr. Sirojul Munir S.Si., M.Kom
- **Asisten Dosen:** Agam
- **Link peta:** _tempel link Google My Maps di sini_

## Struktur Folder

```
sig-praktikum-bersama-dosen/
├── README.md
└── data/
    ├── provinces.json            # data asli (34 provinsi + koordinat GPS)
    ├── provinsi.csv              # hasil konversi JSON → CSV
    ├── sebelum-perbaikan/        # dipisah per wilayah, diimpor ke Google My Maps
    │   ├── sumatera.csv
    │   ├── jawa-bali.csv
    │   ├── kalimantan.csv
    │   ├── sulawesi.csv
    │   └── indonesia_timur.csv
    └── hasil-perbaikan/          # koordinat sudah diperbaiki, 1 file = 1 layer
        ├── sumatera.csv
        ├── jawa-bali.csv
        ├── kalimantan.csv
        ├── sulawesi.csv
        └── indonesia_timur.csv
```

## Layer

| No  | Layer           | File                  | Provinsi                                                                                                                     | Jumlah |
| --- | --------------- | --------------------- | ---------------------------------------------------------------------------------------------------------------------------- | -----: |
| 1   | Sumatera        | `sumatera.csv`        | Aceh, Sumatera Utara, Sumatera Barat, Riau, Jambi, Sumatera Selatan, Bengkulu, Lampung, Kep. Bangka Belitung, Kepulauan Riau |     10 |
| 2   | Jawa-Bali       | `jawa-bali.csv`       | DKI Jakarta, Jawa Barat, Jawa Tengah, DI Yogyakarta, Jawa Timur, Banten, Bali                                                |      7 |
| 3   | Kalimantan      | `kalimantan.csv`      | Kalimantan Barat, Kalimantan Tengah, Kalimantan Selatan, Kalimantan Timur, Kalimantan Utara                                  |      5 |
| 4   | Sulawesi        | `sulawesi.csv`        | Sulawesi Utara, Sulawesi Tengah, Sulawesi Selatan, Sulawesi Tenggara, Gorontalo, Sulawesi Barat                              |      6 |
| 5   | Indonesia Timur | `indonesia_timur.csv` | Nusa Tenggara Barat, Nusa Tenggara Timur, Maluku, Maluku Utara, Papua Barat, Papua                                           |      6 |
|     | **Total**       |                       |                                                                                                                              | **34** |

## Format Data

| Kolom       | Keterangan                           |
| ----------- | ------------------------------------ |
| `id`        | Kode provinsi (Kemendagri)           |
| `name`      | Nama provinsi                        |
| `alt_name`  | Nama alternatif (sama dengan `name`) |
| `latitude`  | Lintang (desimal, WGS84)             |
| `longitude` | Bujur (desimal, WGS84)               |

## Perbaikan Koordinat GPS

Posisi setiap penanda dibandingkan dengan wilayah provinsinya pada peta dasar. Penanda yang jatuh di laut, di negara lain, atau di provinsi lain dianggap salah. Penanda dengan tanda minus yang hilang cukup dibalik tandanya. Penanda lainnya dipindahkan ke ibu kota provinsi.

| No  | Provinsi             | Layer           | Koordinat Awal      | Koordinat Perbaikan | Keterangan                                                                     |
| --- | -------------------- | --------------- | ------------------- | ------------------- | ------------------------------------------------------------------------------ |
| 1   | DKI Jakarta          | Jawa-Bali       | 6.1745, 106.8227    | -6.1745, 106.8227   | Tanda minus latitude hilang, titik berada di Laut Cina Selatan                 |
| 2   | DI Yogyakarta        | Jawa-Bali       | 7.7956, 110.3695    | -7.7956, 110.3695   | Tanda minus latitude hilang, titik berada di Laut Cina Selatan                 |
| 3   | Sumatera Barat       | Sumatera        | -1.34225, 100.0761  | -0.94708, 100.41718 | Titik berada di laut (Selat Mentawai), dipindahkan ke Padang                   |
| 4   | Kep. Bangka Belitung | Sumatera        | -2.75775, 107.58394 | -2.13163, 106.11693 | Titik berada di laut barat Tanjung Pandan, dipindahkan ke Pangkalpinang        |
| 5   | Nusa Tenggara Barat  | Indonesia Timur | -8.12179, 117.63696 | -8.58333, 116.11667 | Titik berada di laut (Laut Flores, utara Sumbawa), dipindahkan ke Mataram      |
| 6   | Papua Barat          | Indonesia Timur | -1.38424, 132.90253 | -0.86145, 134.06204 | Titik jatuh di Kab. Maybrat, kini Papua Barat Daya, dipindahkan ke Manokwari   |
| 7   | Papua                | Indonesia Timur | -3.98857, 138.34853 | -2.5916, 140.669    | Titik jatuh di Kab. Lanny Jaya, kini Papua Pegunungan, dipindahkan ke Jayapura |

Nomor 6 dan 7 terjadi karena pemekaran Papua tahun 2022: lokasi titik aslinya sekarang sudah masuk provinsi lain.

## Cara Import ke Google My Maps

1. Buka [Google Maps](https://maps.google.com) → **Saved** → **Maps** → **Open My Maps** → **Create A New Map**.
2. Beri nama peta: **Propinsi berdasarkan wilayah**.
3. **Add layer**, beri nama sesuai wilayah, lalu **Import** file CSV yang sesuai.
4. Kolom posisi: pilih `latitude` dan `longitude`.
5. Judul penanda: pilih `name`.
6. Ulangi untuk kelima file.

## Laporan & Screenshot

Laporan lengkap beserta screenshot dapat dilihat di [Laporan Praktikum (Google Docs)](https://docs.google.com/document/d/1JGUgPvtPCKKtuTgaPOuf6bqYxMzGxYoW/edit?usp=sharing&ouid=102442940817977066536&rtpof=true&sd=true).
