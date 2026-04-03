## Talitha Fairuzzahwa Nirwasita - 103072400035 - IF0405
# MODUL 4 : DNS
## NsLookup
Nslookup adalah tools yang digunakan untuk mencari informasi DNS (Domain Name System). informasi yang didapat berupa alamat ip, server DNS, dan informasi mail server.

**Langkah-langkah Praktikum**
1. Buka command prompt (CMD)
2. Ketikan perintah

   a. *nslookup www.mit.edu*
      untuk menampilkan alamat IP dari domain serta server DNS default

     <img width="433" height="321" alt="Screenshot 2026-03-30 155145" src="https://github.com/user-attachments/assets/c84fef42-714b-42c8-aba1-ebdaf176bf8a" />

   b. *nslookup -type=NS mit.edu*
      untuk menampilkan nama-nama DNS server dari domain mit.edu. tanpa *-tpe=NS, maka       yang tampil hanyalah informasi default

      <img width="596" height="526" alt="Screenshot 2026-03-30 155316" src="https://github.com/user-attachments/assets/81ad06fd-4ea0-43ea-b77f-56a38bdcbcd2" />
    
   c. *nslookup www.aiit.or.kr bitsy.mit.edu*
      untuk mengirim query ke DNS server tertentu (bukan default)

      <img width="553" height="294" alt="Screenshot 2026-03-30 155756" src="https://github.com/user-attachments/assets/aa214bf8-26e8-42bc-bda3-d0b556539351" />

**Pertanyaan**
1. Mencari IP server web di Asia
- Perintah : *nslookup www.nus.edu.sg*
- Domain : www.nus.edu.sg
- Alamat IP : 45.60.35.225

  <img width="383" height="163" alt="image" src="https://github.com/user-attachments/assets/8065e7bb-5180-4043-84c0-03349ec1e82f" />

2. Mencari DNS otoritatif universitas di Eropa
- Perintah : *nslookup -type=NS ox.ac.uk*
- DNS server : dns0.ox.ac.uk, dns1.ox.ac.uk, dns2.ox.ac.uk, auth4.dns.ox.ac.uk,          auth5.dns.ox.ac.uk, auth6.dns.ox.ac.uk

  <img width="441" height="296" alt="image" src="https://github.com/user-attachments/assets/970edfc3-ef1d-4126-8d6b-6d00b9169bf5" />

3. Mencari mail server Yahoo melalui DNS tertentu
- Perintah : *nslookup -type=MX yahoo.com dns0.ox.ac.uk*
- Hasil : *** auth0.dns.ox.ac.uk can't find yahoo.com: Query refused

  <img width="549" height="103" alt="image" src="https://github.com/user-attachments/assets/f8d5a604-c9b1-46f7-99f0-834ef1f931c0" />
  
- Permintaan tidak berhasil karena server DNS dns0.ox.ac.uk merupakan authoritative      DNS yang hanya melayani domain ox.ac.uk, sehingga menolak permintaan untuk domain      lain seperti yahoo.com


## IPCondif
IPConfig adalah perintah pada Command Prompt yang digunakan untuk melihat dan mengelola konfigurasi jaringan berbasis TCP/IP. Dengan IPConfig kita dapat melihat alamat IP komputer, mengatahui DNS server yang digunakan, melihat dan menghapus cache DNS.

**Langkah-langkah Praktikum**
1. Buka command prompt (CMD)
2. Ketikan perintah *ipconfig /all*. Berfungsi untuk menampilkan informasi jaringan seperti IP address, subnet mask, defaul gateway, DNS server, MAC address

   <img width="724" height="749" alt="Screenshot 2026-03-30 160412" src="https://github.com/user-attachments/assets/4f91257b-39d0-4928-b416-271c2a8ef286" />
   
3. Ketikan perintah *ipconfig /displaydns*. Berfungsi untuk menampikan daftar domain yang pernah diakses

   <img width="730" height="604" alt="Screenshot 2026-03-30 160813" src="https://github.com/user-attachments/assets/df5d7fde-5141-45f0-83fb-0f64e40ee5c7" />

4. Ketikan perintah *ipconfig /flushdns*. Berfungsi untuk menghapus cache DNS sehingga sistem akan melakukan pencarian ulang DNS saat mengakses domain

   <img width="422" height="150" alt="Screenshot 2026-03-30 160822" src="https://github.com/user-attachments/assets/f0a8f025-d831-4f29-868f-75b052fa5ece" />

## Tracing DNS dengan Wireshark
## A.  Analisis DNS Request dan Response pada Akses Website (www.ietf.org)
**Langkah-langkah Praktikum**
1. Buka command prompt (CMD) dan ketikan perontah *ipconfig* untuk menyalin IP Address (10.218.0.23)
2. Buka wireshark dan pilih jaringan yang aktif (wifi)
3. Gunakan filter *ip.addr == 10.218.0.23*
4. Aktifkan tombol start
5. Buka browser *http://www.ietf.org/*
6. Tambahkan filter lagi *ip.addr == 10.218.0.23 && dns.qry.name.contains "ietf"*
   <img width="1365" height="747" alt="Screenshot 2026-03-30 161900" src="https://github.com/user-attachments/assets/b2235b53-7652-41c8-b21c-38f1f69a71fe" />

**Pertanyaan**
1. Apakah DNS menggunakan UDP atau TCP?

   <img width="635" height="60" alt="image" src="https://github.com/user-attachments/assets/40e3a45e-832a-42b3-8fdd-a42e6260e3fb" />

   Dns menggunakan UDP
2. Port tujuan pada DNS request & port sumber pada DNS response

   <img width="635" height="94" alt="image" src="https://github.com/user-attachments/assets/b7e1e406-c0be-4514-a7eb-ef6329e8eb21" />

   - DNS REQUEST -> Source Port (client): 58200 & Destination Port (server): 53
   - DNS RESPONSE -> Source Port (server): 53 & Destination Port (client): 58200

## B. Analisis DNS Menggunakan Perintah nslookup (www.mit.edu)
**Langkah-langkah Praktikum**
1. Buka wireshark dan pilih jaringan yang aktif (wifi) dan aktifkan
2. Buka CMD ketikan perintah *nslookup www.mit.edu*

   <img width="356" height="223" alt="image" src="https://github.com/user-attachments/assets/883ba279-2831-44ef-a6bd-b31f52a8234b" />
4. Matikan wireshark dan gunakan filter DNS
5. Ambil data dari Standard query (request) dan Standard query response dari www.mit.edu
   <img width="673" height="538" alt="image" src="https://github.com/user-attachments/assets/0359a379-0144-456f-aeea-b15624580ded" />

**Pertanyaan**
1. Port tujuan request dan port sumber dari response

   <img width="355" height="143" alt="Screenshot 2026-04-03 134544" src="https://github.com/user-attachments/assets/166eef44-4aee-4b01-aeec-db47aca3e8fd" /> <img width="359" height="134" alt="image" src="https://github.com/user-attachments/assets/b7b93359-3663-495d-a989-5a6759a636d0" />

   - DNS REQUEST -> Destination Port : 53
   - DNS RESPONSE -> Source Port : 53
2. Alamat IP request

   <img width="668" height="525" alt="image" src="https://github.com/user-attachments/assets/817d3d11-eb4c-4455-b3d6-e8dc346da010" />

   Request DNS dikirim ke alamat IP fe80::1. Alamat tersebut merupakan alamat lokal (IPv6) yang digunakan sebagai DNS server dalam jaringan
3. Type dan answers request

   <img width="437" height="335" alt="image" src="https://github.com/user-attachments/assets/28e211f7-2217-4e1e-81c2-f5491300c968" />

   Tipe DNS request adalah A (Address Record). Pesan ini tidak mengandung jawaban karena hanya berupa permintaan
4. Answers response

   <img width="601" height="425" alt="image" src="https://github.com/user-attachments/assets/537f40d0-6872-437e-a9da-0a051151d13c" />

   Terdapat 3 jawaban. Jawaban pertama menunjukkan bahwa domain www.mit.edu merupakan alias (CNAME) dari www.mit.edu.edgekey.net. Jawaban kedua menunjukkan alias lanjutan ke e9566.dscb.akamaiedge.net. Jawaban ketiga berisi alamat IP (A record) yaitu 23.217.163.122 sebagai alamat tujuan akhir

## C. Analisis DNS Record NS Menggunakan nslookup (mit.edu)
**Langkah-langkah Praktikum**
1. Buka wireshark dan pilih jaringan yang aktif (wifi) dan aktifkan
2. Buka CMD ketikan perintah *nslookup -type=NS mit.edu*

   <img width="545" height="483" alt="image" src="https://github.com/user-attachments/assets/4f85f7ae-71e0-43a6-a7e7-e53d107ba895" />
4. Matikan wireshark dan gunakan filter DNS
5. Ambil data dari Standard query (request) dan Standard query response dari NS mit.edu
   <img width="526" height="379" alt="image" src="https://github.com/user-attachments/assets/cf9af133-a016-4a95-a7ae-a2518eb4c492" />

**Pertanyaan**
1. Alamat IP request

   <img width="489" height="59" alt="image" src="https://github.com/user-attachments/assets/c2f7fec8-4aeb-49d1-b766-9e9bda21818e" />

    Request DNS dikirim ke alamat IP fe80::1 yang merupakan DNS default pada jaringan.
2. Type dan answers request

   <img width="646" height="343" alt="image" src="https://github.com/user-attachments/assets/ff39815f-0495-4bd1-a461-d18fe5d1ed7f" />

   Tipe DNS request adalah NS. Pesan ini tidak mengandung jawaban karena hanya berupa permintaan
3. Answers response

   <img width="1599" height="899" alt="image" src="https://github.com/user-attachments/assets/5577c86f-a94e-4d01-9ab6-e8e75e8f4a1b" />

   Pada DNS response, diperoleh beberapa nama server MIT. Pesan balasan ini umumnya hanya menampilkan nama server (NS record), dan tidak alamat IP secara langsung pada bagian answers. Alamat IP muncul di bagian tambahan (Additional record)

## D. Analisis DNS Menggunakan Server Tertentu (www.aiit.or.kr bitsy.mit.edu)
**Langkah-langkah Praktikum**
1. Buka wireshark dan pilih jaringan yang aktif (wifi) dan aktifkan
2. Buka CMD ketikan *nslookup www.aiit.or.kr bitsy.mit.edu*

   <img width="503" height="288" alt="image" src="https://github.com/user-attachments/assets/b9aec835-2d07-450d-a5b2-9122acdf0f9d" />
4. Matikan wireshark dan gunakan filter DNS
5. Ambil data dari Standard query (request) dari www.aiit.or.kr
   <img width="639" height="280" alt="image" src="https://github.com/user-attachments/assets/a12c2c07-002e-4d7a-862a-f9c5cdf977d6" />

**Pertanyaan**
1. Alamat IP request

   <img width="656" height="137" alt="image" src="https://github.com/user-attachments/assets/7bd8a793-bbda-462a-b7ef-403aa16e0a94" />

   Pesan permintaan DNS dikirim ke alamat IP 18.0.72.3. Alamat tersebut merupakan server bitsy.mit.edu yang ditentukan secara manual pada perintah nslookup, sehingga bukan merupakan DNS server lokal
2. Type dan answers request

   <img width="622" height="329" alt="image" src="https://github.com/user-attachments/assets/91fc9bd6-04a2-459e-8bf9-ac72e865f8f3" />

   Tipe DNS request adalah A (Address Record). Pesan ini tidak mengandung jawaban karena hanya berupa permintaan
3. Answers response
   Berdasarkan hasil pada Command Prompt, terlihat bahwa terjadi “DNS request timed out”, yang menunjukkan bahwa server DNS tidak merespon permintaan yang dikirimkan

   <img width="510" height="99" alt="image" src="https://github.com/user-attachments/assets/597af3bd-0d3c-4d04-bdf5-125320b02c5f" />

   Sehingga tidak terdapat pesan balasan (DNS response) pada percobaan ini. Hal ini dikarenakan permintaan DNS mengalami timeout, sehingga server bitsy.mit.edu tidak memberikan respon terhadap query yang dikirimkan. Akibatnya, tidak terdapat answers yang dapat dianalisis
