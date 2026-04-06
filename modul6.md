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


