# Laporan Proyek Machine Learning - Aria Riski Ramadhan

## Project Overview

### Latar belakang
Dalam era digital saat ini, ledakan informasi telah menjadi tantangan sekaligus peluang. Pengguna dihadapkan pada pilihan produk, layanan, atau konten yang tak terbatas, seringkali menimbulkan *information overload* atau kebingungan dalam memilih. Dalam konteks hiburan, khususnya film, jumlah judul yang tersedia di berbagai platform *streaming* terus bertambah secara eksponensial. Tanpa panduan yang efektif, pengguna seringkali kesulitan menemukan film yang sesuai dengan selera mereka, yang dapat mengurangi pengalaman menonton dan bahkan menyebabkan pembatalan langganan.

Masalah ini dapat diselesaikan dengan membangun **sistem rekomendasi film**. Sistem rekomendasi adalah algoritma yang mampu memfilter dan memprediksi preferensi pengguna terhadap suatu item, kemudian menyarankan item yang relevan dan menarik. Dengan demikian, sistem ini membantu pengguna menemukan konten baru yang mungkin mereka sukai, meningkatkan pengalaman pengguna, dan pada akhirnya dapat meningkatkan *engagement* serta retensi pengguna pada platform penyedia konten.

Dalam proyek ini, saya berfokus pada pengembangan **sistem rekomendasi film sederhana menggunakan metode *Content-Based Filtering***. Pendekatan ini dipilih karena kemampuannya untuk merekomendasikan item berdasarkan atribut atau karakteristik konten itu sendiri. Ketika seorang pengguna menyukai suatu film, sistem ini akan merekomendasikan film lain yang memiliki karakteristik serupa (misalnya, genre yang sama).

**Mengapa dan Bagaimana Masalah Ini Diselesaikan:**

* **Mengapa Masalah Ini Harus Diselesaikan:**
    * **Mengatasi *Information Overload***: Membantu pengguna menyaring jutaan pilihan film untuk menemukan yang paling relevan.
    * **Meningkatkan Pengalaman Pengguna**: Menyajikan rekomendasi yang personal dan menarik, membuat pengguna merasa dipahami dan lebih puas.
    * **Meningkatkan *Engagement* dan Retensi**: Pengguna yang menemukan konten yang sesuai cenderung lebih sering menggunakan platform dan memiliki tingkat loyalitas yang lebih tinggi.
    * **Nilai Bisnis**: Platform *streaming* dapat meningkatkan pendapatan melalui peningkatan waktu tonton dan pembelian/langganan.

* **Bagaimana Masalah Ini Diselesaikan (Pendekatan Content-Based Filtering):**
    Saya menyelesaikan masalah ini dengan mengimplementasikan sistem rekomendasi *content-based filtering* yang berfokus pada **kemiripan genre film**. Mekanismenya adalah sebagai berikut:
    1.  **Ekstraksi Fitur Konten**: Menggunakan teknik **TF-IDF (Term Frequency-Inverse Document Frequency)**, genre dari setiap film diubah menjadi representasi numerik. TF-IDF membantu mengukur seberapa penting sebuah genre bagi suatu film relatif terhadap semua film lainnya.
    2.  **Perhitungan Kemiripan**: Setelah genre diwakili dalam bentuk numerik, saya menghitung tingkat kemiripan antara setiap pasangan film menggunakan **Cosine Similarity**. Cosine Similarity adalah metrik yang mengukur sudut antara dua vektor non-nol, di mana nilai yang lebih tinggi menunjukkan kemiripan yang lebih besar.
    3.  **Generasi Rekomendasi**: Ketika seorang pengguna memilih sebuah film, sistem akan mencari film-film lain yang memiliki skor kemiripan kosinus tertinggi dengan film yang dipilih tersebut, dan kemudian merekomendasikannya. Pendekatan ini memungkinkan sistem untuk merekomendasikan film yang memiliki "rasa" yang serupa dengan preferensi eksplisit pengguna.

Dengan demikian, proyek ini bertujuan untuk menunjukkan bagaimana sistem rekomendasi berbasis konten dapat secara efektif membantu pengguna menavigasi lautan pilihan film dan menemukan konten yang paling sesuai dengan selera mereka, hanya berdasarkan karakteristik film itu sendiri.

---

## Business Understanding
Bagian ini menguraikan pemahaman mendalam tentang masalah yang ingin diselesaikan oleh proyek sistem rekomendasi film ini, serta tujuan spesifik yang ingin dicapai.

#### **Problem Statements**

Proyek ini bertujuan untuk mengatasi beberapa tantangan utama yang dihadapi pengguna dan platform penyedia konten film:

1.  **Kesulitan Pengguna Menemukan Film yang Relevan (Information Overload)**: Dengan ribuan hingga jutaan judul film yang tersedia di berbagai platform *streaming*, pengguna seringkali merasa kewalahan dan kesulitan dalam menavigasi pilihan yang luas untuk menemukan film yang benar-benar sesuai dengan selera dan preferensi mereka. Hal ini dapat menyebabkan waktu pencarian yang lama atau bahkan frustrasi.
2.  **Kurangnya Personalisasi dalam Rekomendasi Film**: Banyak platform mungkin memiliki fitur pencarian atau kategori dasar, tetapi seringkali kurang dalam memberikan rekomendasi yang dipersonalisasi secara otomatis berdasarkan riwayat atau preferensi eksplisit pengguna terhadap atribut konten tertentu. Ini menghambat *discovery* film baru yang relevan bagi pengguna.
3.  **Potensi Penurunan Keterlibatan dan Retensi Pengguna**: Jika pengguna secara konsisten kesulitan menemukan konten yang menarik, tingkat *engagement* (seperti waktu tonton atau frekuensi penggunaan platform) dapat menurun. Dalam jangka panjang, ini berpotensi menyebabkan tingkat *churn* (pengguna berhenti berlangganan) yang lebih tinggi karena pengalaman yang tidak memuaskan.

#### **Goals**

Berdasarkan pernyataan masalah di atas, tujuan utama dari proyek sistem rekomendasi film ini adalah sebagai berikut:

1.  **Mempermudah *Discovery* Film yang Relevan**: Mengembangkan sistem yang mampu secara otomatis menyarankan film-film baru yang relevan kepada pengguna, sehingga mengurangi waktu dan usaha yang dibutuhkan pengguna untuk mencari film yang sesuai dengan preferensi mereka. Rekomendasi akan didasarkan pada karakteristik konten film itu sendiri, khususnya genre.
2.  **Meningkatkan Pengalaman Pengguna Melalui Personalisasi Konten (Berbasis Item)**: Menyediakan fitur rekomendasi film yang, meskipun sederhana, mampu memberikan rekomendasi yang terasa lebih personal dan relevan dengan preferensi konten pengguna. Dengan menganalisis genre film yang disukai, sistem dapat merekomendasikan film dengan profil genre yang serupa, meningkatkan kepuasan dan pengalaman menonton pengguna.
3.  **Potensi Peningkatan Keterlibatan Pengguna**: Dengan menyajikan rekomendasi film yang lebih tepat sasaran, proyek ini bertujuan untuk secara tidak langsung berkontribusi pada peningkatan *engagement* pengguna terhadap platform penyedia konten. Pengguna yang menemukan konten yang mereka sukai lebih mungkin untuk menghabiskan lebih banyak waktu di platform dan terus menggunakannya.

Melalui *Business Understanding* ini, proyek sistem rekomendasi *content-based filtering* ini diharapkan dapat menjadi solusi awal yang efektif untuk membantu pengguna menavigasi kompleksitas pilihan film dan meningkatkan pengalaman mereka secara keseluruhan.

---
## **Data Understanding**

Bagian ini menyajikan pemahaman mendalam tentang dataset yang digunakan dalam proyek sistem rekomendasi film ini. Dataset ini merupakan koleksi data rating film dan metadata yang komprehensif, sangat cocok untuk membangun dan mengevaluasi model rekomendasi berbasis pembelajaran mesin.

Dataset ini terdiri dari 100,836 interaksi rating pengguna terhadap film dan metadata dari 9,742 film unik. Kondisi data sangat baik; tidak ditemukan adanya *missing values* pada kolom-kolom penting yang akan digunakan, dan setelah pemeriksaan, tidak ada duplikasi data yang signifikan pada entri film atau rating yang memerlukan penanganan khusus di luar pembersihan genre.

**Sumber Data:**
Dataset ini dapat diunduh dari Kaggle, dengan tautan berikut: [https://www.kaggle.com/datasets/nicoletacilibiu/movies-and-ratings-for-recommendation-system](https://www.kaggle.com/datasets/nicoletacilibiu/movies-and-ratings-for-recommendation-system).

**Variabel-variabel pada Dataset:**

Dataset ini terbagi menjadi dua file utama: `movies.csv` yang berisi metadata film, dan `ratings.csv` yang berisi interaksi rating pengguna.

**📁 `movies.csv` (Berisi data metadata film)**

* **`movieId`** (`int64`): Merupakan ID unik untuk setiap film. Variabel ini berfungsi sebagai kunci penghubung dengan data rating, memastikan setiap film dapat diidentifikasi secara spesifik.
* **`title`** (`object`): Menyimpan judul lengkap dari film, seringkali disertai dengan tahun rilis dalam tanda kurung. Variabel ini digunakan untuk identifikasi film oleh pengguna dan sebagai input untuk fungsi rekomendasi.
* **`genres`** (`object`): Berisi daftar genre dari film, di mana setiap genre dipisahkan dengan karakter pipa (`|`). Contohnya adalah `Action|Adventure|Drama`. Variabel ini merupakan fitur konten utama yang akan diekstraksi dan digunakan untuk menghitung kemiripan antar film dalam sistem *content-based filtering*.

**📁 `ratings.csv` (Berisi data interaksi pengguna dan rating)**

* **`userId`** (`int64`): Merupakan ID anonim yang ditetapkan untuk setiap pengguna. Variabel ini digunakan untuk mengidentifikasi pengguna yang berbeda dalam sistem.
* **`movieId`** (`int64`): Merupakan ID film yang dirating oleh pengguna. Variabel ini berfungsi sebagai *foreign key* yang menghubungkan data rating kembali ke metadata film di `movies.csv`.
* **`rating`** (`float64`): Menyimpan nilai rating yang diberikan pengguna terhadap film, dengan skala umumnya dari 0.5 hingga 5.0. Variabel ini krusial untuk evaluasi model, di mana rating tinggi didefinisikan sebagai indikator relevansi.
* **`timestamp`** (`int64`): Mencatat waktu ketika rating diberikan, dalam format *Unix epoch time*. Meskipun ada dalam dataset, variabel ini tidak digunakan secara langsung dalam pemodelan *content-based filtering* ini.

Pemahaman terhadap struktur dan isi variabel-variabel ini sangat penting untuk tahapan *Data Preparation* dan *Modeling* selanjutnya dalam membangun sistem rekomendasi.

---
---
## **Data Preparation**
Proses persiapan data dilakukan secara berurutan melalui beberapa langkah utama:

1.  **Pembersihan dan Transformasi Kolom `genres` pada `movies_df`**:

      * **Teknik:** Penggantian nilai (`replace()`) dan aplikasi fungsi lambda (`apply()`).
      * **Proses:**
          * Nilai `'(no genres listed)'` pada kolom `genres` diganti dengan string kosong (`''`). Hal ini dilakukan untuk menyeragamkan representasi film yang tidak memiliki genre dan agar tidak mengganggu proses ekstraksi fitur berbasis teks.
          * Karakter pemisah genre `|` pada kolom `genres` diubah menjadi spasi (`     `). Ini menciptakan kolom baru bernama `clean_genres`.
      * **Alasan:** `TfidfVectorizer` (yang akan digunakan dalam tahap *Modeling*) bekerja paling efektif dengan teks yang dipisahkan oleh spasi. Dengan mengubah `Adventure|Animation` menjadi `Adventure Animation`, setiap genre dianggap sebagai "kata" terpisah yang dapat dianalisis oleh TF-IDF. Pembersihan `(no genres listed)` mencegah pembentukan fitur yang tidak relevan.

    <!-- end list -->

    ```python
    # Mengisi nilai "(no genres listed)" dengan string kosong
    movies_df['genres'] = movies_df['genres'].replace('(no genres listed)', '')
    # Mengubah format genres dari 'Action|Adventure' menjadi 'Action Adventure'
    movies_df['clean_genres'] = movies_df['genres'].apply(lambda x: x.replace('|', ' '))
    ```

2.  **Pemeriksaan Film Tanpa Genre Setelah Preprocessing**:

      * **Teknik:** Filtering DataFrame.
      * **Proses:** Saya melakukan pemeriksaan untuk mengidentifikasi berapa banyak film yang, setelah proses pembersihan, berakhir tanpa genre terdaftar (`clean_genres` adalah string kosong).
      * **Alasan:** Untuk memahami potensi dampak pada *content-based filtering*, karena film-film ini tidak akan memiliki fitur genre dan karenanya tidak akan berkontribusi pada atau direkomendasikan berdasarkan kemiripan genre. Dalam kasus ini, ditemukan 34 film tanpa genre.

    <!-- end list -->

    ```python
    # Memeriksa apakah ada film tanpa genre setelah preprocessing
    no_genre_movies = movies_df[movies_df['clean_genres'] == '']
    # print(f"\nJumlah film tanpa genre terdaftar setelah preprocessing: {len(no_genre_movies)}")
    ```

3.  **Penghapusan Kolom `timestamp` pada `ratings_df`**:

      * **Teknik:** Penghapusan kolom (`drop()`).
      * **Proses:** Kolom `timestamp` dihilangkan dari `ratings_df`.
      * **Alasan:** Kolom `timestamp` menyimpan informasi waktu rating diberikan, yang tidak relevan secara langsung untuk pendekatan *content-based filtering* yang berfokus pada atribut item. Penghapusan kolom ini membantu mengurangi jejak memori dan menyederhanakan DataFrame tanpa menghilangkan informasi krusial untuk model yang akan dibangun.

    <!-- end list -->

    ```python
    # Menghilangkan kolom 'timestamp' dari ratings_df
    ratings_df = ratings_df.drop('timestamp', axis=1)
    ```

4.  **Penggabungan DataFrame `ratings_df` dan `movies_df`**:

      * **Teknik:** Penggabungan DataFrame (`pd.merge()`).
      * **Proses:** Kedua DataFrame, `ratings_df` dan `movies_df`, digabungkan menjadi satu DataFrame bernama `df_merged` menggunakan `movieId` sebagai kunci penghubung (`how='left'`). Ini berarti semua rating akan digabungkan dengan informasi film yang sesuai.
      * **Alasan:** Penggabungan ini penting untuk menciptakan satu sumber data terpadu. Meskipun fitur konten utama berasal dari `movies_df`, penggabungan ini memungkinkan kita untuk:
          * Menghubungkan setiap rating pengguna dengan detail film yang relevan (judul dan genre).
          * Memudahkan proses evaluasi model di kemudian hari, di mana kita perlu mengidentifikasi film yang disukai pengguna berdasarkan rating mereka.

    <!-- end list -->

    ```python
    # Menggabungkan movies_df dan ratings_df
    df_merged = pd.merge(ratings_df, movies_df, on='movieId', how='left')
    ```

5.  **Penanganan Nilai Hilang Setelah Penggabungan (Jika Ada)**:

      * **Teknik:** Penghapusan baris (`dropna()`).
      * **Proses:** Setelah penggabungan, dilakukan pemeriksaan apakah ada nilai `NaN` (Not a Number) yang muncul pada kolom `title` atau `genres` di `df_merged`. Jika ada, baris-baris tersebut akan dihapus.
      * **Alasan:** Meskipun dataset aslinya relatif bersih, penggabungan dapat menciptakan `NaN` jika ada `movieId` di `ratings_df` yang tidak memiliki padanan di `movies_df`. Menghapus baris-baris ini memastikan konsistensi dan integritas data untuk pemodelan. Dalam kasus ini, tidak ada nilai `NaN` yang ditemukan, sehingga semua 100,836 entri rating berhasil dipasangkan dengan informasi film.

    <!-- end list -->

    ```python
    # Memeriksa dan menghilangkan baris dengan nilai NaN
    df_merged.dropna(subset=['title', 'genres'], inplace=True)
    ```

6.  **Memastikan Konsistensi Kolom `clean_genres` di `df_merged` (Pencegahan)**:

      * **Teknik:** Pengecekan kolom dan aplikasi fungsi.
      * **Proses:** Sebuah pemeriksaan dilakukan untuk memastikan bahwa kolom `clean_genres` yang telah dibuat di `movies_df` juga tersedia dan konsisten di `df_merged`. Jika tidak (misalnya, jika kode dijalankan secara parsial), transformasi akan diterapkan kembali.
      * **Alasan:** Untuk menjamin bahwa DataFrame final yang digunakan untuk analisis dan pemodelan selalu memiliki kolom `clean_genres` yang siap untuk TF-IDF.

    <!-- end list -->

    ```python
    if 'clean_genres' not in df_merged.columns:
        df_merged['clean_genres'] = df_merged['genres'].apply(lambda x: x.replace('|', ' '))
        df_merged['clean_genres'] = df_merged['clean_genres'].replace('(no genres listed)', '')
    ```

7.  **Ekstraksi Fitur Menggunakan TF-IDF (Persiapan Modeling)**:

      * **Teknik:** Vektorisasi Teks (`TfidfVectorizer`).
      * **Proses:** Setelah kolom `clean_genres` dipersiapkan, `TfidfVectorizer` digunakan untuk mengubah genre tekstual dari setiap film di `movies_df` menjadi representasi numerik dalam bentuk matriks TF-IDF. `stop_words='english'` digunakan untuk mengabaikan kata-kata umum.
      * **Alasan:** Ini adalah langkah fundamental untuk *content-based filtering*. TF-IDF memberikan bobot numerik kepada setiap genre berdasarkan frekuensinya dalam satu film (Term Frequency) dan jarang tidaknya genre tersebut muncul di seluruh korpus film (Inverse Document Frequency). Matriks numerik ini (`tfidf_matrix`) adalah input yang diperlukan untuk menghitung kemiripan kosinus antar film. Matriks yang dihasilkan memiliki dimensi $(9742, 21)$, yang berarti 9742 film direpresentasikan oleh 21 fitur genre unik.

    <!-- end list -->

    ```python
    # 1. Feature Extraction using TF-IDF
    tfidf = TfidfVectorizer(stop_words='english')
    tfidf_matrix = tfidf.fit_transform(movies_df['clean_genres'])
    # print(f"\nShape of TF-IDF matrix: {tfidf_matrix.shape}")
    ```

Melalui langkah-langkah *Data Preparation* ini, data telah berhasil dibersihkan, ditransformasi, dan digabungkan menjadi format yang optimal, menjadikannya siap untuk tahap *Modeling* selanjutnya dalam pembangunan sistem rekomendasi.

-----

---

## **Modeling**

Tahap *Modeling* adalah inti dari pembangunan sistem rekomendasi ini, di mana saya menerapkan algoritma dan teknik untuk memungkinkan sistem mengidentifikasi film-film yang relevan. Model yang dibangun didasarkan pada prinsip *Content-Based Filtering* dengan menggunakan *Cosine Similarity*.

#### **1. Ekstraksi Fitur Menggunakan TF-IDF**

Langkah pertama dalam pemodelan adalah mengubah data genre film yang bersifat tekstual menjadi representasi numerik yang dapat diproses oleh algoritma. Saya menggunakan teknik **TF-IDF (Term Frequency-Inverse Document Frequency)** untuk tujuan ini.

* **`TfidfVectorizer`**: Digunakan untuk mengonversi kumpulan teks (`clean_genres`) menjadi matriks fitur TF-IDF. Setiap baris dalam matriks ini merepresentasikan sebuah film, dan setiap kolom merepresentasikan bobot TF-IDF dari suatu genre dalam film tersebut. `stop_words='english'` digunakan untuk mengabaikan kata-kata umum yang tidak informatif.
* **`tfidf_matrix.shape: (9742, 21)`**: Matriks TF-IDF yang dihasilkan memiliki 9742 baris (sesuai dengan jumlah film unik) dan 21 kolom (mewakili 21 fitur/genre unik yang teridentifikasi dalam dataset). Ini menunjukkan bahwa setiap film sekarang direpresentasikan sebagai vektor 21 dimensi berdasarkan komposisi genrenya.

#### **2. Perhitungan Cosine Similarity**

Setelah fitur genre diekstraksi ke dalam bentuk numerik (matriks TF-IDF), langkah selanjutnya adalah menghitung tingkat kemiripan antara setiap pasangan film. Saya menggunakan metrik **Cosine Similarity** untuk ini.

* **`cosine_similarity(tfidf_matrix, tfidf_matrix)`**: Fungsi ini menghitung kemiripan kosinus antara setiap vektor film dalam `tfidf_matrix` dengan semua vektor film lainnya. Kemiripan kosinus mengukur sudut antara dua vektor; sudut yang lebih kecil (nilai kosinus mendekati 1) menunjukkan kemiripan yang lebih tinggi.
* **`cosine_sim.shape: (9742, 9742)`**: Hasilnya adalah matriks persegi `cosine_sim` berukuran 9742x9742. Setiap sel `(i, j)` dalam matriks ini menyimpan skor kemiripan antara film ke-i dan film ke-j.

#### **3. Pembuatan Peta Indeks Film**

Untuk memudahkan pengambilan rekomendasi berdasarkan judul film, saya membuat pemetaan antara judul film dan indeks baris/kolomnya dalam matriks kemiripan.

* **`indices = pd.Series(movies_df.index, index=movies_df['title']).drop_duplicates()`**: Ini menciptakan objek `Series` yang memungkinkan kita dengan cepat menemukan indeks numerik suatu film dari judulnya, dan sebaliknya. Indeks ini sangat penting karena ia sesuai dengan baris dan kolom di `cosine_sim` matriks.
    ```
    --- Sample of Movie Titles to Index Mapping ---
    title
    Toy Story (1995)                      0
    Jumanji (1995)                        1
    Grumpier Old Men (1995)               2
    Waiting to Exhale (1995)              3
    Father of the Bride Part II (1995)    4
    dtype: int64
    ```

#### **4. Fungsi Rekomendasi Film (`get_recommendations`)**

Fungsi ini adalah implementasi inti dari sistem rekomendasi. Ia mengambil judul film sebagai input, mencari indeksnya, kemudian menggunakan matriks `cosine_sim` untuk menemukan film-film paling mirip.

* **Cara Kerja**:
    1.  Mencari indeks film input menggunakan peta `indices`.
    2.  Mengambil semua skor kemiripan film input dari matriks `cosine_sim`.
    3.  Mengurutkan skor kemiripan secara menurun.
    4.  Mengambil 10 film teratas yang paling mirip (tidak termasuk film input itu sendiri).
    5.  Mengembalikan judul-judul film yang direkomendasikan.

#### **Output Top-N Recommendation:**

Berikut adalah contoh rekomendasi yang dihasilkan oleh model untuk beberapa film:

* **Rekomendasi untuk 'Toy Story (1995)'**:
    Rekomendasi yang diberikan sangat konsisten dengan genre 'Toy Story', yaitu `Adventure|Animation|Children|Comedy|Fantasy`. Film-film seperti 'Antz', 'Toy Story 2', 'Monsters, Inc.', dan 'Shrek the Third' memiliki genre yang sangat mirip, seperti Animation, Children, Comedy, dan Adventure.

    ```
    --- Rekomendasi untuk 'Toy Story (1995)' ---
    1706                                          Antz (1998)
    2355                                   Toy Story 2 (1999)
    2809       Adventures of Rocky and Bullwinkle, The (2000)
    3000                     Emperor's New Groove, The (2000)
    3568                                Monsters, Inc. (2001)
    6194                                     Wild, The (2006)
    6486                               Shrek the Third (2007)
    6948                       Tale of Despereaux, The (2008)
    7760    Asterix and the Vikings (Astérix et les Viking...
    8219                                         Turbo (2013)
    Name: title, dtype: object
    ```

* **Rekomendasi untuk 'Jumanji (1995)'**:
    'Jumanji' memiliki genre `Adventure|Children|Fantasy`. Rekomendasi yang muncul seperti 'Indian in the Cupboard, The', 'NeverEnding Story' series, dan 'Harry Potter' sangat cocok karena mereka berbagi genre Adventure, Children, dan Fantasy.

    ```
    --- Rekomendasi untuk 'Jumanji (1995)' ---
    53                     Indian in the Cupboard, The (1995)
    109                     NeverEnding Story III, The (1994)
    767                       Escape to Witch Mountain (1975)
    1514            Darby O'Gill and the Little People (1959)
    1556                                  Return to Oz (1985)
    1617                        NeverEnding Story, The (1984)
    1618    NeverEnding Story II: The Next Chapter, The (1...
    1799                        Santa Claus: The Movie (1985)
    3574    Harry Potter and the Sorcerer's Stone (a.k.a. ...
    6075    Chronicles of Narnia: The Lion, the Witch and ...
    Name: title, dtype: object
    ```

* **Rekomendasi untuk 'Harry Potter and the Sorcerer\'s Stone (a.k.a. Harry Potter and the Philosopher\'s Stone) (2001)'**:
    Film ini memiliki genre `Adventure|Children|Fantasy|Mystery`. Rekomendasi yang diberikan sangat mirip dengan 'Jumanji' karena film-film ini juga banyak berbagi genre Adventure, Children, dan Fantasy.

    ```
    --- Rekomendasi untuk 'Harry Potter and the Sorcerer's Stone (a.k.a. Harry Potter and the Philosopher's Stone) (2001)' ---
    53                     Indian in the Cupboard, The (1995)
    109                     NeverEnding Story III, The (1994)
    767                       Escape to Witch Mountain (1975)
    1514            Darby O'Gill and the Little People (1959)
    1556                                  Return to Oz (1985)
    1617                        NeverEnding Story, The (1984)
    1618    NeverEnding Story II: The Next Chapter, The (1...
    1799                        Santa Claus: The Movie (1985)
    3574    Harry Potter and the Sorcerer's Stone (a.k.a. ...
    6075    Chronicles of Narnia: The Lion, the Witch and ...
    Name: title, dtype: object
    ```

* **Contoh Film Tidak Ada**:
    Fungsi juga dirancang untuk menangani kasus di mana judul film input tidak ditemukan dalam database, memberikan pesan yang informatif.

    ```
    --- Rekomendasi untuk 'Film Tidak Ada (2025)' (contoh film yang tidak ada) ---
    Film dengan judul 'Film Tidak Ada (2025)' tidak ditemukan dalam database.
    Series([], dtype: object)
    ```

Contoh-contoh di atas menunjukkan bahwa sistem rekomendasi berbasis konten ini berhasil memberikan rekomendasi film yang secara tematis dan genre terkait dengan film input, sesuai dengan prinsip *content-based filtering* menggunakan *cosine similarity*.

---


## **Evaluasi Model**

Pada bagian evaluasi ini, saya mengukur kinerja sistem rekomendasi *content-based filtering* dengan menggunakan metrik standar dalam sistem rekomendasi, yaitu **Precision@k** dan **Recall@k**. Evaluasi dilakukan dengan mensimulasikan rekomendasi untuk sejumlah pengguna berdasarkan film yang mereka sukai (rating $\geq 4.0$) dan membandingkannya dengan film lain yang juga mereka sukai. Nilai $k$ ditetapkan sebesar 10, yang berarti kita mengevaluasi 10 rekomendasi teratas yang diberikan.

**Metrik Evaluasi yang Digunakan:**

1.  **Precision@k**
    Precision@k mengukur proporsi rekomendasi yang benar-benar relevan dari $k$ item teratas yang diberikan. Ini menjawab pertanyaan: "Dari rekomendasi yang diberikan, berapa banyak yang sebenarnya disukai pengguna?"

    Formula yang digunakan:
    $$\text{Precision@k} = \frac{\text{Jumlah rekomendasi relevan di top-k}}{\text{Total rekomendasi di top-k}} = \frac{TP}{TP + FP}$$
    Di mana:
    * $TP$ (True Positives): Jumlah film yang direkomendasikan dan memang disukai pengguna.
    * $FP$ (False Positives): Jumlah film yang direkomendasikan tetapi tidak disukai pengguna.

2.  **Recall@k**
    Recall@k mengukur proporsi item relevan yang berhasil ditemukan dalam $k$ rekomendasi teratas. Ini menjawab pertanyaan: "Dari semua film yang disukai pengguna, berapa banyak yang berhasil direkomendasikan?"

    Formula yang digunakan:
    $$\text{Recall@k} = \frac{\text{Jumlah rekomendasi relevan di top-k}}{\text{Total item relevan}} = \frac{TP}{TP + FN}$$
    Di mana:
    * $TP$ (True Positives): Jumlah film yang direkomendasikan dan memang disukai pengguna.
    * $FN$ (False Negatives): Jumlah film yang disukai pengguna tetapi tidak direkomendasikan.

**Hasil Evaluasi Proyek:**

Setelah melakukan evaluasi terhadap 50 pengguna, hasil metrik Precision@10 dan Recall@10 adalah sebagai berikut:

* **Rata-rata Precision@10:** 0.0660
* **Rata-rata Recall@10:** 0.0020

**Interpretasi Hasil Evaluasi:**

* **Rata-rata Precision 0.0660** menunjukkan bahwa sekitar 6.60% dari film yang direkomendasikan cocok dengan preferensi tinggi pengguna. Ini mengindikasikan bahwa meskipun sistem memberikan rekomendasi, tingkat akurasinya dalam memprediksi film yang benar-benar akan disukai pengguna masih relatif rendah.
* **Rata-rata Recall 0.0020** menunjukkan bahwa hanya sekitar 0.20% dari film yang sebenarnya disukai pengguna berhasil ditangkap oleh sistem rekomendasi. Angka yang sangat rendah ini mengisyaratkan bahwa model memiliki keterbatasan signifikan dalam menemukan sebagian besar film relevan yang disukai pengguna.
* Nilai ini memberikan gambaran awal tentang performa model. Precision yang relatif rendah mengindikasikan bahwa rekomendasi seringkali belum sesuai dengan film lain yang disukai pengguna. Recall yang rendah juga menunjukkan bahwa banyak film yang disukai pengguna tidak berhasil direkomendasikan oleh sistem.
* Perlu diingat bahwa dalam sistem *content-based* murni seperti ini, rekomendasi sangat bergantung pada kemiripan genre input film. Model tidak mempelajari preferensi individual pengguna secara langsung (seperti yang dilakukan oleh *collaborative filtering*), sehingga kemampuannya untuk menangkap preferensi luas pengguna terbatas pada kesamaan genre dari film input. Untuk meningkatkan performa, pendekatan hibrida atau *collaborative filtering* mungkin diperlukan.

---
