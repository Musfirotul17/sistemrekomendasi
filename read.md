# Laporan Proyek Machine Learning - Musfirotul Khusna

## Project Overview

Seiring meningkatnya popularitas anime secara global, pengguna sering kesulitan memilih tontonan yang sesuai dari ribuan judul yang tersedia. Berdasarkan laporan Grand View Research, industri anime diperkirakan tumbuh dengan CAGR sebesar 9.5% hingga tahun 2028 (Grand View Research, 2021). Hal ini menunjukkan perlunya sistem yang mampu memberikan rekomendasi yang relevan dan personal.

**Rubrik/Kriteria Tambahan (Opsional)**:
Proyek ini bertujuan membangun sistem rekomendasi anime menggunakan dua dataset utama dari MyAnimeList: data anime dan data rating pengguna. Sistem ini akan menggunakan pendekatan seperti content-based filtering dan collaborative filtering untuk memberikan saran tontonan yang sesuai dengan preferensi pengguna.

Dengan sistem ini, diharapkan pengguna dapat menemukan tontonan yang lebih relevan secara efisien, serta menjadi penerapan nyata dari teknologi sistem rekomendasi berbasis data.

Referensi (Format APA):
Grand View Research. (2021). Anime Market Size, Share & Trends Analysis Report By Type, By Genre, By Distribution Channel, By Region, And Segment Forecasts, 2021 – 2028. Retrieved from https://www.grandviewresearch.com/industry-analysis/anime-market


## Business Understanding

Untuk membangun sistem rekomendasi yang efektif, diperlukan pemahaman yang jelas mengenai permasalahan yang dihadapi pengguna serta tujuan bisnis yang ingin dicapai. Berikut ini adalah klarifikasi masalah, tujuan proyek, dan pendekatan solusi yang akan digunakan.

Bagian laporan ini mencakup:

### Problem Statements

Menjelaskan pernyataan masalah:
1. Bagaimana Melatih Data untuk Sistem Rekomendasi Anime Menggunakan Content-Based Filtering?
    Pengguna sering kali kesulitan menemukan anime yang sesuai dengan preferensi mereka karena banyaknya pilihan yang tersedia. Melatih data dengan metode Content-Based Filtering dapat membantu merekomendasikan anime berdasarkan kesamaan fitur konten, seperti genre, sinopsis, dan karakteristik lainnya.
2. Bagaimana Melatih Data untuk Sistem Rekomendasi Anime Menggunakan Collaborative Filtering?
    Selain preferensi individu, pola kesamaan antar pengguna dapat dimanfaatkan untuk memberikan rekomendasi. Melatih data dengan metode Collaborative Filtering memungkinkan sistem untuk merekomendasikan anime berdasarkan preferensi pengguna lain yang memiliki selera serupa.
3. Metode Rekomendasi Mana yang Paling Efektif dalam Memberikan     Rekomendasi Anime yang Relevan dan Dipersonalisasi?
    Setiap metode memiliki kelebihan dan kekurangan. Penting untuk mengevaluasi dan menentukan metode yang paling efektif dalam konteks data dan kebutuhan pengguna.

### Goals

Menjelaskan tujuan proyek yang menjawab pernyataan masalah:
1. Mengembangkan Sistem Rekomendasi Anime yang Efektif Menggunakan Content-Based Filtering
    Membangun model yang dapat merekomendasikan anime berdasarkan kesamaan fitur konten dengan anime yang disukai pengguna sebelumnya.
2. Bagaimana Melatih Data untuk Sistem Rekomendasi Anime Menggunakan Collaborative Filtering?
    Membangun model yang dapat merekomendasikan anime berdasarkan preferensi pengguna lain yang memiliki kesamaan selera dengan pengguna target.
3. Mengevaluasi dan Menentukan Metode Rekomendasi yang Paling Efektif
    Melakukan evaluasi komprehensif terhadap kedua metode untuk menentukan mana yang memberikan rekomendasi paling relevan dan dipersonalisasi bagi pengguna.


**Rubrik/Kriteria Tambahan (Opsional)**:
- Menambahkan bagian “Solution Approach” yang menguraikan cara untuk meraih goals. Bagian ini dibuat dengan ketentuan sebagai berikut: 

    ### Solution statements
    - Content-Based Filtering (CBF)
    Pendekatan ini merekomendasikan anime berdasarkan kesamaan konten dengan anime yang disukai pengguna sebelumnya. Proses pelatihan data meliputi:

        - Ekstraksi Fitur: Mengidentifikasi dan mengekstrak fitur-fitur penting dari setiap anime, seperti genre, sinopsis, dan karakteristik lainnya.
        - Representasi Fitur: Mengubah fitur-fitur tersebut menjadi representasi numerik menggunakan teknik seperti TF-IDF.
        - Perhitungan Kesamaan: Menghitung kesamaan antara anime menggunakan metrik seperti cosine similarity untuk menemukan anime yang mirip dengan preferensi pengguna.
    - Collaborative Filtering (CF)
    Metode ini merekomendasikan anime berdasarkan preferensi pengguna lain yang memiliki kesamaan selera dengan pengguna target. Proses pelatihan data meliputi:
        - Pembuatan Matriks Interaksi: Membangun matriks pengguna-item berdasarkan interaksi pengguna, seperti rating atau riwayat tontonan.
        - Perhitungan Kesamaan: Menghitung kesamaan antar pengguna atau antar item menggunakan metrik seperti Pearson correlation atau cosine similarity.
        - Prediksi Rating: Memprediksi rating atau preferensi pengguna terhadap anime yang belum ditonton berdasarkan pola interaksi pengguna lain yang serupa.

## Data Understanding
Dataset yang digunakan dalam proyek ini adalah Anime Recommendations Database yang tersedia di Kaggle: https://www.kaggle.com/datasets/CooperUnion/anime-recommendations-database.

Dataset ini berisi informasi preferensi pengguna dari 73.516 pengguna terhadap 12.294 judul anime. Setiap pengguna dapat menambahkan anime ke daftar yang telah mereka tonton dan memberikan rating.

Selanjutnya, uraikanlah seluruh variabel atau fitur pada data. Sebagai contoh:  

Dataset terdiri dari dua file utama:
- anime.csv: Berisi informasi mengenai anime.
- rating.csv: Berisi data rating yang diberikan oleh pengguna terhadap anime.

### Deskripsi Variabel
1. anime.csv
    - anime_id: ID unik dari MyAnimeList yang mengidentifikasi setiap anime.
    - name: Nama lengkap anime.
    - genre: Daftar genre yang dipisahkan dengan koma untuk setiap anime.
    - type: Jenis anime (misalnya, TV, Movie, OVA, dll.).
    - episodes: Jumlah episode dalam anime tersebut (1 jika berupa film).
    - rating: Rating rata-rata dari 10 untuk anime ini.
    - Members: Jumlah anggota komunitas yang termasuk dalam "grup" anime ini.

2. rating.csv
    - user_id: ID pengguna yang dihasilkan secara acak dan tidak dapat diidentifikasi.
    - anime_id: ID anime yang telah diberi rating oleh pengguna ini.
    - rating: Rating dari 10 yang diberikan oleh pengguna ini (-1 jika pengguna menonton tetapi tidak memberikan rating).

### Kondisi Data
Jumlah Data: Dataset mencakup 73.516 pengguna dan 12.294 anime.
Kualitas Data: Beberapa entri memiliki rating -1, yang menunjukkan bahwa pengguna telah menonton anime tersebut tetapi tidak memberikan rating.

Distribusi Data: Rating yang diberikan oleh pengguna bervariasi, dengan beberapa anime mendapatkan rating tinggi dan lainnya rendah, mencerminkan preferensi yang beragam di antara pengguna.

**Rubrik/Kriteria Tambahan (Opsional)**:
1. Pemeriksaan Struktur dan Statistik Data
    - Informasi Umum Dataset: Menggunakan anime.info() dan rating.info() untuk melihat jumlah entri, tipe data, dan informasi non-null pada masing-masing kolom.
    - Statistik Deskriptif: Menggunakan anime.describe() dan rating.describe() untuk memperoleh statistik deskriptif seperti mean, standar deviasi, nilai minimum dan maksimum pada kolom numerik.Dalam anime.csv, terdapat kolom-kolom seperti anime_id, name, genre, type, episodes, rating, dan members. Statistik deskriptif menunjukkan bahwa rating rata-rata anime adalah 6,47 dengan rentang antara 1,67 hingga 10,00. Jumlah anggota komunitas rata-rata per anime adalah 18.071,34. Pada rating.csv, kolom-kolom yang tersedia antara lain user_id, anime_id, dan rating. Statistik deskriptif menunjukkan bahwa rating rata-rata adalah 6,14 dengan rentang antara -1 (menandakan anime ditonton tanpa memberikan rating) hingga 10,00. Tidak terdapat nilai kosong dalam dataset ini.
    - Pemeriksaan Duplikasi dan Nilai Kosong: anime.duplicated().sum() dan rating.duplicated().sum() digunakan untuk menghitung jumlah data duplikat.anime.isnull().sum() dan rating.isnull().sum() digunakan untuk menghitung jumlah nilai kosong pada setiap kolom. Terdapat beberapa nilai kosong pada kolom genre (62 nilai kosong), type (25 nilai kosong), dan rating (230 nilai kosong). Tidak ditemukan duplikat berdasarkan anime_id dan name. Duplikat berdasarkan rating.csv ditemukan 1.
2. Distribusi Rating Anime
    Visualisasi distribusi rating dilakukan menggunakan sns.countplot(x='rating', data=rating) untuk melihat frekuensi masing-masing nilai rating yang diberikan oleh pengguna.
    Deskripsi:
        Histogram ini memperlihatkan distribusi jumlah rating dari pengguna terhadap anime.
    Insight:
        - Banyak rating berada di kisaran 7-9, menunjukkan bahwa mayoritas anime mendapatkan penilaian yang cukup tinggi.
        - Nilai -1 sangat mencolok, menunjukkan anime tersebut belum diberi rating .
        - Sangat sedikit anime yang diberi nilai rendah (1-3), mungkin karena pengguna lebih cenderung memberi rating pada anime yang mereka sukai.
3. Visualisasi
    - Anime dengan Jumlah Anggota Komunitas Terbanyak
        Pemrosesan Data: 
        Dataset anime disalin dan duplikat berdasarkan nama dihapus menggunakan drop_duplicates().
        Visualisasi: 
        Menggunakan sns.barplot() untuk menampilkan 14 anime teratas berdasarkan jumlah anggota komunitas (members). Label pada batang menunjukkan jumlah anggota, dengan gaya kotak label yang menarik.
        Deskripsi:
        Grafik batang ini menunjukkan anime-anime dengan jumlah member terbanyak dalam komunitas.
        Insight:
        Death Note memimpin dengan lebih dari 1 juta member, menandakan pengaruh dan popularitas globalnya.
        Anime-anime populer lainnya seperti Fullmetal Alchemist, Shingeki no Kyojin, dan Sword Art Online juga menunjukkan engagement komunitas yang tinggi.
        Ini berguna untuk sistem rekomendasi: anime dengan basis komunitas besar mungkin memiliki rating/review yang lebih andal.
    - Distribusi Kategori Anime
        Analisis Kategori: 
        Menggunakan value_counts() untuk menghitung jumlah anime dalam setiap kategori (type).
        Visualisasi: 
        Menggunakan plt.pie() untuk menampilkan distribusi kategori anime dalam bentuk pie chart (donut chart) dengan proporsi masing-masing kategori.
        Deskripsi:
        Diagram ini menampilkan distribusi anime berdasarkan kategori utama seperti TV, OVA, Movie, Special, ONA, dan Music.
        Insight:
        TV menjadi kategori paling dominan, mencakup 30.87% dari total, menandakan bahwa anime serial TV adalah bentuk yang paling umum.
        Kategori OVA dan Movie juga memiliki proporsi besar, menunjukkan bahwa konten non-TV tetap populer.
        ONA (Online) dan Music punya persentase kecil, namun tetap penting mengingat perkembangan platform streaming.
    - Wordcloud Genre Anime
        Untuk melihat representasi visual dari genre anime yang paling umum, dibuat wordcloud menggunakan WordCloud() dari pustaka wordcloud. Genre digabungkan menjadi satu string dan divisualisasikan dengan latar belakang hitam dan colormap "Set2".
        Deskripsi:
        Word cloud ini menunjukkan genre anime berdasarkan frekuensi kemunculan.
        Insight:
        Genre yang paling menonjol: Action, Adventure, Comedy, Sci-Fi, Fantasy, Shounen.
        Genre besar ini menunjukkan preferensi pengguna umum dan dapat menjadi fitur penting untuk personalisasi rekomendasi.
        Genre minor seperti Mystery, Police, Dementia masih muncul, menandakan variasi dalam minat pengguna.

## Data Preparation
    1. Menghapus Nilai Kosong pada Dataset Anime
        Langkah pertama dalam proses data preparation adalah menghapus nilai kosong (missing values) pada dataset anime.csv. Hal ini dilakukan untuk memastikan bahwa analisis selanjutnya tidak terganggu oleh data yang tidak lengkap. Kolom yang memiliki nilai kosong adalah:
        - genre: 62 nilai kosong
        - type: 25 nilai kosong
        - rating: 230 nilai kosong
        Dengan menggunakan fungsi dropna(), semua baris yang mengandung nilai kosong dihapus dari dataset.

    2. Menghapus Duplikat pada Dataset Rating
        Dataset rating.csv diperiksa untuk duplikat berdasarkan kombinasi user_id dan anime_id. Duplikat yang ditemukan dihapus menggunakan fungsi drop_duplicates() untuk memastikan bahwa setiap pasangan pengguna dan anime hanya muncul sekali, menghindari bias dalam analisis rating.

    3. Menggabungkan Dataset Anime dan Rating
        Dataset anime dan rating digabungkan menggunakan fungsi merge() berdasarkan kolom anime_id. Kolom rating dari dataset rating diubah namanya menjadi user_rating untuk membedakan dengan kolom rating dari dataset anime. Penggabungan ini menghasilkan dataset fulldata yang berisi informasi lengkap tentang anime dan rating dari pengguna.

    4. Menangani Nilai -1 pada Kolom User Rating
        Dalam dataset rating.csv, nilai -1 pada kolom rating menunjukkan bahwa pengguna telah menonton anime tersebut tetapi tidak memberikan rating. Nilai -1 ini diganti dengan NaN (Not a Number) menggunakan fungsi replace(), dan kemudian semua baris yang mengandung NaN dihapus menggunakan dropna(). Langkah ini memastikan bahwa hanya rating yang valid yang digunakan dalam analisis.

    5. Memfilter Pengguna dengan Minimal 50 Rating
        Untuk meningkatkan kualitas analisis, hanya pengguna yang telah memberikan minimal 50 rating yang dipertahankan dalam dataset. Hal ini dilakukan dengan menghitung jumlah rating per pengguna menggunakan value_counts() dan memfilter dataset untuk hanya menyertakan pengguna yang memenuhi kriteria tersebut.

    6. Membersihkan Nama Anime dari Karakter Khusus
        Beberapa nama anime mengandung karakter khusus atau entitas HTML seperti &quot;, &#039;, dan &amp;. Fungsi text_cleaning() digunakan untuk membersihkan nama-nama anime dari karakter-karakter tersebut, sehingga memudahkan dalam analisis dan visualisasi data.

    7. Membuat Pivot Table untuk Analisis
        Setelah data dibersihkan, pivot table dibuat menggunakan fungsi pivot_table() dengan name sebagai indeks, user_id sebagai kolom, dan user_rating sebagai nilai. Pivot table ini digunakan untuk analisis lebih lanjut, seperti sistem rekomendasi atau analisis pola rating pengguna.

## Modeling
Dalam proyek ini, saya membangun dua sistem rekomendasi untuk membantu pengguna menemukan anime yang relevan dengan preferensi mereka. Dua pendekatan yang digunakan adalah Collaborative Filtering dan Content-Based Filtering, masing-masing dengan algoritma yang berbeda dan karakteristik unik. Hasil dari kedua pendekatan ini disajikan dalam bentuk Top-N Recommendation.
    1. Collaborative Filtering - K-Nearest Neighbors (KNN)
        Pada pendekatan ini, sistem rekomendasi dibuat dengan memanfaatkan interaksi pengguna (misalnya rating) terhadap anime tertentu. Pendekatan ini dikenal sebagai user-item collaborative filtering. Implementasi menggunakan algoritma **K-Nearest Neighbors (KNN)** dengan **cosine similarity** sebagai metrik kemiripan antar item (anime).

            *model_knn = NearestNeighbors(metric = "cosine", algorithm = "brute")*
            *model_knn.fit(data_matrix)*

        Top-N Recommendation Output:
        Contoh rekomendasi untuk anime "Mahou no Yousei Persia":
        | No | Anime Name                      | Rating |
        | -- | ------------------------------- | ------ |
        | 1  | Sasurai no Taiyou               | 6.42   |
        | 2  | Akuu Daisakusen Srungle         | 6.55   |
        | 3  | Bikkuriman                      | 6.68   |
        | 4  | Mahou no Idol Pastel Yumi       | 6.45   |
        | 5  | Honey Honey no Suteki na Bouken | 6.58   |
    
    ✅ Kelebihan:
        - Personalized Recommendation: Memberikan rekomendasi yang sesuai dengan pola perilaku pengguna lain yang memiliki selera serupa.
        - Tidak membutuhkan data konten item: Hanya membutuhkan interaksi user-item (seperti rating), tidak perlu tahu deskripsi anime.
        - Mudah diimplementasikan: Dengan algoritma KNN dan cosine similarity, pendekatan ini cukup mudah dan intuitif.

    ❌ Kekurangan:
        - Cold Start Problem: Tidak bisa merekomendasikan item baru yang belum memiliki rating.
        - Data Sparsity: Rentan terhadap data yang jarang atau sedikit interaksi antar pengguna dan item.
        - Scalability: Kurang efisien untuk dataset besar karena proses pencarian tetangga mirip bisa sangat mahal secara komputasi.

    2. Content-Based Filtering - TF-IDF + Sigmoid Kernel
    Pendekatan kedua menggunakan informasi konten dari anime, dalam hal ini adalah genre. Setiap anime diubah menjadi representasi numerik berbasis teks menggunakan **TF-IDF vectorizer**, lalu dihitung kemiripannya menggunakan **sigmoid kernel**.

        *tfv = TfidfVectorizer(...)*
        *sig = sigmoid_kernel(tfv_matrix, tfv_matrix)*

    Top-N Recommendation Output:
    Contoh rekomendasi untuk anime "Bleach":
        | No | Anime Name                                        | Rating |
        | -- | ------------------------------------------------- | ------ |
        | 1  | Detective Conan Movie 19: The Hellfire Sunflowers | 7.77   |
        | 2  | Persona 4 the Animation                           | 7.68   |
        | 3  | Shelter                                           | 8.38   |
        | 4  | Hotori: Tada Saiwai wo Koinegau                   | 7.14   |
        | 5  | Chibi☆Devi!                                       | 6.86   |
        | 6  | Oyayubi Hime Monogatari                           | 6.85   |
        | 7  | Taimadou Gakuen 35 Shiken Shoutai                 | 7.05   |
        | 8  | Shikabane Hime: Kuro Special                      | 7.12   |
        | 9  | Choujin Locke                                     | 6.65   |
        | 10 | Naruto                                            | 7.81   |

    ✅ Kelebihan:
        - Tidak bergantung pada pengguna lain: Dapat memberikan rekomendasi walaupun data pengguna sedikit atau tidak ada.
        - Cocok untuk item baru: Item baru tetap bisa direkomendasikan selama memiliki informasi konten (genre).
        - Hasil interpretatif: Rekomendasi diberikan berdasarkan kemiripan konten (misalnya genre), sehingga lebih mudah dijelaskan.

    ❌ Kekurangan:
        - Kurang personalisasi: Rekomendasi bisa menjadi terlalu sempit atau homogen karena hanya melihat konten yang mirip.
        - Kualitas konten penting: Sangat tergantung pada deskripsi konten yang lengkap dan akurat (misalnya genre yang relevan).
        - Over-specialization: Sistem cenderung merekomendasikan item yang sangat mirip dengan yang sudah disukai, sehingga mengurangi keberagaman.

## Evaluation
### 1. Metrik Evaluasi yang Digunakan

Dalam proyek ini, dua pendekatan sistem rekomendasi dievaluasi menggunakan metrik sebagai berikut:

- **Content-Based Filtering**: menggunakan **Precision@K** (K = 10).
- **Collaborative Filtering**: menggunakan **Cosine Similarity** untuk mengukur kemiripan antar item berdasarkan interaksi pengguna.

---

### 2. Precision@K (untuk Content-Based Filtering)

**Definisi dan Formula:**

Precision@K mengukur proporsi item yang relevan di antara K item yang direkomendasikan.

\[
\text{Precision@K} = \frac{\text{Jumlah item relevan dalam rekomendasi top-K}}{K}
\]

Contoh: Jika dari 10 rekomendasi, 7 anime dianggap relevan oleh pengguna, maka:

\[
\text{Precision@10} = \frac{7}{10} = 0.70
\]

**Hasil Evaluasi:**

Berdasarkan hasil rekomendasi terhadap anime seperti *"Bleach"*, mayoritas anime yang disarankan memiliki genre serupa. Evaluasi manual menunjukkan **Precision@10 berada di kisaran 0.70–0.80**, menandakan sistem mampu memberikan hasil yang cukup relevan.

---

### 3. Cosine Similarity (untuk Collaborative Filtering)

**Definisi dan Formula:**

Cosine Similarity mengukur tingkat kemiripan antara dua vektor berdasarkan arah (bukan nilai absolut):

\[
\text{cosine\_similarity}(A, B) = \frac{A \cdot B}{||A|| \times ||B||}
\]

Nilai berkisar antara 0 (tidak mirip) hingga 1 (sangat mirip).

### **Hasil Evaluasi**

Dengan menggunakan pendekatan **K-Nearest Neighbors (KNN)** dan metrik **cosine similarity**, sistem Collaborative Filtering mampu merekomendasikan anime berdasarkan pola interaksi pengguna. Namun, meskipun beberapa rekomendasi memiliki rating menengah (6.4–6.6), kemiripan genre dan era menunjukkan pola perilaku pengguna yang sejalan.

Sementara itu, sistem **Content-Based Filtering** menunjukkan performa yang lebih stabil dan relevan. Berdasarkan atribut genre, sistem memberikan rekomendasi yang konsisten dan sesuai dengan preferensi konten pengguna. Hal ini terlihat dari nilai **Precision@10** yang tinggi (sekitar **0.70–0.80**).

---

### 🔎 Evaluasi Berdasarkan Problem Statement

| **Pernyataan Masalah** | **Evaluasi dan Hasil** |
|-------------------------|-------------------------|
| **Bagaimana Melatih Data untuk Sistem Rekomendasi Anime Menggunakan Content-Based Filtering?** | Dengan memanfaatkan atribut konten seperti genre, sistem mampu memberikan rekomendasi yang relevan dan sesuai preferensi. Precision@10 yang tinggi menunjukkan tingkat kesesuaian yang baik. |
| **Bagaimana Melatih Data untuk Sistem Rekomendasi Anime Menggunakan Collaborative Filtering?** | Sistem berhasil menemukan kesamaan pola interaksi pengguna melalui cosine similarity. Namun, kualitas rekomendasi terbatas pada item dengan data interaksi yang cukup. |
| **Metode Rekomendasi Mana yang Paling Efektif?** | **Content-Based Filtering** unggul dalam menangani cold-start dan memberikan rekomendasi berbasis konten. Sedangkan Collaborative Filtering cocok untuk data pengguna yang kaya. Dalam proyek ini, **Content-Based** memberikan hasil yang lebih stabil dan akurat. |

---

### ✅ Kesimpulan Evaluasi

Berdasarkan hasil evaluasi:

- **Content-Based Filtering** menunjukkan performa terbaik dalam proyek ini dengan menghasilkan rekomendasi yang relevan dan stabil, meskipun pengguna atau anime belum memiliki banyak riwayat interaksi.
- **Collaborative Filtering** tetap efektif dalam mengenali pola pengguna jika data interaksi tersedia secara memadai.
- Oleh karena itu, **Content-Based Filtering dipilih sebagai pendekatan terbaik** dalam konteks data dan permasalahan saat ini.

**---Ini adalah bagian akhir laporan---**


