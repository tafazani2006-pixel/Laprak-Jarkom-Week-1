## Talitha Fairuzzahwa Nirwasita - 103072400035 - IF0405
# MODUL 5 : UDP
## UDP

**Langkah-langkah**
1. Download file http://gaia.cs.umass.edu/wireshark-labs/wireshark-traces.zip
2. Extract file dan cari file *http-ethereal-trace-5*
3. Klik kanan file tersebut, lalu buka (open with) dengan wireshark
   <img width="679" height="563" alt="Screenshot 2026-04-03 154410" src="https://github.com/user-attachments/assets/8e6ff8f6-2a29-4f03-97db-4bacf6db8cff" />
4. Lakukan filter UDP dan pilih 1 paket UDP (bebas)

**Pertanyaan**
1. Field UDP

   <img width="631" height="308" alt="image" src="https://github.com/user-attachments/assets/2921d868-6104-438b-a322-c066bcf8f2c7" />

   Terdapat 4 field : Source Port, Destination Port, Length, Checksum

2. Panjang tiap field
   Bedasarkan teori UDP :
   - Source Port = 2 byte
   - Destination Port = 2 byte
   - Length = 2 byte
   - Checksum = 2 byte
   Maka total = 2+2+2+2 = 8 byte

3. Length

   <img width="283" height="169" alt="Screenshot 2026-04-03 155911" src="https://github.com/user-attachments/assets/06e863bb-e4b8-4803-9013-bc6c0e0246b8" />

   Length (58) menunjukkan total panjang UDP (header (8 byte) + data). maka Data = total - header = 58 - 8 = 50 byte, hal tersebut cocok dengan UDP payload (50 byte)

4. Jumlah maksimum byte UDP
   - Header UDP = 8 byte
   - Max ukuran IP = 65535 byte
   65535 - 20 (IP header) - 8 (UDP header) = 65507 byte. Maka maksimum payload UDP adalah 65507 byte

5. Port terbesar

6. Nomor protokol UDP

   <img width="632" height="272" alt="image" src="https://github.com/user-attachments/assets/acb2bc5b-bbc0-48fb-908a-7f33c7733d9d" />

   Nomor protokol UDP adalah 17 (desimal) atau 0x11 (heksadesimal)

7. Hubungan port

   <img width="466" height="195" alt="image" src="https://github.com/user-attachments/assets/a9eca4c0-a63e-4cf9-9b63-617f358f68c7" /> <img width="500" height="197" alt="image" src="https://github.com/user-attachments/assets/2e1640de-c4f8-4329-8656-51831dbac695" />

   

   

