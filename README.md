# Laporan Proyek Machine Learning - Sri Soerya N
Domain Proyek
# Latar Belakang
Perumahan di India bervariasi dari istana-istana bekas maharaja hingga bangunan apartemen modern di kota-kota besar hingga gubuk-gubuk kecil di desa-desa yang jauh. Telah terjadi pertumbuhan luar biasa di sektor perumahan India karena pendapatan telah meningkat. Inisiatif Pengukuran Hak Asasi Manusia menemukan bahwa India melakukan 60,9% dari apa yang seharusnya dimungkinkan pada tingkat pendapatannya untuk hak atas perumahan.
Menyewa, juga dikenal sebagai menyewa atau membiarkan, adalah perjanjian di mana pembayaran dilakukan untuk penggunaan sementara barang, jasa, atau properti milik orang lain. Sewa kotor adalah ketika penyewa membayar jumlah sewa tetap dan pemilik membayar semua biaya properti yang secara teratur dikeluarkan oleh kepemilikan. Menyewa bisa menjadi contoh ekonomi berbagi.
# Business Understanding
Proyek ini dibangun untuk perusahaan dengan karakteristik bisnis sebagai berikut :
1. Perusahaan memiliki atau membeli rumah dan apartemen kemudian menyewanya ke konsumen.
2. Perusahaan membuka jasa konsultasi harga sewa rumah dan apartemen ke konsumen.
# Problem Statement
1. Fitur apa yang paling berpengaruh terhadap harga sewa rumah atau apartemen?
2. Bagaimana cara memproses data agar dapat dilatih dengan baik oleh model?
3. Berapa harga sewa rumah di pasaran berdasarkan karakteristik tertentu?
# Goals
1. Mengetahui fitur yang paling berpengaruh pada harga sewa rumah atau apartemen.
2. Melakukan persiapan data untuk dapat dilatih oleh model.
3. Membuat model machine learning yang dapat memprediksi harga sewa rumah seakurat mungkin berdasarkan karakteristik tertentu.
# Solution Statement
Menganalisis data dengan melakukan univariate analysis dan multivariate analysis. Memahami data juga dapat dilakukan dengan visualisasi. Memahami data dapat membantu untuk mengetahui kolerasi antar fitur dan mendeteksi outlier.
Menyiapkan data agar bisa digunakan dalam membangun model.
Melakukan hyperparameter tuning menggunakan grid search dan membangun model regresi yang dapat memprediksi bilangan kontinu. ALgoritma yang dipakai dalam proyek ini adalah K-Nearest Neighbour, Random Forest, dan AdaBoost.
# Data Understanding & Removing Outlier
Dataset yang digunakan dalam proyek ini merupakan data harga sewa rumah dengan berbagai karakteristik di India. Dataset ini dapat diunduh di Kaggle : House Rent Prediction Dataset.
Berikut informasi pada dataset :
Dataset memiliki format CSV (Comma-Seperated Values).
Dataset memiliki 4746 sample dengan 12 fitur.
Dataset memiliki 4 fitur bertipe int64 dan 8 fitur bertipe object.
Tidak ada missing value dalam dataset.
# Variable - variable pada dataset
Posted On: Tanggal data diposting.
BHK: Jumlah dari kamar tidur, aula, dan dapur.
Rent: Harga sewa dari rumah/apartemen.
Size: Luas dari rumah/apartemen dalam square feet (sqft).
Floor: Letak dan jumlah lantai rumah/apartemen.
Area Type: Ukuran dari rumah dalam kategori Super Area atau Carpet Area atau Build Area.
Area Locality: Lokasi rumah/apartemen.
City: Kota dimana rumah/apartemen berada.
Furnishing Status: Status perabotan rumah/apartemen, baik Furnished atau Semi-Furnished atau Unfurnished.
Tenant Preferred: Jenis penyewa yang diutamakan pemilik atau agen.
Bathroom: Jumlah kamar mandi.
Point of Contact: Kontak yang dihubungi untuk informasi lebih lanjut mengenai rumah/apartemen.
Dari ke 12 fitur dapat dilihat bahwa fitur Point of Contract dan Posted On tidak mempengaruhi harga sewa rumah sehingga akan dihapus. Hal ini dikarenakan kedua fitur tersebut tidak diperlukan dalam membangun model prediksi harga sewa.
# EDA
# Univariate Analysis
Univariate Analysis adalah menganalisis setiap fitur secara terpisah.
Analisis jumlah nilai unique pada setiap fitur kategorik
Fitur kategorik City, Furnishing Status, dan Tenant Preferred memiliki sebaran sample yang cukup merata.
Berikut adalah fitur dengan sample yang tidak merata :
- Area Type
Hanya terdapat 2 sample Built Area pada fitur Area Type. Untuk menghindari high dimensional data, maka kedua sample ini akan dihapus.
- Floor dan Area Locality
Fitur Floor dan Area Locality memiliki banyak sekali nilai unique. Untuk menghindari high dimensional data, maka kedua fitur ini akan dihapus.
Analisis sebaran pada setiap fitur numerik
Berikut analisis dari grafik di atas :
Sebagian besar rumah memiliki 1 sampai 3 BHK dan 1 sampai 3 kamar mandi.
Sebagian besar rumah memiliki luas di bawah 2000 sqft.
Rentang harga sewa cukup tinggi, yaitu dari 1200 hingga 3500000. Namun, rata-rata harga rumah hanya 35003. Distribusi harga yang kurang bagus seperti ini dapat berimplikasi pada model.
Multivariate Analysis
Multivariate Analysis menunjukkan hubungan antara dua atau lebih fitur dalam data.

Analisis fitur numerik
Fitur Size dan BHK (Menghapus BHK Outlier) Kedua fitur ini dianalisis karena tidak biasa untuk rumah dengan 1 BHK memiliki luas 100 sqft. Untuk itu ditentukan treshold atau batas 300 sqft/bhk. Data yang berada di bawah batas akan dihapus. Hal ini menyebabkan berkurangnya jumlah sample sebesar 548.

Fitur Size dan Rent (Menghapus Price per sqft Outlier) Untuk memudahkan dalam mendeteksi outlier, maka dibuat fitur baru 'Price_per_sqft' dari kedua fitur tersebut untuk menganalisis harga sewa per luas sqft.
Dari sini dapat terlihat bahwa harga 571 per sqft sangat rendah dan harga 1400000 per sqft sangat tinggi. Untuk itu penghapusan outlier price per sqft outlier dengan mean dan one standard deviation yang telah dikelompokkan berdasarkan kota. Hal ini menyebabkan berkurangnya jumlah sample sebesar 497.
- Fitur Bathroom dan BHK (Menghapus Bathroom Outlier) Kedua fitur ini dianalisis karena tidak biasa untuk rumah dengan 2 BHK memiliki 4 kamar mandi. Untuk itu ditentukan batas bahwa jumlah kamar mandi tidak boleh melebihi jumlah BHK + 2. Hal ini menyebabkan berkurangnya sample sebesar 3.

- Melihat kolerasi antara semua fitur numerik
Fitur BHK, Size, dan Bathroom berkorelasi tidak signifikan dengan fitur target (Rent). Hal ini mungkin disebabkan oleh kurangnya data dalam penelitian ini.Fitur BHK dan Bathroom berkolerasi signifikan dengan fitur size. Hal ini sudah sesuai harapan dari penghapusan outlier yang sudah dilakukan sebelumnya.
Analisis fitur kategorik
Analisis ini dilakukan untuk melihat kolerasi antara fitur kategorik dengan fitur target (Rent).
-Fitur Area Type
Fitur Area Type memiliki pengaruh yang kecil terhadap rata-rata harga sewa.
-Fitur City
Fitur City memiliki pengaruh cukup besar terhadap rata-rata harga sewa, terutama jika rumah berada di kota Mumbai. Hal ini dibuktikan dengan sebaran rumah yang mencapai harga tertinggi di kota Mumbai. Mumbai merupakan kota paling mahal di India untuk ditinggali, diikuti dengan Delhi.
-Fitur Furnishing Status
Fitur Furnishing Status memiliki pengaruh cukup besar terhadap rata-rata harga sewa. Merupakan hal biasa bila rumah yang memiliki perabotan lengkap akan diberi harga sewa lebih tinggi daripada rumah tanpa perabotan.
-Fitur Tenant Preferred
Fitur Tenant Preferred memiliki pengaruh yang lumayan terhadap rata-rata harga sewa. Dari grafik dapat terlihat bahwa rumah yang sangat disarankan untuk disewa oleh keluarga memiliki rata-rata harga sewa yang lebih mahal dibanding lainnya.
# Data preparation
One Hot Encoding
One hot encoding adalah teknik mengubah data kategorik menjadi data numerik dimana setiap kategori menjadi kolom baru dengan nilai 0 atau 1. Fitur yang akan diubah menjadi numerik pada proyek ini adalah Area Type, City, Furnishing Status, dan Tenant Preferred.

Train Test Split
Train test split aja proses membagi data menjadi data latih dan data uji. Data latih akan digunakan untuk membangun model, sedangkan data uji akan digunakan untuk menguji performa model. Pada proyek ini dataset sebesar 3696 dibagi menjadi 3511 untuk data latih dan 185 untuk data uji.

Normalization
Algoritma machine learning akan memiliki performa lebih baik dan bekerja lebih cepat jika dimodelkan dengan data seragam yang memiliki skala relatif sama. Salah satu teknik normalisasi yang digunakan pada proyek ini adalah Standarisasi dengan sklearn.preprocessing.StandardScaler.

# Modeling
Algoritma Penelitian ini melakukan pemodelan dengan 3 algoritma, yaitu K-Nearest Neighbour, Random Forest, dan Adaboost

K-Nearest Neighbour K-Nearest Neighbour bekerja dengan membandingkan jarak satu sampel ke sampel pelatihan lain dengan memilih sejumlah k tetangga terdekat. Proyek ini menggunakan sklearn.neighbors.KNeighborsRegressor dengan memasukkan X_train dan y_train dalam membangun model. Parameter yang digunakan pada proyek ini adalah :

n_neighbors = Jumlah k tetangga tedekat.

Kelebihan
Dapat menerima data yang masih noisy
Sangat efektif apabila jumlah datanya banyak
Mudah diimplementasikan

Kekurangan
Sensitif pada outlier
Rentan pada fitur yang kurang informatif

Random Forest Algoritma random forest adalah teknik dalam machine learning dengan metode ensemble. Teknik ini beroperasi dengan membangun banyak decision tree pada waktu pelatihan. Proyek ini menggunakan sklearn.ensemble.RandomForestRegressor dengan memasukkan X_train dan y_train dalam membangun model. Parameter yang digunakan pada proyek ini adalah :

n_estimators = Jumlah maksimum estimator di mana boosting dihentikan.
max_depth = Kedalaman maksimum setiap tree.
random_state = Mengontrol seed acak yang diberikan pada setiap base_estimator pada setiap iterasi boosting.
Kelebihannya 
Dapat mengatasi noise dan missing value
Dapat mengatasi data dalam jumlah yang besar

Kelemahan 
Interpretasi yang sulit 
Membutuhkan tuning model yang tepat untuk data

AdaBoost juga disebut Adaptive Boosting adalah teknik dalam machine learning dengan metode ensemble. Algoritma yang paling umum digunakan dengan AdaBoost adalah pohon keputusan (decision trees) satu tingkat yang berarti memiliki pohon Keputusan dengan hanya 1 split. Pohon-pohon ini juga disebut Decision Stumps. Algoritma ini bertujuan untuk meningkatkan performa atau akurasi prediksi dengan cara menggabungkan beberapa model sederhana dan dianggap lemah (weak learners) secara berurutan sehingga membentuk suatu model yang kuat (strong ensemble learner). Proyek ini menggunakan sklearn.ensemble.AdaBoostRegressor dengan memasukkan X_train dan y_train dalam membangun model. Parameter yang digunakan pada proyek ini adalah :

n_estimators = Jumlah maksimum estimator di mana boosting dihentikan.
learning_rate = Learning rate memperkuat kontribusi setiap regressor.
random_state = Mengontrol seed acak yang diberikan pada setiap base_estimator pada setiap iterasi boosting.
Kelebihan 
relatif lebih mudah untuk diimplementasikan dan waktu
pengujian yang relatif cepat sehingga cocok dipakai dalam
implementasi kondisi real time
Kelemahan
Pendekatan ini tidak berfungsi dengan baik ketika ada korelasi antara fitur atau dimensi data yang tinggi.

# Hyperparameter Tuning (Grid Search) 
Hyperparameter tuning adalah cara untuk mendapatkan parameter terbaik dari algoritma dalam membangun model. Salah satu teknik dalam hyperparameter tuning yang digunakan dalam proyek ini adalah grid search. Berikut adalah hasil dari Grid Search pada proyek ini :

model	best_params
knn	{'n_neighbors': 7}
boosting	{'learning_rate': 0.1, 'n_estimators': 100, 'random_state': 11}
rf	{'max_depth': 8, 'n_estimators': 25, 'random_stste': 11}

# Evaluation
Metrik evaluasi yang digunakan pada proyek ini adalah akurasi dan mean squared error (MSE). Akurasi menentukan tingkat kemiripan antara hasil prediksi dengan nilai yang sebenarnya (y_test). Mean squared error (MSE) mengukur error dalam model statistik dengan cara menghitung rata-rata error dari kuadrat hasil aktual dikurang hasil prediksi. Berikut formulan MSE :
![188412654-f5dc0ae1-901b-470e-aae5-1f6b5fb68b4d](https://user-images.githubusercontent.com/108644038/202385245-87d6932e-d8a7-428e-8d90-8ac0850a216d.png)

Berikut hasil evaluasi pada proyek ini :
Akurasi
model	accuracy
knn	0.726775
boosting	0.898556
rf	0.932057
Mean Squared Error (MSE)
![188413846-7d5454b5-7f83-488e-836f-4f3593eb3d5d](https://user-images.githubusercontent.com/108644038/202385385-e7b44f0f-3986-4fa0-836d-e34893d17787.png)

Dari hasil evaluasi dapat dilihat bahwa model dengan algoritma Random Forest memiliki akurasi lebih tinggi tinggi dan tingkat error lebih kecil dibandingkan algoritma lainnya dalam proyek ini.
