## Talitha Fairuzzahwa Nirwasita - 103072400035 - IF0405
# MODUL 6 : TCP
## TCP
TCP (Transmission Control Protocol) adalah protokol pada layer transport yang bersifat connection-oriented, artinya sebelum mengirim data harus dilakukan proses pembentukan koneksi terlebih dahulu. TCP menjamin keandalan pengiriman data dengan menggunakan mekanisme sequence number, acknowledgment, flow control, dan congestion control.

## Analisis Transfer File Menggunakan Protokol TCP
**Langkah-langkah**
1. Download file http://gaia.cs.umass.edu/wireshark-labs/alice.txt
2. Buka browser http://gaia.cs.umass.edu/wireshark-labs/TCP-wireshark-file1.html dan pilih file alice.txt
   <img width="646" height="300" alt="image" src="https://github.com/user-attachments/assets/395a53f2-8967-44e7-a15b-b65cbf02aa04" />
3. Buka wireshark, pilih wifi, aktifkan (start)
4. Kembali ke browser klik Upload alice.txt hingga muncul tampilan “Congratulations”
   <img width="677" height="202" alt="image" src="https://github.com/user-attachments/assets/6e3d09bc-9bbe-471d-a728-2393502092a3" />
5. Stop wireshark dan lakukan filter *"tcp"*

   Terlihat bahwa paket yang muncul terdiri dari segmen TCP serta beberapa paket HTTP. Hal ini menunjukkan bahwa proses upload file dilakukan menggunakan protokol HTTP yang berjalan di atas
   <img width="953" height="47" alt="image" src="https://github.com/user-attachments/assets/bb52970f-53c7-4a1a-a634-7215f72e2515" />
   Paket SYN digunakan untuk memulai koneksi TCP antara client dan server (proses three-way handshake), bukan untuk mengirim file. Proses ini memastikan bahwa koneksi siap digunakan sebelum data ditransfer. Setelah koneksi berhasil dibuat, data file akan dikirim dalam beberapa segmen kecil melalui TCP. Hal ini terjadi karena TCP membagi data menjadi bagian-bagian kecil agar pengiriman lebih efisien dan dapat dikontrol.
   <img width="784" height="239" alt="image" src="https://github.com/user-attachments/assets/fa246bbe-f80e-4c15-af60-6078ad538ae0" />
   Selanjutnya, setelah proses upload selesai, server mengirimkan respon HTTP/1.1 200 OK. Pesan ini menandakan bahwa file telah berhasil diterima dan diproses oleh server. Setelah itu, halaman web menampilkan pesan “Congratulations” sebagai indikasi bahwa proses upload berhasil.
   
**Pertanyaan**
1. IP dan port TCP komputer klien 
   mencari data di filter "HTTP" dan pilih paket POST
   - IP server : 192.168.1.6
     <img width="768" height="54" alt="image" src="https://github.com/user-attachments/assets/409e45f0-f4e6-4683-a35f-20d8cbb15c32" />
   - Port server : 55216
     <img width="232" height="33" alt="image" src="https://github.com/user-attachments/assets/615f71cb-c43b-4698-9930-85e643c0e92e" />
2. IP dan port TCP server
   mencari data di filter "HTTP" dan pilih paket HTTP/1.1 200 OK
   - IP server : 128.119.245.12
     <img width="594" height="58" alt="Screenshot 2026-04-06 172800" src="https://github.com/user-attachments/assets/c47c2eda-8cf0-4997-8249-6b432ed99abf" />
   - Port server : 80
     <img width="217" height="32" alt="image" src="https://github.com/user-attachments/assets/85db9c11-78f4-4bfc-9b3f-6e86838106db" />

## Dasar TCP
**Langkah-langkah**
1. Download dan extrak file http://gaia.cs.umass.edu/wireshark-labs/wireshark-traces.zip
2. Buka file dan pilih paket paket tcp-ethereal-trace-1, buka dengan wireshark
   <img width="626" height="102" alt="image" src="https://github.com/user-attachments/assets/838098c2-c4c9-4da5-873f-64a34350f9ae" />

**Pertanyaan**
1. Nomor urut SYN, mencari data di filter tcp.flags.syn == 1 && tcp.flags.ack == 0

   <img width="626" height="120" alt="image" src="https://github.com/user-attachments/assets/1af861c6-9e05-4211-a909-81c2a1e3fe66" />

   Nomor urut pada segmen TCP SYN adalah 0. Segmen ini teridentifikasi sebagai SYN karena memiliki flag SYN pada bagian TCP Flags.

   <img width="417" height="72" alt="image" src="https://github.com/user-attachments/assets/3070d184-fb3e-47a7-ba0a-217e23b8425b" />
   <img width="281" height="145" alt="image" src="https://github.com/user-attachments/assets/c066c114-af87-4706-8266-d9a832c981d4" />
2. SYN-ACK, mencari data di filter tcp.flags.syn == 1 && tcp.flags.ack == 1

   <img width="466" height="111" alt="image" src="https://github.com/user-attachments/assets/87731924-bd56-42b4-8176-3fd94259cea4" />

   Nomor urut (sequence number) pada segmen SYN-ACK adalah 0, sedangkan nilai acknowledgment adalah 1. Nilai acknowledgment diperoleh dari sequence number pada segmen SYN sebelumnya yang ditambah 1. Segmen ini dapat diidentifikasi sebagai SYN-ACK karena memiliki flag SYN dan ACK pada bagian TCP Flags

   <img width="437" height="262" alt="image" src="https://github.com/user-attachments/assets/70e38951-dee3-4877-857a-292205f14f58" />
3. Sequence number POST, mencari data di filter tcp.port == 1161 && tcp contains "POST"

   <img width="412" height="98" alt="image" src="https://github.com/user-attachments/assets/f9aaec1f-2dc1-4ed3-b7a9-c69a18137181" />

   Nomor urut segmen TCP yang berisi perintah HTTP POST adalah 1

   <img width="742" height="144" alt="image" src="https://github.com/user-attachments/assets/296a8234-bdda-41a9-8772-88c9cc261e12" />
4. 6 segmen pertama + RTT

   <img width="729" height="613" alt="image" src="https://github.com/user-attachments/assets/dd119ca3-81dc-4680-ae30-1c7d1fd1c091" />

   Nilai RTT diperoleh dari selisih waktu antara pengiriman segmen TCP dan penerimaan acknowledgment. Berdasarkan grafik Round Trip Time, nilai RTT berkisar antara sekitar 100 ms hingga 300 ms. Nilai RTT ini bervariasi karena dipengaruhi oleh kondisi jaringan selama proses transfer
   
5. Panjang 6 segmen
   
   <img width="966" height="344" alt="image" src="https://github.com/user-attachments/assets/6358d958-2ea5-4d39-b8f7-95fdd51284a8" />

   Panjang 6 segmen adalah 7.865 byte

6. Buffer receiver

   <img width="551" height="67" alt="image" src="https://github.com/user-attachments/assets/26f55ccb-174a-45f7-aa2c-eda08042211a" />

   Nilai minimum ruang buffer yang tersedia pada penerima adalah 5840 byte, yang terlihat dari nilai window size pada segmen TCP

7. Retransmission

   <img width="815" height="332" alt="image" src="https://github.com/user-attachments/assets/2e8c7a63-d245-4cef-b3c6-24ca6e90f777" />
   
   Tidak ditemukan retransmission / ditemukan retransmission. Hal ini dapat dilihat dari tidak adanya / adanya label “TCP Retransmission” pada Wireshark.

8. ACK behavior

   <img width="639" height="426" alt="image" src="https://github.com/user-attachments/assets/64aff0eb-426c-4665-a5f1-73c29eb78ad3" />

   Jumlah data yang di-ACK tidak tetap dan bisa banyak. Penerima dapat mengakui beberapa segmen sekaligus, tidak selalu satu per satu

9. Thoroughtput

    <img width="566" height="607" alt="image" src="https://github.com/user-attachments/assets/ff18da6e-68ce-499b-8975-fbe42b20bce0" />

   Throughput adalah jumlah data yang ditransfer per satuan waktu. Berdasarkan grafik throughput, kecepatan transfer meningkat secara bertahap hingga mencapai sekitar 200 kbps hingga 270 kbps. Nilai ini menunjukkan performa koneksi TCP selama proses pengiriman data

## Congestion Control pada TCP 
**Peertanyaan dan Langkah-langkah**
1. Identifikasi Slow Start & Congestion Avoidance (file tcp-ethereal-trace-1)
- Buka file tcp-ethereal-trace-1 dengan wireshark
- Filter "TCP"
- Klik Statistics -> TCP Stream Graph -> Time-Sequence Graph (Stevens)

<img width="790" height="613" alt="Screenshot 2026-04-06 195336" src="https://github.com/user-attachments/assets/73b3db39-9b63-40ff-acb6-ae104ec3b689" />

Fase slow start terjadi pada awal koneksi (0 – ±1 detik) dengan pertumbuhan eksponensial. Fase ini berakhir ketika mencapai threshold, ditandai perubahan grafik menjadi linear. Selanjutnya TCP masuk ke fase congestion avoidance dengan pertumbuhan linear. Data nyata menunjukkan sedikit deviasi dari teori karena kondisi jaringan seperti delay dan variasi ACK. Koneksi TCP pada grafik dapat dikatakan relatif stabil karena tidak menunjukkan penurunan drastis pada sequence number yang mengindikasikan packet loss besar atau timeout. Namun, grafik tidak sepenuhnya halus seperti pada model TCP ideal.

2. Identifikasi Slow Start & Congestion Avoidance (alice.txt)
- Start wireshark
- Uploud file alice.txt ke http://gaia.cs.umass.edu/wireshark-labs/TCP-wireshark-file1.html
- Kembali ke wireshark dan filter "TCP"
- Klik Statistics -> TCP Stream Graph -> Time-Sequence Graph (Stevens)

<img width="538" height="611" alt="image" src="https://github.com/user-attachments/assets/b2297158-03d7-4b08-9db7-febb121a8db1" />

Pada grafik kedua, fase slow start terjadi pada awal koneksi dengan pertumbuhan eksponensial yang sangat cepat. Transisi ke congestion avoidance terjadi lebih cepat dibandingkan grafik sebelumnya. Hal ini menunjukkan bahwa koneksi Wi-Fi memiliki respon yang lebih cepat, namun juga lebih rentan terhadap variasi delay. Secara umum, koneksi tetap stabil, meskipun tidak sepenuhnya mengikuti perilaku ideal TCP akibat kondisi jaringan nirkabel.


   


