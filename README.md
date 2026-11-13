# Electronics Management VB.NET

Aplikasi desktop untuk mengelola inventaris dan transaksi penjualan produk elektronik. Aplikasi ini menyediakan akses terpisah untuk **Admin** dan **Kasir**, sehingga proses penerimaan barang, pengelolaan produk, pengeluaran stok, serta penjualan dapat dicatat dalam satu sistem.

## Fitur Utama

### Admin

- Login sebagai admin.
- Mengelola data produk: menambah, mengubah harga, menghapus, dan melihat stok.
- Mencatat barang masuk dari supplier.
- Melihat riwayat barang masuk.
- Mencatat barang keluar dan alasan pengeluaran.
- Melihat stok terkini.
- Menambah dan menghapus pengguna.

### Kasir

- Login sebagai kasir.
- Mencari produk berdasarkan ID atau nama.
- Menambahkan produk ke keranjang.
- Menghitung total belanja dan kembalian.
- Memproses pembayaran tunai atau e-wallet.
- Mengurangi stok secara otomatis setelah transaksi berhasil.
- Menyimpan detail transaksi dan mencetak struk.

## Tech Stack

- **Bahasa:** Visual Basic .NET
- **Framework:** .NET Framework 4.8
- **Jenis aplikasi:** Windows Forms Desktop Application
- **IDE:** Visual Studio 2022
- **Database:** Microsoft SQL Server / SQL Server Express
- **Data access:** ADO.NET (`System.Data.SqlClient`) dan Typed DataSet
- **Pembuatan struk:** iTextSharp 5.5.13.5
- **Dependensi tambahan:** BouncyCastle.Cryptography 2.6.2

## Prasyarat

Pastikan perangkat sudah memiliki:

1. Windows.
2. Visual Studio 2022 dengan workload **.NET desktop development**.
3. .NET Framework 4.8 Developer Pack.
4. SQL Server Express atau SQL Server.
5. SQL Server Management Studio (SSMS).
6. Git, jika ingin meng-clone repositori.

## Instalasi

### 1. Clone repositori

```bash
git clone https://github.com/Ataya24/Electronics-Management-VB.NET.git
cd Electronics-Management-VB.NET
```

Atau unduh repositori sebagai ZIP, lalu ekstrak ke folder kerja, misalnya:

```text
C:\Users\<username>\source\repos\Electronics-Management-VB.NET
```

### 2. Siapkan database

1. Jalankan SQL Server dan pastikan instance yang digunakan aktif.
2. Buka `DB_Script.txt` di SQL Server Management Studio.
3. Sesuaikan bagian `FILENAME` pada script jika lokasi data SQL Server berbeda.
4. Jalankan script untuk membuat database `KP2`, tabel, relasi, dan default value.

Database yang dibuat memiliki tabel utama berikut:

- `CRUD_Product`: data produk, harga, dan stok.
- `Suppliers`: riwayat barang masuk.
- `GoodsOut`: riwayat barang keluar.
- `Transactions`: data transaksi penjualan.
- `TransactionDetails`: detail item setiap transaksi.
- `TB_User`: akun pengguna.
- `TB_Admin`: tabel admin yang disediakan oleh script database.

Tambahkan akun pengguna secara manual sebelum login, contohnya:

```sql
USE KP2;

INSERT INTO TB_User (Username, Password, Role)
VALUES ('admin', 'admin123', 'Admin');

INSERT INTO TB_User (Username, Password, Role)
VALUES ('kasir', 'kasir123', 'Cashier');
```

> Password pada aplikasi saat ini disimpan langsung sebagai teks biasa. Untuk penggunaan produksi, gunakan hashing password dan mekanisme autentikasi yang lebih aman.

### 3. Sesuaikan koneksi database

Beberapa form aplikasi menggunakan koneksi default berikut:

```text
Data Source=.\SQLEXPRESS;Initial Catalog=KP2;Integrated Security=True
```

Jika nama instance SQL Server berbeda, ubah `Data Source` pada file berikut:

- `KP2/LoginAdmin.vb`
- `KP2/LoginCashier.vb`
- `KP2/Cashier.vb`
- `KP2/CRUD_Product.vb`
- `KP2/Supplier.vb`
- `KP2/GoodsOut.vb`
- `KP2/GoodsInHistory.vb`
- Form lain yang menggunakan `SqlConnection`

Periksa juga connection string di `KP2/App.config`. Pastikan `Data Source` dan `Initial Catalog` menunjuk ke instance serta database yang sama. Script database membuat database bernama `KP2`, sedangkan connection string di `App.config` pada versi proyek ini menggunakan `DB_KP2`; samakan nilainya menjadi `KP2` jika menggunakan konfigurasi tersebut.

### 4. Buka dan jalankan proyek

1. Buka `KP2.sln` menggunakan Visual Studio 2022.
2. Restore NuGet packages jika Visual Studio memintanya.
3. Jika paket belum tersedia, buka **Tools > NuGet Package Manager > Manage NuGet Packages for Solution**, lalu restore atau install paket dari `KP2/packages.config`.
4. Set proyek `KP2` sebagai **Startup Project**.
5. Pilih konfigurasi `Debug` atau `Release`.
6. Jalankan dengan `F5` atau **Debug > Start Without Debugging**.

## Cara Menggunakan

1. Pada halaman awal, pilih login **Admin** atau **Cashier**.
2. Masukkan akun yang sudah tersedia di tabel `TB_User`.
3. Untuk admin:
   - Tambahkan data supplier atau barang masuk.
   - Kelola produk dan harga.
   - Periksa stok, barang keluar, dan riwayat barang masuk.
4. Untuk kasir:
   - Cari produk dan pilih jumlahnya.
   - Tambahkan produk ke keranjang.
   - Pilih metode pembayaran.
   - Selesaikan transaksi dan cetak struk.
5. Gunakan tombol logout untuk kembali ke halaman login.

## Struktur Proyek

```text
.
├── DB_Script.txt          # Script pembuatan database SQL Server
├── KP2.sln                # Solution Visual Studio
├── README.md
└── KP2/
    ├── *.vb               # Form dan logika aplikasi
    ├── *.Designer.vb      # Kode hasil designer Windows Forms
    ├── *.resx             # Resource form
    ├── App.config         # Konfigurasi aplikasi dan koneksi
    ├── packages.config     # Daftar paket NuGet
    └── DB_KP2DataSet*.xsd # Definisi Typed DataSet
```

## Catatan Penggunaan

- Aplikasi ditujukan untuk lingkungan desktop Windows.
- SQL Server harus aktif sebelum aplikasi dijalankan.
- Pastikan stok mencukupi sebelum menyimpan transaksi atau barang keluar.
- Jangan menghapus produk yang masih direferensikan oleh transaksi atau riwayat barang keluar.
- Folder `bin`, `obj`, dan file konfigurasi lokal tidak perlu di-commit ke repositori.

## Lisensi

Belum ada lisensi open source yang ditentukan untuk proyek ini.
