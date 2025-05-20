# Klasifikasi Gambar Hewan dengan TensorFlow

##  Deskripsi Proyek
Proyek ini bertujuan untuk membangun model klasifikasi gambar hewan menggunakan **TensorFlow** dengan arsitektur **Sequential**. Model dilatih menggunakan **dataset gambar hewan** yang terdiri dari beberapa kelas dan dikonversi ke berbagai format untuk inference, termasuk **TF-Lite dan TensorFlow.js**.

##  Struktur Proyek
```
├── dataset/                # Folder dataset (train dan test)
│   ├── train/              # Data training
│   ├── test/               # Data testing
│
├── best_model.h5           # Model terbaik dalam format H5
├── saved_model/            # Model dalam format TensorFlow SavedModel
├── model.tflite            # Model dalam format TensorFlow Lite
├── tfjs_model/             # Model dalam format TensorFlow.js
│
├── Submission_Akhir.ipynb  # Notebook utama untuk analisis & training
│
├── requirements.txt        # Daftar dependensi
├── README.md               # Dokumentasi proyek ini
```

##  Instalasi dan Persiapan
1. **Clone repository** ini ke komputer Anda:
   ```sh
   git clone https://github.com/username/repo-name.git
   cd repo-name
   ```
2. **Buat environment virtual (opsional):**
   ```sh
   python -m venv venv
   source venv/bin/activate  # Untuk Linux/macOS
   venv\Scripts\activate     # Untuk Windows
   ```
3. **Install dependensi:**
   ```sh
   pip install -r requirements.txt
   ```

##  Melatih Model
Jalankan perintah berikut untuk melatih model:
```sh
python Submission_Akhir.ipynb
```
Setelah selesai, model akan disimpan sebagai **best_model.h5**.

##  Konversi Model
Setelah training selesai, model dapat dikonversi ke berbagai format:

**TF-Lite**  
```python
import tensorflow as tf

# Load model
model = tf.keras.models.load_model("best_model.h5")

# Konversi ke format TF-Lite
converter = tf.lite.TFLiteConverter.from_keras_model(model)
tflite_model = converter.convert()

# Simpan model TF-Lite
with open("model.tflite", "wb") as f:
    f.write(tflite_model)

print("Model berhasil dikonversi ke TF-Lite!")
```

**TensorFlow.js**  
```python
import tensorflowjs as tfjs

# Load model
model = tf.keras.models.load_model("best_model.h5")

# Konversi ke TFJS
tfjs.converters.save_keras_model(model, "tfjs_model")

print("Model berhasil dikonversi ke TensorFlow.js!")
```
 **Pastikan `tensorflowjs` sudah diinstal** dengan `pip install tensorflowjs`.

##  Inferensi Menggunakan TF-Lite
Gunakan model TF-Lite untuk melakukan prediksi:
```sh
python scripts/inference_tflite.py --image path/to/image.jpg
```

##  Inferensi Menggunakan TFJS
Untuk menggunakan model di web, jalankan:
```sh
python -m http.server
```
Lalu buka browser dan arahkan ke `http://localhost:8000/tfjs_model/`

##  Teknologi yang Digunakan
- **Python 3.10+**
- **TensorFlow & Keras** (Model training & deployment)
- **TensorFlow Lite** (Inference di perangkat mobile)
- **TensorFlow.js** (Inference di web)
- **OpenCV & PIL** (Preprocessing gambar)
- **Matplotlib** (Visualisasi hasil)

##  Lisensi
Proyek ini menggunakan lisensi **MIT**.

