# Laporan Proyek Machine Learning - Rifki Nova Suryo

## Project Overview
Sistem rekomendasi adalah suatu system yang digunakan oleh para user / customer / pelanggan untuk mendapatkan produk yang diinginkan. Ide awal dari sistem rekomendasi sendiri adalah untuk menggunakan beberapa sumber informasi, tujuan utama dari sistem rekomendasi adalah untuk meningkatkan penjualan produk.

Proyek submission ini adalah membuat sistem rekomendasi buku yang melakukan klasifikasi suka atau tidaknya user terhadap buku yang memiliki genre atau penulis yang sama. Proyek ini dibangun dengan tujuan untuk membantu user untuk mendapatkan buku yang memiliki genre atau penulis yang disukai tanpa perlu bersusah payah untuk mencari secara manual, sehingga user memiliki kepuasan dalam pengalaman mencari dan membaca buku yang sesuai dengan minat yang disukai.

 
Referensi dari proyek ini adalah sebagai berikut:
[BOOK RECOMMENDATION SYSTEM: A SYSTEMATIC REVIEW AND RESEARCH ISSUES](https://www.researchgate.net/publication/352781839_BOOK_RECOMMENDATION_SYSTEM_A_SYSTEMATIC_REVIEW_AND_RESEARCH_ISSUES)

## Business Understanding
### Problem Statements
Bagaimana caranya merekomendasikan buku berdasarkan buku yang pengguna suka
### Goals
Dapat membuat sistem rekomendasi buku berdasarkan suka atau tidaknya pengguna
### Solution statements
Membuat sistem rekomendasi berdasarkan __Collaborative filtering__. Algoritma __Collaborative filtering__ menggunakan pendekatan model dari tingkah laku pengguna sebelumnya seperti kunjungan pengguna pada suatu alamat tayangan atau memberikan rating terhadap beberapa item pilihan pengguna dan juga yang dilakukan oleh pengguna lain yang nantinya item tersebut akan dijadikan acuan untuk memberikan prediksi terhadap pengguna lain atau pengguna yang berkaitan. __Collaborative filtering__ dibagi lagi menjadi dua kategori, yaitu: __model based__ (metode berbasis model machine learning) dan __memory based__ (metode berbasis memori). Pada proyek ini menggunakan __model based__ dengan deep learning.

## Data Understanding
### Sumber Data ###
Dataset yang digunakan pada proyek ini adalah data __Book Recommendation Dataset__ yang didapat dari situs [kaggle](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset). 
### Jumlah Data ###
Dataset yang digunakan memiliki 3 buah dataset yaitu ada dataset Users, Books dan Ratings. Masing-masing dataset memiliki jumlah data yang berbeda, pada dataset Users memiliki data sebanyak 278858 yang terdiri dari tipe data integer, object dan float sedangkan dataset Books memiliki jumlah data sebanyak 271360 yang terdiri dari tipe data object. Dataset Ratings memiliki data sebanyak 1149780 yang terdiri dari tipe data integer dan object. 
### Kondisi Data ###
Pada ketiga dataset yang terdapat pada __Book Recomendation Dataset__ terdapat missing value yaitu dataset Books terdapat missing value di kolom Book-Author, Publisher dan Image-URL-L dan dataset Users terdapat missing value di kolom Age. Dataset Ratings tidak ada missing value
### Variabel-variabel pada __Book Recommendation Dataset__ adalah sebagai berikut:
Pada dataset Users memiliki data:
- USER-ID : Berisikan id pengguna
- Location : Lokasi pengguna
- Age : Usia pengguna

Pada dataset Books memiliki data:
- ISBN : kode untik untuk pengidentifikasian buku
- Book-Title : Judul buku
- Book-Author : Penulis buku
- Year-Of-Publication : Tahun terbit buku
- Publisher : Penerbit buku
- Image-URL-S, Image-URL-M, Image-URL-L : URL yang manutkan cover

pada dataset Rating memiliki data:
- User-ID : Berisikan Id pengguna
- ISBN : Kode untik untuk pengidentifikasian buku
- Book-Rating : Rating buku dari pengguna

Untuk memahami dataset yang digunakan maka dilakukan EDA __Univariate Analysis__.
Seperti mengeksplorasi variabel menggunakan desribe(), mengecek tipe data pada dataset menggunakan info() dan menghitung jumalah __missing value__ menggunakan isna() dan sum().

## Data Preparation
Proses __Data Preparation__ yang digunakan yaitu:
- Menggabungkan variabel : untuk menggabungkan data ratings dan books berdasarkan ISBN.
- Melakukan filtering : untuk memfilter data yang tidak digunakan
- Mengatasi missing value : menyeleksi data, apakah data tersebut ada yang kosong atau tidak, jika ada data kosong maka kemudian akan dihapus.
- Menggunakan LabelEncoder : untuk melakukan encoded pada data kategori
- Melakukan menghitung data unique :  untuk menghitung jumalah data unik pada kolom user dan item
- Melakukan binarisasi : untuk mempermudah dalam proses training
- Membagi data menjadi data training dan validasi : untuk membagi data untuk dilatih dan validasi. Dalam melakukan splitting, digunakan rasio 80:20, yang berarti 80% data training, dan 20% data testing.

## Modeling
Berdasarkan __Solution Statmen__ di atas, proyek ini menggunakan __Collaborative filtering__ __model based__. Dalam pembuatan model menggunakan menggunakan keras dan membuat class RecommenderClassifier. Training dilakukan dengan optimizer Adam dan matriks evaluasi Accuracy. Model akan menghitung skor match di antara dua __embedding layers__ milik user melalui dot_product, dan menambahkan bias ke keduanya. Match skor kemudian akan berada pada skala interval 0 hingga 1 melalui sigmoid.

Tabel 1. Merupakan contoh rekomendasi berdasarkan User-id 276726
| ISBN     |              Book-Title                      | Probability  |
|----------|----------------------------------------------|--------------|
| 13983    | Blackout	                                  |     1.0      |
| 100760   | The Cassandra Compact: A Covert-One Novel    |     1.0      |
| 44068    | Growing Up                                   |     1.0      |
| 133350   | Wolves of the Calla (The Dark Tower, Book 5) |     1.0      |
| 93462    | Stiff: The Curious Lives of Human Cadavers	  |     1.0      |		

## Evaluation
Karena pada proyek ini melakukan klasifikasi maka matriks evaluasi yang digunakan adalah akurasi. Akurasi adalah metrik yang paling sederhana dan sering digunakan untuk mengukur kinerja model klasifikasi. Akurasi dihitung sebagai proporsi dari prediksi benar (baik positif maupun negatif) terhadap seluruh prediksi yang dilakukan oleh model. Cara kerja dari akurasi ini adalah jika model yang sudah dibuat lalu melakukan prediksi sebanyak 100 prediksi dan 90 yang benar, akurasi model itu akan 90%. Jika dituliskan dengan rumus akan sebagai berikut:
Accuracy = (TP + TN)/(TP + TN + FP + FN)
dimana:

- TP (True Positives): model benar memprediksi
- TN (True Negatives): model benar memprediksi
- FP (False Positives): model salah memprediksi 
- FN (False Negatives): model salah memprediksi (gagal mendeteksi)


![Gambar 1. Grafik hasil evaluasi](https://github.com/user-attachments/assets/d19da844-8e86-4871-a890-b528936c9b9b)

​

Gambar 1 merupakan visualisasi training model, diperoleh nilai train accuracy sebesar 98% dan test accuracy sebesar 70%. Berdasarkan hasil itu model ini terlalu > overfitting karena hasil plot dari data test terus mengalami penurunan dibandingkan dengan hasil plot dari data_train. Model yang dibuat berdasarkan __Solution Statment__ ini membantu menjawab __Problem Statment__ dan __Goals__ untuk membuat sistem rekomendasi buku meski perlu melakukan perbaikan pada model agar tidak overfitting.
