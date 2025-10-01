
---

# Jarkom-Modul-1-2025-K-39

## Soal 1

Untuk mempersiapkan pembuatan entitas selain mereka, **Eru** yang berperan sebagai Router membuat dua Switch/Gateway.

* **Switch 1** mengarah ke dua Ainur: **Melkor** dan **Manwe**
* **Switch 2** mengarah ke dua Ainur lainnya: **Varda** dan **Ulmo**
* Keempat Ainur tersebut bertindak sebagai **Client**

### Topologi:

<img width="487" height="335" alt="image" src="https://github.com/user-attachments/assets/42800e5a-0b23-42b8-9224-9cd4c8f99f0f" />

### Koneksi:

* NAT1 → Eru `eth0`
* Switch1 `eth0` → Eru `eth1`
* Switch2 `eth0` → Eru `eth2`
* Melkor `eth0` → Switch1 `eth1`
* Manwe `eth0` → Switch1 `eth2`
* Varda `eth0` → Switch2 `eth1`
* Ulmo `eth0` → Switch2 `eth2`

---

## Soal 2

Karena Arda (Bumi) masih terisolasi dari dunia luar, maka dibuat agar **Eru dapat tersambung ke internet**.

<img width="514" height="301" alt="image" src="https://github.com/user-attachments/assets/3fa3ff5c-191d-4fd4-b930-4dc3f41baac6" />

### Konfigurasi Network Eru

```bash
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
    address 10.83.1.1
    netmask 255.255.255.0

auto eth2
iface eth2 inet static
    address 10.83.2.1
    netmask 255.255.255.0
```

#### Penjelasan:

**1. Interface eth0**

```bash
auto eth0
iface eth0 inet dhcp
```

* `auto eth0`: Aktif saat boot
* `iface eth0 inet dhcp`: Mendapat IP otomatis dari DHCP

**2. Interface eth1**

```bash
auto eth1
iface eth1 inet static
    address 10.83.1.1
    netmask 255.255.255.0
```

* IP statis untuk subnet `10.83.1.0/24`

**3. Interface eth2**

```bash
auto eth2
iface eth2 inet static
    address 10.83.2.1
    netmask 255.255.255.0
```

* IP statis untuk subnet `10.83.2.0/24`

---

## Soal 3

Memastikan agar setiap Ainur (Client) dapat **terhubung satu sama lain**.

<img width="915" height="591" alt="image" src="https://github.com/user-attachments/assets/b565da26-6dbd-46ee-ad83-36f983333763" />

### Konfigurasi Setiap Node

#### Eru

```bash
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
    address 10.83.1.1
    netmask 255.255.255.0

auto eth2
iface eth2 inet static
    address 10.83.2.1
    netmask 255.255.255.0
```

#### Melkor

```bash
auto eth0
iface eth0 inet static
    address 10.83.1.2
    netmask 255.255.255.0
    gateway 10.83.1.1
```

#### Manwe

```bash
auto eth0
iface eth0 inet static
    address 10.83.1.3
    netmask 255.255.255.0
    gateway 10.83.1.1
```

#### Varda

```bash
auto eth0
iface eth0 inet static
    address 10.83.2.2
    netmask 255.255.255.0
    gateway 10.83.2.1
```

#### Ulmo

```bash
auto eth0
iface eth0 inet static
    address 10.83.2.3
    netmask 255.255.255.0
    gateway 10.83.2.1
```

---

## Soal 4

Agar setiap Client dapat **mengakses internet secara mandiri**, dilakukan konfigurasi berikut:

### Pada Eru

```bash
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 10.83.0.0/16
cat /etc/resolv.conf
```

### Pada Melkor, Manwe, Varda, dan Ulmo

```bash
echo nameserver 192.168.122.1 > /etc/resolv.conf
```
---

<img width="719" height="159" alt="image" src="https://github.com/user-attachments/assets/5d3aee6d-052f-4a05-ab8c-5cb5949126ab" />

---

<img width="719" height="214" alt="image" src="https://github.com/user-attachments/assets/c242484f-1618-477f-976e-67c9fd92020f" />

---

<img width="694" height="187" alt="image" src="https://github.com/user-attachments/assets/cbb9b342-f473-472e-9ef8-75853bfb64b4" />

---

<img width="734" height="241" alt="image" src="https://github.com/user-attachments/assets/aa12b253-a142-447c-be34-73d1bec4b825" />

---

<img width="733" height="268" alt="image" src="https://github.com/user-attachments/assets/e2cab122-397a-4299-b7c2-b948c2dedee8" />

## Soal 5
---

Gunakan ```nano /root/.bashrc``` agar dapat mengakses /root dan simpan knfigurasi dan command di file tersebut

---

<img width="801" height="447" alt="image" src="https://github.com/user-attachments/assets/0824e357-b396-45d5-a85b-dd66efddab01" />

---

Gunakan cara yang sama di setiap node dan simpan konfigurasi agar ketika restart tidak diulang dari awal

---

<img width="721" height="278" alt="image" src="https://github.com/user-attachments/assets/0cf871c2-f764-4d89-bec1-1593cc891445" />

---


## Soal 6


gunakan node Manwe dan masuk ke node tersebut, lalu download file traffic.zip dan Unzip paket traffic.zip tersebut. maka akan muncul file traffic.sh.
capture traffic antara Eru dan Manwe
---

<img width="756" height="520" alt="image" src="https://github.com/user-attachments/assets/d5de6bad-5bc5-429b-97a5-d6adf76e0e93" />

---

setelah wireshark terbuka, jalankan file traffic.sh di node manwe

---

<img width="575" height="93" alt="image" src="https://github.com/user-attachments/assets/351073f5-aac2-4c84-acaf-f34d81c52ac6" />

---

maka akan terlihat hasil capture di wireshark. gunakan filter ```ip.src == 10.83.1.3 || ip.dst == 10.83.1.3``` untuk melihat packet mana saja yang dari Manwe dan packet yang menuju Manwe

---

<img width="739" height="272" alt="image" src="https://github.com/user-attachments/assets/1705ac8d-8f8e-46a1-8ab9-033e0d47b6fe" />

---

## Soal 14

kita diminta menganalisis file capture yang disediakan dan melakukan identifikasi brute force. Selanjutnya, kita masuk ke Statistics → Endpoints → IPv4 untuk melihat IP yang memiliki jumlah paket terbanyak.

---

<img width="692" height="208" alt="Screenshot 2025-10-01 173537" src="https://github.com/user-attachments/assets/5839f6e4-8361-410b-8d61-3e478f4d3175" />

---

Setelah kita cari, ternyata ada dua alamat IP yang memiliki jumlah paket terbanyak, yaitu 172.19.5.26 dan 192.168.129.101. Setelah itu, kita coba memfilter trafik yang berhubungan dengan alamat IP tersebut pertama-tama kita ambil 172.19.5.26. Berikut adalah filter yang saya gunakan.

```
http && ip.addr == 172.19.5.26
```

---

<img width="1275" height="236" alt="Screenshot 2025-10-01 173956" src="https://github.com/user-attachments/assets/f073f783-f9e4-40f6-a307-e4e7ace35dd6" />

---

Kemudian kita mencoba memeriksa salah satunya secara acak dengan cara klik kanan → Follow → TCP Stream, atau dengan menekan tombol Ctrl + Alt + Shift + T.

---

<img width="944" height="535" alt="Screenshot 2025-10-01 174339" src="https://github.com/user-attachments/assets/7c9c1f91-d497-4d9d-892e-0bb1492f4695" />

---

Lalu, kita akan memperoleh informasi yang mengarahkan kita pada jawaban akhir soal nomor 14.

---

<img width="540" height="404" alt="Screenshot 2025-10-01 174517" src="https://github.com/user-attachments/assets/76b75e64-e3b7-4daf-a3fb-1c3852ca43ca" />

---

Di sini kita menemukan beberapa kata kunci penting, yaitu “username” dan “password”. Namun ketika kita memfilter menggunakan frame contains "username" dan frame contains "password", hasilnya sama seperti sebelumnya. Oleh karena itu saya mencari kata kunci lain yang lebih relevan dengan soal dan memfilter menggunakan kata kunci tersebut.

```
frame contains "success"
```

Saat dilakukan filter, hanya ada satu IP yang muncul. Kemudian kita melakukan pengecekan dengan cara klik kanan → Follow → TCP Stream, atau dengan menekan kombinasi tombol Ctrl + Alt + Shift + T untuk melihat isi dari IP tersebut.

---

<img width="557" height="402" alt="Screenshot 2025-10-01 175625" src="https://github.com/user-attachments/assets/e1dc1689-5c15-42ad-b365-16a32ee28be8" />

---

Dan yap, kita berhasil menemukan username dan password yang digunakan untuk login.

## Soal 15

Kita perhatikan dari awal bahwa sebagian besar paket protokol adalah USB dengan informasi URB_INTERRUPT, serta memiliki (length) 27 dan 35. Namun, setelah ditelusuri, paket dengan length 35 yang mengandung HID data. Selanjutnya, kita memfilter sesuai dengan informasi yang telah diperoleh.

```
usb.device_address == 11 && usb.endpoint_address == 0x81 && frame.len == 35

```

---

<img width="910" height="749" alt="Screenshot 2025-10-01 193719" src="https://github.com/user-attachments/assets/1891cff5-3fc8-484e-9e6e-a3eac427bba1" />

---

Setelah melakukan filter sesuai kebutuhan sehingga hanya menampilkan seluruh HID Data, kita mengekspornya menjadi satu file teks dengan cara File → Export Packet Dissections → As Plain Text.

---

<img width="934" height="842" alt="Screenshot 2025-10-01 193805" src="https://github.com/user-attachments/assets/d9ea74c2-562b-4257-831f-b3f7e3a1de53" />

---

Setelah menyimpannya sebagai sebuah file teks, kita mencoba menggunakan ChatGPT untuk membantu menerjemahkan keystroke menjadi teks.


---

<img width="572" height="547" alt="Screenshot 2025-10-01 194146" src="https://github.com/user-attachments/assets/f045c196-1143-4df9-baec-868e15b4df02" />

---

Akhirnya, kita mendapatkan sebuah teks dalam bentuk Base64 yaitu “UGx6X3ByMHYxZGVfeTB1cl91czNybjRtZV80bmRfcDRzc3cwcmQ”.
Setelah itu, kita membuka situs https://www.base64decode.org/ untuk melakukan decode pada hasil tersebut, lalu mengubahnya menjadi teks ASCII.

---

<img width="782" height="630" alt="Screenshot 2025-10-01 194828" src="https://github.com/user-attachments/assets/5766d717-7938-4e69-9242-12c3d3801ad7" />

---

Setelah kita decode, kita mendapatkan “Plz_pr0v1de_y0ur_us3rn4me_4nd_p4ssw0rd”, lalu kita melanjutkan ke terminal dan masuk ke netcat sesuai dengan soal.

---

<img width="1074" height="126" alt="Screenshot 2025-10-01 195353" src="https://github.com/user-attachments/assets/296ff167-3ba2-4d64-b436-30b6bb3a320a" />

---

Dan yap, kita mendapatkan flag yaitu “KOMJAR25{K3yb0ard_W4rr10r_sT0UVHySWdqlbKVtCN8IBRmmq}”

## Soal 16













