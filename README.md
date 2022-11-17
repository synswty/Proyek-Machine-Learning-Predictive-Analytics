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
