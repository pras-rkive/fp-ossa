# Minecraft Server Setup dengan CasaOS pada Ubuntu Server 22.04 - 23.83.1033

Panduan ini menjelaskan cara membuat server Minecraft yang terintegrasi dengan CasaOS pada Ubuntu Server 22.04. Konfigurasi ini juga mencakup penggunaan Tailscale untuk akses jarak jauh yang aman, UFW untuk manajemen firewall, serta Home Assistant, FileBrowser, dan qBittorrent yang diinstal dari App Store CasaOS. CasaOS menggunakan Docker container untuk mengelola aplikasi, sehingga memudahkan instalasi dan pemeliharaan.

---

## Daftar Isi
1. [Prasyarat](#prasyarat)
2. [Instalasi Ubuntu Server 22.04](#instalasi-ubuntu-server-2204)
3. [Instalasi CasaOS](#instalasi-casaos)
4. [Instalasi dan Konfigurasi SSH](#instalasi-dan-konfigurasi-ssh)
5. [Instalasi dan Konfigurasi Server Minecraft dengan Crafty](#instalasi-dan-konfigurasi-server-minecraft-dengan-crafty)
6. [Integrasi dengan Home Assistant, FileBrowser, dan qBittorrent](#integrasi-dengan-home-assistant-filebrowser-dan-qbittorrent)
7. [Konfigurasi Tailscale](#konfigurasi-tailscale)
8. [Pengaturan UFW](#pengaturan-ufw)
---

## Prasyarat

- Mesin dengan Ubuntu Server 22.04 terinstal.
- Pengetahuan dasar tentang operasi Linux.
- Koneksi internet untuk mengunduh paket.
- Perangkat yang kompatibel dengan CasaOS.

---

## Instalasi Ubuntu Server 22.04

1. **Software Requirements**
   - [VirtualBox](https://www.virtualbox.org/) (latest version)
   - [Ubuntu Server 22.04 ISO](https://ubuntu.com/download/server)

2. **Recommended Virtual Machine Specifications**
   - **CPU**: 2 Cores
   - **RAM**: 4 GB
   - **Storage**: 20 GB
   - **Network**: Bridged Adapter (untuk membuat server dapat diakses di jaringan lokal)

---

## **Steps**

### **1. Create a Virtual Machine**
1. Open VirtualBox and click **New**.
2. Configure the VM:
   - **Name**: `HomeServer`
   - **Type**: Linux
   - **Version**: Ubuntu (64-bit)
   - **Memory Size**: 4096 MB
   - **Hard Disk**: Create a new virtual hard disk (20 GB, dynamically allocated).
3. Open **Settings** and configure:
   - **Network**: Set the network adapter to *Bridged Adapter*.
   - **Storage**: Add the Ubuntu Server 22.04 ISO as the optical drive.

---

### **2. Install Ubuntu Server 22.04**
1. Start the VM and boot from the ISO.
2. Follow the installation process:
   - Choose **English** as the language.
   - Select default **keyboard layout**.
   - Configure the network (it will auto-detect settings if using *Bridged Adapter*).
   - Choose **Use entire disk** for storage configuration.
   - Create a user account (e.g., `admin`) and set a strong password.
   - Select **Install OpenSSH Server** to enable SSH access.
3. Complete the installation and reboot.

---

### **3. Update and Prepare the System**
After logging into your Ubuntu Server:
1. Update the package list and upgrade the system:
   ```bash
   sudo apt update && sudo apt upgrade -y
2. Install essential tools:
   ```bash
   sudo apt install curl wget git -y

---

## Instalasi CasaOS

1. Perbarui sistem Anda:
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```
2. Instal CasaOS dengan perintah berikut:
   ```bash
   curl -fsSL https://get.casaos.io | bash
   ```
3. Akses CasaOS melalui browser web dengan menggunakan alamat IP server Anda dan port default 80.

---

## Instalasi dan Konfigurasi SSH

Setelah instalasi CasaOS, Anda dapat mengatur SSH untuk memastikan Anda dapat mengakses server secara remote dengan aman:

1. Periksa apakah layanan SSH sudah terinstal:
   ```bash
   sudo systemctl status ssh
   ```
   Jika belum terinstal, instal OpenSSH Server:
   ```bash
   sudo apt install openssh-server
   ```
2. Aktifkan dan mulai layanan SSH:
   ```bash
   sudo systemctl enable ssh
   sudo systemctl start ssh
   ```
3. Konfigurasi firewall untuk mengizinkan akses SSH:
   ```bash
   sudo ufw allow ssh
   ```
4. Uji koneksi SSH dari perangkat lain:
   ```bash
   ssh username@server_ip_address
   ```
5. (Opsional) Untuk keamanan tambahan, ubah port default SSH di file konfigurasi:
   ```bash
   sudo nano /etc/ssh/sshd_config
   ```
   Ubah baris `Port 22` ke nomor port yang diinginkan, lalu restart layanan SSH:
   ```bash
   sudo systemctl restart ssh
   ```

---

## Instalasi dan Konfigurasi Server Minecraft dengan Crafty

1. Buka CasaOS dan navigasikan ke App Store.
2. Cari aplikasi "Crafty" dan instal.
3. Setelah instalasi selesai, buka Crafty dan ikuti panduan dalam aplikasi untuk mengatur server Minecraft.
   - Buat instance server baru dengan pengaturan yang diinginkan (misalnya versi server, mod, dll.).

   
   <img width="560" alt="crafty-1" src="https://github.com/user-attachments/assets/02da23bd-058e-4cda-b0dd-400b831442f3" />

   <img width="933" alt="crafty-2" src="https://github.com/user-attachments/assets/b8ae3005-e9ee-4b36-994d-94842bda9f24" />

   
4. Jalankan server Minecraft dan pantau kinerjanya melalui dashboard Crafty.

   <img width="947" alt="crafty-3" src="https://github.com/user-attachments/assets/246724cf-00ef-411f-b851-ffeb52ab8095" />

   <img width="565" alt="crafty-4" src="https://github.com/user-attachments/assets/6f928bcb-4caa-4cc7-83b9-9dfd8be16594" />

   <img width="946" alt="crafty-5" src="https://github.com/user-attachments/assets/a0d4a669-d85c-4b48-9647-0f1b21d28a2c" />

   <img width="960" alt="crafty-6" src="https://github.com/user-attachments/assets/22e5bc8e-4cc6-4402-9ce4-4d22acf36661" />


---

## Integrasi dengan Home Assistant, FileBrowser, dan qBittorrent

### Home Assistant
1. Instal Home Assistant melalui App Store di CasaOS.
2. Konfigurasikan Home Assistant untuk mengotomasi tugas atau memantau lingkungan server Anda.

   <img width="960" alt="dashboard homeAssist" src="https://github.com/user-attachments/assets/fdf93bb9-f100-4d74-9193-c318363abd10" />


### FileBrowser
1. Instal FileBrowser dari App Store di CasaOS.
2. Gunakan FileBrowser untuk mengelola sistem file server melalui antarmuka web.

   <img width="960" alt="dashboard fileBrowser" src="https://github.com/user-attachments/assets/b4f4af3b-8047-4ed4-9f66-872a80774efa" />


### qBittorrent
1. Instal qBittorrent melalui App Store di CasaOS.
2. Konfigurasikan qBittorrent untuk kebutuhan torrenting Anda dengan aman dan efisien.

---

## Konfigurasi Tailscale

1. Instal Tailscale di server Anda:
   ```bash
   curl -fsSL https://tailscale.com/install.sh | sh
   sudo tailscale up
   ```
   
   <img width="429" alt="tailscale-1" src="https://github.com/user-attachments/assets/6b9a4471-7ade-4cf9-a1ae-203b224fc5e8" />

2. Autentikasi perangkat Anda melalui URL yang diberikan.

   <img width="427" alt="tailscale-2" src="https://github.com/user-attachments/assets/f7629396-4198-45a9-9937-bd15166a35e9" />

3. Gunakan Tailscale untuk mengakses server Minecraft dan aplikasi CasaOS Anda dengan aman dari jarak jauh.

---

## Pengaturan UFW

1. Instal UFW jika belum terinstal:
   ```bash
   sudo apt install ufw
   ```
2. Izinkan port yang diperlukan:
   ```bash
   sudo ufw allow ssh
   sudo ufw allow 80/tcp  # CasaOS
   sudo ufw allow 25565/tcp  # Server Minecraft
   sudo ufw allow 51820/udp  # Tailscale
   ```
3. Aktifkan UFW:
   ```bash
   sudo ufw enable
   ```
4. Periksa status UFW:
   ```bash
   sudo ufw status
   ```

---
