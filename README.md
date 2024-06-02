# MVPCalculator-Regresi
Menghitung point pertandingan pada game Mobile Legends setelah match untuk menentukan MVP (Most Valuable Player) berdasarkan statistik match dengan menggunakan Regresi Linear. Proyek ini dikerjakan bersama dengan teman saya berinisial ADR dan JB.

## Dataset
Dataset dikumpulkan secara MANUAL dengan melihat history pertandingan dan mencatat statustuj hasilnya pada Google Spreadsheet. Dengan kolom-kolom atau variabel yang dicatat adalah:

1. Kill
2. Death
3. Assist
4. Gold
5. Minutes
6. GPM (didapatkan dari Gold / Minutes)
7. Hero Damage
8. Turret Damage
9. Damage Taken
10. Teamfight Participation
11. Win
12. Score

## Data Preprocessing
Dengan melakukan drop column pada Gold dan Minutes, lalu dilakukan seleksi fitur dengan Korelasi Pearson yang memiliki nilai <=-0.5 atau >=0.5

![image](https://user-images.githubusercontent.com/57952404/230865009-4dde559a-71b7-489a-a78f-e4b0bd4fa26b.png)

Sehingga didapatkan
```python
df_match = df_match[['kill', 'death', 'assist', 'gpm', 'teamfight_part', 'win', 'score']]
```

## Modeling
Data dibagi train-test dengan ratio 8:2.
Lalu dilakukan pemodelan machine learning LINEAR REGRESSION dengan label adalah kolom score. Didapakan persamaan linear dengan rumus sebagai berikut:

```
score = 2.584 + 0.271x1 + -0.324x2 + 0.209x3 + 0.003x4 + 0.02x5 + -0.052x6
```

## Evaluation
Dengan menggunakan 20% data test, dilakukan prediksi menggunakan persamaan regresi linear sebelumnya. Kemudian, hasilnya dibandingkan dengan nilai aslinya. Visualisasinya dapat dilihat sebagai berikut:

![image](https://user-images.githubusercontent.com/57952404/230865834-1749ca4c-4b7f-4cac-baf4-9913f7745016.png)

Hasil evaluasi menggunakan metrik R2, RMSE, dan MAE. Nilai R2 yang baik adalah mendekati 1, dan untuk nilai RMSE dan MAE yang baik mendekati 0. Berikut tabel tiap-tiap metrik terhadap data yang diukur:

| Jenis Data | R2 | RMSE | MAE |
| -- | -- | -- | -- |
| Train | 0.962 | 0.425 | 0.340 |
| Test | 0.955 | 0.455 | 0.356 |

## Deployment
Untuk langsung menguji coba MVP Calculator, bisa pergi ke: https://otnielabiezer.com/MVPCalculator/
