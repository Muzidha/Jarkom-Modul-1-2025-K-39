
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






