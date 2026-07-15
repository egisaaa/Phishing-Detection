# Phishing URL Detection

Implementasi deteksi URL phishing berbasis Machine Learning menggunakan **Random Forest**, **XGBoost**, **Optuna**, dan Google Colab. Program melakukan EDA, ekstraksi fitur URL, preprocessing, balancing data, 10-fold cross-validation, evaluasi, serta penyimpanan model terbaik.

## Struktur Proyek

```text
phishing-url-detection/
├── data/
│   └── phishing_site_urls.csv
├── notebooks/
│   └── phishing_url_detection_colab.ipynb
├── src/
│   ├── features.py
│   ├── train.py
│   └── predict.py
├── models/
├── outputs/
├── requirements.txt
├── .gitignore
└── README.md
```

## Dataset

Letakkan dataset pada:

```text
data/phishing_site_urls.csv
```

Dataset wajib memiliki dua kolom:

| Kolom | Isi |
|---|---|
| `URL` | Alamat URL |
| `Label` | `good` atau `bad` |

Dataset tidak disertakan di repository agar ukuran repository tetap kecil dan untuk menghormati lisensi sumber data.

## Instalasi Lokal

```bash
git clone <URL-REPOSITORY-ANDA>
cd phishing-url-detection
python -m venv .venv
```

Aktifkan virtual environment, lalu jalankan:

```bash
pip install -r requirements.txt
```

## Training Model

```bash
python -m src.train --data data/phishing_site_urls.csv --trials 30
```

Hasil training disimpan pada:

- `models/best_xgb_model.joblib`
- `outputs/metrics.json`
- `outputs/classification_report.txt`
- `outputs/label_distribution.png`
- `outputs/confusion_matrix_best_xgb.png`

## Prediksi URL Baru

```bash
python -m src.predict "https://example.com"
```

Contoh keluaran:

```text
URL       : https://example.com
Hasil     : GOOD (AMAN)
Confidence: 98.25%
```

## Menjalankan di Google Colab

Buka file berikut pada Google Colab:

```text
notebooks/phishing_url_detection_colab.ipynb
```

Kemudian jalankan setiap sel secara berurutan. Dataset dapat disimpan di Google Drive atau diunggah langsung ke sesi Colab.

## Fitur URL

Fitur yang digunakan meliputi:

- URL length
- Number of dots
- Number of slashes
- Domain name length
- Entropy
- IP address
- Suspicious keywords
- Repetitions
- Redirections
- Dangerous characters
- Dangerous TLD

## Catatan Metodologis

Daftar karakter dan TLD berbahaya dipelajari hanya dari data training untuk menghindari kebocoran informasi dari data testing. Penyeimbangan kelas juga hanya dilakukan pada data training.

## Lisensi

Tambahkan lisensi sesuai kebutuhan penggunaan proyek dan lisensi dataset yang dipakai.
