**#Step to Automation API with POSTMAN**

**1. 🔹 POST /user – Create User**
📌 Tujuan:
Membuat user baru di sistem dengan data lengkap seperti username, nama, email, dan password.

**📄 Isi request:**
Method: POST

**1. 🔹 POST /user – Create User**
📌 Tujuan:
Membuat user baru di sistem dengan data lengkap seperti username, nama, email, dan password.

**📄 Isi request:**
Method: POST

**Endpoint: {{baseURL}}/user**
(akan terbaca sebagai https://petstore.swagger.io/v2/user)

**Header:**

Content-Type: application/json

**Body:**

{
  "id": 1001,
  "username": "{{username}}",
  "firstName": "John",
  "lastName": "Doe",
  "email": "john.doe@example.com",
  "password": "123456",
  "phone": "123-456-7890",
  "userStatus": 1
}
**{{username}} **akan digenerate otomatis dengan random value lewat script prerequest.

**✅ Test Script:
Mengecek status code harus 200.**

**2. 🔹 GET /user/{username} – Get User by Username**
📌 Tujuan:
Mengambil data user berdasarkan username yang sebelumnya telah dibuat.

**📄 Isi request:
Method: GET**

**Endpoint: {{baseURL}}/user/{{username}}**

**✅ Test Script:
Memastikan status code adalah 200.

Memastikan bahwa firstName yang dikembalikan adalah "John" (sesuai data dari POST).**

**3. 🔹 PUT /user/{username} – Update User**
📌 Tujuan:
Memperbarui data user berdasarkan username.

**📄 Isi request:
Method: PUT**

**Endpoint: {{baseURL}}/user/{{username}}**

Header:

Content-Type: application/json

Body:

{
  "id": 1001,
  "username": "{{username}}",
  "firstName": "Jane",
  "lastName": "Smith",
  "email": "jane.smith@example.com",
  "password": "abcdef",
  "phone": "987-654-3210",
  "userStatus": 1
**}
✅ Test Script:
Memastikan status code adalah 200.**

**✳️ Extra: Prerequest Script
Sebelum setiap request dijalankan, Postman akan menjalankan ini:**

let randomUser = "user_" + Math.random().toString(36).substring(2, 8);
pm.environment.set("username", randomUser);
➡️ Ini akan membuat username unik dan menyimpannya ke environment variable username, sehingga test dapat diulang-ulang tanpa konflik.
(akan terbaca sebagai https://petstore.swagger.io/v2/user)

**🔧 Cara menyimpan script ini di Postman:
Buka Postman**

Klik tab Collections → pilih collection Petstore User API Test

Klik ikon ⚙️ atau nama collection untuk membuka Collection Settings

Pilih tab Pre-request Scripts

Masukkan script ini ke kolom editor:

let randomUser = "user_" + Math.random().toString(36).substring(2, 8);
pm.environment.set("username", randomUser);
Klik Save

**Namun jika script diatas di simpan di collection maka Method GET akan error karena username tergenerate random terus dan tidak ditemuan, solusi :
simpan script diatas hanya di Method POST jadi tidak mengganggu untuk Method GET nya.**

**🔍 Apa fungsinya?
Script ini akan dijalankan sebelum setiap request dalam collection.
Jadi:**

- Ia akan menghasilkan username unik seperti user_a1b2c3
- Menyimpannya ke environment variable username
- Semua request yang pakai {{username}} otomatis ikut berubah
- Ditambahkan delay sekitar 30000 di pre-request Method GET
  
  Cara Run ke tiga Method :

- Click Run Collection
- Click Run "Nama Collection"
- Akan muncul hasil test
