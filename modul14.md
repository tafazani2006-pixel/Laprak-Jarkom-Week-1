## Talitha Fairuzzahwa Nirwasita - 103072400035 - IF0405
# MODUL 14 WIFI
## Dasar Teori

**IEE 802.11** adalah serangkaian standar protokol internasional yang dirancang oleh Institute of Electrical and Electronics Engineers (IEEE) untuk mengatur komunikasi data pada jaringan nirkabel (Wireless LAN atau Wi-Fi). Protokol ini mendefinisikan aturan pada lapisan fisik (Physical Layer) dan lapisan MAC (Media Access Control) untuk pertukaran data via udara.

**Perbandingan Frekuensi Jaringan Wi-Fi**
1. Frekuensi 2.4 GHz
   - Kelebihan : Memiliki jangkauan sinyal yang luas dan daya tembus dinding/objek padat yang baik
   - Kekurangan : Kecepatan transfer data lebih lambat dan rentan terkena gangguan/interferensi karena spektrumnya lebar dan padat (banyak perangkat rumah tangga menggunakannya).
2. Frekuensi 5 GHz
   - Kelebihan : Kecepatan transfer data jauh lebih unggul, interferensi rendah, dan gelombangnya lebih padat.
   - Kekurangan : Jangkauan sinyalnya relatif lebih kecil dan sulit menembus penghalang fisik seperti dinding beton.

**Access Point** bertindak sebagai jembatan jaringan (network bridge) yang menghubungkan klien nirkabel ke jaringan kabel lokal. Selain itu, AP berfungsi sebagai penyebar sinyal nirkabel agar wilayah atau pengguna yang tidak terjangkau kabel tetap dapat terhubung ke dalam jaringan.

Untuk menganalis lebih lanjut praktikum disiapkan dengan mengunduh dan ekstrak berkas ZIP pelacak aktivitas Wireshark dari tautan laboratorium resmi: http://gaia.cs.umass.edu/wireshark-labs/wireshark-traces.zip. Buka berkas pelacakan bernama Wireshark_802_11.pcap menggunakan aplikasi Wireshark.

## Analisis Beacon Frame
Fungsi Utama: Access Point melakukan proses broadcast (penyiaran) Beacon Frame secara terus-menerus dengan tujuan utama untuk mengumumkan keberadaannya (advertising) kepada semua perangkat/klien di sekitarnya, sehingga klien mengetahui parameter jaringan dan SSID yang tersedia untuk disambungkan

Untuk memfilter Beacon Frame, digunakan perintah ekspresi filter pada Wireshark: wlan.fc.subtype == 8 && wlan.fc.type == 0
<img width="975" height="358" alt="image" src="https://github.com/user-attachments/assets/136e1920-bb28-48dd-8e07-9ffc91af1de9" />
Berdasarkan hasil tangkapan layar Wireshark, Beacon Frame dikirimkan secara periodik setiap sekitar 8 milidetik. Tercatat bahwa aktivitas beaconing ini berlangsung selama 73 detik dengan total pengiriman sebanyak 2363 kali.
<img width="711" height="703" alt="image" src="https://github.com/user-attachments/assets/04919c50-a616-468f-a7fd-74aa1b9d635e" />

Berdasarkan ekspansi detail paket pada Frame 3, ditemukan parameter-parameter berikut:  
- PHY Type (802.11b (HR/DSSS)): Menunjukkan tipe lapisan fisik nirkabel yang digunakan adalah standar 802.11b berkecepatan tinggi dengan modulasi High-Rate Direct Sequence Spread Spectrum.
- Short Preamble (False): Menandakan penggunaan Preamble panjang (Long Preamble). Preamble adalah sinkronisasi bagian awal frame. Nilai False berarti sistem memprioritaskan kompatibilitas dengan perangkat lama dibanding optimasi kecepatan.
- Channel (6) / Frequency (2437MHz): Jaringan ini beroperasi pada Saluran 6 di spektrum frekuensi 2.4 GHz.
- Signal Strength / Noise Level: Kekuatan sinyal yang diterima adalah -30 dBm (sangat kuat/bagus) dengan tingkat gangguan (Noise) berada pada -100 dBm.

Analisis Tagged Parameters
- Tag: SSID parameter set: Menampilkan identitas nama jaringan Wi-Fi, yaitu "30 Munroe St".
- Tag: Supported Rates: Menyebutkan kecepatan transfer data yang didukung oleh AP ini, yakni 1, 2, 5.5, dan 11 Mbps.
- Tag: Extended Supported Rates: Menyebutkan kecepatan tambahan yang didukung oleh standar yang lebih baru, berkisar dari 6 Mbps hingga 54 Mbps.

## Analisis Data Transfer
Untuk menganalisis perpindahan data, diterapkan filter alamat IP server: Untuk menganalisis perpindahan data, diterapkan filter alamat IP server:
<img width="816" height="416" alt="image" src="https://github.com/user-attachments/assets/6d1fe970-aad5-4ddd-a180-3864859ee4d1" />

Hasil menunjukkan proses Three-Way Handshake TCP (SYN $\rightarrow$ SYN-ACK $\rightarrow$ ACK) diikuti oleh paket HTTP GET pada Frame 480 untuk mengunduh dokumen teks /wireshark-labs/alice.txt.  

Analisis Protokol: Paket data dibungkus menggunakan protokol kendali tautan logis (Logical-Link Control / LLC) sebelum diteruskan ke Internet Protocol Version 4 (IPv4) dengan alamat asal klien 192.168.1.109 dan alamat tujuan server 128.119.245.12

## Analisis Proses Association & Disassociation
- Association (Asosiasi): Merupakan proses jabat tangan (handshake) awal ketika klien meminta hak akses untuk bergabung/menyambung ke sebuah Access Point.
- Disassociation (Disasosiasi): Merupakan proses pemutusan hubungan koneksi, baik atas permintaan klien maupun akibat instruksi dari AP lama karena alasan tertentu (misal: perpindahan jaringan/roaming).

Diterapkan ekspresi filter untuk melihat manajemen jabat tangan nirkabel:wlan.fc.type_subtype == 0
- expand paket awal
  <img width="749" height="587" alt="image" src="https://github.com/user-attachments/assets/f8965de7-319b-40c3-b49f-704b740fee69" />
- expand paket akhir
  <img width="975" height="948" alt="image" src="https://github.com/user-attachments/assets/0b7f2078-63ee-4de1-adce-ac8e8c87cbb7" />
Jika kita membandingkan paket permintaan asosiasi teratas (Frame 1750) dengan paket asosiasi terbawah (Frame 2162), terjadi perubahan pada bagian parameter SSID:
- Pada Frame 1750, klien mencoba berasosiasi ke AP dengan SSID "linksys_SES_24086".
- Pada Frame 2162 (paling bawah), klien berpindah dan mengirim permintaan asosiasi baru ke AP dengan SSID "30 Munroe St".

Tanggapan Asosiasi (Association Response) dianalisis melalui filter subtype respon: wlan.fc.type_subtype == 1
<img width="687" height="376" alt="image" src="https://github.com/user-attachments/assets/8c5e9666-6383-4110-a216-7b922f8d5ed8" />

Ditemukan Frame 2166 yang merupakan Association Response. Di sini, Transmitter Address diisi oleh MAC Address milik perangkat pengirim respon, yaitu CiscoLinksys_f7:1d:51 , sebagai tanda bahwa Access Point menyetujui permintaan koneksi dari klien (Intel_d1:6b:4f).


