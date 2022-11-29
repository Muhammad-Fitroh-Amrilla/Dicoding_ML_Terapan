# Laporan Proyek Machine Learning - Muhammad Fitroh Amrilla

## Domain Proyek

Pada masa ini, banyak orang yang membutuhkan hiburan untuk menghilangkan penat, penat dan stress dari aktifitas sehari-hari. Salah satu hiburan yang bisa menghilangkan penat dan stress adalah menonton film.
Karena meningkatnya penggemar film, baik film Asia maupun film Barat, hal ini memunculkan ide untuk mengembangkan informasi tentang industri perfilman. Dengan cara memberikan informasi tentang film kepada masyarakat agar masyarakat tertarik untuk menonton film yang disarankan dan masyarakat mengetahui gambaran film yang ingin dilihat menggunakan sistem rekomendasi [ [1](https://openlibrarypublications.telkomuniversity.ac.id/index.php/engineering/article/view/16513/16222) ].


Sistem rekomendasi adalah aplikasi yang digunakan untuk memberikan rekomendasi kepada pengguna untuk membantu mereka membuat keputusan yang diinginkan. Data untuk memberikan rekomendasi kepada pengguna menggunakan filter data dan untuk merekomendasikan produk. Ada beberapa faktor yang dapat mempengaruhi keputusan sistem untuk merekomendasikan pengguna, seperti perilaku pengguna, deskripsi produk, preferensi dan kebiasaan kelompok pengguna yang memiliki kesamaan dalam menilai suatu produk.
Penelitian sejenis pernah dilakukan oleh Rizqi dan Arrie (2021) yang menyatakan bahwa dengan menggunakan sistem rekomendasi berbasis *deep learning* dapat meningkatkan kinerja serta meningkatkan kepuasan pengguna aplikasi 
[ [2](https://journal.uii.ac.id/AUTOMATA/article/view/17426/10934) ].
Oleh karena itu sistem rekomendasi film dikembangkan untuk menjawab permasalahan tersebut.

## Business Understanding

### Problem Statements

Berdasarkan latar belakang yang telah dijelaskan diatas, terdapat beberapa masalah yaitu:
- Berdasarkan data mengenai pengguna, bagaimana membuat sistem rekomendasi film yang dipersonalisasi dengan teknik *content-based filtering*?
- Dengan data rating yang dimiliki, bagaimana merekomendasikan film lain yang mungkin disukai dan belum pernah ditonton oleh pengguna? 

### Goals

Untuk menjawab masalah yang ada, akan dibuat model prediksi dengan tujuan sebagai berikut:
- Menghasilkan sejumlah rekomendasi film yang dipersonalisasi untuk pengguna dengan teknik *content-based filtering*.
- Menghasilkan sejumlah rekomendasi film yang sesuai dengan preferensi pengguna dan belum pernah ditonton sebelumnya dengan teknik *collaborative filtering*.

### Solution statements
Solusi yang dapat dilakukan untuk sistem rekomendasi film dengan menggunakan 2 algoritma *machine learning* yaitu:
- ***Content-based filtering*** : merekomendasikan item yang mirip dengan item yang disukai pengguna di masa lalu. Algoritma ini bekerja dengan menyarankan item serupa yang pernah disukai di masa lalu atau sedang dilihat di masa kini kepada pengguna. Semakin banyak informasi yang diberikan pengguna, semakin baik akurasi sistem rekomendasi.
- ***Collaborative filtering*** : bergantung pada pendapat komunitas pengguna. Ia tidak memerlukan atribut untuk setiap itemnya seperti pada sistem berbasis konten.

Algoritma *content based filtering* digunakan untuk merekomendasikan film berdasarkan aktivitas pengguna pada masa lalu, sedangkan algoritma *collaborative filtering* digunakan untuk merekomendasikan film berdasarkan *rating* yang paling tinggi.

## Data Understanding
Data atau dataset yang digunakan pada proyek *machine learning* ini adalah data *Movie Recommendation* dataset yang didapat dari situs Kaggle. Dataset ini berisikan informasi mengenai film dari tahun 1996 sampai 2016. 
Terdapat 4 file data dalam dataset. 
Link dataset dapat dilihat dari tautan berikut : [*Movie Recommendation* Dataset](https://www.kaggle.com/datasets/bandikarthik/movie-recommendation-system).



### Variabel-variabel pada *Movie Recommendation* dataset adalah sebagai berikut:  

- links : merupakan daftar link film tersebut.
- movies : merupakan daftar film yang tersedia.
- ratings : merupakan daftar penilaian yang diberikan pengguna terhadap film.
- tags : merupakan daftar kata kunci dari film tersebut

Untuk memahami *Movie Recommendation* dataset akan menggunakan beberapa teknik *Univariate Explanatory Data Analysis (EDA)* pada variabel-variabel berikut:
1.   Variabel links

Variabel links memiliki jumlah data sebanyak 34208 data dan jumlah data link film yang unik berdasarkan movieId sebanyak 34208 data. Info variabel links dapat dilihat pada tabel 1 berikut :

Tabel 1. Info variabel links

| # | Column  | Non-Null Count | Dtype   |
|---|---------|----------------|---------|
| 0 | movieId | 34208 non-null | int64   |
| 1 | imdbId  | 34208 non-null | int64   |
| 2 | tmdbId  | 33912 non-null | float64 |

Pada Tabel 1, dapat dilihat bahwa:

* Terdapat 2 buah kolom bertipe int64 yaitu movieId dan imdbId
* Terdapat 1 buah kolom bertipe float64 yaitu tmdbId

2.   Variabel movies

Variabel movies memiliki total jumlah data sebanyak 34208 dan jumlah data movies unik berdasarkan movieId sebanyak 34208. Terdapat judul film sebanyak 34185 judul dan 1446 genre yang berbeda. Info variabel movies dapat dilihat pada tabel 2 berikut :

Tabel 2. Info variabel movies

| # | Column  | Non-Null Count | Dtype  |
|---|---------|----------------|--------|
| 0 | movieId | 34208 non-null | int64  |
| 1 | title   | 34208 non-null | object |
| 2 | genres  | 34208 non-null | object |


Pada Tabel 2, dapat dilihat bahwa:

* Terdapat 1 buah kolom bertipe int64 yaitu movieId
* Terdapat 2 buah kolom bertipe object yaitu title dan genres

3.   Variabel ratings

Variabel ratings memiliki jumlah data sebanyak 22884377 data. Karena data terlalu banyak, maka data yang akan digunakan hanya 30000 data saja. Jumlah data unik ratings dari user sebanyak 351 data
dan dari film sebanyak  5380 data. Info variabel ratings dapat dilihat pada tabel 3 berikut:

Tabel 3. Info variabel ratings

| # | Column    | Dtype   |
|---|-----------|---------|
| 0 | userId    | int64   |
| 1 | movieId   | int64   |
| 2 | rating    | float64 |
| 3 | timestamp | int64   |

Pada Tabel 3, dapat dilihat bahwa:

* Terdapat 3 buah kolom bertipe int64 yaitu userId, movieId dan timestamp
* Terdapat 1 buah kolom bertipe float64 yaitu rating

Deskripsi dari variabel ratings dapat dilihat pada tabel 4 berikut:

Tabel 4. Deskripsi variabel ratings

|       |       userId |       movieId |      ratings | timestamp    |
|------:|-------------:|--------------:|-------------:|--------------|
| count | 30000.000000 |  30000.000000 | 30000.000000 | 3.000000e+04 |
|  mean |   163.875767 |  11711.897767 |     3.487700 | 1.132281e+09 |
|   std |   100.419974 |  24747.244802 |     1.141019 | 1.794357e+08 |
|   min |     1.000000 |      1.000000 |     0.500000 | 8.270984e+08 |
|   25% |    74.000000 |    919.000000 |     3.000000 | 9.742371e+08 |
|   50% |   166.000000 |   2289.000000 |     4.000000 | 1.124478e+09 |
|   75% |   247.000000 |   5060.000000 |     4.000000 | 1.287274e+09 |
|   max |   351.000000 | 148667.000000 |     5.000000 | 1.453995e+09 |

Pada tabel 4, dapat dilihat dari nilai max dan min bahwa nilai rating terbesar yaitu 5 dan nilai rating terkecil yaitu 0.5

4.   Variabel tags

Variabel tags memiliki jumlah data sebanyak 586994 data. Karena data terlalu banyak, maka data yang akan digunakan hanya 30000 data saja. Jumlah data unik tag sebanyak 6509 data. Info variabel tags dapat dilihat pada tabel 4 berikut:

Tabel 5. Info variabel tags

| # |    Column |  Non-Null Count |  Dtype |
|--:|----------:|----------------:|-------:|
| 0 |    userId | 586994 non-null |  int64 |
| 1 |   movieId | 586994 non-null |  int64 |
| 2 |       tag | 586978 non-null | object |
| 3 | timestamp | 586994 non-null |  int64 |

## Data Preparation
Dalam proses persiapan data dibagi menjadi 2 berdasarkan algoritma yang digunakan yaitu pada *content-based filtering* dan *collaborative filtering* . Berikut tahapan-tahapan persiapan data:
***Content-based filtering***

- **Menangani *missing value*** : mengecek data apakah data tersebut ada yang bernilai NaN atau tidak, jika terdapat data yang kosong maka akan dihapus menggunakan fungsi dropna. Hal ini dilakukan karena missing value akan memengaruhi kinerja dan harus ada langkah khusus yang perlu diambil untuk mengatasinya.
- **Mengurutkan data** : mengurutkan data secara *ascending*. Hal ini dilakukan karena data yang terurut akan terlihat lebih rapih.
- **Menangani duplikat data** : Menghapus data yang duplikat dengan fungsi drop_duplicates(). Dalam hal ini, membuang data duplikat pada kolom ‘movieId’. Hal ini dilakukan karena data duplikat memiliki informasi yang sama sehingga apabila dihapus tidak akan mempengaruhi kinerja.
- **Konversi data menjadi list** : Melakukan konversi data *series* menjadi *list*. Dalam hal ini, menggunakan fungsi tolist() dari *library numpy*. Hal ini dilakukan untuk menyederhanakan data menjadi bentuk *list*.
- **Membuat Dictionary** : Membuat *dictionary* untuk menentukan pasangan *key-value* pada data movie_id, movie_name, dan movie_genre yang telah disiapkan sebelumnya. Hal ini dilakukan untuk persiapan data sebelum model dilatih.


***Collaborative filtering***

- ***Encode*** **fitur userId dan movieId** : Melakukan persiapan data untuk menjadikan (*encode*) fitur ‘userId’ dan ‘movieID’ ke dalam indeks integer. Hal ini diperlukan agar data siap digunakan untuk pemodelan.
- **Memetakan userId dan movieId** : Petakan userId dan movieId ke dataframe yang berkaitan. Hal ini diperlukan agar data yang sudah di *encode* dipetakan kemudian dimasukan kedalam dataframe yang berkaitan.
- **Cek data dan ubah nilai rating**: cek beberapa hal dalam data seperti jumlah *user*, jumlah *movie*, dan mengubah nilai *rating* menjadi *float*, cek nilai *minimum* dan *maximum*. Hal ini dilakukan untuk mengecek data yang sudah siap digunakan untuk pemodelan.
- **Membagi data untuk latih dan validasi** : Membagi dataset menjadi data latih dan data validasi dengan perbandingan 80:20 yaitu 80 persen data akan menjadi data latih dan 20 persen data akan menjadi data validasi . Hal ini dilakukan supaya kita dapat melakukan validasi dengan benar tanpa bias dari model.

## Modeling

Pada tahap ini, model *machine learning* yang akan dipakai ada 2 algoritma. Berikut algoritma yang akan digunakan:

1.   *Content-based filtering* : algoritma *content-based filtering* dibuat dengan apa yang disukai pengguna pada masa lalu.
		- **kelebihan** : Model tidak memerlukan data tentang pengguna lain, karena rekomendasi bersifat khusus untuk pengguna ini. Hal ini mempermudah penskalaan ke sejumlah besar pengguna.
		- **kekurangan** : Model hanya dapat membuat rekomendasi berdasarkan minat pengguna yang ada. Dengan kata lain, model memiliki kemampuan terbatas untuk memperluas minat pengguna yang ada.
2.   *Collaborative filtering* : algoritma *collaborative filtering* dibuat dengan memanfaatkan tingkat *rating* dari film tersebut. 
		- **kelebihan** : Tidak memerlukan pengetahuan domain dan model dapat membantu pengguna menemukan minat baru..
		- **kekurangan** :Tidak dapat menangani item baru dan sulit menyertakan fitur samping untuk kueri/item.

Hasil dari masing-masing model:

1. ***Content-based filtering***

Berikut adalah film yang disukai pengguna di masa lalu:

Tabel 6. Film yang disukai pengguna di masa lalu.

| id |       movie_name |                                           genre |
|---:|-----------------:|------------------------------------------------:|
|  1 | Toy Story (1995) | Adventure\|Animation\|Children\|Comedy\|Fantasy |

Pada tabel 6, dapat dilihat bahwa pengguna menyukai film yang berjudul *Toy Story* (1995) yang bergenre *Adventure, Animation, Children, Comedy,* dan *Fantasy*. Maka hasil 5 rekomendasi terbaik berdasarkan algoritma *content-based filtering* adalah sebagai berikut :

Tabel 7. Hasil rekomendasi algoritma *content-based filtering*

|   |                       movie_name |                                           genre |
|--:|---------------------------------:|------------------------------------------------:|
| 0 |            Monsters, Inc. (2001) | Adventure\|Animation\|Children\|Comedy\|Fantasy |
| 1 |                      Antz (1998) | Adventure\|Animation\|Children\|Comedy\|Fantasy |
| 2 |               Toy Story 2 (1999) | Adventure\|Animation\|Children\|Comedy\|Fantasy |
| 3 | Emperor's New Groove, The (2000) | Adventure\|Animation\|Children\|Comedy\|Fantasy |
| 4 |            Boxtrolls, The (2014) | Adventure\|Animation\|Children\|Comedy\|Fantasy | 

Dapat dilihat pada tabel 7, ada 5 film yang direkomendasikan bergenre yang sama yaitu *Adventure, Animation, Children, Comedy,* dan *Fantasy*. Hal ini didasarkan pada kesukaan penonton atau pengguna pada masa lalu.

2. ***Collaborative filtering***

Berikut merupakan film berdasarkan *rating* yang ada :

![Prediksi CF](https://user-images.githubusercontent.com/64821050/204574794-e56af57a-ff4e-48b6-ab5e-5889d7e3ab66.PNG)

Gambar 1. Hasil rekomendasi algoritma *collaborative filtering*

Pada Gambar 1, film yang memiliki *rating* tinggi dari pengguna paling banyak bergenre *drama, action,* dan *western*. Dan hasil rekomendasi juga menunjukan 10 film dengan genre *drama, action,* dan *western*.

## Evaluation
Hasil evaluasi dari masing-masing model:

1. ***Content-based filtering***

Film yang direkomendasikan di masa lalu yaitu fil Toy Story (1995) dengan genre Adventure, Animation, Children, Comedy, dan Fantasy. Top 5 item hasil rekomendasi film semua memilki genre yang sama atau *relevant* yaitu Adventure, Animation, Children, Comedy, dan Fantasy dengan genre film Toy Story. Dengan begitu hasil rekomendasi dapat dievaluasi menggunakan rumus presisi berikut :

*recommender system precision*: P = $\frac{n of our recommendations that are relevant}{n of items we recommended}$

Dengan begitu hasil presisi yang didapat adalah 100 persen .

2.  ***Collaborative filtering***

Evaluasi metrik yang digunakan untuk mengukur kinerja model adalah metrik RMSE (Root Mean Squared Error). RMSE adalah metode pengukuran dengan mengukur perbedaan nilai dari prediksi sebuah model sebagai estimasi atas nilai yang diobservasi. Root Mean Square Error adalah hasil dari akar kuadrat Mean Square Error. Keakuratan metode estimasi kesalahan pengukuran ditandai dengan adanya nilai RMSE yang kecil. Metode estimasi yang mempunyai Root Mean Square Error (RMSE) lebih kecil dikatakan lebih akurat daripada metode estimasi yang mempunyai Root Mean Square Error (RMSE) lebih besa


Rumus dari matriks RMSE adalah sebagai berikut:

MSE = $\sqrt{\frac{1}{n} \Sigma_{i=1}^n({y}-\hat{y})^2}$

Dimana :

y = Nilai Aktual permintaan

$\hat{y}$ = Nilai hasil peramalan

n = banyaknya data

Berikut visualisasi RMSE menggunakan *collaborative filtering*:

![RMSE](https://user-images.githubusercontent.com/64821050/204574857-44721c0c-b8a9-4201-a5c9-00b01b607155.PNG)

Gambar 2. Visualisasi RMSE 

Bisa dilihat pada Gambar 2. proses training model cukup smooth dan model konvergen pada epochs sekitar 50. Dari proses latih, memperoleh nilai error akhir sebesar sekitar 0.17 dan error pada data validasi sebesar 0.21 . Nilai tersebut cukup bagus untuk sistem rekomendasi.

**Kesimpulan** :  Berhasil menghasilkan 5 rekomendasi film terbaik menggunakan teknik *content-based filtering* dengan presisi 100 persen dan berhasil menghasilkan 10 rekomendasi terbaik menggunakan teknik *collaborative filtering* dengan RMSE sebesar 0.17 .

**Referensi** :

[1]	D. Nugraha, T. W. Purboyo, dan R. A. Nugrahaeni, “SISTEM REKOMENDASI FILM MENGGUNAKAN METODE USER BASED COLLABORATIVE FILTERING,” hlm. 11.

[2]	M. R. A. Zayyad, A. Kurniawardhani, S. Si, dan M. Kom, “Penerapan Metode Deep Learning pada Sistem Rekomendasi Film,” hlm. 5.
		
**---Ini adalah bagian akhir laporan---**


