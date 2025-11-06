# Lab Jaringan - Membangun Switch dan Router Network

## Deskripsi
Proyek ini merupakan dokumentasi Tugas Akhir Judul 2. Jaringan sederhana menggunakan satu router, satu switch, dan dua PC.

## Topologi Jaringan
- **PC-A** terhubung ke **Switch S1** (port F0/6)
- **Switch S1** (port F0/5) terhubung ke **Router R1** (port G0/0/1)
- **PC-B** terhubung langsung ke **Router R1** (port G0/0/0)

## Tabel Pengalamatan

| Device | Interface | IP Address IPv4    | IP Address IPv6        | Default Gateway |
|--------|-----------|-------------------|------------------------|-----------------|
| R1     | G0/0/0    | 192.168.0.1/24    | 2001:db8:acad::1/64    | N/A             |
| R1     | G0/0/1    | 192.168.1.1/24    | 2001:db8:acad:1::1/64  | N/A             |
| S1     | VLAN 1    | 192.168.1.2/24    | -                      | 192.168.1.1     |
| PC-A   | NIC       | 192.168.1.3/24    | 2001:db8:acad:1::3/64  | 192.168.1.1     |
| PC-B   | NIC       | 192.168.0.3/24    | 2001:db8:acad::3/64    | 192.168.0.1     |

## Tahapan Konfigurasi

### 1. Persiapan dan Koneksi Perangkat
Menghubungkan semua perangkat sesuai dengan topologi yang telah ditentukan menggunakan kabel ethernet dan console.

### 2. Konfigurasi IP Address pada PC
- **PC-A**: IP 192.168.1.3/24, Gateway 192.168.1.1
- **PC-B**: IP 192.168.0.3/24, Gateway 192.168.0.1

### 3. Ping Test Pertama (Sebelum Konfigurasi Router)
Melakukan ping dari PC-A ke PC-B yang menghasilkan kegagalan karena router belum dikonfigurasi.

**Screenshot:**

![Ping Gagal](screenshot-ping-gagal.png)

**Penjelasan:** Ping gagal karena router yang menjadi penghubung antar subnet belum dikonfigurasi. Paket tidak dapat di-routing antara jaringan 192.168.1.0 dan 192.168.0.0.

### 4. Konfigurasi Router R1
Konfigurasi yang dilakukan pada router:
- Hostname: R1
- Password privileged EXEC: class
- Password console dan VTY: cisco
- Enkripsi password
- Banner MOTD
- Interface G0/0/0: 192.168.0.1/24
- Interface G0/0/1: 192.168.1.1/24
- Konfigurasi IPv6 pada kedua interface
- Aktivasi IPv6 routing

### 5. Konfigurasi Switch S1
Konfigurasi yang dilakukan pada switch:
- Hostname: S1
- Interface VLAN 1: 192.168.1.2/24
- Default gateway: 192.168.1.1

### 6. Ping Test Kedua (Setelah Konfigurasi Router)
Melakukan ping dari PC-A ke PC-B yang menghasilkan keberhasilan setelah router dikonfigurasi.

**Screenshot:**

![Ping Berhasil](screenshot-ping-berhasil.png)

**Penjelasan:** Ping berhasil karena router sudah dikonfigurasi dengan benar. Router berfungsi sebagai gateway yang menghubungkan kedua subnet dan meneruskan paket data antara PC-A dan PC-B.

## Verifikasi Konfigurasi

### Perintah Show pada Router
```
show ip route
show ipv6 route
show ip interface brief
show ipv6 interface brief
show ip interface g0/0/1
```

### Perintah Show pada Switch
```
show ip interface brief
show running-config
```

## File Packet Tracer
File simulasi Packet Tracer tersedia di repository ini dengan nama: `lab-switch-router-network.pkt`

## Video Tutorial
Link YouTube: https://www.youtube.com/watch?v=uarOLoZx_eI

## Kesimpulan
Lab ini berhasil mendemonstrasikan:
- Konfigurasi dasar router dan switch Cisco
- Pentingnya router dalam menghubungkan subnet yang berbeda
- Penggunaan IPv4 dan IPv6 secara bersamaan (dual-stack)
- Verifikasi konektivitas menggunakan perintah ping dan show

---
**Dibuat oleh:** Luthfi Muthathohirin
**NPM:** 2315061112  
**Kelas:** Jaringan Komputer E
