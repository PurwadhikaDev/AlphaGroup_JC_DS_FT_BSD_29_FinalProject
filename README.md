# Estimasi Waktu Pengiriman & Manajemen Risiko Keterlambatan
Disusun oleh:
- Brian Samuel Matthew
- Ferdio Giffary

## Gambaran Umum Proyek
Proyek ini berfokus pada pengembangan model machine learning untuk meningkatkan kualitas estimasi waktu pengiriman pada konteks e-commerce. Permasalahan utama yang ingin diatasi bukan hanya besarnya error prediksi secara rata-rata, tetapi juga risiko keterlambatan ekstrem yang sering menimbulkan dampak operasional dan biaya tambahan.

Pendekatan yang digunakan menekankan pada pengelolaan *tail risk*, sehingga model tidak sekadar akurat secara statistik, tetapi juga lebih relevan untuk kebutuhan operasional sehari-hari.

---

## Latar Belakang Bisnis
Sistem estimasi waktu pengiriman yang umum digunakan biasanya dioptimalkan untuk kesalahan rata-rata. Dalam praktiknya, pendekatan ini dapat menghasilkan estimasi yang terlalu optimistis dan kurang sensitif terhadap potensi keterlambatan signifikan.

Akibatnya, tim operasional kesulitan melakukan mitigasi secara proaktif terhadap pengiriman berisiko tinggi.

---

## Tujuan Proyek
- Meningkatkan akurasi estimasi waktu pengiriman.
- Mengelola risiko keterlambatan tanpa meningkatkan tingkat keterlambatan secara keseluruhan.
- Menyediakan metrik evaluasi yang relevan untuk pengambilan keputusan operasional.

---

## Pendekatan Analisis
Analisis dilakukan melalui alur kerja data science end-to-end, meliputi:

### Persiapan Data
- Pembersihan data dan validasi nilai.
- Pemilihan fitur dengan mempertimbangkan ketersediaan informasi pada waktu estimasi untuk menghindari data leakage.

### Pra-pemrosesan
- Pembagian data train–test dengan rasio 80:20.
- Encoding fitur kategorikal menggunakan frequency encoding.
- Transformasi fitur diterapkan secara konsisten melalui pipeline.

### Pemodelan
- Pendekatan regresi (bukan klasifikasi).
- Menggunakan XGBoost Quantile Regression (P94) untuk memodelkan risiko keterlambatan pada ekor distribusi.
- Penerapan asymmetric loss untuk memprioritaskan risiko underprediction.

---

## Metrik Evaluasi
Evaluasi model tidak hanya berfokus pada satu metrik, tetapi mencakup:

**Akurasi Estimasi**
- Mean Absolute Error (MAE)
- Median error

**Risiko Keterlambatan (diturunkan dari output model)**
- Late delivery rate
- Mean dan median hari keterlambatan
- P90 keterlambatan
- Proporsi keterlambatan lebih dari 7 dan 14 hari

Pendekatan ini memberikan gambaran yang lebih menyeluruh terkait performa model dari sisi teknis maupun operasional.

---

## Hasil Utama
Dibandingkan dengan sistem estimasi baseline (existing), model quantile regression menunjukkan:
- Penurunan MAE sekitar 4%.
- Late delivery rate tetap berada pada kisaran baseline (~6%).
- Penurunan tingkat keparahan keterlambatan, terutama pada median dan P90 hari keterlambatan.

Hasil ini mengindikasikan bahwa peningkatan akurasi dapat dicapai tanpa meningkatkan risiko keterlambatan pada metrik yang dievaluasi.

---

## Ilustrasi Dampak Bisnis
Sebagai gambaran, dilakukan simulasi biaya berbasis asumsi historis dan referensi literatur industri. Simulasi ini bersifat indikatif dan bertujuan untuk menunjukkan potensi manfaat ekonomi dari pendekatan mitigasi berbasis risiko, bukan sebagai pembuktian kausal langsung.

---

## Dashboard Business Intelligence
Proyek ini dilengkapi dengan dashboard interaktif berbasis Tableau untuk memantau pola keterlambatan pengiriman dan tingkat risikonya.

Tautan dashboard:
https://public.tableau.com/app/profile/ferdio.giffary/viz/Book5-test_17689053833700/Dashboard1

Dashboard ini mendukung:
- Monitoring tingkat keterlambatan dan severitasnya.
- Analisis distribusi risiko pengiriman.
- Identifikasi segmen pengiriman dengan risiko tertinggi.

---

## Keterbatasan
- Tidak dilakukan cross-validation atau pengujian robustness.
- Simulasi biaya menggunakan asumsi, bukan data aktual perusahaan.
- Evaluasi trade-off terbatas pada metrik yang dianalisis di notebook.

---

## Struktur Repositori
```
├── data/            # Dataset
├── notebooks/       # Notebook analisis (main.ipynb)
├── model/           # Artefak model
├── README.md        # Dokumentasi proyek
└── requirements.txt # Dependensi Python
```

---

## Tools & Teknologi
- Bahasa Pemrograman: Python  
- Library: Pandas, NumPy, Scikit-Learn, XGBoost, Matplotlib  
- Visualisasi: Tableau  
- Environment: Jupyter Notebook
