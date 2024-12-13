# MACHINE LEARNING API - Tani Care

API untuk aplikasi prediksi berbasis machine learning yang digunakan untuk memproses gambar dan memberikan hasil prediksi terkait dengan data pertanian.

## Langkah-langkah Menggunakan API

### 1. Clone Repository

Pertama-tama, clone repository ini dengan menggunakan perintah git berikut:

```bash
git clone https://github.com/TaniCare/cloud-computing.git tani-care
```

### 2. Masuk ke Folder API

Setelah repository berhasil di-clone, masuk ke folder API dengan perintah berikut:

```bash
cd tani-care/api-ml-tanicare
```

### 3. Install Dependencies

Sebelum menjalankan API, pastikan kamu telah menginstall semua dependencies yang diperlukan. Kamu bisa menggunakan `pip` untuk menginstall dependensi yang ada di file `requirements.txt`:

```bash
pip install -r requirements.txt
```

### 4. Menjalankan API

Setelah dependencies terinstall, kamu bisa menjalankan API dengan perintah berikut:

```bash
python main.py
```

API akan berjalan pada server lokal (biasanya di `http://127.0.0.1:5000/`).

## Endpoints API

### 1. **/predict** (POST)

#### Deskripsi
Endpoint ini digunakan untuk mengirimkan gambar (image) yang akan diproses oleh model machine learning untuk mendapatkan prediksi. Biasanya digunakan untuk memprediksi kondisi atau jenis tanaman berdasarkan gambar.

#### Cara Menggunakan:
- Method: **POST**
- Endpoint: **/predict**
- Data yang Dikirim: File gambar dalam format `.jpg`, `.jpeg`, atau `.png`.

#### Request Body:
Gambar yang akan diprediksi harus dikirim dalam bentuk file, menggunakan form-data dengan key `file`. Contoh menggunakan curl:

```bash
curl -X POST -F "file=@path_to_image.jpg" http://127.0.0.1:5000/predict
```

#### Hasil yang Diharapkan:

API akan mengembalikan response dalam format JSON yang berisi prediksi model terhadap gambar yang diberikan. Response ini bisa berisi informasi seperti kelas atau label yang diprediksi serta tingkat kepercayaan (confidence score).

Contoh Response:
```json
{
  "prediction": "Tanaman Sehat",
  "confidence": 0.95
}
```

#### Penjelasan:
- **prediction**: Hasil prediksi dari model terkait gambar yang dikirim.
- **confidence**: Nilai kepercayaan atau probabilitas yang menunjukkan seberapa yakin model dengan hasil prediksinya.

## Import yang Diperlukan

Sebelum menjalankan aplikasi atau menggunakan API, pastikan untuk mengimpor library berikut pada file Python:

```python
from flask import Flask, request, jsonify
from PIL import Image
import io
import firebase_admin
from firebase_admin import firestore
import os
import json
import numpy as np
from tensorflow import keras
```

## Troubleshooting

- Jika API tidak berjalan, pastikan kamu sudah menginstall semua dependensi.
- Jika terjadi error terkait model, pastikan model sudah dilatih dan siap digunakan (model `.h5` atau file terkait lainnya sudah ada di folder yang tepat).


