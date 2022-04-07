# BetaThinkTank_JC_DS_FT_BSD_JKT_15_FinalProject

### Created By : Beta ThinkTank
Repository ini merupakan salah satu proses dari program Bootcamp Data Science Purwadhika Digital School ini, dan disusun oleh tim Beta ThinkTank yang ber anggotakan :
1. Cristopher Gani
2. Riyan Rafif
3. Rifqi Manufi

Dataset source : https://www.kaggle.com/olistbr/brazilian-ecommerce?select=olist_products_dataset.csv

## Who, What, How?
Olist adalah sebuah perusahaan asal Brazil yang bergerak di bidang E-commerce. Perusahaan saat ini berencana untuk meningkatkan performa penjualan dengan menentukan metode pemasaran yang diberikan kepada pelanggan dengan berbagai kebutuhan, karakteristik atau perilaku yang berbeda. Perusahaan memiliki dataset dari setiap transaksi di E-commerce ini. kita sebagai Data science di perusahaan Olist memiliki peran untuk memberikan insight serta rekomendasi dari dataset tersebut, sehingga perusahaan dapat terus berkembang.
Perusahaan ingin meningkatkan performa penjualan dengan metode pemasaran yang efektif dan efisien, sehingga diperlukan nya Customer Segmentation. Karena itu Langkah-langkah yang perlu kami lakukan  pertama adalah business understanding, data cleaning dan preparation, data overview, EDA dan insight, model dan evaluasi, business insight dan rekomendasi

## Business Understanding
Pada Langkah business understanding kami ingin memahami permasalahan business yang dimiliki oleh perusahaan dan menentukan tujuan dari hasil analysis ini.
  Untuk memahami permasalahan bisnis nya, kami melakukan cohort analysis yaitu metode yang digunakan untuk menganalisis serta mengevaluasi perubahan perilaku sekelompok orang tertentu, yang melibatkan fitur demografis umum dalam kurun waktu tertentu.
Dari hasil cohort analysisnya  bisa kita lihat kalau sekelompok pengguna baru hampir di setiap bulannya  tidak lebih dari 1% yang melakukan pembelian Kembali di bulan bulan berikutnya, kecuali di bulan desember 2016 itupun karena jumlah pelanggan barunya di bulan tersebut  hanya 1 orang dan orang tersebut melakukan pembelian kembali di bulan berikutnya.
Dari 91.445 pelanggan  94%nya tidak melakukan pembelian berulang.
![cohortAnalysis](https://user-images.githubusercontent.com/94157150/162120110-9fda69bb-3ceb-4363-bced-8bf983b2d734.png)

## Goal and Strategy
Setelah mengetahui permasalahan business nya, kita bisa menargetkan tujuan kita yaitu: 
1. Meningkatkan repurchasing dan juga untuk menimalisir potensial lost customer.
2. Melakukan customer segmentasi menggunakan RFM analysis dan membuat model clustering untuk memprediksi cluster yang di targetkan. 
3. Memberikan insight dan rekomendasi yang dapat membantu tim bisnis dan tim pemasaran untuk meningkatkan repurchasing. 

## Data Preprocess dan Cleaning
 Sekarang kita masuk kedalam process data cleaning dan data preprocessing, pada tahap ini kami akan membersihkan data, memilih kolom yang digunakan dan mempersiapkan data untuk keperluan clustering. 
 berikut process cleaning dan preprocessing nya:
 1. Handling Missing values -> Drop, karena missinga value antar kolomnya saling berkorelasi dan tipe data dari missing value nya adalah tipe data timestamp sehingga sulit untuk mengisi missing value.
 2. Check & remove Duplicate -> 15.256 -> Drop, karena dapat mengganggu nilai payment value customer tersebut.
 3. Handling outliers -> Tidak dilakukan treatment apapun, karena karena menurut kami pada dataset ini outlier nya dapat memberikan insight yang baik bukan mengganggu analysis.

## Data Overview
Data Ecommerce Olist yang kami analysis ini berasal dari Kaggle, data ini terdiri dari 8 data set yang berbeda. Setelah kita lakukan proses merge atau penggabungan antar dataset sesuai dengan petunjuk dari schema data set ini, terdapat 44 kolom dan 119.143 baris.
![alt text](https://i.imgur.com/HRhd2Y0.png)

## Data Selected
Setelah penggabungkan dataset, kami memilih 20 kolom yang berasal dari data customer, data payment, data seller dan data location. Meskipun untuk melakukan market segmentasi kita hanya membutuhkan data yang berkaitan dengan customer, disini kami memutuskan untuk memasukan data seller dan lokasi untuk bisa memberikan insight tambahan kepada kami.
<img width="661" alt="Screen Shot 2022-04-07 at 12 17 21" src="https://user-images.githubusercontent.com/94157150/162125544-1260511c-c4c2-499b-b0a9-9dc4452d82bb.png">


## Data Overview dan EDA
Setelah melewati proses cleaning data kami siap digunakan,di tahap data Overview, EDA dan Insight ini kami akan menjabarkan hasil dari analyisis yang sudah kami lakukan.

### Sales Overview

![Sales Overview](https://user-images.githubusercontent.com/94157150/162125819-1bd59c0e-db5a-4320-9874-87ffc3e67aa4.jpeg)

Di sales overview ini kita dapat melihat traffic pembelian berdasarkan hari dan jam nya, dari heatmap ini menunjukan bahwa traffic pembelian tertinggi di ecommerce olist berada di hari weekdays dari jam 10 pagi sampai jam 4 sore, walaupun di jam 5 sore hingga malam traffic pembelian nya masih lumayan tinggi. Dapat kita asumsikan bahwa penyebab traffic pembelian di hari week end lebih rendah dibanding weekdays karena pada sabtu dan minggu orang orang lebih memilih untuk beberlanja ketoko offline.
Berikutnya kita dapat meilihat jumlah transaksi, dan jumlah pembayaran tiap bulan nya dari data ini berbanding lurus, trend dari kedua data positif. Jumlah transaksi dan pembayaran terbesar sama-sama berada di bulan November 2017.
Untuk Metode pembayaran yang tersedia adalah boleto, cc, debit, dan voucher. 74% metode pembayaran yang digunakan adalah credit card.

Rata-rata dari review score yang diberikan customer kepada seller bisa dibilang cukup baik dengan rata-rata score 4.1 dari 5. Hal ini menunjukan pada dasarnya mayoritas dari customer cukup puas dengan barang yang mereka beli.

Jika kita lihat dari jumlah customer dan jumlah seller, dapat diasumsikan bahwa setiap seller mendapatkan 32 customer saja. Total transaksi pembayarannya sebesar 15,1jt real, dan total seluruh produk nya sebanyak 30,2ribu. Jika kita lihat lagi pada metode pembayaran mayoritas menggunakan kartu kredit, sebanyak 50.5% customer di olist melakukan pembayaran dengan cicilan.

### State
![Geolocation](https://user-images.githubusercontent.com/94157150/162126806-e48c3cd2-3f1c-4cdc-983b-1f8d300a8522.jpeg)

Ini adalah peta lokasi seller state dan customer state. Bisa kita lihat dari seller mau pun customer populasi paling banyak nya berada di sao Paulo. Dari hasil analysis kami menunjukan bahwa 64% transaksi melakukan pemesanan antar negara bagian yang berbeda. Mungkin hal itu terjadi karena barang yang mereka inginkan tidak tersedia di daerah mereka walaupun hal tersebut tidak dapat di validasi karena tidak ada data yang menjelaskan secara spesifik tentang produk  apa yang dibeli tetapi hanya berupa kategori.

### Pengiriman
![Delivery Overview](https://user-images.githubusercontent.com/94157150/162127719-f492bb36-739e-44f7-ada1-de3f4579e47e.jpeg)

Selanjutnya kami melakukan analysis terhadap data pengiriman, rute pengiriman paling banyak yaitu pengiriman dari saopaulo ke saopaulo, tetapi sesuai dari data state sebelumnya bahwa 7 dari 10 rute pengiriman terbanyak nya ke negara bagian yang berbeda. 
Jika dilihat dari waktu pengirimannya, 7 dari 10 waktu pengiriman tercepat adalah pengiriman ke negara bagian yang sama. Sedangkan 10 waktu pengiriman terlama nya adalah pengiriman ke negara bagian yang berbeda, bahkan ada waktu pengiriman yang mencapai 138 hari. Rata-rata durasi pengiriman nya adalah 9 hari sedangkan estmasi nya adalah 21 hari, mungkin lamanya waktu pengiriman dan estimasi juga mendukung hasil analysis kami sebelumnya bahwa 64% pengirimannya ke antar negara bagian karena jika barang tersedia di daerah mereka, mereka akan memilih pergi ke toko fisik dari pada harus menunggu lama, apa lagi estimasi yang diberikan rata-ratanya lebih lama 2 kali lipat dari rata-rata pengiriman actual nya.
Analysis kami menunjukan bahwa pengiriman yang tidak sesuai estimasi mencapai 98,7%, walaupun proporsi pengeriman yang lebih lama dari estimasi nya hanya sebesar 6,6% tetapi terdapat 74% estimasi yang lebih dari 7 hari dibanding dengan actual nya. Estimasi pengiriman yang terlalu lama bisa menyebabkan menurunya minat pembeli padahal waktu pengirimannya bisa jauh lebih cepat.

### Kategori 
![Best Category Product](https://user-images.githubusercontent.com/94157150/162127812-acbbcdfe-9f98-4b03-a965-ac018798654d.jpeg)

Ini adalah 35 kategori dengan penjualan tertetinggi, mayoritas dari categori ini adalah barang yang tidak di beli Kembali dalam waktu dekat, sedangkan di data ini hanya dalam kurun waktu 22 bulan. Hal tersebut mungkin menjadi penyebab 94% customer olist di data ini tidak melakukan pembelian berulang. Jika dihubungkan dengan anylsis sebelumnya bahwa 64% transaksi dilakukan antar negara bagian, menyebabkan waktu pengirimannya menjadi lama, untuk barang-barang yang pembeliannya bersifat repeatable seperti makanan, minuman, atau barang-barang yang dibutuhkan sesegara mungkin, membuat customer akan ragu untuk berbelanja di olist. Sehingga kemungkinan barang-barang yang dibeli di Olist adalah barang yang tidak tersedia daerah nya atau sulit dicari membuat mereka rela menunggu lama.


## Model
  Selanjutnya membuat modelin untuk customer segmentasi dan evaluasi dari model. Clustering dibuat untuk mengelompokan customer berdasarkan behavior nya sehingga kami dapat menentukan kelompok mana yang akan menjadi target utama kami untuk meningkatkan penjualan di ecommerce ini.
Pertama-tama kita harus menyiapkan datanya sebelum membuat model, mulai dari membuat fitur RFM, lalu digabungkan dengan fitur-fitur yang sudah kita pilih dari dataframe, masuk ketahap scaling menggunakan standard scaler dan mengurangi dimensi data menggunakan PCA dengan N component 2.

Kami membuat 4 model yang pertama yaitu menggunakan selected feature dengan model KMeans, yang kedua adalah RFM Segmentasi, yang ketiga fitur RFM dengan model KMeans,model yang terakhir adalah menggabungkan fitur yang dipilih dengan fitur RFM dengan model kmeans
Fitur yang dipilih berupa : 
*	order_item_id
*	 price
*	 freight_value
*	 Payment_value
*	 payment_sequential
*	 payment_installments

Kami memilih model keempat yaitu model yang menggunakan fitur pilihan dan fitur RFM, jumlah cluster yang dipilih adalah 4 karena hasil dari clusteringnya dapat menginterpretasi kan tujuan kami. Sillhouette score dari model ini adalah 0.74 

## Hasil Clustering
![WhatsApp Image 2022-04-07 at 12 21 31 PM](https://user-images.githubusercontent.com/94157150/162128041-d9252b16-af16-4c89-8ee8-dfaad4718f4b.jpeg)

Ini adalah hasil dari clusteringnya. Cluster yang pertama adalah Big spender yaitu kelompok customer yang membeli barang dengan quantitas sedikit, frequency sedikit, tetapi melakukan pembayaran yang cukup besar, rata-rata dari cluster ini juga melakukan cicilan saat membeli barang.
Yang kedua adalah Hibernating yaitu kelompok customer yang membeli barang dengan quantitas sedikit, frequency sedikit, jumlah pembayarannya juga sedikit.
Yang ketiga adalah Loyal Customer yaitu kolompok customer yang membeli barang dengan quantitas banyak, frequency nya juga banyak, dengan jumlah pembayaran sedang.
Yang terakhir adalah Need attention yaitu kelompok customer yang membeli barang dengan qunatitas, frequency dan jumlah pembayarannya sedang.

Dari hasil clustering, kami mengetahui bahwa cluster degan proporsi terbanyak yaitu 89% adalah Hibernating, sehingga cluster tersebut merupakan target segmen kami dan didukung dengan keterhubungan permasalahan hasil cohort analisis yang menunjukan 94% customer tidak melakukan pembelian berulang. Menurut F.F Reichheld (1996) “suatu perusahaan sangat penting untuk memuaskan dan mempertahankan pelanggan yang ada karena mencari pelanggan baru biaya nya dapat mencapai lima kali lipat lebih besar dari biaya untuk memuaskan dan mempertahankan pelanggan”.

## Business Insight, recommendation
Dari hasil Analysis dan hasil clustering, juga didasari dari pernyataan Frederick Reichheld, sebaiknya kita melakukan improvement terhadap permasalahan pengiriman dan ketersediaan barang di setiap negara bagian untuk menarik Kembali cluster hibernating, sebelum mencoba membuat campaign untuk menarik pengguna baru yang nantinya akan memiliki pengalaman yang sema dengan pengguna lama.

1. Rekomendasi Untuk tim bisnis

Untuk tim bisnis kami merekomendasikan untuk melakukan improvement di sector pengiriman dengan cara bermitra dengan jasa pengiriman yang berkualitas agar penetapan estimasi dan kecepatan pengirimannya menjadi lebih baik. Yang kedua adalah membuat warehousing di berbagai negara bagian karena selain pengiriman nya menjadi lebih cepat, warehousing juga bisa membuat ketersediaan barang lebih merata di tiap negara bagiannya.
Kami juga menyarankan untuk Meminta feedback user, seperti  survey singkat mengenai apa yang  perlu diubah untuk mendapatkan  pengalaman yang lebih baik saat  melakukan transaksi.

2. Rekomendasi Untuk tim marketing

Yang pertama kami menyarankan untuk tim marketing melakukan pembuatan campaign untuk meningkatkan jumlah seller dengan cara memberikan edukasi dan benefit Ketika mereka mempercayakan usaha mereka di Olist. Karena dengan meningkatkan jumlah seller diharapkan ketersediaan barang lebih merata sehingga pengiriman barang menjadi lebih cepat dan dapat menarik Kembali cluster hibernating. Yang kedua melakukan A/B testing untuk cluster hibernating dengan membandingkan behavior dari cluster tersebut dengan cara memberikan sales promotion seperti cicilan 0% karena 50% dari pelanggan melakukan transaksi dengan cicilan. Kita juga dapat memberikan promo gratis ongkir sehingga lama nya waktu pengiriman dapat dipertimbangkan.

## Conclusion
dari permasalahan bahwa 94% customer di olist tidak melakukan repurchase, kami sudah memberikan rekomendasi-rekomendasi yang ditujukan untuk cluster target kami yaitu cluster hibernating agar. Tujuan yang diharapkan tentu saja untuk meningkatkan  repurchasing dengan menarik Kembali minat membeli dari cluster hibernating tersebut. Untuk melihat impact dari rekomendasi dan analysis kami, kita bisa menggunakan metode A/B testing dan melakukan anylsis terhadap hasil feedback yang diberikan oleh customer.
