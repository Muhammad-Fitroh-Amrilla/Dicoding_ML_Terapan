# Laporan Proyek Machine Learning - Muhammad Fitroh Amrilla

## Domain Proyek

Transportasi sudah semakin berkembang saat ini. Dahulu kita masih berjalan kaki atau menggunakan tenaga hewan untuk berpergian, namun saat ini sudah menggunakan kendaraan beroda seperti sepeda motor. Tentunya sepeda motor lebih mudah digunakan dan lebih terjangkau harganya. 

Semakin hari produksi sepeda motor semakin banyak dan canggih menyebabkan penjualan sepeda motor meningkat baik itu baru atau bekas. Mengapa penjualan motor bekas juga mengalami kenaikan? karena menurut penelitian Imam Sunoto (2015)dikatakan bahwa kebanyakan masyarakat akan menjual sepeda motor lamanya untuk membeli sepeda motor baru yang lebih canggih spesifikasinya  [1](https://jurnal.umk.ac.id/index.php/simet/article/view/466/501).
 
Namun untuk penentuan harga sepeda motor bekas masih mengandalkan perkiraan. Untuk memperkirakan harga motor bekas, jika ia seseorang ahli motor tentu akan mudah melakukannya sedangkan orang yang belum mengerti tentunya akan sulit untuk menentukan harga sebuah sepeda motor. Menurut penelitian Indra Prasetya (2015), untuk mengetahui sebuah harga motor bekas terdapat beberapa variabel yang menentukan [2](http://eprints.dinus.ac.id/16513/1/jurnal_15456.pdf). Namun belum diketahui varibel apa saja yang dapat digunakan untuk memprediksi harga sepeda motor. Oleh karena itu perlu adanya acuan untuk memprediksi harga sepeda motor bekas.

Referensi :
[1]	I. Sunoto dan L. Lukman, “SISTEM PENDUKUNG KEPUTUSAN PENENTUAN HARGA JUAL SEPEDA MOTOR BEKAS DENGAN PENDEKATAN LOGIKA FUZZY INFRENCE SYSTEM MAMDANI,” Simet, vol. 6, no. 2, hlm. 305, Nov 2015, doi: 10.24176/simet.v6i2.466.
[2]	I. Prasetya, D. Y. Rahayu, dan M. Kom, “PENENTUAN HARGA JUAL SEPEDA MOTOR BEKAS MENGGUNAKAN FUZZY LOGIC (METODE TSUKAMOTO) DAN IMPLEMENTASINYA,” hlm. 8.

		

## Business Understanding

### Problem Statements

Berdasarkan latar belakang yang telah dijelaskan diatas, terdapat beberapa masalah yaitu:
- Variabel apa saja yang berpengaruh dalam menentukan harga sepeda motor bekas?
- Berapa harga sepeda motor bekas dengan variabel tertentu? 

### Goals

Untuk menjawab masalah yang ada, akan dibuat model prediksi dengan tujuan sebagai berikut:
- Mengetahui korelasi variabel yang mempengaruhi harga sepeda motor.
- Membuat model *machine learning* yang dapat memprediksi harga sepeda motor bekas dengan akurat dari variabel yang ada.

### Solution statements
Solusi yang dapat dilakukan berupa:
- Melakukan EDA dari variabel yang ada dengan memvisualisasikannya menggunakan heatmap untuk melihat korelasi terhadap harga sepeda motor bekas.
- Menggunakan model *machine learning* yang bervariasi untuk memprediksi harga sepeda motor. Model yang dipakai berupa model klasifikasi, lalu dibandingkan hasil akurasinya untuk dipilih model mana yang memiliki hasil terbaik. Berikut model yang digunakan :
	- *Logistic Regression*
	- *K-Nearest Neighbors*
	- *Random Forest*

## Data Understanding
Data atau dataset yang digunakan pada proyek *machine learning* ini adalah data *Motorcycle* dataset yang didapat dari situs kaggle. Dataset ini berisikan informasi mengenai sepeda motor bekas. 
Terdapat 1061 baris dalam dataset 
Ada 7 Kolom yaitu: name, selling_price, year, seller_type, owner, km_driven, ex_showroom_price
Link dataset dapat dilihat dari tautan berikut: [Motorcycle Dataset](https://www.kaggle.com/datasets/nehalbirla/motorcycle-dataset).



### Variabel-variabel pada Motorcycle dataset adalah sebagai berikut:  
- name : merupakan jenis atau nama dari sepeda motor
- selling_price : merupakan harga ketika penjual menjual sepeda motor
- year : merupakan tahun ketika sepeda motor dibeli
- seller_type : Memberitahukan apakah Penjual adalah Perorangan atau Dealer
- owner : merupakan jumlah pemilik kendaraan sebelumnya.
- km_driven : merupakan jumlah kilometer yang telah ditempuh sepeda motor
- ex_showroom_price : merupakan harga showroom sepeda motor

Untuk memahami *Motorcycle* dataset saya menggunakan beberapa tahapan dari teknik *Explanatory Data Analysis* (EDA) sebagai berikut:
1.   Deskripsi Variabel

![Cek info dataset]( https://github.com/Muhammad-Fitroh-Amrilla/Dicoding_ML_Terapan/blob/main/Dokumentasi/info.PNG )

Gambar 1. Info dataset

Pada Gambar 1, dapat dilihat bahwa:
*   Ada 3 kolom bertipe object, yaitu name, seller_type, owner
*   Terdapat 3 kolom dengan tipe data int64, yaitu selling_price, year, km_driven 
*   Terdapat 1 kolom dengan tipe data float yaitu ex_showroom_price

2.   Menangani *missing value & outliers*
Langkah selanjutnya menggunakan salah satu teknik untuk mengatasi *missing value* yaitu mengganti *missing value* dengan nilai rata-rata. Kemudian menangani *outlier*, *outliers* adalah sampel yang nilainya sangat jauh dari cakupan umum data utama. Pada kasus ini, *outliers* akan dideteksi dengan teknik visualisasi data (boxplot). Kemudian, *ouliers* akan ditangani dengan teknik *IQR method*.

3.   Analisis *Univariate*
Fitur kategorik

![Fitur name](https://github.com/Muhammad-Fitroh-Amrilla/Dicoding_ML_Terapan/blob/main/Dokumentasi/name.PNG )

Gambar 2. Analisis fitur name

Pada Gambar 2, jenis sepeda motor terbanyak yaitu Bajaj Pulsar 150 dengan jumlah sampel sebanyak 39 sampel dan presentase 4.4 %

![Fitur seller_type](https://github.com/Muhammad-Fitroh-Amrilla/Dicoding_ML_Terapan/blob/main/Dokumentasi/seller.PNG )

Gambar 3. Analisis fitur seller_type

Pada Gambar 3, dapat diketahui bahwa 876 penjual sepeda motor merupakan perorangan dan 4 diantaranya merupakan dealer

![Fitur owner](https://github.com/Muhammad-Fitroh-Amrilla/Dicoding_ML_Terapan/blob/main/Dokumentasi/owner.PNG )

Gambar 4. Analisis fitur owner

Pada Gambar 4, dapat dilihat bahwa sebanyak 87.6 % sepeda motor hanya dimiliki oleh orang pertama, 11.5 % dimiliki sampai dengan orang kedua dan yang terkahir 0.9 % sepeda motor dimiliki sampai dengan orang ketiga.

Fitur Numerik

![Fitur numerik](https://github.com/Muhammad-Fitroh-Amrilla/Dicoding_ML_Terapan/blob/main/Dokumentasi/Univariate_numerik.PNG )

Gambar 5. Analisis fitur numerik

Pada Gambar 5, dapat dilihat bahwa :
* Rentang harga jual sepeda motor dari ratusan dollar sampai dengan 130000 Dollar
* Jumlah terbanyak sepeda motor yang dijual berada di rentang harga 20000-40000 Dollar


4.   Analisis *Multivariate* 
Fitur Kategorik

![Fitur numerik](https://github.com/Muhammad-Fitroh-Amrilla/Dicoding_ML_Terapan/blob/main/Dokumentasi/Multivariate_kategorik.PNG )

Gambar 6. Analisis *multivariate* fitur kategorik

Pada gambar 6, dapat dilihat bahwa
*   Kategori dalam fitur name terlalu banyak sehingga fitur name tidak mempengaruhi fitur selling_price
*   Pada fitur seller_type , individual merupakan yang paling tinggi dalam seller_type memiliki harga rendah. Sehingga fitur seller_type memiliki dampak yang kecil terhadap rata-rata harga jual
*   Pada fitur owner rata-rata harga cenderung mirip. Rentangnya berada antara 35000 hingga 45000. Sehingga, fitur cut memiliki pengaruh atau dampak yang kecil terhadap rata-rata harga jual.

Fitur Numerik

![Fitur numerik](https://github.com/Muhammad-Fitroh-Amrilla/Dicoding_ML_Terapan/blob/main/Dokumentasi/Multivariate_numerik.PNG)

Gambar 7. Analisis *multivariate* fitur numerik

Dapat kita lihat bahwa :
*   selling_price memiliki korelasi positip terhadap variabel year dan ex_showroom_price
*   sedangkan variabel km_driven memiliki korelasi negatif terhadap selling_price

*Correlation matrix* untuk fitur numerik

![Correlation Matrix](https://github.com/Muhammad-Fitroh-Amrilla/Dicoding_ML_Terapan/blob/main/Dokumentasi/Corrmap.PNG)

Gambar 8. *Correlation matrix* fitur numerik

Pada Gambar 8, dapat dilihat matriks korelasi diatas, korelasi fitur year dan ex_showroom_price terhadap fitur selling_price berada pada rentang cukup (0.25 - 0.5) dan fitur yang memiliki korelasi paling tinggi terhadap fitur selling_price yaitu year sebesar 0.58

## Data Preparation
Dalam *data preparation*, 3 hal yang akan dilakukan sebelum memasukkan data ke model latih:

- *Encoding* Fitur Kategorik : *Encoding* fitur kategorik dilaksanakan di beberapa fitur yang bertipe *object*. Hal ini dilakukan karena model *machine learning* hanya dapat menerima data dalam bentuk numerik. Untuk *encoding* fitur menggunakan *LabelEncoder*.
- *Train-Test-Split* : Membagi dataset menjadi data latih dan data uji dengan perbandingan 90:10 yaitu 90 persen data akan menjadi data latih dan 10 persen data akan menjadi data uji . Hal ini dilakukan supaya kita dapat melakukan validasi dengan benar tanpa bias dari model.
- *Standarisasi* : Standarisasi menggunakan teknik *StandarScaler* dari *library Scikitlearn*. *StandardScaler* melakukan proses standarisasi fitur dengan mengurangkan mean (nilai rata-rata) kemudian membaginya dengan standar deviasi untuk menggeser distribusi.  *StandardScaler* menghasilkan distribusi dengan standar deviasi sama dengan 1 dan mean sama dengan 0. *Scaling* ini dilaksanakan untuk membantu model *machine learning* yang akan dipakai lebih mudah diolah. 

## Modeling

Pada tahap ini, model *machine learning* yang akan dipakai ada tiga algoritma. Lalu performa masing-masing algoritma akan dievaluasi dan menentukan algoritma mana yang memberikan hasil prediksi terbaik. Ketiga algoritma yang akan digunakan, antara lain:

1.   *K-Nearest Neighbors* (KNN) : KNN bekerja dengan membandingkan jarak satu sampel ke sampel pelatihan lain dengan memilih sejumlah k tetangga terdekat (dengan k adalah sebuah angka positif)
		- **kelebihan** : algoritma KNN yaitu mudah dipahami dan digunakan serta algoritma yang relatif sederhana dibandingkan dengan algoritma lain.
		- **kekurangan** : jika dihadapkan pada jumlah fitur atau dimensi yang besar
2.   *Random Forest* : Algoritma ini disusun dari banyak algoritma pohon (*decision tree*) yang pembagian data dan fiturnya dipilih secara acak.
		- **kelebihan** : Kuat terhadap data *outlier* (pencilan data), berjalan secara efisien pada kumpulan data yang besar, dan bekerja dengan baik dengan data non-linear.
		- **kekurangan** : Pembelajaran bisa berjalan lambat, tergantung pada parameter yang digunakan dan tidak bisa memperbaiki model yang dihasilkan secara berulang.
3.   *Boosting Algorithm* : Algoritma yang menggunakan teknik *boosting* bekerja dengan membangun model dari data latih. Kemudian ia membuat model kedua yang bertugas memperbaiki kesalahan dari model pertama. Model ditambahkan sampai data latih terprediksi dengan baik atau telah mencapai jumlah maksimum model untuk ditambahkan.
		- **kelebihan** : Algoritma ini sangat *powerful* dalam meningkatkan akurasi prediksi. Algoritma *boosting* sering mengungguli model yang lebih sederhana seperti *logistic regression* dan *random forest*
		- **kekurangan** : *Learning* secara progresif dan sangat sensitif terhadap data *noise* dan *outlier*.

*Error* dari masing-masing model:

![Visualisasi Error](https://github.com/Muhammad-Fitroh-Amrilla/Dicoding_ML_Terapan/blob/main/Dokumentasi/msevis.PNG)

Dapat diliat bahwa model *Random Forest* memiliki nilai *error* yang lebih kecil dibanding model lain menandakan bahwa model *Random Forest* merupakan model terbaik yang dapat digunakan untuk memprediksi harga jual sepeda motor bekas.

## Evaluation
Metrik yang akan kita gunakan pada prediksi ini adalah MSE atau *Mean Squared Error* yang menghitung jumlah selisih kuadrat rata-rata nilai sebenarnya dengan nilai prediksi. MSE didefinisikan dalam persamaan berikut

![Rumus MSE](https://github.com/Muhammad-Fitroh-Amrilla/Dicoding_ML_Terapan/blob/main/Dokumentasi/rumusMSE.jpg)

Dimana :

At = Nilai Aktual permintaan

Ft = Nilai hasil peramalan

n = banyaknya data

berikut adalah hasil evaluasi ketiga model menggunakan mse:

![Visualisasi Error](https://github.com/Muhammad-Fitroh-Amrilla/Dicoding_ML_Terapan/blob/main/Dokumentasi/mse.PNG)

Gambar 9. Visualisasi mse

Pada Gambar 9, dapat diliat bahwa model *Random Forest* memiliki nilai *error* yang lebih kecil dibanding model lain pada data latih dan data uji.

Hasil prediksi masing-masing model dari 10 data:

![Hasil Prediksi](https://github.com/Muhammad-Fitroh-Amrilla/Dicoding_ML_Terapan/blob/main/Dokumentasi/pred.PNG)

Dapat kita lihat bahwa prediksi dari ketiga algoritma yang paling mendekati y_true adalah prediksi *Random Forest* menandakan bahwa *Random Forest* merupakan algoritma terbaik dibandingkan dengan algoritma yang lain.


**---Ini adalah bagian akhir laporan---**


