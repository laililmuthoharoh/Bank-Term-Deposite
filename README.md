# Bank-Term-Deposite

## Backround
Sebuah Lembaga perbankan di Portugis ingin melakukan kampanye pemasaran langsung yaitu melalui panggilan telepon untuk mempromosikan produknya yaitu Term Deposite (Deposito Berjangka). Untuk menghemat cost dalam project kampanye Term Deposite ini, tentu pihak bank tidak mungkin menghubingi semua nasabah yang terdaftar. Bank memerlukan suatu cara yang efektif untuk menyeleksi nasabahnasabah yang berpotensi untuk berlangganan Term Deposite.

## Objective
Masalah yang harus diselesaikan di sini adalah bagaimana caranya agar Bank dapat memprediksi dengan benar nasabah-nasabah mana saja yang nantinya akan berlangganan Term Deposite. Untuk menyelesaikan masalah ini, dapat dilakukan pemodelan klasifikasi dengan machine learning dengan tujuan memprediksi apakah nasabah akan berlangganan Term Deposite. Pemodelan ini dilakukan dengan memanfaatkan data nasabah sebagai input, yaitu seperti job, marital, education, default, housing, loan, contact, month, dll, dengan output berupa variabel yang menjelaskan status langganan Term Deposite nasabah.

Kemudian, ada beberapa pemodelan machine learning yang bisa dimanfaatkan untuk penyelesaian masalah ini. Diantaranya adalah pemodelan Logistric Regression dan pemodelan dengan Random Forest.

Akan dilakukan klasifikasi menggunakan dua metode ini. Kemudian dibandingkan hasilnya dan diambil metode yang terbaik untuk kemudian digunakan pada proses deployment.

## Dataset
Dataset yang digunakan merupakan data nasabah dari sebuah Lembaga di Potugis. Data memiliki total 4521 baris dengan 17 variabel. Berikut diberikan penjelasan mengenai masing-masing variabel atau fitur.

Daftar varibel atau fitur:

![image](https://github.com/laililmuthoharoh/Bank-Term-Deposite/assets/124485986/e97322ab-cc40-495f-9525-bdc2a619a55e)

Data Input:
1. age (numerik): usia
2. job (kategorikal): jenis pekerjaan
3. marital (kategorikal): status pernikahan
4. education (kategorikal): pendidikan
5. default (kategorikal): status kepemilikan kredit macet
6. balance (numerik): saldo rekening
7. housing (kategorikal): status kepemilikan housing loan
8. loan (kategorikal): status kepemilikan personal loan
9. contact (kategorikal): jenis kontak untuk komunikasi (cellular/telephone)
10. month (kategorikal): bulan kontak terakhir
11. day_of_week (kategorikal): hari kontak terakhir
12. duration (numerik): durasi kontak terakhir [Catatan penting: variabel ini sangat memengaruhi target output (misalnya, jika durasi=0 maka y=’tidak’) karena durasi diperoleh ketika nasabah sudah dihubungi.
13. kampanye (numerik): jumlah kontak yang dilakukan dalam kampanye ini untuk nasabah ini
14. pdays (numerik): jumlah hari berlalu sejak nasabah dihubungi dari kampanye sebelumnya (999 berarti nasabah belum dikontak sebelumnya)
15. previous (numerik): jumlah kontak yang dilakukan sebelum kampanye ini untuk nasabah ini
16. poutcome (kategorikal): hasil dari marketing kampanye sebelumnya

Data Output:
1. y (kategorik) : Apakah nasabah sudah berlangganan Term Deposite? 

Dengan sumber data yang digunakan: https://archive.ics.uci.edu/dataset/222/bank+marketing

## Metode
Pemodelan Machine Learning Logistic Regression adalah teknik dalam machine learning yang digunakan untuk melakukan klasifikasi data. Logistic Regression mengadopsi fungsi logistik (sigmoid) untuk memodelkan hubungan antara variabel independen (fitur input) dengan variabel dependen (output). Tujuannya adalah untuk memprediksi probabilitas kejadian suatu kelas atau untuk melakukan klasifikasi biner.
![image](https://github.com/laililmuthoharoh/Bank-Term-Deposite/assets/124485986/62fa0406-f49f-49b1-b573-00e8c96ad052)

## Result
Untuk melakukan pemodelan, dilakukan bebrapa tahap berikut:

### Dataset
1. Mengakses Data
   ![image](https://github.com/laililmuthoharoh/Bank-Term-Deposite/assets/124485986/30b0d729-db53-4a21-a656-7f26de9852f5)

2. Data Cleansing
   Dilakukan penggantian isi dari variabel “pdays”, dimana sesuai keterangan awal, untuk input negatif hatus diganti dengan nilai 999, yang artiya belum pernah dilakukan kontak dnegan nasabah.
   ![image](https://github.com/laililmuthoharoh/Bank-Term-Deposite/assets/124485986/4a7199c3-3c7e-407e-b20a-48b6e68142f5)

   Dilakukan pengecekan data duplicate sebagai berikut.
   ![image](https://github.com/laililmuthoharoh/Bank-Term-Deposite/assets/124485986/cc43f0fc-26b2-4af3-8834-d8e61d99630b)
   dan tidak ditemukan data duplicate.

   Dilakukan pengecekan data kosong sebagai berikut.
   ![image](https://github.com/laililmuthoharoh/Bank-Term-Deposite/assets/124485986/413ac8f0-c5d8-4c01-901a-661053005c36)
   dan tidak ditemukan data kosong.
   
5. EDA
   Analisis data eksplorasi ini dilakukan dengan membagi data menjadi dua kategori yaitu:

   i. data numerial
   ![image](https://github.com/laililmuthoharoh/Bank-Term-Deposite/assets/124485986/dd393059-1e47-45c5-806f-6e55708ff09c)

   ii. data categorical
   ![image](https://github.com/laililmuthoharoh/Bank-Term-Deposite/assets/124485986/8970d4ac-94dc-442f-ae79-6ddd49c8dc10)
   Kemudian, dari data numerical dibuat histogram untuk mengetahui sebaran distrbusi masing-masing variabel.
   ![image](https://github.com/laililmuthoharoh/Bank-Term-Deposite/assets/124485986/046f40b2-8193-4272-9ccb-d61cccccdd66)
   Terlihat bahwa ada variabel yang belum berdistribusi normal. Oleh karena itu, untuk proses pemodelan nanti harus dilakukan normalisasi agar diperoleh hasil yang lebih maksimal.
   
### Data Processing
Pada proses ini, dilakukan pembagian data antara data output dan input.

1. data output
   ![image](https://github.com/laililmuthoharoh/Bank-Term-Deposite/assets/124485986/7708f715-a087-4bbc-b888-f48a083a1d81)

2. data input
   ![image](https://github.com/laililmuthoharoh/Bank-Term-Deposite/assets/124485986/46589173-0ce4-4cee-a55f-f550db43838c)
   Selanjutnya, data dibagi menjadi dua bagian yaitu data train dan data test dengan presentasi 3:1.
   ![image](https://github.com/laililmuthoharoh/Bank-Term-Deposite/assets/124485986/5182ec61-2729-4297-846c-50daf6bf2899)
   
### Training Machine Learning
1. Baseline
   Karena ini klasifikasi, Baseline kita ambil dari proporsi kelas target yang terbesar. Dengan kata lain, menebak hasil output marketing response dengan nilai “no” semua tanpa modeling.
   ![image](https://github.com/laililmuthoharoh/Bank-Term-Deposite/assets/124485986/12f48fcc-1577-4d4c-8958-9d47170bb8e1)

3. Pemodelan Logistic Regression
   Data Train
   ![image](https://github.com/laililmuthoharoh/Bank-Term-Deposite/assets/124485986/ab96e9a2-8f38-45a7-a270-f700773c834c)
   ![image](https://github.com/laililmuthoharoh/Bank-Term-Deposite/assets/124485986/584824bb-e98b-4983-91fa-404ca3d1aeae)
   ![image](https://github.com/laililmuthoharoh/Bank-Term-Deposite/assets/124485986/9a9e6fee-fe51-454b-ab40-9d55c512d7f6)
   ![image](https://github.com/laililmuthoharoh/Bank-Term-Deposite/assets/124485986/59e47c03-6208-49e3-98a4-eb0c62c9fd55)

   Data Test
   ![image](https://github.com/laililmuthoharoh/Bank-Term-Deposite/assets/124485986/70220636-bc80-43ee-b72e-3642fc932645)
   ![image](https://github.com/laililmuthoharoh/Bank-Term-Deposite/assets/124485986/a20ea07e-9719-43d2-9871-18f4c1879aa9)
   ![image](https://github.com/laililmuthoharoh/Bank-Term-Deposite/assets/124485986/17b6be55-48c4-4f60-a4a5-9fbce6196d4f)
   ![image](https://github.com/laililmuthoharoh/Bank-Term-Deposite/assets/124485986/fa11329c-1d53-4026-962e-465421e69557)

## Conclution
Tujuan dari pemodelan ini adalah membantu bank mengurangi cost dan menghemat waktu untuk kampanye (menghubungi nasabah satu-satu) dengan untuk memprediksi nasabah yang berpotensi berlangganan Term Deposite. Pemodelan ini difokuskan pada nilai recall dan AUC, dimana bank hanya akan menghubungi nasabah dengan hasil prediksi positif.

Dari hasil pemodelan, diperoleh kesimpulan berikut:

Data train:
`Accuracy Score is 0.898
F1 Score is 0.282
Precission Score is 0.648
Recall Score is 0.18
AUC = 0.58`

Data test:
`Accuracy Score is 0.876
F1 Score is 0.195
Precission Score is 0.548
Recall Score is 0.119
AUC = 0.550`

Dari hasil di atas, diperoleh kesimpulan bahwa akurasi pemodelan untuk memperoleh nilai recall maksimal masing sangat lemah. Oleh karena itu, dapat dikembangkan lagi pemodelan yang lebih baik untuk kasus prediksi nasabah Term Deposite ini.

