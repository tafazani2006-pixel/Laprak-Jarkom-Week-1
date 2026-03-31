## Talitha Fairuzzahwa Nirwasita - 103072400035 - IF0405
# MODUL 4 : DNS
## NSLOOKUP
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
## A. Analisis Paket DNS Menggunakan Wireshark**
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
   DNS RESPONSE -> Source Port (client): 58200 & Destination Port (server): 53
   DNS REQUEST -> Source Port (server): 53 & Destination Port (client): 58200
