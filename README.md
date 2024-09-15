# Airline Customer Value Analysis Case

## Background
Project ini bertujuan melakukan klasterisasi berdasarkan data customer sebuah perusahaan penerbangan yang dapat digunakan sebagai strategi pengembangan bisnis.

### About Dataset
Dataset ini berisi data customer sebuah perusahaan penerbangan dan beberapa fitur yang dapat menggambarkan value dari customer tersebut.

<strong>Penjelasan  Fitur dari Dataset</strong>  
![Capture1.JPG](https://github.com/rialdiharry/Customer_Clustering_Machine_Learning/blob/main/img/Capture1.JPG?raw=true)


## Approach

 Pendekatan yang dilakukan untuk melakukan klasterisasi di antara lain:
 

 - Melakukan EDA (Exploratory Data Analysis) 
 - Mempersiapkan data (Data Prep) di antaranya:
	 - Handling missing values (imputasi data null)
	 - Handling outliers
	 - Feature Engineering
	 Mengadakan fitur baru berupa **'LOYALTY'** yang merupakan jangka waktu keanggotaan pelanggan dari pertama kali mendaftar hingga periode observasi (jarak dalam bulan antara 'FFP_DATE' dan 'LOAD_TIME) 
	 - Feature Selection
	 Fitur yang digunakan untuk klastering: 
		 - Fitur **'LOYALTY'** merepresentasikan Lenght:<br>
		 Jangka waktu keanggotaan pelanggan dari pertama kali mendaftar hingga periode observasi (semakin lama pelanggan menjadi anggota berarti pelanggan semakin "loyal")
		 - Fitur **'AVG_INTERVAL'** merepresentasikan interval:<br>
		 Jangka waktu antara penerbangan (semakin kecil berarti pelanggan baru saja melakukan penerbangan)
		 - Fitur **'FLIGHT_COUNT'** merepresentasikan Frequency:<br>
		 Jumlah penerbangan pelanggan dalam periode observasi (semakin besar semakin sering melakukan penerbangan)
		 - Fitur **'SEG_KM_SUM'** merepresentasikan jarak tempuh:<br>
		Jumlah jarak yang ditempuh selama periode observasi (semakin jauh jarak tempuhnya maka semakin besar biaya yang telah dibayar oleh customer)
	- Feature Transformation 
	Dilakukan ﬁtur transformasi dengan **standardisasi** untuk menyamakan skala semua ﬁtur, serta mengubah mean mendekati 0 dan std mendekati 1.
 -  ***Clustering*** 
	- Menentukan jumlah klaster dengan **Elbow Method**:
	- Melakukan klasterisasi dengan menggunakan algoritma **K-Means Clustering**
	- Melakukan **PCA (Principal Component Analysis)** pada hasil klasterisasi untuk mengurangi dimensi data, menghilangkan redundansi, memfasilitasi visualisasi, agar data lebih mudah diinterpretasikan dan dianalisis.
 - Evaluasi dengan Silhouette Method
 - *Insights and Recommendation*

## Clustering
**Penentuan Jumlah Klaster dengan Elbow Method**<br>
![Capture15.JPG](https://github.com/rialdiharry/Customer_Clustering_Machine_Learning/blob/main/img/Capture15.JPG?raw=true) <br> Ditemukan bahwa jumlah klaster yang optimal adalah 5 klaster <br>

**K-Means Clustering**<br>
![Capture16.JPG](https://github.com/rialdiharry/Customer_Clustering_Machine_Learning/blob/main/img/Capture16.JPG?raw=true)<br> Dilakukan K-Means clustering dengan jumlah *n_clusters* sebanyak 5 terhadap data set. Didapatkan rata-rata nilai setiap ﬁtur dalam masing-masing cluster untuk memahami karakteristik umum dari setiap cluster. <br>

**PCA**<br>
![Capture17.JPG](https://github.com/rialdiharry/Customer_Clustering_Machine_Learning/blob/main/img/Capture17.JPG?raw=true) <br> Dilakukan PCA pada hasil *clustering* dengan *n_component* = 3<br>

**Visualisasi 2 Dimensi**<br>
![Capture18.JPG](https://github.com/rialdiharry/Customer_Clustering_Machine_Learning/blob/main/img/Capture18.JPG?raw=true) 

**Visualisasi 3 Dimensi** <br>
![Capture19.JPG](https://github.com/rialdiharry/Customer_Clustering_Machine_Learning/blob/main/img/Capture19.JPG?raw=true) <br> <br> Berdasarkan hasil PCA :
1. Terdapat titik-titik dari kelas yang berbeda terpisah dengan jelas di plot, ini menunjukkan bahwa model dapat membedakan kelas-kelas tersebut dengan baik.
2. Titik yang berdekatan menunjukkan kemiripan antara observasi, sedangkan titik yang jauh menunjukkan perbedaan signiﬁkan antara observasi.

**Evaluasi dengan Silhouette Method** <br>
![Capture20.JPG](https://github.com/rialdiharry/Customer_Clustering_Machine_Learning/blob/main/img/Capture20.JPG?raw=true) <br> Secara keseluruhan, clustering dengan 5 cluster ini terlihat lebih baik dibandingkan 2/3/4 cluster, karena:
- Average silhouette scorenya paling tinggi >0.4,
- Silhouette score antar cluster tidak terlalu timpang (lebih dari rata2nya),
- Tidak ada nilai negatif.
<br>

## *Insights and Recommendation*

**Hasil Klasterisasi Pelanggan**<br>
![Capture21.JPG](https://github.com/rialdiharry/Customer_Clustering_Machine_Learning/blob/main/img/Capture21.JPG?raw=true)

Karakteristik Klaster Pelanggan:

 - Cluster 0 (*Inexperienced Flyers*)<br>
Merupakan anggota baru dari program maskapai dengan sedikit pengalaman penerbangan dan interval antar penerbangan singkat. Mungkin  terdiri dari mahasiswa atau individu baru dalam karir profesional.
 - Cluster 1 (*Rare Flyers*)<br>
Merupakan anggota lebih lama namun jarang terbang, dengan jumlah penerbangan dan jarak tempuh yang terbatas. Mungkin terdiri dari individu yang cenderung melakukan perjalanan pribadi atau liburan jangka panjang.
 - Cluster 2 (*Infrequent Flyers*)<br>
Anggota paling lama dengan penerbangan sporadis (sangat jarang) dan interval antar penerbangan moderat. Mungkin terdiri dari mereka yang melakukan perjalanan pada kesempatan khusus seperti liburan tahunan atau perjalanan bisnis yang jarang.
 - Cluster 3 (*Regular Flyers*)<br>
Anggota yang termasuk baru tetapi yang tergolong lebih sering terbang, dengan jumlah penerbangan dan jarak signiﬁkan. Mungkin terdiri dari individu yang melakukan perjalanan rutin untuk kepentingan bisnis atau pekerjaan.
 - Cluster 4 (*Frequent Flyers*)<br>
Anggota paling lama kedua setelah Cluster 2, dengan penerbangan sering dan interval antar penerbangan singkat. Mungkin  terdiri dari eksekutif bisnis atau pelancong yang sering melakukan perjalanan internasional atau liburan.
<br>

***Business Recommendations***<br> 
 - Cluster 0 (*Inexperienced Flyers*)<br>
Berikan penawaran khusus untuk memikat pelanggan baru, seperti diskon untuk penerbangan pertama mereka atau poin bonus saat mendaftar. Fokuskan pada layanan yang mudah dipahami dan jangan terlalu rumit karena mereka baru mengenal layanan penerbangan.
 - Cluster 1 (*Rare Flyers*)<br>
Tawarkan paket liburan jangka panjang atau promosi spesial untuk destinasi tertentu yang jarang dikunjungi. Berikan ﬂeksibilitas dalam reservasi dan penawaran istimewa untuk meningkatkan minat mereka dalam bepergian lebih sering.
 - Cluster 2 (*Infrequent Flyers*)<br>
Buat program loyalitas yang menarik dengan poin atau penghargaan yang dapat dikumpulkan dari setiap penerbangan. Tawarkan paket liburan atau kebijakan ﬂeksibel yang memungkinkan mereka merencanakan perjalanan jangka panjang atau liburan secara efektif.
 - Cluster 3 (*Regular Flyers*)<br>
Fokuskan pada layanan premium dan keuntungan bisnis yang cepat, seperti akses prioritas, lounge bandara eksklusif, atau pelayanan pelanggan yang unggul. Tawarkan program loyalitas yang memberikan nilai tambah dan kenyamanan bagi pelanggan yang sering melakukan perjalanan.
 - Cluster 4 (*Frequent Flyers*)<br>
Tingkatkan layanan eksklusif untuk pelanggan yang sering terbang, seperti upgrade otomatis, akses lounge VIP global, atau kesempatan eksklusif untuk pengalaman perjalanan yang lebih mewah. Tawarkan kebijakan ﬂeksibel yang mengakomodasi perjalanan sering mereka.
