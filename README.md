# 🛒 Supermarket Customer Segmentation & Purchase Behavior Analysis

## 📌 Latar Belakang

Dalam industri ritel, pemahaman terhadap **perilaku pelanggan** sangat penting untuk meningkatkan **profit** dan efektivitas **strategi pemasaran**. Supermarket memiliki berbagai jenis pelanggan dengan karakteristik yang berbeda, seperti:

* **Karakteristik Demografis**: tingkat pendidikan, status pernikahan, jumlah anak/remaja dalam rumah tangga, serta tingkat pendapatan.
* **Kebiasaan Belanja**: total pengeluaran pelanggan terhadap berbagai kategori produk (wine, daging, ikan, buah, dll.).
* **Respons terhadap Promosi**: partisipasi pelanggan dalam berbagai kampanye pemasaran.
* **Metode Pembelian**: jumlah pembelian yang dilakukan melalui website, katalog, dan toko fisik.

Melalui analisis data ini, perusahaan dapat memahami pola belanja pelanggan serta menyesuaikan strategi pemasaran agar lebih tepat sasaran dan efisien.

---

## ❓ Pernyataan Masalah

Perusahaan ingin memahami **perilaku pembelian pelanggan** berdasarkan:

* Jenis produk
* Tempat pembelian
* Efektivitas promosi

Tujuan akhirnya adalah untuk **memaksimalkan profit** dan **meningkatkan efektivitas strategi pemasaran** melalui pemahaman hubungan antara **karakteristik demografis pelanggan** (status pernikahan, jumlah anak/remaja, pendapatan) dan **pola belanja mereka**.

---

## 🎯 Tujuan Analisis

Sebagai seorang **Data Analyst**, proyek ini bertujuan untuk menjawab pertanyaan-pertanyaan berikut:

### Bagaimana pola pembelian produk berdasarkan karakteristik pelanggan?

* Apakah pelanggan dengan status pernikahan tertentu cenderung membeli jenis produk tertentu?
* Bagaimana kategori pendapatan memengaruhi pembelian terhadap berbagai jenis produk?
* Apakah jumlah anak dan remaja dalam keluarga berkorelasi dengan pilihan produk?
* Produk apa saja yang paling banyak dibeli oleh pelanggan berdasarkan segmentasi **LRFM**?

### Bagaimana karakteristik tempat pembelian memengaruhi keputusan pelanggan?

* Apakah pelanggan lebih banyak melakukan pembelian secara online, katalog, atau toko fisik?
* Bagaimana status pernikahan dan pendapatan memengaruhi preferensi tempat pembelian?

### Seberapa efektif strategi promosi yang telah dijalankan?

* Apakah pelanggan yang sering menerima kampanye mempengaruhi total pembeliannya?
* Promosi mana yang paling efektif dalam mengurangi risiko **churn**, terutama pada segmen pelanggan dengan nilai **monetary** atau **frequency** yang rendah?

---

## 🧠 Data Understanding

Dataset terdiri dari **2.240 baris** dengan 29 fitur yang menggambarkan karakteristik pelanggan, riwayat pembelian, respons terhadap kampanye, dan atribut demografis.

### Ringkasan Fitur Utama:

* **Demografis**

  * `Year_Birth`, `Education`, `Marital_Status`, `Income`, `Kidhome`, `Teenhome`

* **Waktu & Aktivitas**

  * `Dt_Customer` (tanggal pendaftaran), `Recency` (hari sejak pembelian terakhir)

* **Pengeluaran Produk**

  * `MntWines`, `MntFruits`, `MntMeatProducts`, `MntFishProducts`, `MntSweetProducts`, `MntGoldProds`

* **Saluran Pembelian**

  * `NumDealsPurchases`, `NumWebPurchases`, `NumCatalogPurchases`, `NumStorePurchases`, `NumWebVisitsMonth`

* **Respons Kampanye**

  * `AcceptedCmp1`–`AcceptedCmp5`, `Response` (kampanye terakhir)

* **Lainnya**

  * `Complain` (keluhan), `Z_CostContact`, `Z_Revenue` (nilai tetap)

---


## Data Cleaning

* **Duplicate Check**: Tidak ditemukan data duplikat.
* **Missing Values**: Terdapat 24 nilai hilang (1.07%) pada kolom `Income`, diisi dengan **median per grup `NumCatalogPurchases`** karena distribusi tidak normal dan korelasi tinggi.
* **Marital\_Status**: Nilai `Alone` disetarakan dengan `Single`; nilai tidak valid (`YOLO`, `Absurd`) dihapus.
* **Outlier Removal**:

  * `Income` ekstrem (666,666) dihapus.
  * `Year_Birth` < 1940 (usia tidak wajar) dihapus.
* **Feature Engineering**:

  * Tambah kolom `TotalSpending` sebagai total pengeluaran produk.
  * Tetapkan kolom `place_columns`: `NumWebPurchases`, `NumCatalogPurchases`, `NumStorePurchases`.

---

## 📊 LRFM Analysis

Analisis **LRFM (Length, Recency, Frequency, Monetary)** digunakan untuk segmentasi pelanggan berdasarkan perilaku pembelian.

* **Length**: Lama hubungan pelanggan dengan perusahaan.
* **Recency**: Seberapa baru pelanggan terakhir bertransaksi.
* **Frequency**: Total frekuensi pembelian (web, katalog, toko).
* **Monetary**: Total pengeluaran pelanggan.

<img width="716" height="435" alt="image" src="https://github.com/user-attachments/assets/5860667e-af63-41b1-9d68-88f93bdc4ef8" />


Setiap metrik diskalakan (skor 1–4), lalu digabung menjadi **LRFM Score**. Skor ini dipetakan ke dalam segmen seperti:

* **Loyal Customer**
* **At Risk**
* **Potential Loyal**
* **Prospect**, dll.

## 📦 Analisis Pembelian Produk

### Total Pembelian per Produk
- **Wine** menjadi produk paling banyak dibeli (`$678,674`), disusul **Meat** (`$374,650`).
- Produk **Fruits**, **Fish**, dan **Sweets** memiliki total penjualan lebih rendah.

### Korelasi Antar Produk
- Terdapat korelasi positif sedang (0.5–0.6) antar produk **Fruits**, **Fish**, **Sweets**, dan **Meat**.
- Korelasi ini membuka peluang untuk membuat **bundle produk**.

### Pembelian Berdasarkan Status Pernikahan
- Pelanggan **Widow** memiliki rata-rata pengeluaran tertinggi, terutama pada kategori *Wine*.
- Pelanggan **Single** memiliki rata-rata pengeluaran paling rendah.

### Pembelian Berdasarkan Pendapatan
- Semakin tinggi pendapatan, semakin tinggi pengeluaran untuk semua jenis produk.
- Produk **Wine** dan **Meat** mengalami peningkatan signifikan di kelompok *High Income*.


### Berdasarkan Jumlah Anak & Remaja
- Pelanggan tanpa anak memiliki pengeluaran tertinggi, terutama untuk **Wine**, **Meat**, dan **Gold**.
- Semakin banyak anak, semakin rendah total pengeluaran.
- Kehadiran remaja mendorong pembelian produk **Wine** (hiburan keluarga).


### LRFM x Pembelian Produk
- Segmen **High Potential Prospect** memiliki total pengeluaran tertinggi → menjadi target utama untuk retensi pelanggan.
- Segmen **Inactive** dan **Potential Loyal** menunjukkan peluang aktivasi ulang.

## 🏬 Analisis Tempat Pembelian

### 1. Total Pembelian Berdasarkan Metode
- **Toko fisik** merupakan metode pembelian terbanyak.
- **Website** menempati urutan kedua, menandakan mulai bergesernya perilaku ke arah digital.
- **Katalog** paling jarang digunakan.

### 2. Tempat Pembelian vs Status Pernikahan
- **Widow** paling aktif berbelanja di toko fisik (median = 6).
- **Single** memiliki pembelian terendah di semua metode.
- Katalog adalah metode paling tidak disukai oleh semua status.

### 3. Tempat Pembelian vs Pendapatan
- Toko fisik mendominasi semua kategori pendapatan.
- Segmen **High Income** menggunakan semua metode secara merata.
- Segmen **Very Low** tidak menggunakan katalog sama sekali.

---

# 📊 Customer Campaign Analysis

## Insight Utama

* **Kampanye Terakhir (Response)** paling berhasil, disusul Cmp4 dan Cmp5.
* Pelanggan yang menerima lebih banyak kampanye cenderung memiliki pengeluaran lebih tinggi (korelasi positif 0.46).
* **Segmentasi "High Potential Prospect"** paling banyak merespon kampanye, terutama Cmp1, Cmp4, dan Cmp5.
* Kampanye Cmp3 cukup merata dalam menjangkau seluruh segmen.

---

## Kesimpulan & Rekomendasi

### Kesimpulan

* **Produk Wine dan Meat** memiliki total pembelian tertinggi, terutama dari segmen **berpendapatan tinggi**, **berstatus Widow**, dan **tanpa anak**.
* **Status pernikahan, jumlah anak, dan pendapatan** memengaruhi jenis produk yang dibeli. Pelanggan tanpa anak lebih konsumtif terhadap produk non-esensial.
* **Segmen High Potential Prospect & Loyal Customer** adalah kontributor utama pembelian. Segmen Inactive & Potential Loyal memerlukan pendekatan khusus.
* **Toko fisik** masih menjadi saluran pembelian utama. Website mulai meningkat di segmen atas. Katalog minim digunakan.
* **Kampanye terakhir (Response)** paling sukses. Ada korelasi positif antara jumlah kampanye yang diterima dan total pembelian pelanggan.

### Rekomendasi

* Fokus promosi **Wine & Meat** ke segmen Widow, tanpa anak, dan berpenghasilan tinggi. Tawarkan bundling premium dan loyalty program.
* **Tingkatkan daya tarik produk esensial** (Fish, Fruits, Sweets) lewat bundling hemat dengan produk populer seperti Meat.
* Buat **promo eksklusif** untuk pendapatan tinggi dan **bundling hemat/ekonomis** untuk pendapatan rendah.
* Gunakan strategi **kampanye terakhir dan kampanye ke-3** sebagai referensi untuk promosi selanjutnya.
* Tingkatkan pengalaman belanja di toko fisik & optimalkan UI/UX website.
* Aktifkan kembali segmen Inactive dan Prospect melalui diskon, reminder, dan kampanye personal.

## 📊 Tableau Dashboard

🔗 **Tableau Dashboard**: [View Here](https://public.tableau.com/app/profile/annalia.alfia.rahma/viz/caps2_17442079552650/dbHome)

<img width="1366" height="764" alt="{0C349767-94D1-4A4D-9CF6-B6450E1B6362}" src="https://github.com/user-attachments/assets/acb2dc75-f251-4bb0-89e0-5323b1521c5c" />
<img width="1370" height="769" alt="{D9CBDB94-8A66-4707-A562-B425633DE9CE}" src="https://github.com/user-attachments/assets/85ed07b4-cd56-4e8d-a430-3dc148d53296" />
<img width="1363" height="767" alt="{6C0B9F10-CAB7-4436-BB85-0FAFC77E45C8}" src="https://github.com/user-attachments/assets/de76f1b5-6826-4c8b-b445-251be2c67f74" />
<img width="1365" height="767" alt="{A1DF79E6-E395-4680-8833-9C2603F65C9E}" src="https://github.com/user-attachments/assets/294f2fba-cf86-4374-a6d7-018ddc9a37d8" />



