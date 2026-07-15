# Prediksi Harga Mobil Bekas di Arab Saudi Menggunakan Machine Learning

**Final Project — JCDSAH-025 Gamma Group**

Group Gamma : Didiek Arifman & M. Rafli Dwisanjani

## Business Problem

Syarah.com berperan sebagai pihak ketiga yang membeli mobil bekas dari seller melalui proses inspeksi, sebelum dijual kembali kepada buyer di platform mereka. Proses inspeksi ini membutuhkan biaya dan waktu — sehingga ketika seller membatalkan penjualan karena harga tawaran tidak sesuai ekspektasi, perusahaan mengalami kerugian material maupun waktu.

Tanpa acuan harga yang jelas sejak awal, seller kesulitan menilai apakah tawaran harga dari Syarah.com wajar, yang berpotensi menurunkan kepercayaan konsumen terhadap platform. Namun, harga mobil bekas dipengaruhi oleh banyak faktor sekaligus (merek, tahun produksi, jarak tempuh, ukuran mesin, dll), sehingga estimasi harga tidak dapat dilakukan dengan metode konvensional yang sederhana.

**Problem Statement:**
> Bagaimana membangun sistem estimasi harga mobil bekas yang akurat, untuk diberikan kepada seller sejak awal pendaftaran mobil, guna mengurangi risiko pembatalan transaksi dan meningkatkan kepercayaan terhadap platform?

## Goals

1. **Prediksi harga mobil** — Membangun model machine learning regresi dengan tingkat kesalahan (error) yang rendah.
2. **Analisis faktor yang memengaruhi harga mobil** — Mengidentifikasi faktor-faktor utama yang paling berpengaruh terhadap harga mobil bekas, seperti tahun pembuatan, jarak tempuh, ukuran mesin, dan lain-lain.

## Analytic Approach

Project ini dilakukan melalui dua tahap utama:
1. **Exploratory Data Analysis (EDA)** untuk menemukan pola dan hubungan antar fitur pada data listing mobil bekas.
2. **Model Building** — membangun model machine learning regresi yang dapat diimplementasikan sebagai alat prediksi harga, sehingga dapat dimanfaatkan seller dalam menentukan estimasi harga saat mendaftarkan mobilnya di platform.

## Dataset

Dataset merupakan data listing mobil bekas yang diperoleh melalui web scraping di platform Syarah.com pada tahun 2021.

| Attribute | Data Type | Description |
|---|---|---|
| Make | String | Merk mobil |
| Type | String | Tipe model mobil |
| Year | Integer | Tahun pembuatan |
| Origin | String | Asal negara mobil |
| Color | String | Warna mobil |
| Options | String | Tipe pilihan mobil |
| Engine_Size | Float | Ukuran mesin |
| Fuel_Type | String | Jenis bahan bakar |
| Gear_Type | String | Jenis transmisi mobil |
| Mileage | Integer | Riwayat jarak tempuh dalam KM |
| Region | String | Asal area mobil |
| Price | Integer | Harga mobil (target variable) |
| Negotiable | Boolean | Ketersediaan negosiasi |

## Evaluation Metrics

Model dievaluasi menggunakan tiga metrik regresi:
- **RMSE** (Root Mean Squared Error)
- **MAE** (Mean Absolute Error)
- **MAPE** (Mean Absolute Percentage Error)

## Tech Stack

- **Bahasa:** Python
- **Data Processing:** Pandas, NumPy
- **Visualisasi:** Matplotlib, Seaborn, GeoPandas
- **Preprocessing & Modeling:** Scikit-learn, Category Encoders, XGBoost
- **Model Interpretation:** SHAP
- **Model Deployment:** Joblib

## Model Terbaik

Model **XGBoost Regressor** (dengan hyperparameter tuning) terpilih sebagai model terbaik dari 5 algoritma yang dibandingkan (Linear Regression, KNN, Decision Tree, Random Forest, dan XGBoost), dengan hasil evaluasi pada data test sebagai berikut:

| Metrik | Hasil | Target |
|---|---|---|
| RMSE | 16.039,47 | < 20.000 |
| MAE | 10.917,13 | < 15.000 |
| MAPE | 17,2% | < 20% |

## Business Impact

### Ringkasan Perbandingan: Inspeksi Manual vs Estimasi ML (100 Seller)

| Komponen | Tanpa ML (Inspeksi Manual) | Dengan ML (Estimasi Instan) |
|---|---|---|
| Biaya Proses (SAR) | 10.000 | 1.000 |
| Total Biaya (SAR) | 10.000 | 1.000 |
| Total Waktu Proses | 300 hari | 500 menit (~8,3 jam) |

**Penghematan total biaya dengan ML untuk 100 seller: 9000 SAR**

- **Efisiensi biaya proses**: biaya inspeksi manual untuk 100 seller jauh lebih besar dibanding biaya estimasi ML untuk jumlah seller yang sama, karena proses manual membutuhkan biaya logistik dan tenaga appraiser untuk tiap unit, sedangkan ML dapat memproses seluruh seller secara otomatis dan paralel.

- **Efisiensi waktu**: proses inspeksi manual membutuhkan waktu berhari-hari untuk 100 seller (dihitung secara kumulatif dari waktu kerja appraiser), sedangkan ML dapat menyelesaikan estimasi untuk 100 seller hanya dalam hitungan jam, mempercepat pengalaman seller secara signifikan dan berpotensi meningkatkan retensi seller yang mengajukan penjualan.

- **Trade-off risiko harga**: proses manual diasumsikan sebagai harga acuan (tanpa risiko deviasi karena dinilai langsung dari kondisi fisik), sedangkan proses ML membawa risiko finansial berupa deviasi antara harga prediksi dan harga aktual pada tiap unit. Total risiko ini dihitung langsung dari hasil prediksi model pada 100 sampel data riil.

- **Keputusan bisnis**: ML layak digunakan apabila penghematan biaya proses lebih besar dari total risiko deviasi harga yang ditanggung. Berdasarkan hasil simulasi pada 100 sampel ini, penghematan biaya proses (SAR) dapat dibandingkan langsung dengan besaran risiko deviasi harga (SAR) untuk menentukan apakah trade-off ini menguntungkan secara agregat.

## Conclusions

- Berdasarkan hasil dari Cost-Based Analysis terhadap 100 seller yang membatalkan proses akuisisi mobilnya oleh perusahaan, model machine learning hanya memakan biaya sebesar 1000 SAR, dibandingkan biaya yang harus dikeluarkan perusahaan ketika seller harus melalui proses inspeksi terlebih dahulu sebelum membatalkan prosesnya, yaitu 10000 SAR. Total biaya yang dapat dihemat oleh perusahaan pada analisis yang telah dilakukan sebesar 9000 SAR. Fitur estimasi harga mobil ini dapat membuat proses akuisisi mobil menjadi lebih efisien. Seller dapat mempertimbangkan keputusannya dalam melanjutkan proses bisnis berdasarkan gambaran harga yang diberikan oleh perusahaan.

- Faktor yang paling mendorong harga mobil untuk semakin naik adalah ukuran mesin yang kecil, sebaliknya jika ukuran mobil besar maka model cenderung memberikan prediksi harga yang lebih kecil. Selain itu model mobil yang berbeda, area listing mobil, dan merk dari mobil juga turut mempengaruhi hasil prediksi harga mobil secara signifikan.

- Model XGBoost berhasil memberikan performa yang optimal dalam memberikan prediksi harga mobil. Model mampu memberikan prediksi dengan MAPE 17,2%, RMSE 16039.47, dan MAE 10917.13 pada mobil yang berada dalam jangkauan harga 18.500 hingga 200.000. Pendekatan ini merupakan upaya forecasting harga dengan tingkat akurasi 'Good' berdasarkan Interpretation of MAPE for forecasting Accuracy (Lewis, 1982) dan mampu memberikan fitur estimasi yang dapat membantu seller memiliki gambaran akan harga mobilnya, sesuai dengan tujuan dari project ini.

## Recommendations

- Investigasi ulang fitur mileage dan target harga, data anomali dapat mengacaukan proses latihan model dalam mempelajari pola pada data. Monitor dan validasi kebenaran data agar model mampu menangkap hubungan antara fitur dengan target secara lebih akurat.

- Departmen operasional dan teknologi perlu melakukan A/B Testing untuk menguji coba fitur estimasi harga dengan pendekatan model machine learning terhadap sebagian seller sebagai grup treatment dan bandingkan dengan proses bisnis eksisting sebagai grup kontrol. Analisia hasil perbandingan conversion rate, waktu rata-rata proses bisnis, serta drop-off rate. Integrasikan model ke alur proses bisnis akuisisi mobil seller sebagai fitur estimasi harga real-time, tetap libatkan human review untuk transaksi bernilai tinggi, dan tampilkan hasil SHAP ke seller untuk meningkatkan transparansi.

- Monitor metrik RMSE/MAE/MAPE secara berkala untuk mendeteksi model drift, lakukan retraining dengan data terbaru, dan validasi asumsi dampak bisnis dengan data operasional riil perusahaan.

- Tim Data Engineering perlu memperkaya dataset dengan fitur eksternal (kondisi inspeksi, riwayat servis, harga kompetitor) dan eksplorasi prediction interval untuk memberikan rentang harga, bukan hanya satu angka estimasi.

## 📚 References

- [How to Sell a Car in Saudi Arabia — Syarah.com](https://syarah.com/carsguide/en/how-sell-car-saudi-arabia/)
- [Car Inspection Price in Saudi Arabia — Syarah.com](https://syarah.com/carsguide/en/car-inspection-price-saudi-arabia/)
- [Using the R-MAPE Index as a Resistant Measure of Forecast Accuracy — ResearchGate](https://www.researchgate.net/publication/257812432_Using_the_R-MAPE_index_as_a_resistant_measure_of_forecast_accuracy)
