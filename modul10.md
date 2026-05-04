## Talitha Fairuzzahwa Nirwasita - 103072400035 - IF0405
# MODUL 10 : IP
## IP
IP Address (Internet Protocol Address) adalah alamat unik yang digunakan untuk mengidentifikasi perangkat dalam jaringan, baik di internet maupun jaringan lokal. IP address berfungsi seperti “alamat rumah” supaya data bisa dikirim ke tujuan yang benar.

**Jenis-jenis**
- IPv4 : menggunakan 32-bit (contoh: 192.168.1.1)
- IPv6 : menggunakan 128-bit (contoh: 2001:db8::1)

**Cara menghitung**

IPv4 terdiri dari 4 oktet (masing-masing 8 bit) ex : 192.168.1.1
- 192 = 11000000
- 168 = 10101000
- 1 = 00000001

Subnetting digunakan untuk membagi jaringan menjadi Network ID (identitas jaringan) dan Host ID (identitas perangkat).

**Mengamati IP Address**
1. Buka CMD
2. Ketik ipconfig
<img width="975" height="860" alt="image" src="https://github.com/user-attachments/assets/345ee8f5-f33f-4109-a3a6-9835b1a21b1f" />
Perangkat menggunakan IP 10.218.10.188 (kelas A private). Subnet mask 255.255.240.0 (/20) membagi network dan host. Network ID adalah 10.218.0.0. Jumlah host dalam jaringan mencapai 4094 perangkat. Default gateway 10.218.0.253 sebagai penghubung ke internet. Terdapat juga IPv6 jenis link-local.

## Traceroute
Traceroute adalah teknik untuk mengetahui jalur yang dilewati paket data dari komputer kita menuju suatu tujuan (misalnya website).

**Fungsi Traceroute**
- Menampilkan router (hop) yang dilewati
- Mengetahui waktu tempuh tiap hop
- Mendeteksi gangguan jaringan

**Mengamati Traceroute dari suatu Website**
1. Buka CMD
2. Ketik tracert google.com
<img width="747" height="578" alt="image" src="https://github.com/user-attachments/assets/0208ca2a-3981-42c9-a949-ae1f14da3a61" />
Paket melewati 23 router sebelum sampai ke server Google. Hop 1 adalah router lokal / gateway Wi-Fi yang digunakan. Hop 2-3 adalah jaringan internal ISP. Hop 4-7 sudah masuk ke jaringan publik. Hop 8-13 sudah masuk ke jaringan Google. RTO pada hop 12-22 terjadi karena router tidak merespon traceroute. Pada hop ke 23 paket berhasil sampai ke server Google (142.251.12.113 = google.com). Waktuk yang ditempuh realtif secepat dalam 1 ms - 30 ms, maka jaringan dalam kondisi yang baik.

## IMCP, MTU, TTL
**IMCP** adalah protokol yang digunakan untuk mengirim pesan kontrol dalam jaringan. ICMP digunakan untuk:
- Mengecek koneksi (ping)
- Mengirim pesan error
- Digunakan pada traceroute

**MTU** adalah ukuran maksimum paket data yang bisa dikirim dalam satu kali transmisi. Contoh: Ethernet -> 1500 byte. Jika paket lebih besar dari MTU akan terjadi fragmentasi.

**TTL** adalah batas jumlah hop (router) yang bisa dilewati paket. Setiap melewati router maka TTL berkurang 1. Jika TTL = 0 maka paket dibuang. TTL digunakan untuk mencegah 
looping jaringan.

## Fragmentasi
Fragmentasi adalah proses pemecahan paket data menjadi beberapa bagian yang lebih kecil karena ukuran paket melebihi MTU (Maximum Transmission Unit) jaringan. Fragmentasi terjadi ketika paket terlalu besar dan melewati jaringan dengan MTU lebih kecil.

**Percobaan Fragmentasi**
1. Jalankan Wireshark pilih interface Wifi yang aktif
2. Klik Start
3. Buka CMD
4. Ketik ping google.com -l 2000 (mengirim paket besar (2000 byte) yg melebihi MTU sehingga memicu fragmentasi)
5. Kembali ke Wireshark, gunakan filter ip.flags.mf == 1 || ip.frag_offset > 0
<img width="1163" height="366" alt="Screenshot 2026-05-04 184858" src="https://github.com/user-attachments/assets/61f5405c-8a3f-4afb-9a49-cd34e6623187" />

Berdasarkan hasil capture menggunakan Wireshark, ditemukan paket dengan keterangan:

- Fragmented IP protocol (proto=ICMP) yang menunjukkan terjadinya fragmentasi
- Paket memiliki ukuran sebesar 1514 bytes, melebihi batas MTU (±1500 byte)
- Terdapat nilai Identification yang menandakan setiap fragment berasal dari satu paket yang sama
- Nilai Fragment Offset (off=0) menunjukkan urutan fragment pertama
- Ditemukan keterangan Reassembled in #203 yang menunjukkan bahwa fragment berhasil digabung kembali

Sehingga dapat disimpulkan bahwa paket ICMP yang dikirim mengalami fragmentasi karena ukurannya melebihi MTU jaringan.

## IPv6
IPv6 (Internet Protocol version 6) adalah versi terbaru dari IP yang digunakan untuk menggantikan IPv4. Ciri-ciri IPv6 adalah menggunakan 128-bit address dan ditulis dalam bentuk heksadesimal.

**Analisis IPv6 di Wireshark**
1. Membuka file ipv6_sample dengan wireshark <img width="566" height="91" alt="image" src="https://github.com/user-attachments/assets/7c2a8e45-73e6-4df5-ac31-b19eae26e70f" />
2. Gunakan filter IPv6 <img width="1195" height="412" alt="image" src="https://github.com/user-attachments/assets/932a861e-d838-4697-8301-9a3568f40b17" />

Berdasarkan hasil capture menggunakan Wireshark, ditemukan paket dengan protokol IPv6. Hal ini dibuktikan dengan adanya informasi:

- Internet Protocol Version 6 pada detail paket
- Alamat source: 2001:db8:1::10 dan Alamat destination: 2a00:1450:4009:80b::200e
- Alamat tersebut memiliki format heksadesimal dengan tanda titik dua (:) yang merupakan ciri khas IPv6.
- Next Header menunjukkan penggunaan TCP
- Paket dikirim ke port 443 (HTTPS) yang menandakan komunikasi web
- Ditemukan juga TCP Retransmission yang menunjukkan adanya pengiriman ulang paket

Sehingga dapat disimpulkan bahwa komunikasi jaringan menggunakan IPv6 berhasil diamati dan digunakan untuk akses layanan web.
