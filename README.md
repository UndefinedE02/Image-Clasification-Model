# Image-Clasification-Model-TensorFlowLite
Proyek ini bertujuan untuk membangun dan melatih model Convolutional Neural Network (CNN) yang robust untuk mengklasifikasikan 3 hewan yaitu: 
1. kucing
2. anjing
3. harimau
   
Dengan memanfaatkan kekuatan deep learning, proyek ini berupaya menyediakan alat bantu untuk mengidentifikasi foto/gambar hewan yang samar/kurang jelas.

pada repositori ini kita akan menggunakan tensorflowlite untuk melakukan inferensi pada model yang sudah dilatih
silahkan unduh sendiri dataset yang diperlukan pada link yang sudah di sediakan atau dapat gunakan drive untuk melakukan modeling secara mandiri

##  Struktur Proyek
```
├── dataset/                # Folder dataset (train dan test)
│   ├── train/              # Data training
│   ├── test/               # Data testing
│
├── Src/                    # Folder untuk menyimpan model dan modeling
|  ├── best_model.h5        # Model dengan kualitas terbaik selama pelatihan berlangsung              
|  ├── model.tflite         # Model dalam format TensorFlow Lite
|  ├── Modeling.ipynb       # Notebook utama untuk analisis & training
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
4. **Dataset:**
   ```Dataset yang digunakan dalam proyek ini adalah gambar hewan yang diunduh dari Kaggle. Dataset ini berisi gambar-gambar yang dikategorikan sebagai Cats,                      Pneumonia Dogs, dan Tigers.
   
   Sumber Dataset: [https://www.kaggle.com/datasets/nicopalv/dataset-klasifikasi-gambar-hewan]
   Struktur Awal Dataset:
   Training Set: 12.000 gambar 3 folder
   Test Set: 3.000 gambar 3 folder
   ```
##  Melatih Model
Jalankan perintah berikut untuk melatih model:
```sh
python Modeling.ipynb
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

## Hasil
Model dilatih selama beberapa epoch dan dievaluasi berdasarkan akurasi dan loss pada data latih, validasi, dan uji.

Akurasi Pelatihan (Training Accuracy): 89.33%
Loss Pelatihan (Training Loss): 0.2531
Akurasi Uji (Test Accuracy): 89.55%
Loss Uji (Test Loss): 0.2393

##  Teknologi yang Digunakan
- **Python 3.10+**
- **TensorFlow & Keras** (Model training & deployment)
- **TensorFlow Lite** (Inference di perangkat mobile)
- **TensorFlow.js** (Inference di web)
- **OpenCV & PIL** (Preprocessing gambar)
- **Matplotlib** (Visualisasi hasil)

### Arsitektur Model
Model ini dibangun menggunakan Convolutional Neural Network (CNN) dengan pendekatan sekuensial. Arsitektur ini dirancang untuk secara otomatis mempelajari fitur-fitur penting untuk klasifikasi yang akurat.

Berikut adalah komponen utama model:
- Lapisan Konvolusi (Conv2D): Bertugas untuk mengekstrak fitur-fitur spasial dari gambar, seperti tepi, tekstur, dan pola yang lebih kompleks. Digabungkan dengan fungsi
- aktivasi ReLU untuk menangani non-linieritas.
- Lapisan Pooling (MaxPooling2D): Digunakan setelah lapisan konvolusi untuk mengurangi dimensi spasial (downsampling) dari peta fitur, mengurangi kompleksitas komputasi, dan membuat model lebih tangguh terhadap variasi posisi objek.
- Lapisan Perataan (Flatten): Mengubah output multidimensional dari lapisan konvolusi dan pooling menjadi satu vektor satu dimensi, mempersiapkannya untuk lapisan fully connected.
- Lapisan Dense (Dense): Lapisan fully connected yang menerima fitur yang telah diratakan. Lapisan terakhir menggunakan fungsi aktivasi Softmax untuk menghasilkan probabilitas klasifikasi untuk setiap kelas (KUcing, Anjing, dan Harimau).
- Model dikompilasi menggunakan optimizer Adam yang efisien dan fungsi loss categorical_crossentropy, yang merupakan pilihan umum dan efektif untuk tugas klasifikasi multi-kelas.


##  Lisensi
Proyek ini menggunakan lisensi **MIT**.

