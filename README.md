# Factor Analysis - Study Case: Indikator Kemiskinan Jawa Timur

## Deskripsi Proyek

Proyek ini merupakan implementasi **Analisis Faktor (Factor Analysis)** menggunakan Python untuk mengidentifikasi faktor-faktor laten yang mendasari indikator kemiskinan di Kabupaten/Kota se-Jawa Timur. Analisis faktor digunakan untuk mereduksi sejumlah besar variabel yang saling berkorelasi menjadi kelompok-kelompok faktor yang lebih sedikit, sehingga struktur data yang kompleks dapat dipahami dengan lebih sederhana.

Dataset yang digunakan mencakup berbagai indikator sosial-ekonomi seperti tingkat pengangguran terbuka, tingkat partisipasi angkatan kerja, pengeluaran perkapita, indeks pembangunan manusia, gini rasio, dan indikator lainnya.

## Alur Analisis

Analisis dalam proyek ini mengikuti tahapan berikut:

1. **Import Library** -- Memuat seluruh pustaka yang dibutuhkan.
2. **Inisialisasi Data** -- Membaca dataset dari file Excel (`Data_AF.xlsx`).
3. **Pengecekan Missing Value** -- Mengidentifikasi data yang hilang.
4. **Handling Missing Value** -- Menangani data yang hilang agar tidak mengganggu analisis.
5. **Menentukan Variabel** -- Memilih variabel-variabel yang relevan untuk analisis faktor.
6. **Deteksi Outlier (Z-Score)** -- Mengidentifikasi dan menangani data pencilan.
7. **Matriks Korelasi** -- Membuat dan memvisualisasikan matriks korelasi antar variabel.
8. **Uji Kelayakan KMO** -- Menguji kelayakan data untuk analisis faktor menggunakan Kaiser-Meyer-Olkin test dan Bartlett's Test of Sphericity.
9. **Penentuan Jumlah Faktor (Eigenvalue)** -- Menentukan jumlah faktor optimal berdasarkan kriteria Kaiser (eigenvalue > 1).
10. **Visualisasi Scree Plot** -- Memvisualisasikan eigenvalue untuk membantu penentuan jumlah faktor.
11. **Ekstraksi Faktor dan Rotasi Varimax** -- Mengekstrak faktor menggunakan metode MINRES dan merotasi dengan metode Varimax.
12. **Interpretasi Faktor** -- Menginterpretasikan setiap faktor berdasarkan loading yang signifikan (>= 0.4).
13. **Evaluasi Model (RMSE)** -- Mengevaluasi kualitas model menggunakan residual dan RMSE.
14. **Dimension Loadings** -- Menghasilkan tabel loading akhir untuk pelaporan.

## Prasyarat

Pastikan perangkat lunak berikut sudah terinstal di sistem Anda:

- **Python** versi 3.10 atau lebih baru
- **Git**
- **pip** (biasanya sudah termasuk dalam instalasi Python)

## Instalasi

### 1. Clone Repository

```bash
git clone https://github.com/yowxy/Analysys-Factor-based-on-Study-Case.git
```

### 2. Masuk ke Direktori Proyek

```bash
cd Analysys-Factor-based-on-Study-Case
```

### 3. Buat Virtual Environment

```bash
python -m venv .env
```

### 4. Aktifkan Virtual Environment

Windows:
```bash
.env\Scripts\activate
```

macOS / Linux:
```bash
source .env/bin/activate
```

### 5. Instal Dependensi

```bash
pip install pandas numpy scipy scikit-learn matplotlib seaborn openpyxl factor-analyzer ipykernel
```

### 6. Daftarkan Kernel Jupyter

```bash
python -m ipykernel install --user --name=.env --display-name "Python (.env)"
```

### 7. Jalankan Notebook

Buka file `index.ipynb` menggunakan Jupyter Notebook, JupyterLab, atau Visual Studio Code, lalu pastikan kernel yang digunakan adalah **Python (.env)**.

## Catatan Penting

Jika Anda menggunakan `scikit-learn` versi 1.6 atau lebih baru bersamaan dengan `factor-analyzer` versi 0.5.1, akan muncul error berikut saat menjalankan `FactorAnalyzer.fit()`:

```
TypeError: check_array() got an unexpected keyword argument 'force_all_finite'
```

Hal ini terjadi karena `scikit-learn` versi 1.6+ telah me-rename parameter `force_all_finite` menjadi `ensure_all_finite`, sementara `factor-analyzer` belum diperbarui untuk mengikuti perubahan tersebut.

**Solusi:**

Buka file berikut di dalam virtual environment:

```
.env/Lib/site-packages/factor_analyzer/factor_analyzer.py
```

Cari semua kemunculan `force_all_finite` dan ganti dengan `ensure_all_finite`. Lakukan hal yang sama pada file:

```
.env/Lib/site-packages/factor_analyzer/confirmatory_factor_analyzer.py
```

Setelah itu, hapus folder cache Python:

```bash
# Windows
rmdir /s /q .env\Lib\site-packages\factor_analyzer\__pycache__

# macOS / Linux
rm -rf .env/lib/python*/site-packages/factor_analyzer/__pycache__
```

Kemudian restart kernel Jupyter dan jalankan ulang seluruh cell.

## Tech Stack

| Komponen | Keterangan |
|---|---|
| **Python 3.13** | Bahasa pemrograman utama |
| **Jupyter Notebook** | Lingkungan pengembangan interaktif untuk analisis data |
| **pandas** | Manipulasi dan analisis data tabular |
| **NumPy** | Komputasi numerik dan operasi array |
| **SciPy** | Fungsi-fungsi ilmiah dan statistik |
| **scikit-learn** | Preprocessing data (StandardScaler) dan utilitas machine learning |
| **matplotlib** | Visualisasi data dan pembuatan grafik |
| **seaborn** | Visualisasi statistik tingkat lanjut (heatmap korelasi) |
| **factor-analyzer** | Implementasi analisis faktor, uji KMO, dan Bartlett's Test |
| **openpyxl** | Membaca file Excel (.xlsx) sebagai sumber data |

## Struktur Proyek

```
Analysys-Factor-based-on-Study-Case/
├── .env/                 # Virtual environment Python (tidak di-commit)
├── .git/                 # Direktori Git
├── Data_AF.xlsx          # Dataset indikator kemiskinan Jawa Timur
├── FacLoads.csv          # Hasil factor loadings (output)
├── index.ipynb           # Notebook utama berisi seluruh alur analisis
└── README.md             # Dokumentasi proyek
```

## Lisensi

Proyek ini dibuat untuk keperluan akademis pada mata kuliah Praktikum Model Statistik.
