# DaVinviCTF 2021

## PWN

## Web


### Authentication

#### Deskripsi Soal
Can you find a way to authenticate as admin?

http://challs.dvc.tf:1337/
#### Penyelesaian
Jadi di sini saya terpikirkan untuk bagaimana saya bisa masuk dalam autentikasi tersebut sebagai admin, di mana tidak diketahui password, saya harus mencoba me-bypass beberapa metode autentikasi.
Serangan umum yang saya gunakan di sini adalah dengan metode sql injection. Saya mencoba dengan menggunakan:

```Username: admin```

```Password: ' or 1 -- -```

Dan berhasil. Kemudian saya melakukan inspect elemen web dan memperoleh flag yang dimaksud.

**Flag: dvCTF{!th4t_w4s_34sy!}**


### Members
Can you get more information about the members?

http://challs.dvc.tf:1337/members

#### Penyelesaian
Jadi untuk menyelesaikan challenge ini diharuskan menyelesaikan challenge Web: Authentication terlebih dahulu, yang kemudian akan diberikan izin untuk mengakses layanan web http://challs.dvc.tf:1337/members. 

Saat dilihat pada website nya, terdapat page berisi table yang mengandung informasi tentang anggota di sebelah kanan dan formulir yang memungkinkan untuk mencari anggota di sebelah kiri. Dengan menganalisis kode sumber halaman, saya melihat bahwa form tersebut menggunakan metode ```GET``` untuk mengirimkan parameter pencarian, sehingga semua teks yang ditulis akan dikodekan ke dalam url. Setelah server menerima data yang saya kirim, server tersebut akan mengembalikan informasi tentang anggota. Jadi sepertinya ada Database MySQL yang mendukung aplikasi tersebut, sehingga saya memasukkan beberapa kode berbahaya ke dalam text field yang ada:

```SQL
Leonard" OR 1=1; --
```
Secara khusus, ```tabel information_schema.tables``` berisi informasi tentang semua tabel yang terletak di db. Kemudian dimasukkan kode berikut:
```SQL
Leonard "UNION (SELECT TABLE_NAME, 2,3 FROM INFORMATION_SCHEMA.TABLES); -
```
Dan aplikasi akan mengembalikan semua nama tabel yang disimpan dalam database. Jika kita menggulir ke bawah dapat melihat dua tabel: anggota yaitu tabel yang berisi semua informasi anggota dan tabel lain bernama ```supa_secret_table```.
Tabel bernama ```information_schema.columns``` berisi semua informasi tentang kolom dari semua tabel yang disimpan. Jadi kita bisa mendapatkan nama field ```supa_secret_table``` dengan memasukkan kode:

```SQL
Leonard" UNION (SELECT COLUMN_NAME,2,3 FROM INFORMATION_SCHEMA.COLUMNS WHERE TABLE_NAME='supa_secret_table'); --
```

Aplikasi akan mengembalikan dua record dengan nama field: ```id``` dan ```flag```.

```SQL
Leonard" UNION (SELECT flag,2,3 FROM supa_secret_table); --
```

dan kemudian aplikasi akan mencetak flag nya.

**Flag: dvCTF{1_h0p3_u_d1dnt_us3_sqlm4p}**

## Forensics

## Reverse

## Scripting

## Crypto

## Stega

## OSINT
