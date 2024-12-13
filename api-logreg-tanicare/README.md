# API REGIS-LOGIN - Tani Care

API ini menyediakan endpoint untuk registrasi, login, dan pengelolaan profil pengguna. Anda bisa menggunakan API ini untuk mengelola sesi autentikasi pengguna dengan cara yang sederhana.

## Langkah-langkah Penggunaan API

1. **Clone Repository**
   Clone repository ini dengan perintah berikut di terminal atau command prompt:
   ```bash
   git clone https://github.com/TaniCare/cloud-computing.git tani-care
   ```

2. **Masuk ke Direktori API**
   Setelah berhasil meng-clone repository, masuk ke folder `api-logreg` dengan perintah:
   ```bash
   cd tani-care/api-logreg-tanicare
   ```

3. **Buat File `.env`**
   Buat file `.env` pada folder yang sama dengan file `index.js` dan isikan variabel lingkungan seperti yang ada di contoh file `.env.example`. Variabel yang perlu diisi bisa berupa konfigurasi untuk koneksi database, secret key untuk JWT, dll.

4. **Inisialisasi Project Node.js**
   Jalankan perintah berikut untuk membuat file `package.json`:
   ```bash
   npm init --yes
   ```

5. **Install Dependencies**
   Install dependensi yang dibutuhkan oleh project menggunakan npm:
   ```bash
   npm install
   ```

6. **Jalankan API**
   Jalankan API menggunakan perintah berikut:
   ```bash
   node index.js
   ```

7. **API Berjalan di Port 3000**
   Setelah menjalankan perintah tersebut, API akan berjalan pada `http://localhost:3000`.

---

## Endpoint API

API ini memiliki beberapa endpoint yang dapat digunakan untuk registrasi, login, mengelola profil, dan melakukan refresh token.

### 1. **/signup** (POST)
Endpoint untuk melakukan registrasi pengguna baru.

- **Request Body**:
  - `name` (string): Nama pengguna yang ingin digunakan.
  - `email` (string): Alamat email pengguna.
  - `password` (string): Kata sandi pengguna.

- **Response**:
  - **Status**: `201 Created`
  - **Body**:
    ```json
    {
    "status": 201,
    "message": "You have been successfully registered.",
    "user_id": 9
    }
    ```

  - **Error (400 Bad Request)**: Jika data yang diberikan tidak lengkap atau tidak valid.
    ```json
    {
    "statusCode": 400,
    "error": "Bad Request",
    "message": "Invalid request payload input"
    }
    ```

### 2. **/login** (POST)
Endpoint untuk login pengguna dan mendapatkan token autentikasi.

- **Request Body**:
  - `email` (string): Alamat email pengguna.
  - `password` (string): Kata sandi pengguna.

- **Response**:
  - **Status**: `200 OK`
  - **Body**:
    ```json
    {
      "status": "201",
      "token": "JWT_Token_Here",
      "refreshToken": "JWT_Refresh_Token_Here"
    }
    ```

  - **Error (401 Unauthorized)**: Jika kredensial salah.
    ```json
    {
     "message": "Invalid email or password"
    }
    ```

### 3. **/profile** (GET)
Endpoint untuk mendapatkan data profil pengguna yang sedang login. Pengguna harus mengirimkan token autentikasi pada header.

- **Request**:
  - Header:
    ```json
    {
      "Authorization": "Bearer JWT_Token_Here"
    }
    ```

- **Response**:
  - **Status**: `200 OK`
  - **Body**:
    ```json
    {
    "status": 200,
    "user": {
        "id": 1,
        "name": "YOUR NAME",
        "email": "YOUR EMAIL"
      }
    }
    ```

  - **Error (401 Unauthorized)**: Jika token tidak valid atau kadaluarsa.
    ```json
    {
      "message": "Invalid refresh token"
    }
    ```

### 4. **/refresh** (POST)
Endpoint untuk memperbarui token autentikasi (refresh token). Pengguna harus mengirimkan refresh token yang valid.

- **Request Body**:
  - `refreshToken` (string): Refresh token yang valid.

- **Response**:
  - **Status**: `200 OK`
  - **Body**:
    ```json
    {
    "status": 200,
    "access_token":JWT_Token_Here,
    "refresh_token": JWT_Token_Here
    }
    ```

  - **Error (400 Bad Request)**: Jika refresh token tidak valid atau sudah kadaluarsa.
    ```json
    {
      "message": "Invalid refresh token"
    }
    ```

---

## Catatan
- Pastikan untuk selalu menjaga kerahasiaan `JWT_Token_Here` dan `JWT_Refresh_Token_Here` karena itu digunakan untuk autentikasi pengguna.
- Anda bisa menggunakan Postman atau alat lainnya untuk melakukan pengujian terhadap API ini.
