# Image-Clasification-Model-TensorFlowLite
image clasification adalah salah satu cabang computer vision yang dimana bertujuan untuk meng-klasifikasikan gambar sesuai dengan label yang ada pada gambar tersebut, di repositori ini saya membuat model klasifikasi untuk 3 hewan yaitu: 
- 1.kucing
- 2.anjing
- 3.harimau

pada repositori ini kita akan menggunakan tensorflowlite untuk melakukan inferensi pada model yang sudah dilatih
silahkan unduh sendiri dataset yang diperlukan pada link yang sudah di sediakan atau dapat gunakan drive untuk melakukan modeling secara mandiri

##  Struktur Proyek
```
├── dataset/                # Folder dataset (train dan test)
│   ├── train/              # Data training
│   ├── test/               # Data testing
│
├── Src/                     # Folder untuk menyimpan model dan modeling
|  ├── model.tflite            # Model dalam format TensorFlow Lite
|  ├── Modeling.ipynb  # Notebook utama untuk analisis & training
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

##  Inferensi Menggunakan TF-Lite
Gunakan model TF-Lite untuk melakukan prediksi:
```sh
python scripts/inference_tflite.py --image path/to/image.jpg
```

##  Teknologi yang Digunakan
- **Python 3.10+**
- **TensorFlow & Keras** (Model training & deployment)
- **TensorFlow Lite** (Inference di perangkat mobile)
- **TensorFlow.js** (Inference di web)
- **OpenCV & PIL** (Preprocessing gambar)
- **Matplotlib** (Visualisasi hasil)

##  Lisensi
Proyek ini menggunakan lisensi **MIT**.

