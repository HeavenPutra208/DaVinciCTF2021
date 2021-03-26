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

Username: admin
Password: ' or 1 -- -

Dan berhasil. Kemudian saya melakuakn inspect elemen web dan memperoleh flag yang dimaksud.

Flag: dvCTF{!th4t_w4s_34sy!}

## Forensics

## Reverse

## Scripting

## Crypto

## Stega

## OSINT
