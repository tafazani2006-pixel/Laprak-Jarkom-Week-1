## Talitha Fairuzzahwa Nirwasita - 103072400035 - IF0405
# MODUL 9 : Web Server
## Web Server
Web server merupakan komponen penting dalam sistem komunikasi berbasis internet. Web server berfungsi untuk menerima permintaan (request) dari klien, seperti browser, kemudian mengirimkan respons berupa halaman web atau data yang diminta. Proses komunikasi ini umumnya menggunakan protokol HTTP (HyperText Transfer Protocol) yang berjalan di atas TCP (Transmission Control Protocol).

## Web Server Sederhana
**Langkah-langkah**
1. Membuat file serverweb.py
2. Tulis code
```python
from socket import *
import sys

# membuat socket server (TCP)
serverSocket = socket(AF_INET, SOCK_STREAM)

# Prepare a server socket
serverPort = 6789
serverSocket.bind(('', serverPort))
serverSocket.listen(1)

while True:
    # Establish the connection
    print('Ready to serve...')
    connectionSocket, addr = serverSocket.accept()

    try:
        # menerima request dari client
        message = connectionSocket.recv(1024).decode()
        print(message)

        # mengambil nama file
        filename = message.split()[1]

        # membuka file
        f = open(filename[1:])
        outputdata = f.read()

        # Send HTTP header
        connectionSocket.send("HTTP/1.1 200 OK\r\n".encode())
        connectionSocket.send("Content-Type: text/html\r\n".encode())
        connectionSocket.send("\r\n".encode())

        # kirim isi file
        for i in range(len(outputdata)):
            connectionSocket.send(outputdata[i].encode())

        connectionSocket.send("\r\n".encode())
        connectionSocket.close()

    except IOError:
        # kirim 404 jika file tidak ada
        connectionSocket.send("HTTP/1.1 404 Not Found\r\n".encode())
        connectionSocket.send("Content-Type: text/html\r\n".encode())
        connectionSocket.send("\r\n".encode())
        connectionSocket.send("<html><body><h1>404 Not Found</h1></body></html>".encode())

        # tutup koneksi
        connectionSocket.close()

serverSocket.close()
sys.exit()
```
3. Buat file HelloWorld.html di folder yang sama
4. Isi dengan
```html
<html>
<head>
    <title>Test Server</title>
</head>
<body>
    <h1>Hello World!</h1>
    <p>Ini hasil server Python TCP</p>
</body>
</html>
```
5. Buka terminal dan jalanan file code tersebut (py serverweb.py)
6. Buka browser ketikan URL: http://localhost:6789/HelloWorld.html
7. Buka tab lain dan ketikan ERL: http://localhost:6789/salah.html

Program dimulai dengan membuat socket TCP menggunakan library socket. Server kemudian diikat pada port tertentu dan masuk ke mode listening untuk menunggu koneksi dari klien. Ketika klien terhubung, server menerima request HTTP dan mengekstrak nama file yang diminta. Jika file tersedia, server mengirimkan response dengan status 200 OK beserta isi file HTML. Jika file tidak ditemukan, server mengirimkan response 404 Not Found. Program ini bersifat single-threaded, sehingga hanya dapat menangani satu permintaan dalam satu waktu.

**Hasil Percobaan**

<img width="809" height="272" alt="image" src="https://github.com/user-attachments/assets/db796dd9-e8fc-48b0-9b63-9377c00a0aa8" />
Server berhasil menampilkan isi file HTML pada browser.

<img width="817" height="245" alt="image" src="https://github.com/user-attachments/assets/0c8f69c0-3725-4b9c-9432-4438de4837d2" />
Pada bercobaan kedua, server menampilkan "404 Not Found". Hal ini menunjukkan bahwa server berhasil menangani request valid dan error dengan benar.

## Latian Web Tambahan (Multithreaded Server)
**Langkah-langkah**
1. Membuat file server.py
2. Tulis code
```python
from socket import *
import threading

def handle_client(connectionSocket):
    try:
        # menerima pesan user
        message = connectionSocket.recv(1024).decode() # decode = 10101010 = "message"

        # index.html, hello.html
        # message isinya = /GET /index.html HTTP/1.1
        message = message[4:15]
        print(message)
        # filename = message.split()[1]

        # membuka index.html serta menghilangkan "/"
        f = open(message[1:])

        # membaca file html
        outputData = f.read()

        # kirim respon
        connectionSocket.send(
            "HTTP/1.1 200 OK\r\n\r\n".encode()
        )

        # kirim data
        connectionSocket.sendall(outputData.encode())

        # tutup koneksi
        connectionSocket.close()
    
    except IOError:
        # kirim respon bila tidak ditemukan
        connectionSocket.send(
            "HTTP/1.1 404 Not Found\r\n\r\n".encode()
        )

        # kirim data
        connectionSocket.send(
            "<h1>404 Not Found</h1>".encode()
        )

        # tutup koneksinya
        connectionSocket.close()


serverSocket = socket(AF_INET, SOCK_STREAM)
serverSocket.bind(('', 6789))
serverSocket.listen(5) # dapat menerima sebanyak 5 client
print("[SYSTEM] server is running...")

while True:
    connectionSocket, addr =  serverSocket.accept()

    # membuat thread dan target threadnya, beseerta parameter
    thread = threading.Thread(
        target = handle_client,
        args = (connectionSocket,)
        )
    # menjalankan
    thread.start()
```
3. Buat file index.html di folder yang sama
4. Isi dengan
```html
<h1>Alhamdulillah bisa kak aku sudah berusaha sebaik mungkin dan ini adalah hasil amal baikku</h1>
```
5. Buka terminal dan jalanan file code tersebut (py server.py)
6. Buka browser ketikan URL: http://localhost:6789/index.html

Pada versi ini, server menggunakan multithreading untuk menangani beberapa klien secara bersamaan. Setiap koneksi yang masuk akan dibuatkan thread baru yang menjalankan fungsi handle_client(). Dengan pendekatan ini, server tidak perlu menunggu satu klien selesai sebelum melayani klien lain, sehingga meningkatkan efisiensi dan performa server.

**Hasil Percobaan**

<img width="975" height="164" alt="image" src="https://github.com/user-attachments/assets/47f72b3b-95a8-4997-b444-f391dfe0350a" />

Ketika beberapa browser atau tab dibuka secara bersamaan, semua request tetap dapat diproses dengan baik

## Kesimpulan
Pada percobaan pertama, server web sederhana berhasil dibuat untuk menangani permintaan HTTP dan mengirimkan response sesuai dengan file yang diminta.
Pada percobaan kedua, server dikembangkan menjadi multithreaded sehingga mampu menangani banyak permintaan secara bersamaan. Hal ini menunjukkan bahwa penggunaan thread dapat meningkatkan performa server dalam lingkungan jaringan.
