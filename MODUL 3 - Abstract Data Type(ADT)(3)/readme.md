# <h1 align="center">Laporan Praktikum Abstract Data Type</h1>
<p align="center">Panji Wahyu Nugroho</p>

## Dasar Teori

Pertama ada array fungsinya untuk menyimpan sekumpulan data, Array 2 dimensi untuk operasi aritmatika, pointer yang berfungsi sebagai variable yang menyimpan alamat memori dan yang terakhir ada switch case.

## Guided 

### 1. [Pengenalan Bahasa C++]

```C++

```
Kode di atas yang pertama ada Struktur, lalu kedua ada Perulangan.

## Unguided 

### 1. []

```C++
#include <iostream>
using namespace std;

float hitungNilaiAkhir(float uts, float uas, float tugas) {
    return 0.3 * uts + 0.4 * uas + 0.3 * tugas;
}

int main() {
    const int MAX = 10;
    string nama[MAX];
    string nim[MAX];
    float uts[MAX], uas[MAX], tugas[MAX], nilaiAkhir[MAX];
    int n;

    cout << "Masukkan jumlah mahasiswa (maks 10): ";
    cin >> n;

    if (n > MAX) {
        cout << "Jumlah mahasiswa tidak boleh lebih dari 10!\n";
        return 0;
    }

    for (int i = 0; i < n; i++) {
        cout << "\nData mahasiswa ke-" << i + 1 << endl;
        cout << "Nama (tanpa spasi) : ";
        cin >> nama[i];
        cout << "NIM                : ";
        cin >> nim[i];
        cout << "Nilai UTS          : ";
        cin >> uts[i];
        cout << "Nilai UAS          : ";
        cin >> uas[i];
        cout << "Nilai Tugas        : ";
        cin >> tugas[i];

        nilaiAkhir[i] = hitungNilaiAkhir(uts[i], uas[i], tugas[i]);
    }

    cout << "\n==============================================\n";
    cout << "No\tNama\tNIM\tNilai Akhir\n";
    cout << "==============================================\n";
    for (int i = 0; i < n; i++) {
        cout << i + 1 << "\t" << nama[i] << "\t" << nim[i]
             << "\t" << nilaiAkhir[i] << endl;
    }

    return 0;
}
```
#### Output:



Program di atas digunakan untuk mencari operasi penjumlahan, pengurangan, dan perkalian matriks 3x3.

#### Full code Screenshot:


### 2. []

```C++

```
#### Output:


Program diatas fungsinya untuk menukar nilai dari 3 variabel.

#### Full code Screenshot:


### 3. []
```C++

```
#### Output:

Program diatas kita diminta untuk mencari nilai minimum, maximum, dan rata rata dari array yang disediakan.

#### Full code Screenshot:


## Kesimpulan


## Referensi













