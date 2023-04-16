# Final Project: E-Commerce Shipping Data

kelompok 5 (pentagon)
Rakamin Academy Data Science Bootcamp Batch 31:
1. Ilman Nafiian (Leader)
2. Adam Adiwangsa
3. Akmalia Lutfiaturrosyida
4. Divyah Laksmi
5. Freddy Kurniawan
6. M. Lutfhi
7. Putri Qonitah
8. Salma Immala

Dataset dapat diakses [E-Commerce Shipping Data](https://www.kaggle.com/datasets/prachi13/customer-analytics)

# 1. Problem Statement
Perusahaan Pentagon sedang menganalisis bagaimana data shipping di perusahaan e-commerce yang terdiri dari 10999 observasi data. Dari data tersebut dikrtahui tingkat keterlambatan pengiriman yang terjadi di perusahaan adalah sebesar 59.7%. Menurut reference yang kami ambil dari shopee tingkat keterlambatan pengiriman barang e-commerce yang baik adalah dibawah 10%. Hal ini menunjukkan bahwa perusahaan e-commerce ini memiliki tingkat keterlambatan pengiriman yang cukup tinggi. Tingkat keterlambatan yang tinggi dapat memberikan dampak pada <em>revenue</em> yang akan terus menerus menurun.

![late shippment precentage](https://user-images.githubusercontent.com/130851526/232289332-b233e498-f882-4b61-a5a0-aaabc16e2517.jpg)

late shippment precentage
## 2. Objective, Business Metrics dan Goal
- Objective:
1. Membuat model prediksi keterlambatan delivery untuk memberikan notification internal perusahaan.
2. Root cause Analysis.
3. Memberikan insight menaikan nilai on time delivery.


- Business Metrics:
Delivery On Time.

- Goal:
Mengurangi tingkat keterlambatan delivery menjadi 10% dalam kurun waktu 12 bulan.

## 3. Exploratory Data Analysis (EDA)
### Descriptive Analysis
Dataset terdiri atas 10 feature dan 1 target, yaitu:
- 10 features
1. Numerical
- Cost
- Weight
- Discount
- Calls
- Prior_Purchases
2. Categorical
- Importance
- Gender
- Warehouse
- ID
- Rating

target: 
Reached On Time yang diubah menjadi Late (keterlambatan pengiriman)

- data duplicate 0

![Screenshot 2023-04-16 171958](https://user-images.githubusercontent.com/130851526/232295882-30aaad04-d877-4193-a482-9dfbb9692576.png)

- missing value 0

![Screenshot 2023-04-16 171925](https://user-images.githubusercontent.com/130851526/232296029-d9b4dd0f-d603-4c64-a87e-f1f3b788c87b.png)

### Univariate Analysis
![blob 7](https://user-images.githubusercontent.com/130851526/232291141-a08b9bb8-d3c0-4b34-8996-b26df0fd3fd7.jpg)
Berdasarkan distribution plot di atas dapat diketahui bahwa:
- Fitur diskon memiliki distribusi positively skewed, untuk pesanan yang tidak telat kebanyakan memiliki diskon yang tidak terlalu besar <10%. 
- Terdapat ketimpangan data dimana pesanan dengan berat 2-4 kg hampir tidak ada yang tepat waktu. Terdapat pola menarik dimana transaksi dengan weight_gram berkisar 1-2 kg & 4-6 kg menunjukkan pengiriman tepat waktu.


![blob 6](https://user-images.githubusercontent.com/130851526/232291165-39b148fc-305d-4e28-bb97-783661b4a76c.jpg)
Pada boxplot, ditemukan adanya outlier pada feature discount dan prior_purchases. Terutama prior_purchases memiliki beberapa outlier yang cukup jauh.

### Multivariate Analysis
![blob (3)](https://user-images.githubusercontent.com/130851526/232291725-00ec8791-1ec7-4fa8-8ac4-df9b73fca226.jpg)
dari heatmap plot terlihat, Fitur discount terhadap late memiliki korelasi paling tinggi sebesar 0,4 dan Fitur weight_gram memiliki korelasi negatif terhadap late senilai -0.27.

## 4. Data Pre-Processing
![WhatsApp Image 2023-04-16 at 5 07 32 PM 1](https://user-images.githubusercontent.com/130851526/232293304-03b96614-ec0d-40b2-a40d-64457f54d145.jpeg)

## 5. Data Cleansing
### Handle Outliers & Feature Transformation
![Screenshot 2023-04-16 173205](https://user-images.githubusercontent.com/130851526/232298683-9521a5ea-486f-4aa8-86a6-485e5456fdca.png)
- Log Transformasi 

Sebelum melakukan pengecekan outlier, seluruh data numerical kami pastikan memiliki distribusi normal terlebih dahulu. Setelah melihat semua distribusi numerical data, dapat dilihat bahwa pada feature discount dan prior purchase memiliki distribusi positively skewed. Kami melakukan log transformasi pada dua feature tersebut, setelah melakukan log transformasi skewness dari dua feature tersebut berkurang dan mendekati distribusi normal.

- Remove outlier menggunakan Z-Score
- Normalization (Scalling)

### Feature Encoding

Kami melakukan dua tipe encoding yaitu one hot encoding dan label encoding. Pada data ini kami melakukan one hot encoding pada feature warehouse dan shipment karena kategorikal yang tidak bersifat ordinal, dan label encoding kami lakukan pada feature gender dan importance karena kategorikal yang bersifat ordinal.

### Handle Class Imbalance
Pada gambar diatas dapat dilihat bahwa perbandingan ratio late 59.03 dan ratio on time 40.97, dikarenakan proporsi kelas minoritas ratio diatas 40, maka tidak diperlukan handle class imbalance. 

## 6. Feature Engineering
### Feature selection 
Berdasarkan Heatmap plot, Fitur ID dihapuskan karena tidak memiliki makna penting pada saat pemodelan
### Feature Extraction 
Kami memutuskan untuk tidak menambah feature apapun dikarenakan untuk pemodelan yang akan kami lakukan feature yang ada sudah cukup menginterpretasikan modelling yang akan kami buat.
### Feature tambahan 
1. Data Repurchase
2. Expedition Data
3. Shipping address 
4. Time of purchase  


## 7. Insight Bisnis dan Rekomendasi
### Bussiness Insight
1. produk dengan diskon produk >10% cenderung akan mengalami keterlambatan.
2. produk dengan berat berkisar antara 2-4 kg, berpotensi besar mengalami keterlambatan pengiriman.

## Rekomendasi
1. Berdasarkan distribution plot discount dapat diketahui bahwa barang dengan diskon diatas 20% cenderung terlambat, hal ini dapat dijadikan sebuah himbauan bagi perusahaan agar lebih memperhatikan barang-barang dengan diskon yang tinggi. Apabila diskon yang tinggi ini diadakan di saat tertentu seperti harbolnas maka ada kemungkinan terjadi overload pesanan yang membuat pesanan-pesanan dengan diskon besar menjadi terlambat. Beberapa langkah untuk mengatasi hal tersebut adalah dengan memastikan paket telah siap diambil saat kurir datang, memperpanjang SLA apabila diperlukan dan memberikan early warning atau pengertian ke pembeli agar ekspektasi pelanggan tetap terjaga. 
2. Berdasarkan distribusi scatter plot fitur cost terhadap weight_gram menunjukkan produk dengan kisaran berat 2000-4000 mengalami keterlambatan sebesar 100%. Hal ini dapat menjadi himbauan agar dapat memberkan opsi rekomendasi pengiriman yang lebih cepat agar keterlambatan dapat diminimalisir, seperti pemilihan jalur udara dengan estimasi kedatangan 2-3 hari.
3. Berdasarkan analisis data yang didapatkan fitur customer calls memiliki korelasi yang cukup kuat dengan tingkat keterlambatan, semakin banyak customer calls yang dilakukan maka semakin rendah tingkat keterlambatan pengiriman. Untuk mengetahui mengapa hal ini terjadi harus dilakukan investigasi isi dari percakapan customer call. Salah satu hal yang mungkin terjadi adalah dengan customer call maka perusahaan / tim gudang melakukan  follow up ke pihak ekspedisi sehingga dilakukan investigasi pengiriman yang dapat mempercepat pesanan tiba. Kedepannya perusahaan dapat mempergunakan hal ini dengan cara melakukan follow up ke pihak ekspedisi apabila ada pesanan terindikasi terlambat tanpa harus dilaporkan oleh customer. 
