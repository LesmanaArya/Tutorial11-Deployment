# Tutorial 11

## 1. Compare the application logs before and after you exposed it as a Service.
Sebelum di expose sebagai service, log yang akan muncul adalah mengenai aplikasi tersebut yang di run di container sehingga pesan yang akan muncul adalah semacam: <br>
```
I0517 12:31:53.964787       1 log.go:195] Started HTTP server on port 8080
I0517 12:31:53.965366       1 log.go:195] Started UDP server on port  8081
```
![log](img/Screenshot%20(1701).png)
Ketika sudah di expose sebagai service, log yang muncul adalah terkait dengan komunikasi antar service dan client seperti request yang dihandle oleh service tersebut. Itulah sebabnya pada ss diatas muncul beberapa request GET/ karena setiap kali kita membuka browser atau tab baru ke url service tersebut, maka ia akan melakukan GET baru. Bertambahnya log ini saat kita mengakses service tersebut menandakan bahwa aplikasinya berjalan dengan normal

## 2. Notice that there are two versions of kubectl get invocation during this tutorial section. The first does not have any option, while the latter has -n option with value set to kube-system. What is the purpose of the -n option and why did the output not list the pods/services that you explicitly created? Hint: Do some reading about Namespace in Kubernetes documentation.
Berdasarkan dokumentasi, -n berguna untuk menentukan namespace secara spesifik ketika menjalankan kubernertes. Untuk namespace sendiri tujuannya adalah membagi atau mempartisi resources dan cluster. Perintah -n biasa digunakan apabila terdapat service dengan nama yang sama di berbagai namespace. Hal ini berguna apabila ada lebih dari satu user yang ingin berbagi cluster sehingga tidak mengganggu yang lain.  Dengan menggunakan -n, kube-system akan menampilkan resource dari namespace yang berisi komponen inti dari sistem Kubernetes, seperti DNS dan server API. Apabila kita tidak menggunakan opsi -n, akan ditampilkan resource yang dibuat pengguna secara eksplisit.


