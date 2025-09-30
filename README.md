# Jarkom-Modul-1-2025-K-39

## Soal 1
Untuk mempersiapkan pembuatan entitas selain mereka, Eru yang berperan sebagai Router membuat dua Switch/Gateway. Dimana Switch 1 akan menuju ke dua Ainur yaitu Melkor dan Manwe. Sedangkan Switch 2 akan menuju ke dua Ainur lainnya yaitu Varda dan Ulmo. Keempat Ainur tersebut diberi perintah oleh Eru untuk menjadi Client.
<img width="487" height="335" alt="image" src="https://github.com/user-attachments/assets/42800e5a-0b23-42b8-9224-9cd4c8f99f0f" />
- NAT 1 dihubungkan ke Eru eth0
- Switch1 eth0 disambung ke Eru eth1
- Switch2 eth0 disambung ke Eru eth2
- Melkor eth0 disambung ke switch1 eth1
- Manwe eth0 disambung ke switch1 eth2
- Varda eth0 disambung ke switch2 eth1
- Ulmo eth0 disambung ke switch2 eth2 

## Soal 2 
Karena menurut Eru pada saat itu Arda (Bumi) masih terisolasi dengan dunia luar, maka buat agar Eru dapat tersambung ke internet.
<img width="514" height="301" alt="image" src="https://github.com/user-attachments/assets/3fa3ff5c-191d-4fd4-b930-4dc3f41baac6" />
```
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
#### 1. **Interface eth0**

```bash
auto eth0
iface eth0 inet dhcp
```

* **auto eth0**: Interface `eth0` akan otomatis aktif saat sistem boot.
* **iface eth0 inet dhcp**: IP untuk interface ini diperoleh secara otomatis dari DHCP server.

---

#### 2. **Interface eth1**

```bash
auto eth1
iface eth1 inet static
    address 10.83.1.1
    netmask 255.255.255.0
```

* **auto eth1**: Interface `eth1` juga akan aktif secara otomatis saat sistem menyala.
* **iface eth1 inet static**: IP ditetapkan secara statis (manual).
* **address 10.83.1.1**: IP yang digunakan oleh interface `eth1`.
* **netmask 255.255.255.0**: Subnet mask yang digunakan, berarti jaringan memiliki rentang IP 10.83.1.0/24.

---

#### 3. **Interface eth2**

```bash
auto eth2
iface eth2 inet static
    address 10.83.2.1
    netmask 255.255.255.0
```

* **auto eth2**: Interface `eth2` juga langsung aktif saat booting.
* **iface eth2 inet static**: Pengaturan IP dilakukan secara manual.
* **address 10.83.2.1**: IP yang ditetapkan untuk `eth2`.
* **netmask 255.255.255.0**: Subnet mask untuk jaringan 10.83.2.0/24.

## Soal 3
Sekarang pastikan agar setiap Ainur (Client) dapat terhubung satu sama lain.

<img width="915" height="591" alt="image" src="https://github.com/user-attachments/assets/b565da26-6dbd-46ee-ad83-36f983333763" />

#### Eru
```
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
```
auto eth0
iface eth0 inet static
	address 10.83.1.2
	netmask 255.255.255.0
	gateway 10.83.1.1
```
#### Manwe
```
auto eth0
iface eth0 inet static
	address 10.83.1.3
	netmask 255.255.255.0
	gateway 10.83.1.1
```
#### Varda
```
auto eth0
iface eth0 inet static
	address 10.83.2.2
	netmask 255.255.255.0
	gateway 10.83.2.1
```
#### Ulmo
```
auto eth0
iface eth0 inet static
	address 10.83.2.3
	netmask 255.255.255.0
	gateway 10.83.2.1
```

## Soal 4
Setelah berhasil terhubung, sekarang Eru ingin agar setiap Ainur (Client) dapat mandiri. Oleh karena itu pastikan agar setiap Client dapat tersambung ke internet.

#### Eru
```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 10.83.0.0/16
cat /etc/resolv.conf
```
#### Manwe, Melkor, varda dan Ulmo
```
echo nameserver 192.168.122.1 > /etc/resolv.conf
```





