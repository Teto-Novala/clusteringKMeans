# 📄 Clustering Data Mall Customer 📄

Kami Dari Kelompok 4 akan meng-clustering data mall customer untuk membuat strategi yang cocok pada setiap cluster agar pendapatan dapat naik.

Dataset kami cari melalu website Kaggle, berikut linknya
https://www.kaggle.com/code/rajeshjnv/mall-customer-visually-analysis-k-means

# Struktur Dataset

| CustomerID | Gender | Age | Annual Income (k$) | Spending Score (1-100) |
| ---------- | ------ | --- | ------------------ | ---------------------- |
| .......... | ...... | ... | .................. | ...................... |
## Metode
Metode yang kami gunakan adalah metode K-Means

## Penjelasan Perintah yang di jalankan
- import 
Perintah import dipakai untuk mengimpor modul-modul yang diperlukan untuk analisis data, pemodelan klaster, dan visualisasi.

- drive.mount('/content/drive')
Perintah ini digunakan untuk memasang (mount) Google Drive ke dalam lingkungan Google Colab. Lokasi pemasangan adalah direktori /content/drive, yang memungkinkan Anda mengakses file dan folder di Google Drive dari Google Colab.

- dataset_path = '/content/drive/My Drive/data mining/Mall_Customers.csv'
Perintah ini mendefinisikan jalur (path) ke file dataset yang disimpan di Google Drive. Dalam hal ini, file dataset yang dimaksud adalah Mall_Customers.csv yang berada di dalam folder data mining di Google Drive.

- data = pd.read_csv(dataset_path)
Perintah ini menggunakan fungsi read_csv dari pustaka pandas untuk membaca file CSV yang ditunjuk oleh dataset_path dan menyimpannya ke dalam variabel data sebagai DataFrame pandas.

- data.head(100)
Perintah ini menampilkan 100 baris pertama dari DataFrame data. Fungsi head() digunakan untuk melihat sebagian kecil dari dataset, yang berguna untuk mendapatkan gambaran awal tentang struktur dan konten data.

- x = data.iloc[:, 2:5]
Perintah ini menggunakan fungsi iloc dari pandas untuk memilih subset dari kolom dalam DataFrame data. data.iloc[:, 2:5] berarti memilih semua baris (ditunjukkan dengan :) dan kolom dari indeks 2 hingga 4 (karena 5 tidak termasuk dalam range 2:5). Kolom yang dipilih kemudian disimpan dalam variabel x.

- x.head()
Perintah ini menampilkan 5 baris pertama dari DataFrame x. Fungsi head() berguna untuk melihat sebagian kecil dari data yang baru dipilih, membantu untuk memverifikasi bahwa kolom yang diinginkan telah dipilih dengan benar.

- x.shape
Perintah x.shape digunakan untuk mendapatkan dimensi dari DataFrame x. Ini akan mengembalikan tuple yang berisi dua elemen: jumlah baris dan jumlah kolom dalam DataFrame tersebut.

- x.isnull().sum()
Perintah ini digunakan untuk memeriksa keberadaan nilai-nilai yang hilang (missing values) dalam DataFrame x.

- x.describe()
Perintah x.describe() digunakan untuk menghasilkan statistik deskriptif dari DataFrame x. 

- wcss = []
Inisialisasi daftar kosong untuk menyimpan nilai WCSS (Within-Cluster Sum of Squares) untuk setiap jumlah cluster.

- for i in range (1,15):
Memulai loop yang berjalan dari 1 hingga 14 (nilai batas atas range adalah eksklusif).

- kmeans = KMeans(n_clusters= i, random_state= 14)
Untuk setiap iterasi, inisialisasi objek KMeans dari scikit-learn dengan jumlah cluster i dan random_state untuk memastikan hasil yang dapat direproduksi.

- kmeans.fit(x)
Melatih model KMeans pada dataset x

- wcss.append(kmeans.inertia_)
Menambahkan nilai inertia (yang merupakan WCSS) dari model KMeans ke dalam daftar wcss. Inertia mengukur jumlah total kesalahan kuadrat dalam cluster, yang digunakan untuk menentukan seberapa baik data di-cluster.

- plt.plot(range(1, 15), wcss)
Membuat plot garis dari nilai WCSS terhadap jumlah cluster (dari 1 hingga 14).

- plt.title("The Elbow Method")
Menambahkan judul ke plot.

- plt.xlabel("Number of Clusters")
Menambahkan label sumbu x, yaitu "Number of Clusters".

- plt.ylabel("WCSS")
Menambahkan label sumbu y, yaitu "WCSS".

- plt.show()
Menampilkan plot.

- kmeans = KMeans(n_clusters = 6, random_state = 14)
Membuat objek KMeans dengan 6 cluster dan random_state 14 untuk hasil yang konsisten.

- kmeans.fit(x)
Melatih model KMeans pada dataset x, menentukan pusat (centroid) untuk setiap cluster.

- kmeans.labels_
Atribut ini memberikan array yang berisi label atau penugasan cluster untuk setiap data point dalam dataset setelah model KMeans dilatih. Setiap elemen dalam array adalah nomor cluster (dari 0 hingga n_clusters-1) yang ditetapkan ke data point yang bersangkutan.

- hasil_kmeans = x.copy()
Membuat salinan DataFrame x ke hasil_kmeans. Ini dilakukan untuk tetap mempertahankan data asli di x dan memodifikasi hasil_kmeans dengan menambahkan informasi cluster

- hasil_kmeans["clusters"] = kmeans.labels_
Menambahkan kolom baru dengan nama "clusters" ke DataFrame hasil_kmeans. Nilai dalam kolom ini adalah label cluster yang ditetapkan oleh model KMeans untuk setiap data point dalam x.

- hasil_kmeans.head()
Menampilkan lima baris pertama dari DataFrame hasil_kmeans beserta kolom "clusters" yang baru ditambahkan.

- cluster_x = hasil_kmeans["clusters"].value_counts().index
Menghitung jumlah data point yang termasuk dalam setiap cluster dan mengambil indeks dari hasil perhitungan ini. Ini akan memberikan label cluster dalam urutan frekuensi menurun.

- cluster_y = hasil_kmeans["clusters"].value_counts().values
Mengambil nilai frekuensi dari setiap cluster, yang mencerminkan jumlah data point yang termasuk dalam masing-masing cluster.

- sns.barplot(x=cluster_x,y=cluster_y)
Membuat plot bar menggunakan seaborn (sns). Pada sumbu x (x=cluster_x), ditempatkan label cluster, dan pada sumbu y (y=cluster_y), ditempatkan nilai frekuensi.

- plt.title("Frekuensi Data pada Masing-Masing Clusters (KMeans)")
Memberi judul pada plot untuk menjelaskan konten visualisasi.

- plt.xlabel("Clusters") dan plt.ylabel("Frekuensi")
Memberi label sumbu x dan sumbu y untuk memberikan konteks lebih lanjut tentang apa yang ditunjukkan oleh masing-masing sumbu dalam plot.

- age_kmeans0, ann_kmeans0, spend_kmeans0
Memilih data untuk Cluster 0 dari hasil_kmeans untuk kolom Age, Annual Income, dan Spending Score secara berturut-turut.
Proses ini diulang untuk Cluster 1 (age_kmeans1, ann_kmeans1, spend_kmeans1), Cluster 2 (age_kmeans2, ann_kmeans2, spend_kmeans2), dan seterusnya hingga Cluster 5.

- centroid_cluster
ariabel ini menyimpan koordinat dari pusat cluster (centroid) yang dihasilkan oleh model KMeans setelah dilatih. Koordinat ini mewakili titik tengah atau "pusat" dari masing-masing cluster dalam ruang fitur (di sini, dalam konteks Age, Annual Income, dan Spending Score).

- Fungsi plot_3d_scatter
digunakan untuk membuat visualisasi scatter plot dalam tiga dimensi (3D) dari data yang dikelompokkan menggunakan model KMeans. 

- hasil_kmeans["CustomerID"] = data["CustomerID"]
digunakan untuk menambahkan kolom "CustomerID" dari DataFrame data ke DataFrame hasil_kmeans

- hasil_kmeans.head()
Menampilkan lima baris pertama dari DataFrame hasil_kmeans beserta kolom "CustomerID" yang baru ditambahkan.

# Kelompok 4
- Alma Ashofi
- Cindy Bela Amelia
- I Putu Reza Pratama
- Teto Novala