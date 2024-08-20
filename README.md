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
Data yang digunakan pada proyek kali ini adalah [Indonesia Tourism Destination](https://www.kaggle.com/datasets/aprabowo/indonesia-tourism-destination/data) yang dapat dibuka dan diunduh pada link tersebut. Dataset terdiri dari 4 file dengan kurang lebih 400 destinasi wisata. Dataset ini merupakan kumpulan informasi beberapa destinasi wisata di 5 kota besar Indonesia yaitu Jakarta, Yogyakarta, Semarang, Bandung, Surabaya.

Variabel-variabel pada dataset Indonesia Tourism Destination adalah sebagai berikut:
- package : merupakan paket-paket destinasi tempat wisata yang ditawarkan dari dari berbagai kota
- rating : merupakan rating yang diberikan user terhadap destinasi tempat wisata
- destination : merupakan destinasi tempat-tempat wisata di 5 kota besar di Indonesia (Jakarta, Bandung, Semarang, Surabaya, Yogyakarta)
- user : merupakan pengguna yang melakukan rating

Beberapa insight yang diperoleh dari hasil exploratory data analysis yaitu sebagai berikut:
- Terdapat 6 kategori destinasi wisata, kategori terbanyak yaitu Taman Hiburan dengan jumlah lebih dari 130 data dan kategori tersedikit yaitu Pusat Perbelanjaan dengan jumlah kurang dari 15 data
- Terdapat 5 kota besar, urutan kota dengan destinasi terbanyak hingga tersedikit yaitu kota yogyakarta, bandung, jakarta, semarang dan surabaya
- 4 Destinasi dengan rating tertinggi yaitu Freedom Library, Desa Wisata Sungai Code Jogja Kota, Kauman Pakualam Yogyakarta, Wisata Kuliner Pecenongan memiliki rating 5/5
- Pengguna terbanyak yang melakukan rating berasal dari provinsi Jawa Barat
- Pengguna yang melakukan rating memiliki distribusi umur 18 hingga 40 tahun

## Data Preparation
Beberapa yang dilakukan dalam menyiapkan data untuk model yaitu dengan:

### Menggabungkan rating dengan fitur-fitur pada destinasi
Menggabungkan rating dengan fitur-fitur pada destinasi adalah proses mengintegrasikan data rating yang diberikan oleh pengguna dengan informasi fitur-fitur lain yang dimiliki oleh setiap destinasi wisata. Hal ini bertujuan untuk memperkaya dataset dengan informasi yang lebih lengkap, sehingga model rekomendasi dapat mempelajari pola preferensi pengguna dengan lebih baik. Fitur yang dapat digabungkan meliputi kategori destinasi, harga, durasi kunjungan (time_minutes), lokasi (city), dan rating. Data yang digabungkan ini akan digunakan sebagai input bagi model rekomendasi untuk memberikan saran destinasi wisata yang sesuai dengan preferensi pengguna.

### Pengecekan fitur kategorikal
Pengecekan fitur kategorikal adalah proses untuk memastikan bahwa fitur-fitur yang bersifat kategorikal telah teridentifikasi dengan benar sebelum dilakukan proses encoding. Fitur kategorikal adalah fitur yang memiliki nilai dalam bentuk kategori atau label, seperti 'Category' (kategori wisata) dan 'City' (kota). Dalam proyek ini, penting untuk memeriksa apakah semua fitur kategorikal sudah benar dan konsisten dalam formatnya sebelum menerapkan teknik encoding seperti OneHotEncoder. Pengecekan ini dapat dilakukan dengan menggunakan fungsi value_counts() atau unique() pada setiap fitur kategorikal untuk melihat distribusi nilai kategori dan memastikan tidak ada nilai yang salah atau tidak sesuai.

### Mengubah nilai pada fitur 'Category' dengan snake case style
Mengubah nilai pada fitur 'Category' dengan snake case style adalah proses mengubah nama kategori dalam fitur 'Category' agar sesuai dengan format snake case (huruf kecil dengan pemisah underscore). Snake case digunakan untuk membuat nama kategori lebih konsisten dan mudah diproses dalam analisis data dan pemodelan. Langkah ini penting untuk memastikan bahwa nama kategori tidak mengandung spasi atau karakter khusus yang dapat menyebabkan masalah saat data digunakan dalam model machine learning.

## Modeling
Pada tahap modeling, terdapat dua sistem rekomendasi yang dibangun yaitu Content-based Filtering dan User-based Collaborative Filtering.

### Content-based Filtering
Dalam metode ini, rekomendasi diberikan berdasarkan kemiripan antara destinasi wisata yang pernah dinilai atau dikunjungi oleh pengguna dengan destinasi lainnya yang belum pernah dikunjungi. Sistem ini menganalisis fitur-fitur deskriptif dari destinasi wisata, seperti kategori (seperti alam, budaya, hiburan), harga, durasi kunjungan (time_minutes), dan lokasi (city).

Kelebihan:
- Tidak memerlukan data dari pengguna lain; hanya memerlukan informasi tentang item dan preferensi pengguna.
- Dapat merekomendasikan item baru yang belum pernah diberi rating oleh pengguna lain.
- Pengguna memiliki kendali lebih besar atas hasil rekomendasi berdasarkan preferensi yang diketahui.

Kekurangan:
- Terbatas pada item yang mirip dengan yang sudah pernah dipilih pengguna, sehingga rekomendasi cenderung monoton.
- Kesulitan dalam menangkap selera yang lebih kompleks atau berubah-ubah dari pengguna.
- Membutuhkan deskripsi item yang detail dan relevan untuk bekerja dengan baik.

Langkah-langkah pengembangan model dengan pendekatan Content-based Filtering yaitu sebagai berikut:
- Ekstraksi Fitur: Pertama yaitu mengekstraksi fitur-fitur dari setiap destinasi wisata. Fitur-fitur ini bisa berupa kategori wisata, harga, durasi kunjungan, dan kota tempat destinasi tersebut berada.
- Pembobotan Fitur: Fitur-fitur yang telah diekstraksi kemudian diberi bobot menggunakan metode seperti TF-IDF (Term Frequency-Inverse Document Frequency) untuk fitur kategorikal dan Standarisasi nilai pada fitur numerical. Ini membantu model memahami pentingnya setiap fitur dalam konteks rekomendasi.
- Membangun Model: Dengan menggunakan fitur-fitur yang telah diekstraksi dan dibobot, selanjutnya yaitu membangun model yang menghitung kemiripan antara destinasi wisata yang telah dikunjungi dan destinasi lainnya menggunakan metode seperti cosine similarity.
- Mendapatkan Rekomendasi: Berdasarkan kemiripan yang telah dihitung, sistem menghasilkan top-N rekomendasi destinasi wisata yang paling mirip dengan destinasi yang telah dinilai oleh pengguna. Hasil rekomendasi ini menampilkan nama destinasi beserta fitur-fitur relevan lainnya.

Sebagai contoh keluaran dari model yaitu saat ingin mendapatkan rekomendasi destinasi wisata yang mirip dengan Monumen Nasional, model akan memberikan top 3 rekomendasi destinasi wisata yaitu Monumen Selamat Datang, Museum Tekstil, dan Museum Sasmita Loka Ahmad Yani

### User-based Collaborative Filtering
Dalam metode ini, rekomendasi diberikan dengan menganalisis pola rating dari pengguna yang mirip. Jika pengguna A dan B memiliki pola rating yang serupa, destinasi yang dinilai tinggi oleh pengguna B namun belum dikunjungi oleh pengguna A akan direkomendasikan kepada pengguna A. Pembuatan model dilakukan dengan deep learning.

Kelebihan:
- Dapat merekomendasikan item baru yang belum pernah dinilai oleh pengguna, selama ada pengguna lain dengan pola rating serupa.
- Mampu menangkap selera pengguna yang tidak jelas atau eksplisit, dengan memanfaatkan preferensi pengguna lain yang serupa.
- Relevan untuk item yang sulit untuk dideskripsikan secara eksplisit.

Kekurangan:
- Memerlukan data pengguna lain untuk bekerja; kurang efektif untuk pengguna baru (cold start problem).
- Memerlukan banyak data rating untuk memberikan rekomendasi yang akurat.
- Rentan terhadap masalah sparsity, di mana data rating yang tersedia sangat jarang atau tidak mencakup banyak item.

Langkah-langkah pengembangan model dengan pendekatan User-based Collaborative Filtering yaitu sebagai berikut:
- Membagi dataset (train dan test): Dataset dibagi menjadi dua subset: data pelatihan (training) dan data pengujian (testing). Data pelatihan digunakan untuk melatih model, sementara data pengujian digunakan untuk mengevaluasi kinerja model pada data yang belum pernah dilihat sebelumnya.
- Membangun kelas RecommenderNet: 'RecommenderNet' adalah kelas custom yang didefinisikan untuk membangun model rekomendasi. Dalam kelas ini, layer embedding untuk pengguna dan destinasi serta layer tambahan untuk pemrosesan data didefinisikan. Kelas ini juga akan mengimplementasikan logika untuk memprediksi rating yang akan diberikan pengguna pada destinasi tertentu.
- Inisiasi, compile, dan training model: Setelah kelas model didefinisikan, langkah berikutnya adalah menginisiasi objek model, mengatur parameter optimasi, seperti loss function dan optimizer, dan melakukan pelatihan model (training).
- Mendapatkan Rekomendasi: Setelah model dilatih, rekomendasi dapat dihasilkan. Berdasarkan pola rating yang telah dipelajari, model dapat memprediksi rating untuk destinasi yang belum dinilai oleh pengguna tertentu dan merekomendasikan destinasi dengan prediksi rating tertinggi.

Sebagai contoh keluaran dari model yaitu saat ingin mendapatkan rekomendasi destinasi wisata untuk user dengan id 260, model akan mempelajari destinasi wisata dengan rating tertinggi dari user tersebut lalu memberikan top 10 rekomendasi destinasi wisata berdasarkan preferensi user lain yang memiliki destinasi wisata mirip dengan user 260.

## Evaluation
Pada tahap evaluasi  metriks evaluasi yang digunakan untuk mengevaluasi model diatas yaitu dengan root mean squared error (RMSE).

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
- Berdasarkan data mengenai pengguna dan destinasi wisata, proyek yang dibangun berhasil membuat sistem rekomendasi yang dipersonalisasi dengan menggunakan teknik content-based filtering. Sistem ini mampu memberikan rekomendasi destinasi wisata kepada pengguna berdasarkan kemiripan fitur destinasi yang sudah pernah dikunjungi oleh pengguna sebelumnya. Dengan menggunakan fitur-fitur seperti kategori destinasi, lokasi, dan durasi waktu kunjungan, sistem dapat menyesuaikan rekomendasi sesuai preferensi individu.
- Berdasarkan data rating yang dimiliki, kita mengembangkan model rekomendasi menggunakan teknik user-based collaborative filtering dengan pendekatan deep learning. Hasil akhir dari evaluasi model dengan matriks RMSE sebesar 0.3304 pada data training dan 0.3464 pada data testing. Hasil ini menunjukkan sistem rekomendasi dapat memberikan hasil yang baik dalam merekomendasikan destinasi wisata lain yang mungkin disukai oleh pengguna dan belum pernah dikunjungi sebelumnya.
- Dari kedua sistem rekomendasi yang dibangun menunjukkan bahwa keduanya dapat digunakan untuk menciptakan sistem rekomendasi yang efektif dalam membantu pengguna menemukan destinasi wisata yang sesuai dengan preferensi mereka di Pulau Jawa.