# DataScie-Physionet

Data science project for the International Data Science Challenge 2026 focused on detecting Brugada Syndrome from ECG signals.

## Deteksi Brugada Syndrome dari Sinyal ECG

### Deskripsi Proyek

Proyek ini menganalisis sinyal ECG untuk mendeteksi kemungkinan **Brugada Syndrome** menggunakan machine learning. Proyek ini dibuat untuk mengikuti International Data Science Challenge 2026 dengan tema _Mathematics for Hope in Healthcare_.

### Latar Belakang

Brugada Syndrome adalah kelainan genetik pada jantung yang bisa menyebabkan gangguan irama jantung serius dan bahkan henti jantung mendadak. Pola tertentu pada sinyal ECG sering menjadi tanda kondisi ini. Dengan analisis data dan machine learning, pola tersebut bisa dipelajari oleh model sehingga deteksi awal menjadi lebih memungkinkan.

### Dataset

Dataset yang digunakan berasal dari PhysioNet:
https://physionet.org/lightwave/?db=brugada-huca/1.0.0

### Tools yang Digunakan

- Python
- Google Colab
- NumPy
- Pandas
- Scikit-learn

### Instalasi dan Setup

#### Prasyarat

- Python 3.8 atau lebih tinggi
- pip atau conda

#### Langkah Instalasi

1. **Clone repository**

   ```bash
   git clone https://github.com/Nosreme1234/DataScie-Physionet.git
   cd DataScie-Physionet
   ```

2. **Buat virtual environment**

   ```bash
   # Menggunakan venv
   python -m venv .venv

   # Activate virtual environment
   # Untuk Linux/Mac:
   source venv/bin/activate

   # Untuk Windows:
   venv\Scripts\activate
   ```

3. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ```

4. **Download dataset dari PhysioNet**
   ```bash
   wget -r -N -c -np https://physionet.org/files/brugada-huca/1.0.0/
   ```

### Referensi

https://physionet.org/lightwave/?db=brugada-huca/1.0.0

https://litfl.com/brugada-syndrome-ecg-library/

https://heartology.id/health-library/content/elektrokardiografi-ekg-atau-ecg-gambaran-umum-manfaat-dan-hasil-yang-diharapkan/
