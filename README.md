# Laporan Proyek Machine Learning - R. Damanhuri

## Domain Proyek

GoalZone adalah jaringan klub fitnes di Kanada. GoalZone menawarkan berbagai kelas fitnes dalam dua kapasitas: 25 dan 15. Beberapa kelas selalu dipesan penuh. Kelas yang dipesan penuh seringkali memiliki tingkat kehadiran yang rendah. <br><br>
GoalZone ingin **memprediksi apakah anggota akan menghadiri kelas atau tidak.** Dengan demikian, mereka dapat **memaksimalkan penggunaan kapasitas kelas** dan **menghindari penerimaan kelas untuk anggota yang kemungkinan tidak hadir**.
## Business Understanding

### Problem statement
* Atribut apa yang paling berpengaruh terhadap kehadiran anggota di kelas fitnes?
* Apakah anggota akan menghadiri kelas fitnes atau tidak berdasarkan atribut yang diketahui?

### Goals
* Mengetahui atribut paling berkorelasi dengan kehadiran anggota pada kelas fitnes pesanan.
* Membuat model prediktif kehadiran anggota fitnes pada kelas pesanan berdasarkan atribut yang ada.

### Solution statement
* Mentransformasi atribut sesuai kebutuhan dan memilih atribut berdasarkan fungsi correlation
* Membandingkan 6 algoritma machine learning klasik dan memilih performa terbaik

## Data Understanding
Dataset bersumber dari Kaggle.com, yakni [Fitness Club Dataset for ML Classification](https://www.kaggle.com/datasets/ddosad/datacamps-data-science-associate-certification?resource=download)

Dataset terdiri dari 1500 baris data dan 8 kolom atribut. <br>
Deskripsi Atribut:<br>
*   booking_id: Nominal. Nomor identifikasi untuk pemesanan
*   months_as_member: Diskrit. Lama terdaftar sebagai anggota dalam bulan, minimal 1
*   weight: Kontinu. Berat anggota dalam kilogram, dibulatkan 2 desimal
*   days_before: Diskrit. Jumlah hari sebelum kelas yang didaftar anggota
*   day_of_week: Nominal. Hari pelaksanaan kelas
*   time: Ordinal. Waktu pelaksanaan kelas, AM atau PM
*   category: Nominal. Kategori kelas fitnes
*   attended: Nominal. Kehadiran anggota di kelas (1: hadir, 0: tidak)

Tahapan yang dilakukan: missing value handling, univariate analysis, dan multivariate analysis.

## Data Preparation
* Encoding: dilakukan one-hot encoding untuk atribut kategorikal karena model prediktif klasifikasi yang dibuat hanya menerima masukan numerik
* Data splitting: dilakukan train_test_split dengan perbandingan 80% data train dan 20% data test karena model perlu dilatih dan diuji dengan data yang berbeda
* Data normalization: dilakukan normalisasi dengan StandardScaler untuk atribut numerik yang bukan biner (0/1) agar jangkauan value tidak luas sehingga inferensi model lebih cepat

## Modeling
Model yang dikembangkan kali ini berupa 6 model machine learning klasik: SVM, Logistic Regression, Decision Tree, Random Forest, XGBoost, dan KNN. Nantinya akan dipilih 1 model dengan performa terbaik berdasarkan metrik evaluasi yang digunakan.

## Evaluation
Business goal dari proyek adalah:
* memaksimalkan penggunaan kapasitas kelas:  memaksimalkan prediksi benar keseluruhan (true positive dan true negative)
* menghindari penerimaan kelas untuk anggota yang kemungkinan tidak hadir: meminimalkan kesalahan prediksi benar (false positive)

Sehingga metrik evaluasi yang digunakan adalah:
* Accuracy: berapa persen prediksi yang benar bahwa anggota menghadiri dan tidak menghadiri kelas dari seluruh anggota.
* Precision: berapa persen anggota yang benar hadir dari keseluruhan anggota yang diprediksi hadir

Hasil eksperimen menunjukkan bahwa model dengan performa terbaik adalah SVM dengan Train Accuracy 0.785833 Test Accuracy 0.766667, Train Precision 0.735, dan Test Precision 0.823529. <br>
Atribut paling berkorelasi dengan kehadiran anggota pada kelas fitnes adalah months_as_member atau berapa bulan anggota bergabung, berupa korelasi positif (0.49)
