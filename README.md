# Laporan Praktikum Analisis Data E-Commerce

**Kelompok:**
**Elang Dipa Purwadhiyaksa (14)**
**Sayoga Sindhunata Narutama (30)**

## 1. Business Question

Dalam praktikum ini dilakukan analisis data penjualan e-commerce untuk menjawab beberapa pertanyaan bisnis berikut:

* Bagaimana tren penjualan pada setiap bulan?
* Apakah budget iklan (*Ad_Budget*) memiliki hubungan dengan total penjualan (*Total_Sales*)?
* Produk mana yang termasuk kategori *underperformer*?
* Siapa pelanggan terbaik berdasarkan metode *RFM Analysis*?
* Seberapa besar hubungan antara iklan dan penjualan berdasarkan analisis regresi linear?

---

## 2. Data Wrangling

Tahap data wrangling dilakukan untuk memastikan data siap digunakan dalam proses analisis.

### a. Membaca Dataset

Dataset dibaca menggunakan library **Pandas**.

```python
df = pd.read_csv('data_praktikum_analisis_data.csv')
```

### b. Mengecek Struktur Data

Pengecekan dilakukan untuk melihat isi data, jumlah kolom, serta tipe data yang digunakan.

```python
print(df.head())
df.info()
```

### c. Mengecek Missing Value

Pemeriksaan dilakukan untuk memastikan tidak terdapat data kosong yang dapat memengaruhi hasil analisis.

```python
df.isnull().sum()
```

### d. Membersihkan Data Tidak Valid

Data dengan nilai **Price_Per_Unit** kurang dari atau sama dengan nol dihapus karena dianggap tidak valid dalam transaksi penjualan.

```python
df = df[df['Price_Per_Unit'] > 0]
```

### e. Konversi Format Tanggal

Kolom **Order_Date** diubah menjadi format *datetime* agar dapat digunakan dalam analisis berbasis waktu.

```python
df['Order_Date'] = pd.to_datetime(df['Order_Date'])
```

### f. Membuat Kolom Bulan

Kolom bulan dibuat untuk mempermudah analisis tren penjualan bulanan.

```python
df['Month'] = df['Order_Date'].dt.to_period('M').astype(str)
```

---

## 3. Insights

### A. Tren Penjualan Bulanan

Visualisasi *line chart* digunakan untuk melihat perubahan total penjualan setiap bulan.

**Insight:**

* Penjualan mengalami fluktuasi dari bulan ke bulan.
* Terdapat beberapa periode yang menunjukkan peningkatan penjualan cukup signifikan dibandingkan periode lainnya.
* Informasi ini dapat dimanfaatkan perusahaan untuk mengidentifikasi periode dengan potensi penjualan tertinggi.

### B. Heatmap Korelasi

Analisis korelasi dilakukan pada variabel:

* **Total_Sales**
* **Ad_Budget**

**Insight:**

* Heatmap menunjukkan adanya hubungan positif antara budget iklan dan total penjualan.
* Semakin besar budget iklan yang dikeluarkan, penjualan cenderung mengalami peningkatan.
* Hasil korelasi dapat membantu perusahaan dalam mengevaluasi efektivitas strategi pemasaran yang diterapkan.

### C. Identifikasi Produk Underperformer

Analisis dilakukan menggunakan *scatter plot* dengan mempertimbangkan:

* **Price_Per_Unit** (harga produk)
* **Quantity** (jumlah pembelian)

**Insight:**

* Produk dengan harga relatif tinggi namun jumlah pembelian rendah dapat dikategorikan sebagai produk *underperformer*.
* Produk tersebut berpotensi memberikan kontribusi yang kurang optimal terhadap penjualan.
* Perusahaan dapat melakukan evaluasi harga maupun strategi promosi untuk meningkatkan performa produk.

### D. Uji Hipotesis Sederhana

Data dibagi menjadi dua kelompok berdasarkan nilai median **Ad_Budget**, yaitu:

* Kelompok Iklan Tinggi
* Kelompok Iklan Rendah

**Insight:**

* Kelompok dengan budget iklan lebih tinggi memiliki rata-rata penjualan yang lebih besar dibandingkan kelompok dengan budget iklan rendah.
* Hasil ini menunjukkan adanya indikasi hubungan positif antara pengeluaran iklan dan peningkatan penjualan.

### E. RFM Analysis

Metode RFM digunakan untuk mengelompokkan pelanggan berdasarkan:

* **Recency** → Seberapa baru transaksi terakhir dilakukan.
* **Frequency** → Seberapa sering pelanggan melakukan pembelian.
* **Monetary** → Total pengeluaran pelanggan.

**Insight:**

* Pelanggan dengan skor RFM tinggi merupakan pelanggan yang paling loyal dan bernilai bagi perusahaan.
* Segmentasi pelanggan membantu perusahaan dalam menentukan strategi promosi yang lebih tepat sasaran.
* Hasil analisis juga dapat dimanfaatkan untuk meningkatkan retensi pelanggan.

### F. Regresi Linear Sederhana

Regresi linear digunakan untuk menganalisis hubungan antara **Ad_Budget** dan **Total_Sales**.

**Insight:**

* Nilai koefisien regresi menunjukkan adanya hubungan positif antara budget iklan dan total penjualan.
* Nilai **R² Score** menunjukkan seberapa baik model menjelaskan variasi data penjualan berdasarkan budget iklan.
* Model regresi dapat digunakan sebagai dasar analisis prediktif sederhana dalam mendukung pengambilan keputusan bisnis.

---

## 4. Recommendation

Berdasarkan hasil analisis yang telah dilakukan, beberapa rekomendasi yang dapat diberikan adalah:

1. Meningkatkan budget iklan pada periode yang memiliki potensi penjualan tinggi.
2. Melakukan evaluasi terhadap produk *underperformer*, baik dari sisi harga maupun strategi promosi.
3. Memberikan program loyalitas atau promo khusus kepada pelanggan dengan skor RFM tinggi.
4. Memanfaatkan hasil analisis regresi sebagai dasar dalam pengambilan keputusan pemasaran.
5. Melakukan analisis data secara rutin untuk memantau performa bisnis dan perilaku pelanggan.

---

## 5. Kesimpulan

Berdasarkan hasil praktikum yang telah dilakukan, analisis data memberikan wawasan yang bermanfaat dalam memahami pola penjualan, efektivitas iklan, performa produk, serta perilaku pelanggan. Analisis menunjukkan adanya hubungan positif antara budget iklan dan total penjualan, sehingga strategi pemasaran dapat disusun secara lebih terarah.

Selain itu, identifikasi produk *underperformer* membantu perusahaan dalam melakukan evaluasi produk yang kurang optimal, sedangkan *RFM Analysis* membantu dalam mengenali pelanggan yang memiliki nilai tinggi bagi bisnis. Dengan memanfaatkan visualisasi data dan metode analisis sederhana, perusahaan dapat mengambil keputusan yang lebih tepat, efektif, dan berbasis data untuk mendukung pertumbuhan bisnis di masa mendatang.
