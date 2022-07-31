# **Laporan Proyek Machine Learning - Abdul Azis**

## **Project Overview**
### **Latar Belakang**
Menurut Mohammad Irfan, Andharini Dwi Cahyani dan Fika Hastarita R (2014) didalam jurnal yang mereka tulis berjudul [Sistem Rekomendasi: Buku Online dengan metode _Collaborative Filtering_](https://ejournal.akprind.ac.id/index.php/technoscientia/article/view/612) menyatakan bahwa buku merupakan informasi segala kebutuhan yang diperlukan, dimulai dari iptek, seni budaya, ekonomi, politik, sosial dan pertahanan keamanan dan lain-lain. Upaya membaca buku membuka wawasan dunia intelek sehingga dapat mengubah masa depan serta mencerdaskan akal, pikiran dan iman.Dengan membaca buku, selain pengetahuan akan semakin bertambah, pribadi akan  semakin kaya, yang kesemuannya jelas akan menurunkan efek negatif terhadap anak-anak, yakni kenakalan. Sedangkan anak yang tidak terbina minat bacanya sejak dini akan menghadapi peluang yang semakin kecil untuk mengembangkan pengetahuan setinggi-tingginya. Namun berdasarkan laporan Bank Dunia, Indonesia merupakan negara yang memiliki minatbaca sangat rendah. Hal tersebut sungguh disayangkan, mengingat sebagai negara besar, Indonesia memiliki potensi besar untuk menjadi negarayang unggul.

Rendahnya minat baca dikalangan masyarakat menjadi persoalan penting didunia pendidikan saat ini. Untuk itu diperlukan sebuah sistem yang dapat membantu merekomendasikan para pembaca agar lebih mudah mendapatkan informasi buku-buku yang akan dibaca selanjutnya. Banyaknya jumlah buku akan membuat pembaca terkadang kesulitan dalam menentukan buku yang hendak mereka baca selanjutnya.Terkadang dijumpai pembaca yang hanya ingin membaca buku-buku yang dengan reputasi penjualan terbaik. Ada pula pembaca yang hanya ingin membaca buku yang mirip dengan buku-buku yang pernah dibaca sebelumnya. Tidak jarang juga ditemui pembaca yang menentukan buku-buku yang akan dibaca selanjutnya berdasarkan rating dari buku-buku yang telah dilihatnya. Semakin tinggi rating dari buku tersebut, semakin tertarik pula pembaca untuk membacanya. Semakin rendah rating dari buku tersebut, maka pembaca cenderung enggan untuk membacanya. Tinggi rendahnya rating tersebut mempengaruhi buku-buku yang akan direkomendasikan. Nilai kemiripan antar buku dan rating buku dapat dijadikan landasan untuk memberikan rekomendasi buku kepada pembaca.

Berdasarkan latar belakang yang telah dijelaskan di atas, topik proyek ini diambil dengan tujuan sebagai domain proyek machine learning yang akan dibuat. Selain itu, proyek ini dibuat untuk dapat melengkapi fitur yang dapat digunakan pada proyek aplikasi yang akan dibuat oleh penulis. Diharapkan sistem rekomendasi ini dapat digunakan pada sebuah aplikasi dan memberikan rekomendasi yang relevan sesuai dengan preferensi pengguna dan dapat meningkatkan kenyamanan pengguna saat menggunakan aplikasi.

## **Business Understanding**
### **Problem Statement**
Berdasarkan pada latar belakang di atas, permasalahan yang dapat diselesaikan pada proyek ini adalah sebagai berikut:

* Bagaimana cara melakukan pengelolahan data sehingga dapat menghasilkan rekomendasi yang baik dan relevan?
* Bagaimana cara membangun sistem untuk merekomendasikan buku yang yang sesuai dengan preferensi pengguna?
### **Goals**
Tujuan dibuatnya proyek ini adalah sebagai berikut:

* Melakukan pengolahan data yang baik agar dapat digunakan dalam membangun sistem rekomendasi yang baik.
* Membangun model machine learning untuk merekomendasikan sebuah buku yang sesuai dengan preferensi pengguna.
### **Solution**
Solusi yang dapat diterapkan agar goals diatas terpenuhi adalah sebagai berikut:

* Melakukan analisa pada data untuk dapat memahami data yang ada seperti: Memeriksa _missing value_ dan duplikasi data.
* Melakukan pemrosesan pada data seperti Normalisasi data rating.
* Membangung sistem rekomendasi menggunakan 2 teknik yang umum digunakan yaitu: _Content-Based Filtering_ dan _Collaborative Filtering_. 

## **Data Understanding**
Dataset yang di gunakan pada proyek machine learning ini merupakan dataset buku lengkap dengan rating, pengarang dan penerbit-nya. Dataset tersebut dapat di unduh di website kaggle: [Book Recommendation Dataset](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset).

Terdapat 3 file pada dataset, antara lain:
* Books.csv
* Ratings.csv
* Users.csv

Pada proyek ini hanya menggunakan 2 file data, yaitu:
* Books.csv</br>
    File ini memiliki total jumlah 271360 data buku dan dan memiliki 8 kolom variabel data. Berikut penjelasan untuk masing-masing variabel:</br>
    * `ISBN`: Kode pengidentifikasian buku yang bersifat unik.
    * `Book-Title`: Judul Buku.
    * `Book-Author`: Nama pengarang buku.
    * `Year-Of-Publication`: Tahun penerbitan buku.
    * `Publisher`: Pihak penerbit buku.
    * `Image-URL-S`: URL yang menautkan ke gambar sampul berukuran kecil.
    * `Image-URL-M`: URL yang menautkan ke gambar sampul berukuran normal.
    * `Image-URL-L`: URL yang menautkan ke gambar sampul berukuran besar.

* Ratings.csv</br>
    File ini memiliki total jumlah 1149780 data rating dan dan memiliki 3 kolom variabel data. Berikut penjelasan untuk masing-masing variabel:</br>
    * `User-ID`: Nomer unik user yang memberikan rating.
    * `ISBN`: Kode pengidentifikasian buku yang bersifat unik.
    * `Book-Rating`: Skor dari rating yang diberikan.

Untuk dapat lebih memahami data perlu dilakukan eksplorasi pada data, eksplorasi yang di lakukan antara lain: 

* Memeriksa informasi pada data</br>
    * Books
    <image src='https://raw.githubusercontent.com/ziszz/book-recommendation/master/visualizations/info_books.png' width=100% /></br>
    Berdasarkan output di atas, dapat diketahui bahwa file Books.csv memiliki 271360 entri. Kemudian, semua kolom data memiliki type data object, sedangkan untuk kolom data `Year-Of-Publication` memiliki tipe data object yang mana seharusnya data tersebut memiliki tipe data number, tetapi hal ini tidak menjadi masalah sebab data ini tidak diperlukan untuk membuat sistem rekomendasi.</br>
    <image src='https://raw.githubusercontent.com/ziszz/book-recommendation/master/visualizations/book_count.png' width=100% /></br>
    <image src='https://raw.githubusercontent.com/ziszz/book-recommendation/master/visualizations/authors_count.png' width=100% /></br>
    Kemudian terdapat jumlah 242135 buku dan 102023 _author_ (pengarang) pada data.
    
    * Ratings
    <image src='https://raw.githubusercontent.com/ziszz/book-recommendation/master/visualizations/info_ratings.png' width=100% /></br>
    Untuk data ratings, memiliki 1149780 entri dan terdapat 2 tipe pada data yaitu number (int64) dan object.
    <image src='https://raw.githubusercontent.com/ziszz/book-recommendation/master/visualizations/ratings_count.png' width=100% /></br>
    dapat dilihat pada gambar di atas, nilai maksimum rating adalah 10 dan nilai minimumnya adalah 0. Artinya, skala rating berkisar antara 0 hingga 10. Lalu mayoritas buku memiliki rating=0 yaitu sebanyak 716109 buku.

* Memeriksa _Missing Value_</br>
    <image src='https://raw.githubusercontent.com/ziszz/book-recommendation/master/visualizations/ratings_count.png' width=100% /></br>
    