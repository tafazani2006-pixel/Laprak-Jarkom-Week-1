## Talitha Fairuzzahwa Nirwasita - 103072400035 - IF0405

# MODUL 1 : RUNNING MODUL
## Instalasi Modul
Langkah pertama dalam praktikum ini adalah mengunduh installer Wireshark melalui situs resmi https://www.wireshark.org.
<img width="1067" height="699" alt="Screenshot 2026-03-02 192417" src="https://github.com/user-attachments/assets/2c5fe4cf-cc0f-4e57-a23c-0472efa91a55" />
Setelah proses unduhan selesai, dilakukan instalasi perangkat lunak Wireshark versi 4.6.4 x64 hingga proses setup dinyatakan berhasil.

<img width="490" height="385" alt="jarkom 1" src="https://github.com/user-attachments/assets/e46425e6-8542-4d7b-bb93-516786eeeca8" />

## Tampilan Awal
Setelah aplikasi dijalankan, Wireshark menampilkan daftar interface jaringan yang tersedia pada komputer.
<img width="1128" height="317" alt="Screenshot 2026-03-02 160241" src="https://github.com/user-attachments/assets/9d45ef7c-e24d-4f3d-9de3-043f07c8e324" />
Pada bagian Capture, terdapat grafik berupa "garis-garis" di sebelah kanan nama interface (seperti Wi-Fi). Garis ini merupakan penanda **kerja atau indikator adanya lalu lintas data** yang sedang berlangsung pada jalur tersebut. Apabila koneksi Wi-Fi dimatikan, grafik tersebut akan berubah menjadi garis lurus, yang menunjukkan bahwa tidak ada aktivitas data yang terdeteksi atau **interface dalam kondisi Non-Aktif**.
<img width="969" height="419" alt="Screenshot 2026-03-02 160330" src="https://github.com/user-attachments/assets/116bcd2e-3e44-4608-9300-728c47f2443f" />

# MODUL 2 : PENGENALAN TOOLS
## Fungsi Tools
<img width="1365" height="604" alt="Screenshot 2026-03-02 160412" src="https://github.com/user-attachments/assets/ed58f212-6e77-40b1-938e-854dc88ec22a" />

**1. Toolbar Control** bagian ini berisi ikon-ikon utama untuk mengendalikan proses pengambilan data.
- Sirip Hiu (Biru): Berfungsi untuk memulai (Start) proses penangkapan paket data pada interface yang dipilih.
- Kotak Merah: Berfungsi untuk menghentikan (Stop) proses penangkapan paket data yang sedang berjalan.
- Ikon Hijau (Restart): Berfungsi untuk mengulang kembali proses capture dari awal atau melanjutkan (Continue) tanpa menyimpan data sebelumnya.

**2. Packet List Pane** bagian tengah ini menampilkan ringkasan dari setiap paket yang berhasil ditangkap oleh Wireshark secara real-time.

**3. Packet Details Pane** bagiab ini menunjukkan rincian hierarki protokol dari satu paket yang dipilih pada bagian daftar. Setiap baris dapat diklik (tanda panah kecil) untuk melihat detail parameter di dalam setiap lapisan protokol tersebut.

**4. Packet Bytes Pane** bagian kanan bawah ini menampilkan isi data paket dalam bentuk mentah (raw data). Data ditampilkan dalam format Heksadesimal (sebelah kiri) dan representasi ASCII (sebelah kanan).
