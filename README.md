# Module 10 - Reflection
> Tegar Wahyu Khisbulloh (2206082032) - Pemrograman Lanjut A
## Reflection on Hello Minikube
**1. Compare the application logs before and after you exposed it as a Service. Try to open the app several times while the proxy into the Service is running. What do you see in the logs? Does the number of logs increase each time you open the app?**

![Gambar 1](images/Gambar%201.png)
>Sebelum aplikasi diekspos sebagai sebuah `Service` di Kubernetes, aplikasi hanya berjalan di dalam satu atau lebih `Pod` di dalam `cluster` Kubernetes. `Pod` ini hanya dapat diakses dari dalam `cluster` itu sendiri, dan tidak memiliki alamat IP atau port yang dapat diakses dari luar `cluster`. Log awal yang terlihat hanya mencatat informasi bahwa aplikasi telah dimulai dan siap menerima request pada port tertentu, seperti yang terlihat pada gambar 1. Namun, karena tidak ada request yang dapat masuk dari luar `cluster`, maka log aplikasi tidak akan bertambah.

![Gambar 2](images/Gambar%202.png)
>Setelah aplikasi diekspos sebagai sebuah `Service` di Kubernetes, `Service` ini akan bertindak sebagai *gateway* atau *access point* bagi aplikasi yang berjalan di dalam `Pod`. `Service` menyediakan sebuah IP dan port yang dapat diakses dari dalam maupun luar `cluster`. Ketika aplikasi diakses melalui `Service`, request HTTP akan diteruskan ke `Pod` yang menjalankan aplikasi tersebut. Setiap request yang masuk akan dicatat dalam log aplikasi, seperti terlihat pada gambar 2 dengan contoh log "GET /". Jumlah log akan terus bertambah setiap kali ada request baru yang masuk ke aplikasi melalui `Service` tersebut.

**2. Notice that there are two versions of kubectl get invocation during this tutorial section. 13 The first does not have any option, while the latter has -n option with value set to kube-system. What is the purpose of the -n option and why did the output not list the pods/services that you explicitly created?**

>Opsi `-n` dalam `kubectl get` digunakan untuk menyebutkan namespace tempat kita ingin melihat daftar resource. Ketika dijalankan tanpa opsi, `kubectl get` akan menampilkan resource di namespace default. Namun, dengan menambahkan `-n kube-system`, outputnya akan menampilkan pod dan service sistem yang berjalan di namespace `kube-system` (namespace khusus untuk komponen inti Kubernetes) bukan resource yang kita buat di namespace lain. Opsi ini memungkinkan kita mengelola resource di berbagai namespace dalam satu cluster, karena Kubernetes menggunakan namespace untuk memisahkan resource berdasarkan tim, proyek, atau environment.

