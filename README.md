---

# 📘 **README – Praktikum 10: PHP OOP**

---

**Mata Kuliah:** Pemrograman Web1

**Dosen Pengampu:** Agung Nugroho, S.Kom., M.Kom.

**Nama:** Zaenal Maulana Rizki

**NIM:** 312410332

**Kelas:** TI.2A.A.4

---

## **🔍 Tujuan Praktikum**

1. Mahasiswa memahami konsep dasar **Object Oriented Programming (OOP)** dalam PHP.
2. Mahasiswa memahami struktur dasar **Class dan Object**.
3. Mahasiswa mampu membuat program **OOP sederhana** menggunakan PHP.
4. Mahasiswa dapat menerapkan **class library** dan **modularisasi file**.

---

# 📁 **Struktur Folder**

```
lab10_php_oop/
│
├── mobil.php
├── form.php
├── form_input.php
├── config.php
├── database.php
```

---

# 🧪 **Langkah-langkah Praktikum**

---

## **1. Membuat Folder Project**

Buat folder baru pada direktori web server:

```
htdocs/lab10_php_web
```

---

## **2. Program Class & Object — mobil.php**

Pada file **mobil.php** dibuat class `Mobil` yang berisi atribut dan method sederhana.

### **Kode:**

```php
<?php 
/**
* Program sederhana pendefinisian class dan pemanggilan class.
**/

class Mobil 
{ 
   private $warna; 
   private $merk; 
   private $harga; 

   public function __construct() 
   { 
       $this->warna = "Biru"; 
       $this->merk = "BMW"; 
       $this->harga = "10000000"; 
   } 

   public function gantiWarna ($warnaBaru) 
   { 
       $this->warna = $warnaBaru; 
   } 

   public function tampilWarna () 
   { 
       echo "Warna mobilnya : " . $this->warna; 
   } 
} 

// Membuat objek
$a = new Mobil(); 
$b = new Mobil(); 

echo "<b>Mobil pertama</b><br>"; 
$a->tampilWarna(); 
echo "<br>Mobil pertama ganti warna<br>"; 
$a->gantiWarna("Merah"); 
$a->tampilWarna(); 

echo "<br><b>Mobil kedua</b><br>"; 
$b->gantiWarna("Hijau"); 
$b->tampilWarna(); 

?>
```

Program ini menampilkan warna mobil dan cara mengganti nilai atribut melalui method.

---

## **3. Membuat Class Library — form.php**

File ini berisi class untuk membuat form input secara dinamis.

### **Kode:**

```php
<?php 
class Form 
{ 
   private $fields = array(); 
   private $action; 
   private $submit = "Submit Form"; 
   private $jumField = 0; 

   public function __construct($action, $submit) 
   { 
       $this->action = $action; 
       $this->submit = $submit; 
   } 

   public function displayForm() 
   { 
       echo "<form action='".$this->action."' method='POST'>"; 
       echo '<table width="100%" border="0">'; 
       for ($j=0; $j<count($this->fields); $j++) { 
           echo "<tr><td align='right'>".$this->fields[$j]['label']."</td>"; 
           echo "<td><input type='text' name='".$this->fields[$j]['name']."'></td></tr>"; 
       } 
       echo "<tr><td colspan='2'>"; 
       echo "<input type='submit' value='".$this->submit."'></td></tr>"; 
       echo "</table>"; 
   } 

   public function addField($name, $label) 
   { 
       $this->fields [$this->jumField]['name'] = $name; 
       $this->fields [$this->jumField]['label'] = $label; 
       $this->jumField++; 
   } 
} 
?>
```

Class ini akan digunakan di file lain untuk menampilkan form otomatis.

---

## **4. Menggunakan Class Form — form_input.php**

File ini memanggil class Form dan **ditambahkan fungsi penyimpanan ke database**.

### **Kode:**

```php
<?php 

include "form.php";
include "database.php";

echo "<html><head><title>Mahasiswa</title></head><body>";

$form = new Form("form_input.php", "Simpan Data");
$form->addField("txtnim", "Nim");
$form->addField("txtnama", "Nama");
$form->addField("txtalamat", "Alamat");

echo "<h3>Silahkan isi form berikut ini :</h3>";
$form->displayForm();

if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $db = new Database();

    $simpan = $db->insert("mahasiswa", [
        "nim"    => $_POST['txtnim'],
        "nama"   => $_POST['txtnama'],
        "alamat" => $_POST['txtalamat']
    ]);

    if ($simpan) {
        echo "<p><b>Data berhasil disimpan!</b></p>";
    } else {
        echo "<p><b>Gagal menyimpan data!</b></p>";
    }
}

echo "</body></html>";

?>
```

---

## **5. Konfigurasi Database — config.php**

```php
<?php
$config['host'] = "localhost";
$config['username'] = "root";
config['password'] = "";
$config['db_name'] = "lab10web";
?>
```

---

## **6. Class Database — database.php**

Class ini digunakan untuk koneksi, insert, update, delete, dan get data.

(Sudah ditulis lengkap sesuai modul)

---

## **7. Membuat Database MySQL**

Buka phpMyAdmin → SQL → jalankan:

```sql
CREATE DATABASE lab10web;
USE lab10web;

CREATE TABLE mahasiswa (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nim VARCHAR(20),
    nama VARCHAR(100),
    alamat TEXT
);
```

---

# 🎯 **Hasil Praktikum**

* Program OOP (class & object) berjalan.
* Class library form berhasil digunakan.
* Modularisasi file berjalan baik.
* Form input berhasil menyimpan data ke database MySQL.

---

# 📎 **Screenshots**

### Hasil tampilan form_input untuk mengisi Nim< Nama, Alamat di browser nya:

---

<img width="861" height="242" alt="image" src="https://github.com/user-attachments/assets/88f0f976-2be9-45c5-803e-8b4d9cd0e87d" />


---

### Hasil tampilan form tersimpan di database PhpMyAdmin:

---

<img width="702" height="260" alt="image" src="https://github.com/user-attachments/assets/cf00bdc2-9cdc-4ab6-9945-266c65895cdf" />

---
