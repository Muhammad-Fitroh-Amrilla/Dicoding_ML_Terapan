# Laporan Proyek Machine Learning - Muhammad Fitroh Amrilla

## Domain Proyek

Pada masa ini, banyak orang yang membutuhkan hiburan untuk menghilangkan penat, penat dan stress dari aktivitas sehari-hari. Salah satu hiburan yang bisa menghilangkan penat dan stress adalah menonton film.
Karena meningkatnya penggemar film, baik film Asia maupun film Barat, hal ini memunculkan ide untuk mengembangkan informasi tentang industri perfilman. Dengan cara memberikan informasi tentang film kepada masyarakat agar masyarakat tertarik untuk menonton film yang disarankan dan masyarakat mengetahui gambaran film yang ingin dilihat menggunakan sistem rekomendasi [ [1](https://openlibrarypublications.telkomuniversity.ac.id/index.php/engineering/article/view/16513/16222) ]..


Sistem rekomendasi adalah aplikasi yang digunakan untuk memberikan rekomendasi kepada pengguna untuk membantu mereka membuat keputusan yang diinginkan. Data untuk memberikan rekomendasi kepada pengguna menggunakan filter data dan untuk merekomendasikan produk. Ada beberapa faktor yang dapat mempengaruhi keputusan sistem untuk merekomendasikan pengguna, seperti perilaku pengguna, deskripsi produk, preferensi dan kebiasaan kelompok pengguna yang memiliki kesamaan dalam menilai suatu produk.
Penelitian sejenis pernah dilakukan oleh Rizqi dan Arrie (2021) yang menyatakan bahwa dengan menggunakan sistem rekomendasi berbasis deep learning dapat meningkatkan kinerja serta meningkatkan kepuasan pengguna aplikasi 
[ [2](https://journal.uii.ac.id/AUTOMATA/article/view/17426/10934) ].
Oleh karena itu sistem rekomendasi film dikembangkan untuk menjawab permasalahan tersebut.

## Business Understanding

### Problem Statements

Berdasarkan latar belakang yang telah dijelaskan diatas, terdapat beberapa masalah yaitu:
- Berdasarkan data mengenai pengguna, bagaimana membuat sistem rekomendasi yang dipersonalisasi dengan teknik content-based filtering?
- Dengan data rating yang dimiliki, bagaimana merekomendasikan film lain yang mungkin disukai dan belum pernah ditonton oleh pengguna? 

### Goals

Untuk menjawab masalah yang ada, akan dibuat model prediksi dengan tujuan sebagai berikut:
- Menghasilkan sejumlah rekomendasi film yang dipersonalisasi untuk pengguna dengan teknik content-based filtering.
- Menghasilkan sejumlah rekomendasi film yang sesuai dengan preferensi pengguna dan belum pernah ditonton sebelumnya dengan teknik collaborative filtering.

### Solution statements
Solusi yang dapat dilakukan untuk sistem rekomendasi film dengan menggunakan 2 algoritma *machine learning* yaitu:
- Content-based filtering yaitu merekomendasikan item yang mirip dengan item yang disukai pengguna di masa lalu. Algoritma ini bekerja dengan menyarankan item serupa yang pernah disukai di masa lalu atau sedang dilihat di masa kini kepada pengguna. Semakin banyak informasi yang diberikan pengguna, semakin baik akurasi sistem rekomendasi.
- Collaborative filtering bergantung pada pendapat komunitas pengguna. Ia tidak memerlukan atribut untuk setiap itemnya seperti pada sistem berbasis konten.

Algoritma Content Based Filtering digunakan untuk merekemondesikan movie berdasarkan aktivitas pengguna pada masa lalu, sedangkan algoritma Collaborative Filltering digunakan untuk merekomendasikan movie berdasarkan ratings yang paling tinggi.

## Data Understanding
Data atau dataset yang digunakan pada proyek *machine learning* ini adalah data *Movie Recommendation* dataset yang didapat dari situs kaggle. Dataset ini berisikan informasi mengenai film dari tahun 1996 sampai 2016. 
Terdapat 4 file data dalam dataset. 
Link dataset dapat dilihat dari tautan berikut : [Motorcycle Dataset](https://www.kaggle.com/datasets/nehalbirla/motorcycle-dataset).



### Variabel-variabel pada *Movie Recommendation* dataset adalah sebagai berikut:  

- links : merupakan daftar link film tersebut.
- movies : merupakan daftar film yang tersedia.
- ratings : merupakan daftar penilaian yang diberikan pengguna terhadap film.
- tags : merupakan daftar kata kunci dari film tersebut

Untuk memahami *Movie Recommendation* dataset akan menggunakan beberapa teknik *Univariate Explanatory Data Analysis (EDA)* pada variabel-variabel berikut:
1.   Deskripsi Variabel

| # | Column            | Non-Null Count | Dtype   |
|---|-------------------|----------------|---------|
| 0 | name              | 1061 non-null  | object  |
| 1 | selling_price     | 1061 non-null  | int64   |
| 2 | year              | 1061 non-null  | int64   |
| 3 | seller_type       | 1061 non-null  | object  |
| 4 | owner             | 1061 non-null  | object  |
| 5 | km_driven         | 1061 non-null  | int64   |
| 6 | ex_showroom_price | 626 non-null   | float64 |

Gambar 1. Info dataset

Pada Gambar 1, dapat dilihat bahwa:
*   Ada 3 kolom bertipe object, yaitu name, seller_type, owner
*   Terdapat 3 kolom dengan tipe data int64, yaitu selling_price, year, km_driven 
*   Terdapat 1 kolom dengan tipe data float64 yaitu ex_showroom_price

2.   Menangani *missing value & outliers*

Langkah selanjutnya menggunakan salah satu teknik untuk mengatasi *missing value* yaitu mengganti *missing value* dengan nilai rata-rata. Kemudian menangani *outlier*, *outliers* adalah sampel yang nilainya sangat jauh dari cakupan umum data utama. Pada kasus ini, *outliers* akan dideteksi dengan teknik visualisasi data (boxplot). Kemudian, *ouliers* akan ditangani dengan teknik *IQR method*.

3.   Analisis *Univariate*
Fitur kategorik

![name](https://user-images.githubusercontent.com/64821050/204170314-a77fd41e-51e1-43a0-86c4-18652150df5e.PNG)


Gambar 2. Analisis fitur name

Pada Gambar 2, jenis sepeda motor terbanyak yaitu Bajaj Pulsar 150 dengan jumlah sampel sebanyak 39 sampel dan presentase 4.4 %

![seller](https://user-images.githubusercontent.com/64821050/204170333-60e1d74a-10d1-47bc-a3e6-eeff7a9df45e.PNG)

Gambar 3. Analisis fitur seller_type

Pada Gambar 3, dapat diketahui bahwa 876 penjual sepeda motor merupakan perorangan dan 4 diantaranya merupakan dealer

![owner](https://user-images.githubusercontent.com/64821050/204170359-b74dc667-e38f-4caf-834f-0de4b1af7e3e.PNG)

Gambar 4. Analisis fitur owner

Pada Gambar 4, dapat dilihat bahwa sebanyak 87.6 % sepeda motor hanya dimiliki oleh orang pertama, 11.5 % dimiliki sampai dengan orang kedua dan yang terkahir 0.9 % sepeda motor dimiliki sampai dengan orang ketiga.

Fitur Numerik

![Univariate_numerik](https://user-images.githubusercontent.com/64821050/204170385-2a96773a-c0c0-46fc-8570-848013c83907.PNG)

Gambar 5. Analisis fitur numerik

Pada Gambar 5, dapat dilihat bahwa :
* Rentang harga jual sepeda motor dari ratusan dollar sampai dengan 130000 Dollar
* Jumlah terbanyak sepeda motor yang dijual berada di rentang harga 20000-40000 Dollar


4.   Analisis *Multivariate* 
Fitur Kategorik

![Multivariate_kategorik](https://user-images.githubusercontent.com/64821050/204170437-1c941849-bd55-42bd-acb4-8ebb0f7a896d.PNG)

Gambar 6. Analisis *multivariate* fitur kategorik

Pada gambar 6, dapat dilihat bahwa :
*   Kategori dalam fitur name terlalu banyak sehingga fitur name tidak mempengaruhi fitur selling_price
*   Pada fitur seller_type , individual merupakan yang paling tinggi dalam seller_type memiliki harga rendah. Sehingga fitur seller_type memiliki dampak yang kecil terhadap rata-rata harga jual
*   Pada fitur owner rata-rata harga cenderung mirip. Rentangnya berada antara 35000 hingga 45000. Sehingga, fitur cut memiliki pengaruh atau dampak yang kecil terhadap rata-rata harga jual.

Fitur Numerik

![Multivariate_numerik](https://user-images.githubusercontent.com/64821050/204170412-2b7b1404-720a-4418-bcc1-442a846e08db.PNG)

Gambar 7. Analisis *multivariate* fitur numerik

Dapat kita lihat bahwa :
*   selling_price memiliki korelasi positip terhadap variabel year dan ex_showroom_price
*   sedangkan variabel km_driven memiliki korelasi negatif terhadap selling_price

*Correlation matrix* untuk fitur numerik

![Corrmap](https://user-images.githubusercontent.com/64821050/204170454-af0706e0-ff98-44dc-9f9f-c4beed636e92.PNG)

Gambar 8. *Correlation matrix* fitur numerik

Pada Gambar 8, dapat dilihat matriks korelasi diatas, korelasi fitur year dan ex_showroom_price terhadap fitur selling_price berada pada rentang cukup (0.25 - 0.5) dan fitur yang memiliki korelasi paling tinggi terhadap fitur selling_price yaitu year sebesar 0.58

## Data Preparation
Dalam *data preparation*, 3 hal yang akan dilakukan sebelum memasukkan data ke model latih:

- *Encoding* Fitur Kategorik : *Encoding* fitur kategorik dilaksanakan di beberapa fitur yang bertipe *object*. Hal ini dilakukan karena model *machine learning* hanya dapat menerima data dalam bentuk numerik. Untuk *encoding* fitur menggunakan *LabelEncoder*.
- *Train-Test-Split* : Membagi dataset menjadi data latih dan data uji dengan perbandingan 90:10 yaitu 90 persen data akan menjadi data latih dan 10 persen data akan menjadi data uji . Hal ini dilakukan supaya kita dapat melakukan validasi dengan benar tanpa bias dari model.
- *Standarisasi* : Standarisasi menggunakan teknik *StandarScaler* dari *library Scikitlearn*. *StandardScaler* melakukan proses standarisasi fitur dengan mengurangkan mean (nilai rata-rata) kemudian membaginya dengan standar deviasi untuk menggeser distribusi.  *StandardScaler* menghasilkan distribusi dengan standar deviasi sama dengan 1 dan mean sama dengan 0. *Scaling* ini dilaksanakan untuk membantu model *machine learning* yang akan dipakai lebih mudah diolah. 

## Modeling

Pada tahap ini, model *machine learning* yang akan dipakai ada tiga algoritma. Lalu performa masing-masing algoritma akan dievaluasi dan menentukan algoritma mana yang memberikan hasil prediksi terbaik. Ketiga algoritma yang akan digunakan, antara lain:

1.   *K-Nearest Neighbors* (KNN) : KNN bekerja dengan membandingkan jarak satu sampel ke sampel pelatihan lain dengan memilih sejumlah k tetangga terdekat (dengan k adalah sebuah angka positif). Untuk parameter yang akan digunakan yaitu n_neighbors dengan nilai sebesar 10.
		- **kelebihan** : algoritma KNN yaitu mudah dipahami dan digunakan serta algoritma yang relatif sederhana dibandingkan dengan algoritma lain.
		- **kekurangan** : jika dihadapkan pada jumlah fitur atau dimensi yang besar
2.   *Random Forest* : Algoritma ini disusun dari banyak algoritma pohon (*decision tree*) yang pembagian data dan fiturnya dipilih secara acak.  Untuk parameter yang akan digunakan yaitu n_estimators=50, max_depth=16, random_state=55, n_jobs=-1.
		- **kelebihan** : Kuat terhadap data *outlier* (pencilan data), berjalan secara efisien pada kumpulan data yang besar, dan bekerja dengan baik dengan data non-linear.
		- **kekurangan** : Pembelajaran bisa berjalan lambat, tergantung pada parameter yang digunakan dan tidak bisa memperbaiki model yang dihasilkan secara berulang.
3.   *Boosting Algorithm* : Algoritma yang menggunakan teknik *boosting* bekerja dengan membangun model dari data latih. Kemudian ia membuat model kedua yang bertugas memperbaiki kesalahan dari model pertama. Model ditambahkan sampai data latih terprediksi dengan baik atau telah mencapai jumlah maksimum model untuk ditambahkan.  Untuk parameter yang akan digunakan yaitu learning_rate=0.05, random_state=55.
		- **kelebihan** : Algoritma ini sangat *powerful* dalam meningkatkan akurasi prediksi. Algoritma *boosting* sering mengungguli model yang lebih sederhana seperti *logistic regression* dan *random forest*
		- **kekurangan** : *Learning* secara progresif dan sangat sensitif terhadap data *noise* dan *outlier*.

*Error* dari masing-masing model:

![msevis](https://user-images.githubusercontent.com/64821050/204170536-61960d51-e2c2-40ec-984c-8bdc9cc07c62.PNG)

Gambar 9. Visualisasi mse

Pada Gambar 9, dapat diliat bahwa model *Random Forest* memiliki nilai *error* yang lebih kecil dibanding model lain menandakan bahwa model *Random Forest* merupakan model terbaik yang dapat digunakan untuk memprediksi harga jual sepeda motor bekas.

## Evaluation
Metrik yang akan kita gunakan pada prediksi ini adalah MSE atau *Mean Squared Error* yang menghitung jumlah selisih kuadrat rata-rata nilai sebenarnya dengan nilai prediksi. MSE didefinisikan dalam persamaan berikut

MSE = $\frac{1}{n} \Sigma_{i=1}^n({y}-\hat{y})^2$

Dimana :

y = Nilai Aktual permintaan

$hat{y}$ = Nilai hasil peramalan

n = banyaknya data

berikut adalah hasil evaluasi ketiga model menggunakan mse pada tabel 1.

Tabel 1. Nilai mse pada data uji dan data latih dari ketiga model

|              |   **Train**   |    **Test**   |
|--------------|:-------------:|:-------------:|
|    **KNN**   | 187692.530355 | 408256.640368 |
|    **RF**    | 21742.955798  | 191000.645023 |
| **Boosting** | 211202.420774 | 248793.555393 |

Pada Tabel 1, dapat diliat bahwa model *Random Forest* memiliki nilai *error* yang lebih kecil dibanding model lain pada data latih dan data uji.

Hasil prediksi masing-masing model dari 10 data dapat dilihat pada tabel 2.

Tabel 2. Hasil prediksi ketiga model dari 10 data
|          | **y_true** | **prediksi_KNN** | **prediksi_RF** | **prediksi_Boosting** |
|----------|-----------:|-----------------:|----------------:|----------------------:|
|  **491** |      55000 |          31550.0 |         27342.2 |               28580.3 |
|  **637** |      65000 |          48300.0 |         52330.0 |               37077.8 |
| **1043** |      27000 |          25699.9 |         29220.0 |               38776.2 |
|  **203** |      30000 |          27650.0 |         17340.0 |               25483.2 |
|  **415** |      38000 |          31840.0 |         30802.0 |               32782.8 |
|  **525** |      25000 |          29420.0 |         27883.1 |               28580.3 |
|  **939** |      30000 |          30970.0 |         31870.0 |               28580.3 |
|  **212** |      15000 |          27300.0 |         20978.0 |               25129.9 |
|  **778** |      20000 |          20460.0 |         17548.0 |               24911.5 |
|  **826** |     100000 |         107200.0 |         84346.0 |               81196.1 |

Pada tabel 2, dapat kita lihat bahwa prediksi dari ketiga algoritma yang paling mendekati y_true adalah prediksi *Random Forest* menandakan bahwa *Random Forest* merupakan algoritma terbaik dibandingkan dengan algoritma yang lain.

**Kesimpulan** :  Korelasi variabel yang mempengaruhi harga sepeda motor bekas terdapat beberapa variabel yang memiliki korelasi positif dan negatif terhadap variabel harga jual dan untuk model *machine learning* yang memiliki nilai *error* paling rendah yaitu model *Random Forest* yang menandakan bahwa *Random Forest* merupakan algoritma terbaik dibandingkan dengan algoritma yang lain dalam hal memprediksi harga sepeda motor bekas.

**Referensi** :

[1]	I. Sunoto dan L. Lukman, “SISTEM PENDUKUNG KEPUTUSAN PENENTUAN HARGA JUAL SEPEDA MOTOR BEKAS DENGAN PENDEKATAN LOGIKA FUZZY INFRENCE SYSTEM MAMDANI,” Simet, vol. 6, no. 2, hlm. 305, Nov 2015, doi: 10.24176/simet.v6i2.466.

[2]	I. Prasetya, D. Y. Rahayu, dan M. Kom, “PENENTUAN HARGA JUAL SEPEDA MOTOR BEKAS MENGGUNAKAN FUZZY LOGIC (METODE TSUKAMOTO) DAN IMPLEMENTASINYA,” hlm. 8.

		
**---Ini adalah bagian akhir laporan---**


