# Estimasi Waktu Pengiriman & Manajemen Risiko Keterlambatan
Disusun oleh:
- Brian Samuel Matthew
- Ferdio Giffary

## Gambaran Umum Proyek
Proyek ini berfokus pada pengembangan model machine learning untuk meningkatkan kualitas estimasi waktu pengiriman pada konteks e-commerce. Fokus utama proyek bukan hanya pada penurunan error prediksi rata-rata, tetapi juga pada pengelolaan risiko keterlambatan ekstrem yang sering menimbulkan dampak operasional dan biaya tambahan.

Pendekatan yang digunakan menekankan pengendalian *tail risk*, sehingga model yang dihasilkan tidak hanya akurat secara statistik, tetapi juga lebih relevan untuk kebutuhan operasional dan pengambilan keputusan.

---

## Latar Belakang Bisnis
Sistem estimasi waktu pengiriman yang umum digunakan biasanya dioptimalkan untuk kesalahan rata-rata. Dalam praktiknya, pendekatan ini sering menghasilkan estimasi yang terlalu optimistis dan kurang sensitif terhadap potensi keterlambatan signifikan.

Kondisi tersebut menyulitkan tim operasional untuk melakukan mitigasi lebih awal terhadap pengiriman dengan risiko keterlambatan tinggi.

---

## Tujuan Proyek
- Meningkatkan akurasi estimasi waktu pengiriman.
- Mengelola risiko keterlambatan tanpa meningkatkan tingkat keterlambatan secara keseluruhan.
- Menyediakan metrik evaluasi yang lebih relevan untuk kebutuhan operasional.

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
Evaluasi model mencakup beberapa aspek berikut:

**Akurasi Estimasi**
- Mean Absolute Error (MAE)
- Median error

**Risiko Keterlambatan (diturunkan dari output model)**
- Late delivery rate
- Mean dan median hari keterlambatan
- P90 keterlambatan
- Proporsi keterlambatan lebih dari 7 dan 14 hari

Pendekatan ini memberikan gambaran performa model yang lebih menyeluruh dari sisi teknis maupun operasional.

---

## Hasil Utama
Dibandingkan dengan sistem estimasi baseline (existing), model quantile regression menunjukkan:
- Penurunan MAE sekitar 4%.
- Late delivery rate tetap berada pada kisaran baseline (~6%).
- Penurunan tingkat keparahan keterlambatan, khususnya pada median dan P90 hari keterlambatan.

Hasil ini menunjukkan bahwa peningkatan akurasi estimasi dapat dicapai tanpa peningkatan risiko keterlambatan pada metrik yang dievaluasi.

---

## Ilustrasi Dampak Bisnis
Sebagai gambaran, dilakukan simulasi biaya berbasis asumsi historis dan referensi literatur industri. Simulasi ini bersifat indikatif dan bertujuan untuk memberikan perspektif potensi manfaat ekonomi dari pendekatan mitigasi berbasis risiko, bukan sebagai pembuktian kausal langsung.

---

## Aplikasi Prediksi (Streamlit)
Model yang dikembangkan juga diimplementasikan dalam bentuk aplikasi web interaktif menggunakan **Streamlit**, sehingga hasil prediksi dapat diakses dengan lebih mudah oleh pengguna non-teknis.

Tautan aplikasi:
https://olistdelivery-eta-model-dashboard-papstr7gpebbjdbejqgjce.streamlit.app/

Fitur utama aplikasi:
- Antarmuka input sederhana untuk memasukkan informasi pengiriman.
- Prediksi estimasi waktu pengiriman secara real-time.
- Tampilan hasil prediksi yang mudah dipahami untuk kebutuhan operasional.

---

## Dashboard Business Intelligence
Selain aplikasi prediksi, proyek ini dilengkapi dengan dashboard interaktif berbasis Tableau untuk memantau pola keterlambatan pengiriman dan tingkat risikonya.

Tautan dashboard:
https://public.tableau.com/views/OlistMonitoringDashboard/Monitoring?:language=en-US&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link

Dashboard ini mendukung:
- Monitoring tingkat keterlambatan dan tingkat keparahannya.
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
├── app.py           # Aplikasi Streamlit
├── README.md        # Dokumentasi proyek
└── requirements.txt # Dependensi Python
```

---

## Tools & Teknologi
- Bahasa Pemrograman: Python  
- Library: Pandas, NumPy, Scikit-Learn, XGBoost, Matplotlib  
- Visualisasi: Tableau  
- Deployment: Streamlit  
- Environment: Jupyter Notebook
