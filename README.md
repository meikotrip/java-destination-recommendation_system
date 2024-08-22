# Laporan Proyek Machine Learning - Muhamad Meiko Triputra

## Project Overview

Pulau Jawa merupakan salah satu destinasi wisata terpopuler di Indonesia dengan berbagai pilihan tempat wisata yang meliputi alam, budaya, kuliner, dan sejarah. Namun, dengan banyaknya pilihan, wisatawan seringkali kesulitan menentukan destinasi yang sesuai dengan preferensi mereka. Oleh karena itu, diperlukan sistem rekomendasi yang dapat membantu wisatawan menemukan destinasi yang paling cocok berdasarkan preferensi individu dan pengalaman pengguna lain.

Dalam sebuah artikel ilmiah berjudul [Analisis Faktor-Faktor yang Mempengaruhi Keputusan Pemilihan Destinasi Wisata bagi Wisatawan Domestik Nusantara](https://jurnal.darmajaya.ac.id/index.php/jmmd/article/view/364/352) diketahui bahwasannya terdapat banyak sekali faktor yang mempengaruhi keputusan penentuan destinasi wisata oleh wisatawan. Dengan banyaknya faktor yang harus dipertimbangkan oleh wisatawan membuat penyelenggara/stakeholder kepariwisataan harus lebih peka untuk membantu wisatawan dalam menentukan pilihannya. Diharapkan dengan proyek yang dibangun ini dapat memudahkan wisatawan dalam menentukan destinasi wisatanya dan memfasilitasi penyelenggara/stakeholder kepariwisataan dalam mengembangkan bisnisnya

## Business Understanding

Pulau Jawa menjadi tujuan favorit bagi wisatawan lokal maupun internasional karena kekayaan dan variasi destinasi yang dimilikinya. Namun, dengan banyaknya pilihan yang tersedia, wisatawan seringkali menghadapi tantangan dalam memilih destinasi yang sesuai dengan preferensi dan kebutuhan mereka. Penyedia jasa pariwisata dan badan pariwisata lokal menghadapi tantangan untuk meningkatkan pengalaman wisatawan, memperpanjang durasi kunjungan, dan menarik lebih banyak pengunjung ke destinasi yang mungkin kurang populer namun memiliki potensi besar. Di tengah persaingan yang ketat, penyedia layanan pariwisata perlu memahami preferensi wisatawan dengan lebih baik dan menawarkan rekomendasi yang tepat untuk meningkatkan kepuasan dan loyalitas pelanggan.

Bagian laporan ini mencakup:

### Problem Statements

Berdasarkan kondisi yang telah diuraikan diatas, Kami mengembangkan sebuah proyek untuk prediksi harga laptop untuk menjawab permasalahan berikut.
- Berdasarkan data mengenai pengguna dan destinasi wisata, bagaimana membuat sistem rekomendasi yang dipersonalisasi dengan teknik content-based filtering?
- Dengan data rating yang dimiliki, bagaimana penyelenggara/stakeholder dapat merekomendasikan destinasi wisata lain yang mungkin disukai dan belum pernah dikunjungi oleh pengguna?

### Goals

Untuk  menjawab pertanyaan tersebut, buatlah sistem rekomendasi dengan tujuan atau goals sebagai berikut:
- Menghasilkan sejumlah rekomendasi destinasi wisata yang dipersonalisasi untuk pengguna dengan teknik content-based filtering.
- Menghasilkan sejumlah rekomendasi destinasi wisata yang sesuai dengan preferensi pengguna dan belum pernah dikunjungi sebelumnya dengan teknik user-based collaborative filtering.

### Solution statements
Solusi yang diberikan yaitu dengan :
- Dalam membangun model sistem rekomendasi dengan content-based filtering dilakukan penggabungan fitur yang diperlukan menggunakan hstack dalam mendapatkan rekomendasi seperti fitur numeric (price, time_minutes, rating) dengan standarisasi dan fitur categoric (category, city) dengan TF-IDF Vectorizer
- Dalam membangun model sistem rekomendasi dengan user-based collaborative filtering menggunakan pendekatan deep learning yaitu Neural Collaborative Filtering (NCF) mengguanakan layer Embedding. 

## Data Understanding
Data yang digunakan pada proyek kali ini adalah [Indonesia Tourism Destination](https://www.kaggle.com/datasets/aprabowo/indonesia-tourism-destination/data) yang dapat dibuka dan diunduh pada link tersebut. Dataset terdiri dari 4 file dengan detail informasi sebagai berikut:
- package_tourism.csv: merupakan file yang berisi paket-paket destinasi tempat wisata yang ditawarkan dari berbagai kota. Pada file ini memiliki jumlah data sebanyak 100 dengan 7 fitur yaitu Package, City, Place_Tourism1, Place_Tourism2, Place_Tourism3, Place_Tourism4, dan Place_Tourism5. Nilai setiap baris terhadap setiap kolom tidak semuanya diisi. File ini tidak ada tautan dengan file lain. Fitur Package berisi kode paket dengan tipe data integer, fitur City berisi 5 kota besar yang ada di pulau Jawa, Place_Torism1 hingga Place_Tourism5 berisi setiap nama destinasi yang ditawarkan paket pada kota tersebut dengan tipe data obejct.
- tourism_rating.csv: merupakan file yang berisi rating yang diberikan user terhadap destinasi tempat wisata. Pada file ini memiliki jumlah data sebanyak 10000 dengan 3 fitur yaitu User_Id, Place_Id, dan Place_Ratings. Setiap baris memiliki nilai terhadap setiap kolomnya (tidak ada missing value). File ini memiliki tautan dengan file yaitu dengan file tourism_with_id.csv pada field 'Place_Id' dan file user.csv pada field 'User_Id'. Fitur User_Id berisi id user dengan tipe data integer, fitur Place_Id berisi id destinasi wisata dengan tipe data integer, dan fitur Place_Ratings berisi rating terhadap destinasi tempat wisata dengan tipe data integer.
- tourism_with_id.csv: merupakan file yang berisi destinasi tempat-tempat wisata dengan karakteristiknya. Pada file ini memiliki jumlah data sebanyak 437 dengan 13 fitur yaitu Place_Id, Place_Name, Description, Category, City, Price, Rating, Time_Minutes, Coordinate, Lat, Long, Unnamed: 11 dan Unnamed: 12. Terdapat beberapa fitur yang memiliki missing values(fitur Time_Minutes) dan fitur yang tidak relevan(fitur Unnamed:11 dan Unnamed:12). File ini memiliki tautan dengan file yaitu dengan file tourism_rating.csv pada field 'Place_Id'. Fitur Place_Id berisi id destinasi wisata dengan tipe data integer, fitur Place_Name berisi nama destinasi wisata dengan tipe data object, fitur Description berisi deskripsi destinasi tempat wisata dengan tipe data object, fitur Category berisi kategori destinasi wisata dengan tipe data object, fitur City berisi Kota destinasi wisata dengan tipe data object, fitur Price berisi tiket masuk destinasi wisata dengan tipe data integer, fitur Rating berisi rating destinasi wisata dengan tipe data float, fitur Time_Minutes berisi lama waktu destinasi wisata dengan tipe data float, fitur Coordinate berisi koordinat destinasi wisata dengan tipe data object, fitur Lat berisi koordinat latitude destinasi wisata dengan tipe data float, fitur Long berisi koordinat longitude destinasi wisata dengan tipe data float, Unnamed: 11 dan Unnamed: 12 yang merupakan fitur tidak relevan dengan tipe data float dan integer.
- user.csv: merupakan file yang berisi informasi tentang user. Pada file ini memiliki jumlah data sebanyak 300 dengan 3 fitur yaitu User_Id, Location, dan Age. Setiap baris memiliki nilai terhadap setiap kolomnya (tidak ada missing value). File ini memiliki tautan dengan file yaitu dengan file tourism_rating.csv pada field 'User_Id'. Fitur User_Id berisi id user dengan tipe data integer, fitur Location berisi asal daerah user dengan tipe data object, dan fitur Age berisi usia user dengan tipe data integer.

Beberapa insight yang diperoleh dari hasil exploratory data analysis yaitu sebagai berikut:
- Terdapat 6 kategori destinasi wisata, kategori terbanyak yaitu Taman Hiburan dengan jumlah lebih dari 130 data dan kategori tersedikit yaitu Pusat Perbelanjaan dengan jumlah kurang dari 15 data
- Terdapat 5 kota besar, urutan kota dengan destinasi terbanyak hingga tersedikit yaitu kota yogyakarta, bandung, jakarta, semarang dan surabaya
- 4 Destinasi dengan rating tertinggi yaitu Freedom Library, Desa Wisata Sungai Code Jogja Kota, Kauman Pakualam Yogyakarta, Wisata Kuliner Pecenongan memiliki rating 5/5
- Pengguna terbanyak yang melakukan rating berasal dari provinsi Jawa Barat
- Pengguna yang melakukan rating memiliki distribusi umur 18 hingga 40 tahun

## Data Preparation
Beberapa yang dilakukan dalam menyiapkan data untuk model yaitu dengan:

### Untuk Pengembangan model Content-based Filtering
#### Menggabungkan rating dengan fitur-fitur pada destinasi
Menggabungkan rating dengan fitur-fitur pada destinasi adalah proses mengintegrasikan data rating yang diberikan oleh pengguna dengan informasi fitur-fitur lain yang dimiliki oleh setiap destinasi wisata. Hal ini bertujuan untuk memperkaya dataset dengan informasi yang lebih lengkap, sehingga model rekomendasi dapat mempelajari pola preferensi pengguna dengan lebih baik. Fitur yang dapat digabungkan meliputi kategori destinasi, harga, durasi kunjungan (time_minutes), lokasi (city), dan rating. Data yang digabungkan ini akan digunakan sebagai input bagi model rekomendasi untuk memberikan saran destinasi wisata yang sesuai dengan preferensi pengguna.

#### Pengecekan fitur kategorikal
Pengecekan fitur kategorikal adalah proses untuk memastikan bahwa fitur-fitur yang bersifat kategorikal telah teridentifikasi dengan benar sebelum dilakukan proses encoding. Fitur kategorikal adalah fitur yang memiliki nilai dalam bentuk kategori atau label, seperti 'Category' (kategori wisata) dan 'City' (kota). Dalam proyek ini, penting untuk memeriksa apakah semua fitur kategorikal sudah benar dan konsisten dalam formatnya sebelum menerapkan teknik encoding seperti OneHotEncoder. Pengecekan ini dapat dilakukan dengan menggunakan fungsi value_counts() atau unique() pada setiap fitur kategorikal untuk melihat distribusi nilai kategori dan memastikan tidak ada nilai yang salah atau tidak sesuai.

#### Mengubah nilai pada fitur 'Category' dengan snake case style
Mengubah nilai pada fitur 'Category' dengan snake case style adalah proses mengubah nama kategori dalam fitur 'Category' agar sesuai dengan format snake case (huruf kecil dengan pemisah underscore). Snake case digunakan untuk membuat nama kategori lebih konsisten dan mudah diproses dalam analisis data dan pemodelan. Langkah ini penting untuk memastikan bahwa nama kategori tidak mengandung spasi atau karakter khusus yang dapat menyebabkan masalah saat data digunakan dalam model machine learning.

#### Melakukan Konsolidasi Data dengan group berdasarkan 'Place_Id'
Langkah ini bertujuan untuk menggabungkan data yang memiliki Place_Id yang sama. Ini dilakukan agar setiap tempat wisata memiliki satu entri tunggal, yang mencakup informasi gabungan dari seluruh rating pengguna. Misalnya, jika terdapat beberapa entri untuk satu tempat wisata yang sama, entri-entri tersebut akan digabungkan menjadi satu baris, dan informasi seperti kategori, rating, dan lainnya dapat digabungkan atau dirata-ratakan sesuai kebutuhan. Selain itu juga setelah konsolidasi dilakukan penggabungan fitur Category dan City menjadi satu fitur Category_City.

#### Mengkonversi fitur-fitur kedalam list
fitur-fitur yang telah dilakukan konsolidasi selanjutnya di convert dalam list. Hal ini karena dengan struktur yang lebih simple dan homogen serta memiliki fleksibilitas tinggi untuk merubah elemen didalamnya menjadi alasan untuk memudahkan dalam proses model rekomendasi yang kita buat.

#### Ekstraksi data dengan TF-IDF Vecorizer
fitur Category_City yang telah digabung sebelumnya dilakukan ekstraksi dengan TF-IDF Vectorizer. dari hasil ekstrasi data didapatkan 27 fitur berdasarkan kategori destinasi wisata dan asal kotanya. Fitur ini akan digabungkan dengan fitur numerikal lainnya untuk pengembangan model rekomendasi content-based filtering dengan cosine similarity.

#### Standarisasi fitur numerikal
Standarisasi dilakukan untuk memastikan bahwa fitur numerik seperti Rating, Price, dan Time_Minutes berada dalam skala yang sama. Ini penting agar model tidak terlalu condong pada fitur dengan rentang nilai yang lebih besar. Fitur ini akan digabungkan dengan fitur kategorikal (Category_City) untuk pengembangan model rekomendasi content-based filtering dengan cosine similarity.

### Untuk Pengembangan model User-based Collaborative Filtering
#### Melakukan encoding untuk fitur User_Id dan Place_Id pada file rating dan menyimpan fitur baru.
fitur-fitur pada file rating seperti User_Id dan Place_Id dilakukan proses encoding yang hasilnya dimasukkan kedalam fitur baru yaitu fitur 'user' dan 'destination'

#### Pembagian Data menjadi train dan val
langkah selanjutnya adalah membagi data menjadi set training dan validation untuk melatih dan mengevaluasi model. dilakukan pemisahan pada data dengan x berupa fitur 'user' dan 'destination' dan y berupa fitur 'Place_Ratings' yang sebelumnya sudah di normalisasi nilainya. variabel x dan y tersebut kemudian dibagi dengan proposi 80% data training dan 20% data validasi.

## Modeling
Pada tahap modeling, terdapat dua sistem rekomendasi yang dibangun yaitu Content-based Filtering dan User-based Collaborative Filtering.

### Content-based Filtering
Dalam metode ini, rekomendasi diberikan berdasarkan kemiripan antara destinasi wisata yang pernah dinilai atau dikunjungi oleh pengguna dengan destinasi lainnya yang belum pernah dikunjungi. Sistem ini menganalisis fitur-fitur deskriptif seperti fitur category_city, dan fitur numerik seperti harga, durasi kunjungan (time_minutes), rating dari destinasi wisata yang telah digabungkan.

Kelebihan:
- Tidak memerlukan data dari pengguna lain; hanya memerlukan informasi tentang item dan preferensi pengguna.
- Dapat merekomendasikan item baru yang belum pernah diberi rating oleh pengguna lain.
- Pengguna memiliki kendali lebih besar atas hasil rekomendasi berdasarkan preferensi yang diketahui.

Kekurangan:
- Terbatas pada item yang mirip dengan yang sudah pernah dipilih pengguna, sehingga rekomendasi cenderung monoton.
- Kesulitan dalam menangkap selera yang lebih kompleks atau berubah-ubah dari pengguna.
- Membutuhkan deskripsi item yang detail dan relevan untuk bekerja dengan baik.

Langkah-langkah pengembangan model dengan pendekatan Content-based Filtering yaitu sebagai berikut:
- Membangun Model: Dengan menggunakan fitur-fitur yang telah dilakukan preparation sebelumnya, dilakukan pengembangan model yang menghitung kemiripan antara destinasi wisata yang telah dikunjungi dan destinasi lainnya menggunakan metode  cosine similarity. Vector atau matrix satu destinasi wisata dihitung kedekatan sudutnya dengan vector atau matrix destinasi wisata yang lain.
- Mendapatkan Rekomendasi: Berdasarkan kemiripan yang telah dihitung dari kedekatan sudutnya (cosine similarity), sistem menghasilkan top-N rekomendasi destinasi wisata yang paling mirip dengan destinasi yang telah dinilai oleh pengguna. Hasil rekomendasi ini menampilkan nama destinasi beserta fitur-fitur relevan lainnya.

Hasil dari sistem rekomendasi content-based filtering yaitu ketika dilakukan pencarian rekomendasi destinasi wisata yang mirip dengan destinasi wisata 'Monumen Nasional'. Dari hasil itu diberikan 3 rekomendasi destinasi wisata yaitu 'Monumen Selamat Datang', 'Museum Tekstil', dan 'Museum Sasmita Loka Ahmad Yani' yang mana jika dilihat secara langsung saja dari tiap-tiap fitur yang dibandingkan, didapatkan bahwa ketiga rekomendasi ini memiliki kesamaan fitur yang tinggi dengan nilai fitur yang tedapat pada destinasi wisata 'Monumen Nasional'.

### User-based Collaborative Filtering
Dalam metode ini, rekomendasi diberikan dengan menganalisis pola rating dari pengguna yang mirip. Jika pengguna A dan B memiliki pola rating yang serupa, destinasi yang dinilai tinggi oleh pengguna B namun belum dikunjungi oleh pengguna A akan direkomendasikan kepada pengguna A. Pembuatan model dilakukan dengan pendekatan deep learning (Collaborative Neural Filtering).

Kelebihan:
- Dapat merekomendasikan item baru yang belum pernah dinilai oleh pengguna, selama ada pengguna lain dengan pola rating serupa.
- Mampu menangkap selera pengguna yang tidak jelas atau eksplisit, dengan memanfaatkan preferensi pengguna lain yang serupa.
- Relevan untuk item yang sulit untuk dideskripsikan secara eksplisit.

Kekurangan:
- Memerlukan data pengguna lain untuk bekerja; kurang efektif untuk pengguna baru (cold start problem).
- Memerlukan banyak data rating untuk memberikan rekomendasi yang akurat.
- Rentan terhadap masalah sparsity, di mana data rating yang tersedia sangat jarang atau tidak mencakup banyak item.

Langkah-langkah pengembangan model dengan pendekatan User-based Collaborative Filtering yaitu sebagai berikut:
- Membangun kelas RecommenderNet: 'RecommenderNet' adalah kelas custom yang didefinisikan untuk membangun model rekomendasi. Model ini dirancang untuk mempelajari representasi laten dari pengguna dan destinasi wisata, dan kemudian menghitung skor prediksi yang menunjukkan seberapa besar kemungkinan seorang pengguna akan menyukai destinasi wisata tertentu.
- Inisiasi, compile, dan training model: Setelah kelas model didefinisikan, langkah berikutnya adalah menginisiasi objek model, mengatur parameter optimasi, seperti loss function dan optimizer, dan melakukan pelatihan model (training).
- Mendapatkan Rekomendasi: Setelah model dilatih, rekomendasi dapat dihasilkan. Berdasarkan pola rating yang telah dipelajari, model dapat memprediksi rating untuk destinasi yang belum dinilai oleh pengguna tertentu dan merekomendasikan destinasi dengan prediksi rating tertinggi.

Hasil dari sistem rekomendasi user-based collaborative filtering yaitu ketika dilakukan pencarian rekomendasi destinasi wisata untuk user 204 yang mirip dengan destinasi wisata yang telah ia kunjungi dengan rating tertinggi. Diketahui bahwa destinasi wisata yang telah ia kunjungi dengan rating tertinggi yaitu 'Pantai Goa Cemara', 'Bukit Jamur', 'Taman Pandanan', 'Wisata Lereng Kelir', dan 'Monumen Tugu Pahlawan'. Dari beberapa destinasi tersebut didapatkan beberapa destinasi wisata yang telah di rating oleh user lain yang memiliki pola rating yang serupa dengan user 204 yaitu seperti destinasi wisata 'Museum Tekstil', 'Pantai Baron', 'Tafso Barn'

## Evaluation
Pada tahap evaluasi  metriks evaluasi yang digunakan untuk mengevaluasi model diatas yaitu dengan menghitung akurasi model secara manual dan root mean squared error (RMSE).

### Metriks Accuracy
Menghitung akurasi dari hasil rekomendasi secara manual dengan mempertimbangkan beberapa variabel yaitu ground_truth sebagai kebenaran dasarnya untuk mencari correct_recommendations, correct recommendation sebagai jumlah rekomendasi yang sesuai dengan ground_truth, recommendation sebagai total rekomendasi yang diberikan.

Rumus :

$$
\text{Accuracy} = \left( \frac{\text{Correct Recommendation}}{\text{Recommendations}} \right) \times 100\%
$$

Di mana:

- Correct recommendations adalah jumlah destinasi wisata dalam rekomendasi yang terdapat dalam ground truth.
- Recommendations adalah total semua destinasi wisata yang direkomendasikan.

### Root Mean Squared Error (RMSE)
Root Mean Squared Error (RMSE) adalah metrik yang mengukur akar kuadrat dari rata-rata kuadrat perbedaan antara nilai yang diprediksi oleh model dan nilai aktual dari data. RMSE memberikan gambaran tentang seberapa besar kesalahan model dalam hal nilai numerik dan lebih mudah diinterpretasikan karena berada dalam satuan yang sama dengan nilai aktual.

Rumus :

$$
\text{RMSE} = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2}
$$

- \( y_i \) is the actual value.
- \( \hat{y}_i \) is the predicted value by the model.
- \( n \) is the number of data points.

Sebagai kesimpulan akhir dari analisis yang telah kita lakukan dari awal dapat ditarik beberapa poin bahwasannya :
- Berdasarkan data mengenai pengguna dan destinasi wisata, proyek yang dibangun berhasil membuat sistem rekomendasi yang dipersonalisasi dengan menggunakan teknik content-based filtering. Sistem ini mampu memberikan rekomendasi destinasi wisata kepada pengguna berdasarkan kemiripan fitur destinasi yang sudah pernah dikunjungi oleh pengguna sebelumnya. Evaluasi yang dilakukan dengan menghitung jumlah rekomendasi yang benar untuk destinasi 'Monumen Nasional' didapatkan hasil akurasi yaitu 100%.
- Berdasarkan data rating yang dimiliki, kita mengembangkan model rekomendasi menggunakan teknik user-based collaborative filtering dengan pendekatan deep learning. Hasil akhir dari evaluasi model dengan matriks RMSE sebesar 0.3432 pada data training dan 0.3491 pada data testing. Hasil ini menunjukkan sistem rekomendasi dapat memberikan hasil yang baik dalam merekomendasikan destinasi wisata lain yang mungkin disukai oleh pengguna dan belum pernah dikunjungi sebelumnya.
- Dari kedua sistem rekomendasi yang dibangun menunjukkan bahwa keduanya dapat digunakan untuk menciptakan sistem rekomendasi yang efektif dalam membantu pengguna menemukan destinasi wisata yang sesuai dengan preferensi mereka di Pulau Jawa.