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

## What is the difference between Rolling Update and Recreate deployment strategy? Hint: Read the Deployments documentation.

Pada Rolling Update, update akan dilakukan secara bertahap. Pod-pod sebelumnya atau yang lama akan tetap tersedia sambil kubernertes membuat pod yang baru secara bertahap . Dengan Rolling Update, aplikasi akan tetap tersedia selama proses update. Recreate Deployment berarti kita membuat ulang versi aplikasinya. Seluruh pod yang pernah dibuat akan dihentikan sehingga aplikasi tidak akan berjalan selama proses update.

## Try deploying the Spring Petclinic REST using Recreate deployment strategy and document
Berikut merupakan tahapan yang saya lakukan ketika menggunakan Recreate Deployment
![2](img/Screenshot%20(1709).png)
Tahapan ini adalah me delete minikube kemudian membuat ulang dengan minikube create
![3](img/Screenshot%20(1708).png)
Tahapan ini adalah mengecek deployment setelah dibuat ulang

### 3. Prepare different manifest files for executing Recreate deployment strategy.

#### 4.What do you think are the benefits of using Kubernetes manifest files? Recall your experience in deploying the app manually and compare it to your experience when deploying the same app by applying the manifest files (i.e., invoking kubectl apply -f command) to the cluster.
Dengan manifest file, kita dapat mencatat hal terkait infratsruktur aplikasi seperti deployment, service, kode, dan sebagainya. Hal ini berguna apabila kita ingin memonitoring proses deployment atau membuat ulang enviroment. Manifest file juga berguna pada proses otomasi karena kita dapat menggunakan kubectl apply -f untuk secara otomatik menggunaka manifest file untuk deployment sehingga apabila ada perubahan dan kita butuhd deploy ulang, kita bisa lebihmudah mengerjakan deploynya
