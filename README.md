# **Minecraft Server Setup with CasaOS on Ubuntu Server 22.04**

Panduan ini menjelaskan cara menyiapkan home server menggunakan CasaOS pada VM VirtualBox yang menjalankan Ubuntu Server 22.04. Server akan menjadi host bagi beberapa layanan seperti berbagi file, streaming media, dan banyak lagi.

---

## **Prerequisites**

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

### **4. Install CasaOS**
1. Install CasaOS using the official installation script:
   ```bash
   curl -fsSL https://get.casaos.io | sudo bash
2. Wait for the installation to complete. This script will:
   - Install Docker and necessary dependencies.
   - Set up CasaOS services.
3. Verify the installation by accessing CasaOS via a web browser:
   - Get the server's IP address:
   ```bash
   ip a
   ```
   - Open http://<your-server-ip> in a web browser (port 80 is the default).

---

### **5. Configure Server Services**
Setelah CasaOS terinstal, Anda dapat mengatur layanan berikut:

