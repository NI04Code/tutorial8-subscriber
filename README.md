### Reflection Tutorial 8
#### Nama: Naufal Ichsan
#### NPM: 2206082013
#### Kelas: A  

1. **what is amqp?**   
AMQP, atau Advanced Message Queuing Protocol, adalah protokol standar terbuka yang digunakan dalam middleware berbasis pesan. Protokol ini memfasilitasi komunikasi yang efisien antara berbagai aplikasi dengan memungkinkan pertukaran pesan. AMQP umumnya digunakan dalam pembangunan sistem pesan, memungkinkan interaksi yang lancar di antara aplikasi-aplikasi tersebut.

2. **what it means? guest:guest@localhost:5672 , what is the first quest, and what is the second guest, and what is localhost:5672 is for?**     
- String ```guest:guest@localhost:5672``` merupakan string koneksi untuk sebuah server AMQP
- ```guest:guest``` merupakan nama user dan password untuk autentikasi pada server. Dalam kasus ini, baik nama user maupun password keduanya adalah "guest". Dalam banyak konfigurasi default broker pesan seperti RabbitMQ, nama user dan default password keduanya adalah "guest". Namun, dalam lingkungan produksi, sangat disarankan untuk mengubah kredensial default ini karena alasan keamanan.
- ```@localhost:5672``` menentukan host dan port. "localhost" mengacu pada mesin lokal, yang berarti bahwa message brocker (RabbitMQ) berjalan di mesin yang sama di mana kode ini dieksekusi. Port 5672 adalah port default yang digunakan oleh RabbitMQ untuk komunikasi AMQP.

#### foto simulasi slow response rabbitmq
![alt text](assets/images/slow.png)     
Penjelasan: Dapat dilihat bahwa queue sampai 10 ketika saya mencoba menjalankan cargo run pada publisher sebanyak 2x sehingga harus mengirim dan menunggu ke 2x5 data subscriber

#### Reflection dan foto Running at least three subscriber
![alt text](assets/images/1.png) 
![alt text](assets/images/2.png) 
![alt text](assets/images/3.png) 
![alt text](assets/images/4.png) 
![alt text](assets/images/5.png)    
Screenshot ketika saya menjalankan cargo run sebanyak 3 kali pada publisher. Dapat terlihat bahwa spike dari message queue berkurang yang menandakan lebih cepat daripada sebelumnya karena request yang diterima queue akan ditugaskan kepada 3 subscriber instance yang jalan sehingga masing" subscriber menghandle 5 object subscriber

Beberapa code yang dapat di improve adalah,

Hindari menggunakan unwrap() sebab menggunakan unwrap() pada kode produksi tidak disarankan karena dapat menyebabkan program panic jika Result adalah Err. Sebagai gantinya, kita dapat menangani kesalahan secara elegan menggunakan match atau if let.
Gunakan konstanta untuk string yang diulang sebab jika kita memiliki string yang digunakan beberapa kali (seperti amqp://guest:guest@localhost:5672), lebih baik mendefinisikannya sebagai konstanta di bagian atas file.
