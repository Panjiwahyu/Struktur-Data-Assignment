# <h1 align="center">Laporan Praktikum Pengenalan Bahasa C++</h1>
<p align="center">Panji Wahyu Nugroho</p>

## Dasar Teori

Pertama ada array fungsinya untuk menyimpan sekumpulan data, Array 2 dimensi untuk operasi aritmatika, pointer yang berfungsi sebagai variable yang menyimpan alamat memori dan yang terakhir ada switch case.

## Guided 

### 1. [Struktur Dan Perulangan]

```C++
#include <iostream>
using namespace std;

struct Mahasiswa {
    string nama;
    int umur;
};

int main () {
    int jumlah;

    cout << "Masukan jumlah mahasiswa: ";
    cin >> jumlah;

    Mahasiswa mhs[jumlah];

    // Input data menggunakan loop
    for (int i = 0; i < jumlah; i++) {
        cout << "\nMahasiswa ke-" << i + 1 << endl;
        cout << "Nama: ";
        cin >> mhs[i].nama;
        cout << "Umur: ";
        cin >> mhs[i].umur;
    }

    // Tampilkan data
    cout << "\n== Data Mahasiswa ===\n";
    for (int i = 0; i < jumlah; i++) {
        cout << "Mahasiswa ke-" << i + 1
             << " | Nama: " << mhs[i].nama
             << " | Umur: " << mhs[i].umur << endl;
    }

    return 0;
}

#include <iostream>
using namespace std;

int main () {
    int i;
    int j;

    for (int i = 0; i <= 10; i++) {
        cout << i << "-";
    } 

    cout << endl;

    for (int j = 20; j >= 10; j--) {
        cout << j << "-";
    }

    return 0;
}
```
Kode di atas yang pertama ada Struktur, lalu kedua ada Perulangan.

## Unguided 

### 1. [Program matriks 3x3]

```C++
#include <iostream>
using namespace std;

int main() {
    int A[3][3], B[3][3], C[3][3];
    int i, j, k;

    cout << "\nMasukkan elemen matriks A (3x3):\n";
    for (i = 0; i < 3; i++) {
        for (j = 0; j < 3; j++) {
            cout << "A[" << i << "][" << j << "] = ";
            cin >> A[i][j];
        }
    }

    cout << "\nMasukkan elemen matriks B (3x3):\n";
    for (i = 0; i < 3; i++) {
        for (j = 0; j < 3; j++) {
            cout << "B[" << i << "][" << j << "] = ";
            cin >> B[i][j];
        }
    }

    cout << "\n=== HASIL PENJUMLAHAN (A + B) ===\n";
    for (i = 0; i < 3; i++) {
        for (j = 0; j < 3; j++) {
            C[i][j] = A[i][j] + B[i][j];
            cout << C[i][j] << "\t";
        }
        cout << endl;
    }

    cout << "\n=== HASIL PENGURANGAN (A - B) ===\n";
    for (i = 0; i < 3; i++) {
        for (j = 0; j < 3; j++) {
            C[i][j] = A[i][j] - B[i][j];
            cout << C[i][j] << "\t";
        }
        cout << endl;
    }

    cout << "\n=== HASIL PERKALIAN (A x B) ===\n";
    for (i = 0; i < 3; i++) {
        for (j = 0; j < 3; j++) {
            C[i][j] = 0;
            for (k = 0; k < 3; k++) {
                C[i][j] += A[i][k] * B[k][j];
            }
            cout << C[i][j] << "\t";
        }
        cout << endl;
    }

    return 0;
}
```
#### Output:
<img width="311" height="487" alt="Image" src="https://github.com/user-attachments/assets/f5a8480a-02f5-4200-91b4-bd58657241a5" />

Program di atas digunakan untuk mencari operasi penjumlahan, pengurangan, dan perkalian matriks 3x3.

#### Full code Screenshot:
<img width="421" height="970" alt="Image" src="https://github.com/user-attachments/assets/d0948005-e169-4211-9a06-7c0839c0c5f9" />

### 2. [Menukar nilai 3 variable]

```C++
#include <iostream>
using namespace std;

void tukar3(int *a, int *b, int *c) {
    int temp = *a;
    *a = *b;
    *b = *c;
    *c = temp;
}

int main() {
    int x, y, z;
    cout << "Masukkan nilai x, y, z: ";
    cin >> x >> y >> z;

    cout << "Sebelum ditukar: x=" << x << ", y=" << y << ", z=" << z << endl;
    tukar3(&x, &y, &z);
    cout << "Setelah ditukar: x=" << x << ", y=" << y << ", z=" << z << endl;

    return 0;
}
```
#### Output:
<img width="481" height="157" alt="Image" src="https://github.com/user-attachments/assets/ab064933-f9cd-425f-b05c-41de4b01ba47" />

Program diatas fungsinya untuk menukar nilai dari 3 variabel.

#### Full code Screenshot:
<img width="829" height="910" alt="Image" src="https://github.com/user-attachments/assets/be6ca6a2-239e-4c0c-aefa-81ef4013eff8" />

### 3. [Mencari nilai minimum, maksimum, dan rata - rata]
```C++
#include <iostream>
using namespace std;

int cariMaksimum(int arr[], int n) {
    int maks = arr[0];
    for(int i=1; i<n; i++)
        if(arr[i] > maks) maks = arr[i];
    return maks;
}

int cariMinimum(int arr[], int n) {
    int min = arr[0];
    for(int i=1; i<n; i++)
        if(arr[i] < min) min = arr[i];
    return min;
}

float hitungRataRata(int arr[], int n) {
    int total = 0;
    for(int i=0; i<n; i++)
        total += arr[i];
    return (float)total / n;
}

int main() {
    int arrA[] = {11, 8, 5, 7, 12, 26, 3, 54, 33, 55};
    int n = sizeof(arrA)/sizeof(arrA[0]);
    int pilihan;

    do {
        cout << "\n--- Menu Program Array ---\n";
        cout << "1. Tampilkan isi array\n";
        cout << "2. Cari nilai maksimum\n";
        cout << "3. Cari nilai minimum\n";
        cout << "4. Hitung nilai rata-rata\n";

        cout << "Pilih: ";
        cin >> pilihan;

        switch(pilihan) {
            case 1:
                cout << "Isi array: ";
                for(int i=0; i<n; i++)
                    cout << arrA[i] << " ";
                cout << endl;
                break;
            case 2:
                cout << "Nilai maksimum: " << cariMaksimum(arrA, n) << endl;
                break;
            case 3:
                cout << "Nilai minimum: " << cariMinimum(arrA, n) << endl;
                break;
            case 4:
                cout << "Nilai rata-rata: " << hitungRataRata(arrA, n) << endl;
                break;
            case 5:
                cout << "Program selesai.\n";
                break;
            default:
                cout << "Pilihan tidak valid!\n";
        }
    } while(pilihan != 5);

    return 0;
}

```
#### Output:
<img width="334" height="630" alt="Image" src="https://github.com/user-attachments/assets/7efe2201-3578-4253-82b7-1b55c953fdeb" />

Program diatas kita diminta untuk mencari nilai minimum, maximum, dan rata rata dari array yang disediakan.

#### Full code Screenshot:
<img width="479" height="911" alt="Image" src="https://github.com/user-attachments/assets/e0e09717-8c3d-4452-9c78-b87ae73a9a8a" />

## Kesimpulan
Modul ini mengajarkan konsep dasar menggunakan array dan matriks, lalu penerapan fungsi, prosedur, pointer dalam pemrograman c++.

## Referensi
[1] Ginting, S. H. N., Effendi, H., Kumar, S., Marsisno, W., Sitanggang, Y. R. U., Anwar, K & Smrti, N. N. E. (2024).

[2] Sianipar, R. H. (2012). Pemrograman C++: Dasar Pemrograman Berorientasi Objek (Vol. 1).









