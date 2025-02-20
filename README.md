# opencore-0.9.9-thinkpad-x270-osx-ventura

Repositori ini berisi file - file EFI untuk kebutuhan hackintosh di Lenovo Thinkpad X270


### Hardware

- **Model** : Lenovo Thinkpad x270
- **Prosesor** : i5-6300U (Skylake-U)
- **GPU** : Intel(R) HD Graphics 520 (integrated)
- **RAM** : 16GB DDR4 2133 Mhz
- **Audio** : Realtek ALC298 @ Intel Sunrise Point-LP PCH - High Definition Audio Controller
- **Trackpad** : HID-Compilant Mouse
- **Storage** : Samsung SSD SATA 128 GB
- **Baterai** : Dual battery (Internal (Sanyo), Eksternal (Lenovo))
- **Wireless + Bluetooth** : Intel(R) Dual Band Wireless-AC 8260
- **Ethernet** : Intel(R) Ethernet Connection I219-LM
- **Bootloader** : OpenCore 0.9.9
- **Versi OS** : MacOS Ventura 13.6.6


### Apa saja yang bisa jalan?

- [x] Internal GPU (graphics acceleration juga bisa)
- [x] CPU Power Management
- [x] Baterai (hanya yang internal saja yang terdeteksi)
- [x] All USB ports
- [x] HDMI port (HDMI Audio juga)
- [x] Ethernet port
- [x] Audio (headphone jack juga bisa)
- [x] Camera (Facetime)
- [x] Trackpad (gesture bisa tetapi klik trackpad tidak. tap to click bisa.)
- [x] Shutdown, Reboot
- [x] Keyboard (termasuk tombol`fn`)
- [x] Wi-Fi & Bluetooth (Apple Services juga bisa jalan)
- [x] iMessage, FaceTime, App Store, iTunes Store (SMBIOS valid)
- [x] Sleep / Wake (buka-tutup engsel juga bisa)


### Apa saja yang nggak jalan?

- [x] DRM (iTunes Movies, Apple TV+, Amazon Prime, Netflix, dll)  - bisa nonton di web browser


## Persiapan
 1. Laptop Lenovo Thinkpad X270 yang sudah terinstall Windows 10/11 64bit untuk membuat bootable media
 2. Flashdisk 16GB atau yang lebih besar
 2. Python 3
 3. File recovery boot MacOS Ventura untuk Thinkpad X270 [Download](https://drive.google.com/file/d/1yzPJPglbM4rZ0673S1tu0AEaNVLl8t9P/view?usp=sharing)
 4. Download file-file EFI diari repositori ini [Download](https://github.com/esyede/opencore-0.9.9-thinkpad-x270-osx-ventura/archive/main.zip)
 5. Aplikasi tambahan:
  - https://mackie100projects.altervista.org/download-opencore-configurator (untuk mount & replace EFI di flashdisk ke partisi EFI MacOS agar bisa boot tanpa flashdisk, untuk tweak `config.plist` juga)
  - https://github.com/mlch911/one-key-hidpi (untuk menaikan reolusi layar agar bisa HiDPI)
  - https://www.bresink.com/osx/0TinkerTool/download.php (untuk tweak/disable fitur - fitur MacOS yang didak saya butuhkan)


## Instalasi

### Pengaturan BIOS:
<small>Tekan & tahan tombol`Enter` saat laptop dinyalakan, lalu `F1` untuk masuk ke BIOS Setup Utility</small>

**Pada tab Security**
- `Security Chip` **Disabled**
- `Memory Protection -> Execution Prevention` **Enabled**
- `Virtualization -> Intel Virtualization Technology` **Enabled**
- `Virtualization -> Intel VT-d Feature` **Enabled**
- `Anti-Theft -> Computrace -> Current Setting` **Disabled**
- `Secure Boot -> Secure Boot` **Disabled**
- `Intel SGX -> Intel SGX Control` **Disabled**
- `Device Guard` **Disabled**

**Pada tab Startup**
- `UEFI/Legacy Boot` **UEFI Only**
- `CSM Support` **No**


## Instalasi (di windows)
 1. Install Python 3 [64bit](https://www.python.org/ftp/python/3.11.9/python-3.11.9-amd64.exe) untuk download base system recovery MacOS
 2. Download OpenCorePkg (Skip, sudah ada di repository ini)
 3. Download base system MacOS (Skip, sudah ada di repository ini)
 4. Colok flashdisk lalu format ke FAT32, beri nama flashdisknya 'FLASHDISKKU' agar nanti mudah dicari
 5. Copy folder `com.apple.recovery.boot` dan folder `EFI` dari repository ini ke flashdisk yang sudah diformat tadi
 6. Setting `config.plist`, mengunpulkan Kexts, Drivers, SSDT dll yang cocok untuk Thinkpad X270 (Skip, sudah ada)
 7. Alokasikan partisi hardisk untuk install MacOS nya, Beri nama "MacOS" * (ini untuk yang mau dualboot, yang mau singleboot nanti bisa format seluruh hardisk ke format APFS lewat Disk Utility nya Mac ketika instalasi MacOS nya berlangsung). Disini kita buat dualboot saja dulu.
    - Panduan video: https://www.youtube.com/watch?v=CxKtzT9BFD4&t=44m5s
 8. Lanjut setting BIOS: Restart laptop, tekan & tahan tombol `Enter` saat laptop sudah nyala, lalu `F1` untuk masuk ke BIOS Setup Utility. Ubah setingan BIOS di bagian ini:
    - Tab Security:
        - `Security Chip` **Disabled**
        - `Memory Protection -> Execution Prevention` **Enabled**
        - `Virtualization -> Intel Virtualization Technology` **Enabled**
        - `Virtualization -> Intel VT-d Feature` **Enabled**
        - `Anti-Theft -> Computrace -> Current Setting` **Disabled**
        - `Secure Boot -> Secure Boot` **Disabled**
        - `Intel SGX -> Intel SGX Control` **Disabled**
        - `Device Guard` **Disabled**
    - Tab Startup
        - `UEFI/Legacy Boot` **UEFI Only**
        - `CSM Support` **No**
 9. Jika sudah semua, tekan `F10` lalu `Yes` lalu `Enter` agar laptopnya restart lagi, tekan & tahan tombol `Enter` saat laptop sudah nyala
 10. Lalu tekan `F12` agar masuk ke menu Boot Options, setelah itu pilih nama flashdisk anda, gunakan tombol panah atas-bawah kiri-kanan untuk memilih flasdisk anda, lalu `Enter`
 11. Tunggu beberapa menit sampai logo loading MacOS muncul (indikasi sukses booting lewat flashdisk)
 12. Tunggu lagi sampai muncul tampilan Mac Recovery
 12. Setelah itu, jangan lupa sambungkan ke wifi dengan cara klik logo wifi di pojok kanan atas tampilan Mac Recovery tersebut karena kita akan download file MACOS Ventura nya lewat wifi
 13. Oke, sekarang lanjut format partisi kita tadi ke formatnya Apple (APFS), lalu download file MacOS Ventura nya lewat wifi. Panduan video: https://www.youtube.com/watch?v=CxKtzT9BFD4&t=48m10s
 14. Setelah proses download + install selesai, laptop akan restart, flasdisk jangan dicabut dulu agar tetap bisa booting karena file-file EFI yang cocvok dengan laptop kita masih ada di flashdisk
 15. Laptop akan restart lagi, biarkan saja, jika sudah selesai bisa pilih partisi "MacOS" agar boot ke partisi MacOS seperti di video tersebut
 16. Sampai sini kita sudah masuk ke stup akun di MacOS kita, silahkan di setup sesuai akun masing-masing
 17. Setelah setup akun selesai, silahkan install aplikasi OpenCore Configurator
 18. Sekarang buka aplikasi OpenCore Configurator, kita akan timpa file-file EFI bawaan MacOS dengan EFI dari flashdisk kita tadi agar booting sukses tanpa colok flashdisk
 19.  Klik menu Tools > Mount EFI > klik Mount Partition di partisi bernama "MacOS" tadi
 20. Lalu klik Open Partition kemudian hapus folder `EFI` di partisi MacOS tersebut, kemudian copy folder EFI dari flashdisk dan paste ke partisi MacOS nya
 21. Cabut flashdisk, kemudian restart laptopnya
 22. Done




## Kustomisasi tambahan

Naikkan resolusi ke HiDPI:
https://github.com/mlch911/one-key-hidpi (untuk menaikan reolusi layar agar bisa HiDPI)

Tweak atau jika perlu disable fitur - fitur MacOS yang tidak diinginkan
https://www.bresink.com/osx/0TinkerTool/download.php

Enable MacOS HiDPI untuk layar non-retina display:
```sh
bash -c "$(curl -fsSL https://raw.githubusercontent.com/mlch911/one-key-hidpi/master/hidpi.sh)"
```
<small>Referensi: https://github.com/mlch911/one-key-hidpi</small>


Fix lag ketika maximize/minimize window (disable animation):
```sh
defaults write -g NSWindowResizeTime -float 0.001
```
 
Untuk mengaktifkan kembali animation:
```sh
defaults delete -g NSWindowResizeTime
```

Untuk cek/set timezone:
```sh
sudo systemsetup -listtimezones | more      # untuk melihat list timezones
sudo systemsetup -settimezone Asia/Jakarta  # untuk set timezone
sudo systemsetup -gettimezone               # untuk cek timezone saat ini
```



Happy hackintoshing!
