## Talitha Fairuzzahwa Nirwasita - 103072400035 - IF0405

# MODUL 3 : HTTP
## Basic HTTP GET
Proses ini bertujuan untuk mengamati proses komunikasi antara client (browser) dan server yang menggunakan HTTP GET dan HTTP Response

**Langkah-langkah**
1. Buka aplikasi wireshark
2. Pilih Wi-Fi lalu lakukan proses capture packet
3. Start capture
4. Membuka browser http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file1.html
5. Stop capture
6. Menggunakan filter "http" untuk menampilkan paket HTTP

ini gambar

Pada percobaan ini terlihat bahwa browser mengirimkan HTTP GET request ke server gaia.cs.umass.edu untuk meminta file HTML. Server kemudian merespon dengan HTTP/1.1 200 OK, yang menunjukkan bahwa permintaan berhasil diproses dan file HTML berhasil dikirim ke browser.

## Web Not Found
**Langkah-langkah**
1. Start capture
2. Membuka browser asal
3. Stop capture
4. Menggunakan filter "http" untuk menampilkan paket HTTP

ini gambar

Pada percobaan ini dilakukan pengujian dengan mengakses URL yang tidak tersedia pada server. Browser mengirimkan request HTTP GET ke server dengan alamat yang tidak valid. Berdasarkan hasil capture menggunakan Wireshark terlihat bahwa server merespon dengan kode status HTTP/1.1 404 Not Found. Kode status ini menunjukkan bahwa server berhasil menerima request dari client, namun file atau resource yang diminta tidak ditemukan pada server tersebut.

## Retrieving Long Documents
Proses ini bertujuan untuk mengamati proses pengambilan dokumen HTML berukuran lebih besar melalui protokol HTTP

**Langkah-langkah**
1. Start capture
2. Membuka browser http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file3.html
3. Stop capture
4. Menggunakan filter "http" untuk menampilkan paket HTTP

ini gambar

Browser berhasil menampilkan halaman Bill of Rights yang berisi dokumen teks yang lebih panjang Pada percobaan ini browser mengirimkan HTTP GET request untuk meminta dokumen HTML yang lebih panjang. Server kemudian merespon dengan HTTP/1.1 200 OK yang menandakan bahwa permintaan berhasil diproses. Dokumen HTML yang dikirim oleh server berisi teks yang lebih panjang dibandingkan percobaan sebelumnya. Browser kemudian menampilkan isi dokumen tersebut dalam bentuk halaman web.

## HTML Documents dengan Embedded Objects
Proses ini bertujuan untuk mengamati bagaimana browser mengambil objek tambahan yang terdapat pada halaman HTML, seperti gambar

**Langkah-langkah**
1. Start capture
2. Membuka browser http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file4.html
3. Stop capture
4. Menggunakan filter "http" untuk menampilkan paket HTTP

ini gambar

Halaman web menampilkan dua gambar yang merupakan objek yang disematkan dalam HTML. Pada percobaan ini terlihat bahwa browser tidak hanya mengirim satu HTTP GET request untuk mengambil file HTML utama, tetapi juga mengirim beberapa request tambahan untuk mengambil objek yang disematkan di dalam halaman tersebut. Setiap gambar atau objek lain dalam halaman web memiliki URL tersendiri sehingga browser harus mengirim HTTP GET request terpisah untuk setiap objek tersebut. Setelah server merespon dengan HTTP 200 OK, browser kemudian menampilkan gambar tersebut pada halaman web.
