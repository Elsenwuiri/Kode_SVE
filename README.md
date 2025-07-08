# 📝 Prediksi Harga Jual Produk Berdasarkan Atribut Produk dan Historis Penjualan Menggunakan Model Machine Learning per Kategori

## Abstrak

Pertumbuhan pesat platform e-commerce telah mengubah lanskap ritel secara fundamental. Bagi penjual, khususnya reseller, lingkungan ini menawarkan jangkauan pasar yang luas namun dengan persaingan yang sangat ketat. Dalam konteks ini, penetapan harga menjadi alat strategis utama. Sayangnya, banyak penjual masih mengandalkan intuisi atau metode sederhana, tanpa memanfaatkan data historis yang mereka miliki.

Penelitian ini bertujuan membangun model machine learning untuk memprediksi harga jual optimal berdasarkan atribut produk dan histori penjualan. Model dilatih secara terpisah untuk setiap kategori produk, dengan hasil yang menunjukkan akurasi sangat tinggi (R² > 0.98). Temuan ini membuka peluang penerapan sistem prediktif harga yang lebih adaptif dan menguntungkan di dunia e-commerce.

---

## 1. Pendahuluan

Harga jual merupakan komponen krusial dalam strategi penjualan. Penetapan harga yang tidak tepat dapat menyebabkan hilangnya daya saing atau berkurangnya margin keuntungan. Terlebih di era digital, di mana pelanggan memiliki banyak pilihan dan dapat membandingkan harga dengan sangat mudah.

Sebagian besar penjual masih menggunakan pendekatan manual dalam menetapkan harga, padahal data historis transaksi menyimpan pola-pola yang berharga. Dengan pendekatan machine learning, kita dapat menggali pola tersebut untuk merekomendasikan harga secara lebih presisi dan adaptif.

---

## 2. Kajian Teori

### Machine Learning untuk Prediksi Harga
Machine learning memungkinkan pemodelan hubungan kompleks antara berbagai fitur (atribut produk, diskon, waktu transaksi, dll.) dengan target variabel (harga jual). Beberapa algoritma populer untuk regresi dalam konteks ini meliputi:
- Random Forest Regressor
- Gradient Boosting Regressor
- Ridge Regression
- XGBoost

### Evaluasi Model Regresi
Kinerja model regresi biasanya dievaluasi menggunakan:
- **R² (R-squared)**: Proporsi variasi yang dijelaskan oleh model.
- **MAE (Mean Absolute Error)**: Rata-rata selisih absolut antara prediksi dan nilai aktual.
- **RMSE (Root Mean Squared Error)**: Akar dari rata-rata kuadrat kesalahan prediksi.

---

## 3. Solusi

### 3.1 Data

Dataset dapat diakses melalui GitHub:  
🔗 [FinalProjectDA11 Repository](https://github.com/dataskillsboost/FinalProjectDA11)

Dataset terdiri dari 5884 baris data transaksi dengan 19 kolom, di antaranya:
- `base_price`, `discount_amount`, `after_discount`, `qty_ordered`, `category`, `cogs`, dll.
- Kategori produk meliputi:  
  `Appliances`, `Beauty & Grooming`, `Computing`, `Entertainment`, `Mobiles & Tablets`, dll.

### 3.2 Pra-pemrosesan

Beberapa tahapan preprocessing yang dilakukan:
- **Data cleaning**: Memastikan tidak ada data duplikat atau tidak valid.
- **Log-transform**: Untuk menstabilkan varians pada variabel harga.
- **Encoding**: Konversi data kategorikal menjadi numerik.
- **Scaling**: Normalisasi fitur numerik agar skala seragam.

### 3.3 Pendekatan Per Kategori

Setiap kategori produk dibangun model tersendiri agar mampu menangkap karakteristik unik dari masing-masing segmen. Model terbaik per kategori ditentukan berdasarkan evaluasi R², MAE, dan RMSE.

---

## 4. Eksperimen

### 4.1 Model Boosting Awal

| Category           | Model                      |
|--------------------|----------------------------|
| Appliances         | GradientBoostingRegressor  |
| Beauty & Grooming  | XGBRegressor               |
| Computing          | GradientBoostingRegressor  |
| Entertainment      | Ridge                      |
| Mobiles & Tablets  | RandomForestRegressor      |

### 4.2 Model Terbaik Setelah Tuning

| Category           | Model             | MAE     | RMSE    | R²       |
|--------------------|------------------|---------|---------|----------|
| Appliances         | RandomForest     | 0.0086  | 0.0184  | 0.9971   |
| Beauty & Grooming  | GradientBoosting | 0.0361  | 0.0709  | 0.9844   |
| Computing          | RandomForest     | 0.0127  | 0.0253  | 0.9988   |
| Entertainment      | GradientBoosting | 0.0110  | 0.0269  | 0.9939   |
| Mobiles & Tablets  | RandomForest     | 0.0070  | 0.0124  | 0.9954   |

> **Insight**:  
> - Random Forest menjadi model paling konsisten dan akurat di banyak kategori.  
> - Kesalahan rata-rata (MAE) sangat kecil pada skala logaritmik, menunjukkan prediksi yang sangat presisi.

---

## 5. Kesimpulan dan Saran

### 5.1 Kesimpulan

- Model machine learning yang dibangun per kategori mampu memprediksi harga dengan tingkat akurasi sangat tinggi (R² > 0.98).
- Faktor `base_price` terbukti sebagai penentu harga jual yang paling berpengaruh.
- Pendekatan granular per kategori lebih efektif dibanding pendekatan umum menyeluruh.

### 5.2 Saran Pengembangan

- **Integrasi Data Kompetitor**: Menambahkan data eksternal dari harga pesaing untuk meningkatkan presisi.
- **Investigasi Kategori Tertentu**: Fokus pada kategori dengan error tinggi (misalnya Beauty & Grooming) dengan memperkaya fitur.
- **Model Dinamis**: Bangun pipeline retraining otomatis agar model adaptif terhadap dinamika pasar.
- **Optimasi Margin**: Tambahkan logika optimasi agar model tidak hanya memprediksi harga, tetapi merekomendasikan harga yang memaksimalkan keuntungan.

---

## 6. Referensi

- Géron, A. (2019). *Hands-On Machine Learning with Scikit-Learn, Keras & TensorFlow*. O'Reilly Media.
- Hastie, T., Tibshirani, R., & Friedman, J. (2009). *The Elements of Statistical Learning*.
- [Scikit-learn Documentation](https://scikit-learn.org/)
- [XGBoost Documentation](https://xgboost.readthedocs.io/)
- Dataset dan kode lengkap: [https://github.com/dataskillsboost/FinalProjectDA11](https://github.com/dataskillsboost/FinalProjectDA11)