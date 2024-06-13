

# Praktikum3

```
Nama    : Taufik Hidayat
NIM     : 312310576
Kelas   : TI.23.A6
Matkul  : Basis Data
Dosen   : Agung Nugroho, S.Kom., M.Kom.
```

# **SQL Constraint**

- SQL Constraint digunakan untuk menentukan aturan untuk data dalam tabel.
- Constraint digunakan untuk membatasi jenis data yang bisa masuk ke tabel. Ini memastikan keakuratan dan keandalan data dalam tabel.
- Constraint dapat berupa level kolom atau level tabel.
- Constraint level kolom berlaku untuk kolom, dan batasan level tabel berlaku untuk seluruh tabel.

## **Tugas Praktikum**

- Implementasikan penggunaan **_CONSTRAINT FOREIGN KEY_** pada semua tabel yang berelasi.
- yang perlu diperhatikan:
  - tipe data pada field yang berelasi harus sama termasuk juga ukuran datanya.
  - misal: pada tabel dosen, kd_ds VARCHAR(10) maka tabel yang merujuk yaitu tabel mahasiswa, kd_ds juga harus bertipe VARCHAR(10).

1. Lakukan penambahan data pada tabel mahasiswa dengan mengisi kd_ds yang belum ada pada data dosen.
2. Hapus satu record data pada tabel dosen yang telah dirujuk pada tabel mahasiswa.
3. Ubah mode menjadi ON UPDATE CASCADE ON DELETE RESTRICT
4. Lakukan perubahan data pada tabel dosen (kd_ds)
5. Lakukan penghapusan data pada tabel dosen
6. Ubah mode menjadi ON UPDATE CASCADE ON DELETE SET NULL
7. Lakukan penghapusan data pada tabel dosen



### Syntax SQL
## Implementasi CONSTRAINT FOREIGN KEY
Berikut ini adalah langkah-langkah dan penerapan dalam pengimplementasian CONSTRAINT FOREIGN KEY pada Tabel mahasiswa dalam kolom kd_ds

* Pastikan kamu sudah mempunyai sebuah database yang berisi Tabel mahasiswa dan Tabel dosen, dan juga didalam tabel tersebut sudah berisi sebuah data. Berikut adalah contohnya:

![image](ss/ss6.png)

- Membuat foreign key

  - Dalam ALTER TABLE:
    ```SQL
    ALTER TABLE mahasiswa
    ADD CONSTRAINT fk_dosenwali FOREIGN KEY (kd_ds)
    REFERENCES dosen(kd_ds)
    ```

![image](ss/ss4.png)

- Dalam CREATE TABLE:
    ```sql
    CREATE TABLE mahasiswa(
    nim VARCHAR(10) NOT NULL,
    nama VARCHAR(100) NOT NULL,
    kd_ds VARCHAR(10),
    PRIMARY KEY(nim),
    CONSTRAINT fk_DosenWali FOREIGN KEY (kd_ds)
    REFERENCES dosen(kd_ds)
    );
    ```

  ```

  ```
![image](ss/ss3.png)


1. Lakukan penambahan data pada tabel mahasiswa dengan mengisi kd_ds yang belum ada pada data dosen.

dengan menggunakan kode berikut :


```sql
INSERT INTO dosen (kd_ds, nama) VALUES
('DS001', 'Abdillah'),
('DS002', 'Bima'),
('DS003', 'Catur'),
('DS004', 'Deni'),
('DS005', 'Endang');
```

![image](ss/ss2.png)

berikut outputnya : 


![image](ss/ss18.png)


2. Hapus satu record data pada tabel dosen yang telah dirujuk pada tabel mahasiswa.
Menghapus data
```sql
  DELETE FROM dosen WHERE kd_ds = 'DS001';
```

output :


![image](ss/ss7.png)

output eror.
Jika Anda ingin menghapus record dari tabel "dosen" yang memiliki referensi dari tabel "mahasiswa", Anda dapat menggunakan opsi ON DELETE CASCADE pada konstrain kunci asing untuk melakukan penghapusan secara otomatis dari tabel "mahasiswa" saat record dihapus dari tabel "dosen".

Berikut adalah perbaikan yang perlu dilakukan pada konstrain kunci asing fk_dosenwali di tabel "mahasiswa":

```sql
ALTER TABLE mahasiswa DROP  
    FOREIGN KEY fk_dosenwali;
```
    


``` sql
ALTER TABLE mahasiswa
ADD CONSTRAINT fk_dosenwali
FOREIGN KEY (kd_ds)
REFERENCES dosen (kd_ds)
ON DELETE CASCADE;
```


Dengan perubahan di atas, ketika Anda menghapus record dari tabel "dosen" yang memiliki referensi di tabel "mahasiswa", record terkait dalam tabel "mahasiswa" juga akan secara otomatis dihapus.


![image](ss/ss20.png)


Setelah menjalankan perintah di atas, Anda dapat kembali mencoba menghapus record dengan menggunakan perintah berikut:

```sql
DELETE FROM dosen WHERE kd_ds = 'DS001';
```


![image](ss/ss8.png)


output :


![image](ss/ss9.png)


![image](ss/ss10.png)

3. Ubah mode menjadi ON UPDATE CASCADE ON DELETE RESTRICT
Untuk mengubah konstrain kunci asing menjadi ON UPDATE CASCADE dan ON DELETE RESTRICT, Anda perlu menghapus konstrain kunci asing yang ada dan menambahkan konstrain baru dengan opsi yang diinginkan. Berikut adalah langkah-langkahnya:

Hapus konstrain kunci asing yang ada pada tabel "mahasiswa":

```sql
ALTER TABLE mahasiswa
DROP FOREIGN KEY fk_dosenwali;
```

Tambahkan kembali konstrain kunci asing dengan opsi ON UPDATE CASCADE dan ON DELETE RESTRICT:

```sql
ALTER TABLE mahasiswa
ADD CONSTRAINT fk_dosenwali
FOREIGN KEY (kd_ds)
REFERENCES dosen (kd_ds)
ON UPDATE CASCADE
ON DELETE RESTRICT;
```

![image](ss/ss11.png)


4. Lakukan perubahan data pada tabel dosen (kd_ds)

Berikut adalah contoh perintah untuk melakukan perubahan data pada tabel "dosen" dengan kolom "kd_ds":

```sql
UPDATE dosen
SET kd_ds = 'DS006'
WHERE kd_ds = 'DS001';
```

Perintah di atas akan mengubah nilai kolom "kd_ds" dari "DS001" menjadi "DS006" pada tabel "dosen". Anda dapat menyesuaikan nilai yang ingin Anda ubah dan kondisi WHERE sesuai dengan kebutuhan Anda.

Pastikan untuk menjalankan perintah dengan hati-hati dan memastikan bahwa perubahan data yang Anda lakukan sesuai dengan kebutuhan dan kebijakan yang berlaku dalam basis data Anda.


output: 


![image](ss/ss12.png)

5. Lakukan penghapusan data pada tabel dosen

Untuk menghapus data dari tabel "dosen" dengan kondisi "kd_ds = 'DS003'", Anda dapat menggunakan perintah DELETE dengan sintaks yang benar. Berikut adalah contoh perintah yang dapat Anda gunakan:

```sql
DELETE FROM dosen
WHERE kd_ds = 'DS003';
```

output :


![image](ss/ss15.png)

output eror
Jika Anda ingin menghapus record dari tabel "dosen" yang memiliki referensi dari tabel "mahasiswa", Anda dapat menggunakan opsi ON DELETE SET NULL pada konstrain kunci asing untuk mengatur nilai yang mengacu pada record yang akan dihapus menjadi NULL. Berikut adalah perbaikan yang perlu dilakukan pada konstrain kunci asing fk_dosenwali di tabel "mahasiswa".


6. Ubah mode menjadi ON UPDATE CASCADE ON DELETE SET NULL

```sql
ALTER TABLE mahasiswa
DROP FOREIGN KEY fk_dosenwali;
```

```sql
ALTER TABLE mahasiswa
ADD CONSTRAINT fk_dosenwali
FOREIGN KEY (kd_ds)
REFERENCES dosen (kd_ds)
ON DELETE SET NULL;
```


![image](ss/ss16.png)


Dengan perubahan di atas, ketika Anda menghapus record dari tabel "dosen" yang memiliki referensi di tabel "mahasiswa", nilai kolom "kd_ds" dalam tabel "mahasiswa" yang mengacu pada record yang dihapus akan diatur menjadi NULL.

Setelah menjalankan perintah di atas, Anda dapat kembali mencoba menghapus record dengan menggunakan perintah berikut:

7. Lakukan penghapusan data pada tabel dosen

```sql
DELETE FROM dosen WHERE kd_ds = 'DS003';

```

![image](ss/ss17.png)


Perintah ini akan menghapus record dengan nilai "DS003" dari tabel "dosen", dan karena menggunakan opsi ON DELETE SET NULL, nilai kolom "kd_ds" dalam tabel "mahasiswa" yang mengacu pada record yang dihapus akan diatur menjadi NULL.


## Evaluasi dan Pertanyaan
* Tulis semua perintah-perintah SQL percobaan di atas beserta outputnya!

### Syntax SQL

- Membuat foreign key

  - Dalam ALTER TABLE:
    ```SQL
    ALTER TABLE mahasiswa
    ADD CONSTRAINT fk_dosenwali FOREIGN KEY (kd_ds)     REFERENCES dosen(kd_ds)
    ```
  - Dalam CREATE TABLE:
    ```sql
    CREATE TABLE mahasiswa(
    nim VARCHAR(10) NOT NULL,
    nama VARCHAR(100) NOT NULL,
    kd_ds VARCHAR(10),
    PRIMARY KEY(nim),
    CONSTRAINT fk_DosenWali FOREIGN KEY (kd_ds)
    REFERENCES dosen(kd_ds)
    );
    ```

  ```

  ```

- Mengubah data
  ```sql
  UPDATE mahasiswa
  SET kd_ds = 'DS011' WHERE nim = 112233445;
  ```
- Menampilkan CREATE TABLE
  ```sql
  SHOW CREATE TABLE  mahasiswa;
  ```
- Mode ON UPDATE CASCADE ON DELETE CASCADE
  ```sql
  ALTER TABLE mahasiswa
  DROP FOREIGN KEY fk_mahasiswa_dosen,
  ADD CONSTRAINT fk_dosenwali FOREIGN KEY (kd_ds) REFERENCES dosen(kd_ds) ON UPDATE CASCADE ON DELETE CASCADE;
  ```
- Menghapus data
  ```sql
  DELETE FROM dosen WHERE kd_ds = 'DS001';
  ```
- Mode ON UPDATE CASCADE ON DELETE NOT NULL
  ```sql
  ALTER TABLE <table>
  DROP FOREIGN KEY <nama_constraint_lama>,
  ADD CONSTRAINT <nama_constraint_baru> FOREIGN KEY (field) REFERENCES <table_references(filed_references)> ON UPDATE CASCADE ON DELETE NOT NULL;
  ```
- Mengubah data
  ```sql
  UPDATE dosen
  SET kd_ds = 'DS006' WHERE nama = 'Haha Hihi';
  ```
- Menghapus data
  ```sql
  DELETE FROM dosen WHERE nim = 'DS003';
    ```

* Apa bedanya penggunaan RESTRICT dan penggunaan CASCADE
- RESTRICT : ketika menggunakan opsi RESTRICT dalam keterkatian, aturan keterkaitan akan membatasi aksi yang dapat dilakukan pada data yang terkait. Jika ada aksi yang menyebabkan konflik atau melanggar aturan keterkaitan. RESTRICT akan mencegaah aksi tersebut dilakukan. Misalnya, jika ada keterkaitan antara Tabel A dan Tabel B, dan kita mencoba untuk menghapus baris dari Tabel A yang memiliki keterkaitan dengan Tabel B, RESTRICT akan mencegah penghapusan tersebut jika ada baris yang masih terkait dalam Tabel B. Dengan menggunakan RESTRICT, aksi yang melanggar keterkaitan akan ditolak.
- CASCADE : ketika menggunakan opsi CASCADE dalam keterkaitan, aturan keterkaitan akan menyebabkan aksi yang dilakukan pada satu tabel juga mempengaruhi tabel yang terkait. Jadi, jika ada aksi yang dilakukan pada tabel yang memiliki ketertakitan dengan tabel lain, CASCADE akan mengakibatkan aksi tersebut juga berdampak pada tabel yang terkait. Misalnya, jika ada keterkaitan antara Tabel A dan Tabel B, dan kita menghapus baris dari Tabel A, CASCADE akan menghapus semua baris yang terkait dengan Tabel B secara otomatis. Dengan menggunakan CASCADE, aksi yang dilakukkan pada satu tabel akan menyebabkan kaskade aksi pada tabel yang terkait.
* Berikan kesimpulan anda!

SQL Constraint digunakan untuk menentukan aturan untuk data dalam tabel.

Constraint digunakan untuk membatasi jenis data yang bisa masuk ke tabel. Ini memastikan keakuratan dan keandalan data dalam tabel.

Constraint dapat berupa level kolom atau level tabel.

Constraint level kolom berlaku untuk kolom, dan batasan level tabel berlaku untuk seluruh tabel.

RESTRICT : RESTRICT membatasi aksi yang melanggar keterkaitan antara tabel.
CASCADE : CASCADE mempengaruhi tabel yang terkait dengan aksi yang dilakukan pada tabel utama. Keitka memilih antara RESTRICT dan CASCADE, pertimbangkan tujuan dan kebutuhan skema basis data yang sedang Anda bangun. RESTRICT cocok jika Anda ingin menerapkan pembatasan yang ketat pada aksi yang melanggar keterkaitan, sementara CASCADE memungkinkan aksi pada satu tabel juga berdampak pada tabel terkait.

Buat laporan praktikum yang berisi, langkah-langkah praktikum beserta screenshot yang sudah dilakukan dalam bentuk dokumen

dokumen terlampir.
