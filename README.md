# Airplane Passenger Satisfaction Prediction

# Domain Proyek

<p>
  <img src="https://github.com/IbraHarsye/airplane-passenger-satisfaction-prediction/assets/56579824/9105c443-daa8-4d75-9590-bf4085cf7cb2" width="600">
	<figcaption>Gambar 1. Ilustrasi <i>Pesawat Terbang</i></figcaption>
</p>

Pesawat udara merupakan salah satu moda transportasi pilihan utama bagi masyarakat untuk berpergian, karena kemudahan dan keamanan yang ditawarkan. Semenjak pandemi coronavirus di tahun 2020, industri pesawat terbang di berbagai dunia harus menghadapi beberapa tantangan diantaranya adalah kepuasan pelanggan pada kualitas pelayanan yang ditawarkan oleh maskapai penerbangan demi keamanan dan kenyamanan saat berpergian.

Dengan perkembangan gaya hidup masyarakat tentunya maskapai penerbangan juga berkembang, dan masyarakat menginginkan standar kualitas pelayanan yang lebih tinggi dari maskapai penerbangan. Meningkatkan kualitas pelayanan adalah bagian yang sangat penting dari daya saing dan sangat penting untuk menciptakan perkembangan yang baik bagi maskapai penerbangan. Dengan memprediksi kepuasan pelanggan pada kualitas pelayanan tentu akan membantu maskapai penerbangan dalam meningkatkan pelayanan mereka dan menjadi alat untuk mengetahui layanan apa yang harus ditingkatkan.

* Fokus proyek ini adalah mengembangkan model machine learning yang dapat mengklasifikasikan kepuasan pelanggan ke dalam 2 kategori berdasarkan kepuasannya terhadap pelayanan dari maskapai penerbangan. 
* Tujuan dari proyek ini adalah untuk memberikan masukan dan pandangan kepada perusahaan maskapai penerbangan tentang kepuasan pelanggan pada kualitas pelayanan mereka.
* Terdapat beberapa penelitian yang dilakukan dalam pembuatan model machine learning untuk memprediksi kepuasan penumpang pesawat udara. Beberapa diantaranya adalah:
	* Menggunakan algoritma *Random Forest* dan mendapatkan akurasi hingga 96% [1].
	* Menggunakan Algoritma deep learning CNN-LSTM dan mendapatkan akurasi hingga 94% [2].

# Business Understanding

## Problem Statement
* Peningkatan gaya hidup masyarakat berpengaruh pada permintaan masyarakat akan kualitas pelayanan maskapai penerbangan
* Maskapai penerbangan bersaing untuk menyediakan kualitas pelayanan terbaik

## Goals
* Membantu maskapai penerbangan dalam menentukan pelayanan yang harus ditingkatkan untuk kepuasan pelanggan.
* Membuat model machine learning untuk memprediksi kepuasan pelanggan dengan rating dan data informasi penerbangan.

## Solution Statement
* Proyek machine learning ini akan menggunakan 2 algoritma *machine learning*, yaitu *Support Vector Machine* (SVM) dan *Decision Tree Classifier*. SVM adalah salah satu algoritma supervised learning yang digukana untuk mengklasifikasikan data dengan menggunakan pendekatan geometris dengan menggukan hyperplane. Decision Tree juga merupakan algoritma supervised learning yang berbasis pada pohon keputusan, di mana setiap simpul dalam pohon mewakili keputusan atau aturan untuk memisahkan dan mengklasifikasikan data.
* Akan dilakukan hyperparameter tuning pada kedua model baseline untuk memperoleh hasil klasifikasi terbaik dengan menggunakan metrik evaluasi precision, recall, accuracy, dan f1-score.
* Akan digunakan dataset yang terdiri dari informasi penumpang dan penerbangan serta nilai yang diberikan terhadap maskapai penerbangan.

# Data Understanding
Dataset yang digunakan pada proyek machine learning ini adalah data kepuasan penumpang pesawat terbang yang terdapat di Kaggle. Data dapat diakses melalui [tautan berikut](https://www.kaggle.com/datasets/teejmahal20/airline-passenger-satisfaction).

Dataset ini terbagi menjadi 2 bagian, yaitu data training dengan total 103904 baris dan data test dengan total 25976 baris.

## Variabel-variabel pada dataset
Berikut penjelasan kolom pada dataset, yaitu:
1. Gender: Jenis kelamin penumpang (Female, Male)
2. Customer Type: Tipe pelanggan (Loyal customer, disloyal customer)
3. Age: Umur penumpang
4. Type of Travel: Tujuan penerbangan pelanggan (Personal Travel, Business Travel)
5. Class: Kelas penerbangan penumpang (Business, Eco, Eco Plus)
6. Flight distance: Jarak penerbangan
7. Inflight wifi service: Tingkat kepuasan terhadap WiFi  (0:Not Applicable;1-5)
8. Departure/Arrival time convenient: Tingkat kepuasan terhadap waktu keberangkatan/tiba
9. Ease of Online booking: Tingkat kepuasan terhadap online booking
10. Gate location: Tingkat kepuasan terhadap lokasi gate penerbangan
11. Food and drink: Tingkat kepuasan terhadap makanan dan minuman
12. Online boarding: Tingkat kepuasan terhadap online boarding
13. Seat comfort: Tingkat kepuasan terhadap kenyamanan kursi
14. Inflight entertainment: Tingkat kepuasan terhadap hiburan dalam pesawat
15. On-board service: Tingkat kepuasan terhadap layanan On-Board
16. Leg room service: Tingkat kepuasan terhadap layanan leg room
17. Baggage handling: Tingkat kepuasan terhadap penanganan bagasi
18. Check-in service: Tingkat kepuasan terhadap layanan Check-in
19. Inflight service: Tingkat kepuasan terhadap layanan penerbangan
20. Cleanliness: Tingkat kepuasan terhadap kebersihan
21. Departure Delay in Minutes: Keterlambatan keberangkatan (menit)
22. Arrival Delay in Minutes: Keterlambatan tiba (menit)
23. Satisfaction: Kepuasan terhadap kualitas pelayanan(Satisfaction, neutral or dissatisfaction)

## Kondisi Data
Pada Data *training* dan data *testing*, terdapat beberapa kolom NaN atau missing value pada kolom *Arrival Delay in Minute*. Kolom kosong ini akan diisi dengan rata-rata dari kolom tersebut sehingga dataset menjadi lengkap.

Outliers pada data ini akan ditangani menggunakan Robust Scaler pada library Scikit-Learn.

## Exploratory Data Analysis
Langkah pertama dari EDA adalah melakukan univariate analysis yaitu dengan menampilkan histogram dari kolom numerik
<p>
  <img src="https://github.com/IbraHarsye/airplane-passenger-satisfaction-prediction/assets/56579824/42ffe26a-c2ab-4b12-b582-656caf6c45bd" alt="histogram " width="1000">
  <figcaption>Gambar 2. Histogram kolom data numerik</figcaption>
</p>

* Pada histogram di atas terlihat kolom Age, Flight Distance , Departure delay in minutes, dan Arrival delay in minutes persebaran data yang cukup luas.

Selanjutnya menampilkan boxplot dari kolom numerik untuk melihat outliers yang terdapat pada data.
<p>
  <img src="https://github.com/IbraHarsye/airplane-passenger-satisfaction-prediction/assets/56579824/a69aee6a-da35-4948-90b9-dfb379d5d179" alt="boxplot" width="1000">
  <figcaption>Gambar 3. Boxplot dari kolom data numerik</figcaption>
</p>
Terdapat banyak outliers pada kolom numerik, untuk menangani ini akan dilakukan standarisasi menggunakan Robust Scaler.


Selanjutnya dilihat korelasi antar fitur pada kolom numerik.

<p>
  <img src="https://github.com/IbraHarsye/airplane-passenger-satisfaction-prediction/assets/56579824/35cba508-1bee-4ec7-a56e-b06d190fde36" alt="correlation heatmap" width="1000">
  <figcaption>Gambar 4. Korelasi antar fitur data numerik</figcaption>
</p>

Kebanyakan fitur pada dataset memiliki korelasi yang tidak terlalu kuat. Hanya beberapa saja fitur yang memiliki korelasi yang cukup tinggi karena memang kedua fitur tersebut saling terkait. Seperti waktu keterlambatan pada fitur *Departure delay in minutes* dan *Arrival delay in minutes*, kemudian kebersihan dengan kenyamanan tempat duduk, makanan dan minuman, dan hiburan dalam penerbangan.

berikut tabel nilai korelasi yang telah diurutkan dari yang terbesar hingga yang terkecil.

Tabel 1. Korelasi variabel fitur dengan variabel target

| fitur         	            | korelasi dengan satisfaction    |
|-----------------------------------|---------------------------------|
| satisfaction   	            | 1.000000                        |
| Online boarding                   | 0.501749                        |
| Inflight entertainment            | 0.398234                        |
| Seat comfort     	            | 0.348829                        |
| On-board service    	            | 0.322205                        |
| Leg room service                  | 0.312424                        |
| Cleanliness                       | 0.307035                        |
| Flight Distance  	            | 0.298085                        |
| Inflight wifi service             | 0.283460                        |
| Baggage handling                  | 0.248680                        |
| Inflight service                  | 0.244918                        |
| Checkin service                   | 0.237252                        |
| Food and drink     	            | 0.211340                        |
| Ease of Online booking            | 0.168877                        |
| Age          	                    | 0.134091                        |
| Arrival Delay in Minutes          | 0.058187                        |
| Departure/Arrival time convenient | 0.054270                        |
| Departure Delay in Minutes   	    | 0.050740                        |
| Gate location       	            | 0.002793                        |

Dapat dilihat bahwa Online boarding adalah fitur yang memiliki korelasi tertinggi dengan satisfaction.

# Data Preparation
Proses data preparation pada proyek ini adalah melakukan encode pada kolom kategorikal, Melakukan standarisasi dengan menggunakan robust scaler dan minmax scaler, dan melakukan data splitting ke dalam 2 bagian yaitu training set dan test set.

## Standarisasi
Standarisasi digunakan karena kolom-kolom pada data ini tidak terdistribusi normal dan terdapat outlier, maka dari itu digunakan Robust Scaler dari library scikit learn untuk menghapus outlier pada data agar tidak mempengaruhi kualitas data yang digunakan. Kemudian dilakukan standarisasi menggunakan min max scaler yang berguna agar data menjadi lebih mudah dibandingkan karena value data diperkecil antara 0 sampai 1.

## Feature and Target Splitting
Pada tahap ini dataframe akan dipisahkan antara variabel fitur dan variabel target. Komposisi pada training set dan test set adalah 90% dan 10% dari total keseluruhan dataset. Hanya dipakai 10% test set dikarenakan data yang tersedia cukup banyak jadi, lebih baik lebih banyak data yang masuk ke dalam training set. Tujuan dari pemisahan antara fitur dan target ini agar dapat dilakukan fitting data dan testing pada model machine learning.

# Modelling
Algoritma machine learning yang akan digunakan pada project ini adalah *Support Vector Machine* (SVM) dan *Decision Tree*.

## SVM

<p>
  <img src="https://github.com/IbraHarsye/airplane-passenger-satisfaction-prediction/assets/56579824/3921a46d-27f5-4964-a8df-61edd993b7ce" alt="SVM" width="600">
  <figcaption>Gambar 5. Ilustrasi SVM</figcaption>
</p>

Kelebihan dari algoritma SVM adalah dapat berkerja sangat baik bila terdapat batas pemisah yang jelas diantara kelas-kelas, SVM juga lebih efektif digunakan pada data yang mempunyai dimensi tinggi dan hanya membutuhkan sedikit memory.
Kelemahan dari algoritma SVM antara lain tidak disarakan digunakan pada dataset yang sangat banyak. SVM juga memiliki performa yang buruk jika dataset memiliki banyak noise. SVM tidak memiliki nilai penjelasan probabilitas dari klasifikasi yang dilakukan. 

Dilakukan *hyperparameter tuning* pada algoritma SVM menggunakan *Grid Search* untuk mencari *hyperparameter* terbaik yang dapat digunakan. *Hyperparameter* yang digunakan adalah:
* kernel': 'linear', 'poly', 'rbf'
* C': 8, 9

## Decision Tree

<p>
  <img src="https://github.com/IbraHarsye/airplane-passenger-satisfaction-prediction/assets/56579824/bc4f7a98-493e-4fdb-b1ad-d08e9f05c3a4" alt="decision tree" width="600">
	<figcaption>Gambar 6. Ilustrasi <i>Decision Tree</i></figcaption>
</p>

Kelebihan dari algoritma *Decision Tree* adalah kemudahan dalam melakukan data preparation pada proses pre-processing. Kemudian algoritma ini juga tidak memerlukan normalisasi dan scaling dataset. Selain itu algoritma ini juga tidak terpengaruh dengan adanya missing values pada dataset dan mudah dijelaskan secara teknikal kepada stakeholder.
Namun algoritma Decision *Decision Tree* ini memiliki kelemahan yaitu, jika terdapat perubahan pada data akan mempengaruhi keseluruhan model yang menyebabkan ketidakstabilan. Terkadang algoritma ini juga mempunyai waktu training yang lebih lama dari model lainnya dan algoritma ini tidak bisa digunakan untuk regresi dan memprediksi nilai kontinu.

Dilakukan *hyperparameter tuning* pada algoritma *Decision Tree* menggunakan *Grid Search CV* untuk mencari *hyperparameter* terbaik yang dapat digunakan. *Hyperparameter* yang digunakan adalah:
* criterion': 'gini', 'entropy', 'log_loss'
* max_depth': 16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35


# Evaluation
Untuk mengevaluasi kinerja model dari masing-masing algoritma machine learning, digunakan beberapa metrik evaluasi yang umum digunakan dalam klasifikasi. Metrik evaluasi yang digunakan adalah:

## 1. Accuracy
Metrik evaluasi ini Merupakan rasio prediksi Benar (positif dan negatif) dengan keseluruhan data. Akurasi memberikan gambaran umum tentang seberapa baik model dapat mengklasifikasikan kepuasan penumpang secara benar. Akurasi dapat dihitung dengan membagi jumlah prediksi yang benar dibagi dengan jumlah total data. 

$$akurasi = {TP + TN \\over TP + TN + FP + FN}.$$

Dimana:
* True Negative (TN): Model memprediksi data ada di kelas Negatif dan yang sebenarnya data memang ada di kelas Negatif.
* True Postive (TP): Model memprediksi data ada di kelas Positif dan yang sebenarnya data memang ada di kelas Positif.
* False Negative (FN): Model memprediksi data ada di kelas Negatif, namun yang sebenarnya data ada di kelas Positif.
* False Positive (FP): Model memprediksi data ada di kelas Positif, namun yang sebenarnya data ada di kelas Negatif.

## 2. Precision
Precision Merupakan rasio prediksi benar positif dibandingkan dengan keseluruhan hasil yang diprediksi positif. Dalam konteks proyek ini, presisi mengukur seberapa baik model dalam mengklasifikasikan kepuasan pelanggan sebagai puas dan tidak puas/netral dengan benar.

$$presisi = {TP \\over TP + FP}.$$

## 3. Recall
Merupakan rasio prediksi benar positif dibandingkan dengan keseluruhan data yang benar positif. Dalam konteks proyek ini, recall mengukur seberapa baik model dalam mengidentifikasi kepuasan pelanggan dengan kepuasan yang sesuai dengan kelasnya.

$$recall = {TP \\over TP + FN}.$$

## 4. F1-Score
F1 Score merupakan perbandingan rata-rata presisi dan recall yang dibobotkan.

$$f1 score = 2 * {precision * recall \\over precision + recall}.$$

## Evaluasi SVM
Nilai Metrik Evaluasi Algoritma SVM:
* **Akurasi: 96%**
* **Presisi: 96%**
* **Recall: 96%**
* **F1-score: 96%**

## Evaluasi Decision Tree
Nilai Metrik Evaluasi Algoritma *Decision Tree*:
* **Akurasi: 96%**
* **Presisi: 96%**
* **Recall: 95%**
* **F1-score: 96%**


Dari hasil evaluasi diatas dapat dilihat model SVM memiliki Recall yang lebih tinggi sebanyak 1% 

Model SVM menghasilkan akurasi, presisi, F1-score yang sama dengan model Decision Tree. Tetapi model SVM memiliki keunggulan pada recall yang lebih besar dari model Decision Tree yaitu 96%. Hal ini menunjukkan bahwa model SVM memiliki performa sedikit lebih baik dari model Decision tree dan dapat melakukan klasifikasi lebih baik pada dataset Airline Customer Satisfaction kedalam 2 kelas yang tersedia.

# Kesimpulan
Dari hasil project machine learning yang telah dilakukan, dapat disimpulkan bahwa model SVM dengan parameter terbaik yang ditentukan melalui Grid Search CV merupakan model yang memiliki performa optimal dalam melakukan klasifikasi kepuasan pelanggan ke dalam 2 kategori yaitu satisfied dan neutral/disatisfied. Maka dengan ini perusahaan maskapai penerbangan dapat melakukan pertimbangan untuk melakukan perbaikan pelayanan mereka sesuai dengan prediksi yang dihasilkan.

# Referensi

[1]	[Jiang, X., Zhang, Y., Li, Y. et al. Forecast and analysis of aircraft passenger satisfaction based on RF-RFE-LR model. Sci Rep 12, 11174 (2022). https://doi.org/10.1038/s41598-022-14566-3](https://www.nature.com/articles/s41598-022-14566-3)

[2] 	[Park S-H, Kim M-Y, Kim Y-J, Park Y-H. A Deep Learning Approach to Analyze Airline Customer Propensities: The Case of South Korea. Applied Sciences. 2022; 12(4):1916. https://doi.org/10.3390/app12041916](https://www.mdpi.com/2076-3417/12/4/1916)
