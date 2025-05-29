# Klasifikasi Sel Darah Menggunakan DenseNet121 dan Fitur GLCM

## Ringkasan
Proyek ini mengimplementasikan model pembelajaran mendalam (deep learning) hybrid untuk mengklasifikasikan citra sel darah dari dataset ALLIDB. Model ini menggabungkan jaringan saraf konvolusional DenseNet121 yang telah dilatih sebelumnya dengan fitur tekstur Gray-Level Co-occurrence Matrix (GLCM) untuk meningkatkan akurasi klasifikasi.

## Dataset
Acute Lymphoblastic Leukemia Image Database (ALLIDB) yang digunakan dalam proyek ini berisi gambar mikroskopi sel darah yang dibagi menjadi dua kelas:
- Kelas 1: Sel darah normal
- Kelas 2: Sel dengan tanda-tanda potensial Acute Lymphoblastic Leukemia (ALL)

## Fitur
- **Arsitektur Model Hybrid**: Menggabungkan fitur CNN dengan analisis tekstur GLCM
- **Transfer Learning**: Memanfaatkan arsitektur DenseNet121 yang telah dilatih sebelumnya untuk ekstraksi fitur
- **Ekstraksi Fitur GLCM**: Menganalisis pola tekstur dalam gambar menggunakan ukuran statistik
- **Preprocessing Data**: Mencakup pengubahan ukuran gambar, normalisasi, dan ekstraksi fitur
- **Evaluasi Model**: Menyediakan laporan klasifikasi dan matriks kebingungan (confusion matrix) yang detail

## Struktur Proyek
```
├── main.ipynb             # Notebook Jupyter utama yang berisi semua kode
├── requirements.txt       # Paket Python yang diperlukan
├── ALLIDB/                # Folder dataset
│   ├── Kelas 1/           # Sel normal
│   └── Kelas 2/           # Sel ALL
└── Models/                # File model tersimpan
    └── densenet_glcm_model.h5
```

## Pendekatan Teknis

### 1. Pemahaman Data
- Memuat dan mengorganisir data gambar dari dataset ALLIDB
- Menganalisis distribusi kelas dan memvisualisasikan sampel gambar

### 2. Preprocessing & Ekstraksi Fitur GLCM
- Mengubah ukuran gambar menjadi 224x224 piksel
- Normalisasi nilai piksel
- Mengekstrak fitur tekstur GLCM (kontras, dissimilarity, homogenitas, energi, korelasi, ASM)

### 3. Arsitektur Model
- Model dasar: DenseNet121 yang telah dilatih pada ImageNet
- Input tambahan untuk fitur GLCM
- Lapisan penggabungan fitur untuk menggabungkan fitur CNN dan GLCM
- Lapisan Dense untuk klasifikasi

### 4. Pelatihan & Evaluasi
- Melatih selama 10 epoch dengan ukuran batch 16
- Pembagian data latih-uji 80/20 dengan stratifikasi
- Evaluasi menggunakan laporan klasifikasi dan matriks kebingungan

### 5. Prediksi
- Fungsi untuk memprediksi kelas gambar baru
- Preprocessing dan ekstraksi fitur untuk inferensi

## Persyaratan
- Python 8
- TensorFlow
- NumPy
- Matplotlib
- scikit-learn
- scikit-image
- dan dependensi lain yang tercantum dalam requirements.txt

## Penggunaan

### Instalasi Dengan Anaconda Navigator untuk CUDA
1. Pertama Pastikan Membuat ENV dengan Anacoda Model Python 8.
2. Instal tensorflow-gpu
3. Install cudnn
4. Instal ipykernel
5. Install semua dependensi yang ada di requirements.txt di vscode

### Instalasi
```bash
pip install -r requirements.txt
```

### Pelatihan
Jalankan notebook main.ipynb di lingkungan Jupyter untuk:
1. Memuat dan memproses dataset ALLIDB
2. Mengekstrak fitur GLCM
3. Membuat dan melatih model hybrid
4. Mengevaluasi kinerja model

### Inferensi
Gunakan fungsi `predict_new_image` untuk mengklasifikasikan gambar sel darah baru:
```python
new_image_path = './path/to/your/image.jpg'
predicted_class, prediction_scores = predict_new_image(
    new_image_path, model, image_size, distances, angles, le
)
print("Kelas yang diprediksi:", predicted_class)
```

## Kinerja Model
Model telah dilatih dan dievaluasi pada dataset ALLIDB. Lihat laporan klasifikasi dan output matriks kebingungan dalam notebook untuk metrik kinerja yang detail.

## Referensi
- DenseNet: https://arxiv.org/abs/1608.06993
- Fitur GLCM: Haralick, R.M., Shanmugam, K., Dinstein, I. (1973). "Textural Features for Image Classification"
- Dataset ALLIDB: https://homes.di.unimi.it/scotti/all/

