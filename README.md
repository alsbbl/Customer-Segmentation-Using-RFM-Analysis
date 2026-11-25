# Customer Segmentation Using RFM Analysis

## Deskripsi Proyek

Proyek ini bertujuan melakukan segmentasi pelanggan (*Customer Segmentation*) menggunakan pendekatan Recency, Frequency, Monetary (RFM) pada dataset Online Retail.

Analisis menerapkan dua algoritma unsupervised machine learning, yaitu K-Means Clustering dan Hierarchical Clustering, untuk mengidentifikasi kelompok pelanggan berdasarkan perilaku transaksi.

Proyek ini mencakup tahapan data preprocessing, exploratory data analysis (EDA), feature engineering, outlier treatment, data scaling, pemodelan clustering, evaluasi model, hingga interpretasi hasil segmentasi dan penyusunan rekomendasi strategi bisnis.

## Tujuan Proyek

1. Mengidentifikasi karakteristik pelanggan berdasarkan riwayat transaksi.
2. Membangun fitur Recency, Frequency, dan Monetary (RFM).
3. Mengelompokkan pelanggan menggunakan algoritma K-Means dan Hierarchical Clustering.
4. Membandingkan performa kedua algoritma menggunakan metrik evaluasi clustering.
5. Mengidentifikasi karakteristik setiap kelompok pelanggan.
6. Menghasilkan rekomendasi strategi pemasaran berdasarkan hasil segmentasi.

## Dataset

Dataset yang digunakan adalah Online Retail Dataset yang berisi data transaksi penjualan retail.

**Informasi dataset:**
- Total data awal: 541.909 baris.
- Jumlah variabel: 8 kolom.
- Periode transaksi: 1 Desember 2010 hingga 9 Desember 2011.
- Negara: 38 negara pada data awal.

**Variabel utama:**

| Variabel | Deskripsi |
|---|---|
| InvoiceNo | Nomor transaksi |
| StockCode | Kode produk |
| Description | Deskripsi produk |
| Quantity | Jumlah produk yang dibeli |
| InvoiceDate | Tanggal transaksi |
| UnitPrice | Harga satuan produk |
| CustomerID | Identitas pelanggan |
| Country | Negara pelanggan |

## Metodologi

### 1. Data Understanding
Melakukan pemeriksaan struktur dataset, tipe data, statistik deskriptif, missing values, duplikasi, dan kualitas data transaksi.

### 2. Data Cleaning
Melakukan pembersihan data melalui:
- Menghapus data dengan CustomerID kosong.
- Menghapus baris duplikat.
- Menghapus transaksi pembatalan (InvoiceNo berawalan C).
- Menghapus transaksi dengan Quantity tidak valid.
- Menghapus transaksi dengan UnitPrice tidak valid.

Hasil preprocessing menghasilkan 392.692 baris transaksi dan 4.338 pelanggan unik.

### 3. Exploratory Data Analysis (EDA)
Melakukan eksplorasi terhadap:
- Distribusi Quantity dan UnitPrice.
- Jumlah transaksi berdasarkan negara.
- Produk dengan jumlah penjualan tertinggi.
- Tren pendapatan bulanan.
- Distribusi jumlah transaksi per pelanggan.

### 4. Feature Engineering: RFM Analysis

Membangun tiga variabel utama:

- Recency: jumlah hari sejak transaksi terakhir pelanggan.
- Frequency: jumlah transaksi unik pelanggan.
- Monetary: total nilai pembelian pelanggan.

Ketiga variabel digunakan sebagai dasar pembentukan segmentasi pelanggan.

### 5. Outlier Treatment

Menggunakan:
- Log Transformation untuk mengurangi skewness distribusi.
- Winsorization pada persentil 1% hingga 99% untuk membatasi pengaruh nilai ekstrem tanpa menghapus observasi.

### 6. Data Scaling

Menerapkan StandardScaler untuk menstandarkan fitur RFM agar setiap variabel memiliki skala yang sebanding sebelum proses clustering.

### 7. Penentuan Jumlah Cluster

Menggunakan beberapa pendekatan:
- Elbow Method.
- Silhouette Score.
- Dendrogram dengan Ward Linkage.

Analisis awal menunjukkan Silhouette Score tertinggi pada K=2. Namun, eksperimen perbandingan model selanjutnya menggunakan K=4.

### 8. Machine Learning Modeling

Mengimplementasikan dua algoritma:

**K-Means Clustering**
- Menggunakan 4 cluster.
- Random State: 42.
- N_init: 10.
- Maximum Iterations: 500.

**Hierarchical Clustering**
- Menggunakan Agglomerative Clustering.
- Jumlah cluster: 4.
- Linkage: Ward.

### 9. Model Evaluation

Membandingkan performa kedua model menggunakan:

- Silhouette Score.
- Davies-Bouldin Index.
- Calinski-Harabasz Index.

### 10. Cluster Visualization & Profiling

Menggunakan:
- Principal Component Analysis (PCA).
- t-SNE.
- Heatmap.
- Radar Chart.
- Bar Chart.

Selanjutnya, melakukan profiling berdasarkan nilai Recency, Frequency, dan Monetary untuk memahami karakteristik setiap cluster.

### 11. Business Insight & Recommendation

Menyusun segmentasi pelanggan dan rekomendasi strategi bisnis berdasarkan karakteristik masing-masing kelompok, seperti loyalty program, cross-selling, upselling, dan customer reactivation.

## Hasil Analisis

### 1. Hasil Data Preprocessing

| Keterangan | Hasil |
|---|---:|
| Data awal | 541.909 |
| Data setelah cleaning | 392.692 |
| Data yang dipertahankan | 72,5% |
| Pelanggan unik | 4.338 |
| Transaksi unik | 18.532 |

### 2. Hasil Evaluasi Model

Perbandingan performa K-Means dan Hierarchical Clustering:

| Metrik | K-Means | Hierarchical |
|---|---:|---:|
| Silhouette Score | 0.3394 | 0.2462 |
| Davies-Bouldin Index | 1.0099 | 1.2537 |
| Calinski-Harabasz Index | 3538.4538 | 2835.6516 |

Berdasarkan ketiga metrik evaluasi, K-Means menghasilkan performa clustering yang lebih baik dibandingkan Hierarchical Clustering pada konfigurasi K=4.

### 3. Customer Segmentation

Hasil K-Means menghasilkan empat kelompok pelanggan:

| Cluster | Jumlah Pelanggan | Persentase |
|---|---:|---:|
| Cluster 0 | 836 | 19,3% |
| Cluster 1 | 1.597 | 36,8% |
| Cluster 2 | 735 | 16,9% |
| Cluster 3 | 1.170 | 27,0% |

**Profil pelanggan:**

- Champions: pelanggan dengan frekuensi transaksi dan nilai pembelian tinggi.
- Potential Loyalists: pelanggan yang berpotensi menjadi pelanggan loyal.
- Inactive / At Risk: pelanggan yang sudah cukup lama tidak melakukan transaksi.

### 4. Business Insight

Beberapa temuan utama:

- Cluster Champions terdiri dari 735 pelanggan atau 16,9% dari keseluruhan pelanggan.
- Kelompok Champions menghasilkan kontribusi pendapatan sebesar £5,81 juta atau 65,4% dari total pendapatan.
- Kelompok Potential Loyalists dapat dikembangkan melalui program loyalitas dan strategi cross-selling.
- Kelompok pelanggan yang berisiko tidak aktif dapat menjadi sasaran kampanye reaktivasi pelanggan.

## Tools & Technologies

**Programming Language**
- Python

**Data Processing**
- Pandas
- NumPy

**Machine Learning**
- Scikit-learn
- K-Means Clustering
- Agglomerative Clustering

**Statistical & Data Analysis**
- RFM Analysis
- Log Transformation
- Winsorization
- StandardScaler

**Model Evaluation**
- Silhouette Score
- Davies-Bouldin Index
- Calinski-Harabasz Index

**Data Visualization**
- Matplotlib
- Seaborn
- PCA
- t-SNE

**Environment**
- Google Colab
- Jupyter Notebook

## Repository Structure

```text
Customer-Segmentation-RFM/
│
├── Project Machine Learning.ipynb
├── Online Retail.xlsx
├── README.md
│
└── outputs/
    ├── eda_distributions.png
    ├── eda_country.png
    ├── eda_top_products.png
    ├── eda_monthly_trend.png
    ├── rfm_distributions.png
    ├── model_evaluation.png
    ├── tsne_clusters.png
    ├── cluster_profiling.png
    └── segment_distribution.png
```

## Kesimpulan

Proyek ini menunjukkan penerapan Unsupervised Machine Learning untuk melakukan segmentasi pelanggan berdasarkan perilaku transaksi menggunakan pendekatan RFM.

Berdasarkan hasil evaluasi, K-Means memberikan performa lebih baik dibandingkan Hierarchical Clustering pada konfigurasi empat cluster.

Hasil segmentasi dapat digunakan untuk memahami karakteristik pelanggan, mengidentifikasi pelanggan bernilai tinggi, serta mendukung penyusunan strategi pemasaran yang lebih terarah.

---

**Author:** Safira Khoirulanisa Salsabila

**Project Category:** Machine Learning | Customer Analytics | Data Science | Customer Segmentation
