# <h1 align="center">Laporan Praktikum Modul Code Blocks IDE & Pengenalan Bahasa C++ (1)</h1>
<p align="center">Panji Wahyu Nugroho</p>

## Dasar Teori

Kita diperkenalkan oleh identifier lalu ada input / output disini kita di perkenalkan berbagai macam operator. selanjutnya if, if else, switch. dan ada perulangan, struktur.

## Guided 

### 1. [Nama Topik]

```C++
#include <iostream>
using namespace std;

int main () {
    int n;
    const float pl = 3.14;

    cout << "Masukan Angka: ";
    cin >> n;

    cout << "Angka dikeluarkan: " << n << endl;
    cout << "Nilai Konstanta pl: " << pl << endl;
    return 0;
}

#include <iostream>
using namespace std;

int main () {
    int a;
    int b;

    cout << "Masukan Angka1: ";
    cin >> a;
    cout << "Masukan Angka2: ";
    cin >> b;

    //Operator Aritmatika
    cout << "a + b = " << (a+b) << endl;
    cout << "a - b = " << (a-b) << endl;
    cout << "a * b = " << (a*b) << endl;
    cout << "a / b = " << (a/b) << endl;
    cout << "a % b = " << (a+b) << endl;

    //Operator Logika
    cout << "a < b = " << (a<b) << endl;
    cout << "a > b = " << (a>b) << endl;
    cout << "a <= b = " << (a<=b) << endl;
    cout << "a >= b = " << (a>=b) << endl;
    cout << "a == b = " << (a==b) << endl;
    cout << "a != b = " << (a!=b) << endl;
    return 0;
}
```
Kode di atas yang pertama ada input / output, lalu kedua ada Operator percabangan aritmatika

## Unguided 

### 1. [Soal]

```C++
#include <iostream>
using namespace std;

int main() {

    float bilangan1, bilangan2;

    cout << "Masukkan bilangan pertama: ";
    cin >> bilangan1;
    cout << "Masukkan bilangan kedua: ";
    cin >> bilangan2;

    cout << "\n--- Hasil Operasi ---" << endl;
    cout << "Penjumlahan: " << bilangan1 + bilangan2 << endl;
    cout << "Pengurangan: " << bilangan1 - bilangan2 << endl;
    cout << "Perkalian: " << bilangan1 * bilangan2 << endl;

    if (bilangan2 != 0) {
        cout << "Pembagian: " << bilangan1 / bilangan2 << endl;
    } else {
        cout << "Pembagian: Tidak bisa membagi dengan nol." << endl;
    }

    return 0;
}
```
#### Output:
<img width="579" height="199" alt="Image" src="https://github.com/user-attachments/assets/b7d08961-7632-4a40-be44-ef1fa11983c0" />

Kode di atas digunakan untuk mengambil dua input angka yang kita masukan dan menampilkan hasil dari empat operasi aritmatika.

#### Full code Screenshot:
<img width="766" height="997" alt="Image" src="https://github.com/user-attachments/assets/07861d97-f511-413c-8831-d0b4b63cb459" />

### 2. [Soal]

```C++
#include <iostream>
using namespace std;

int main() {
    int angka;
   string tulisan = "";
   string satuan[] = {"", "satu", "dua", "tiga", "empat", "lima", "enam", "tujuh", "delapan", "sembilan"};

   cout << "Masukkan angka (0-100): ";
   cin >> angka;

    if (angka < 0 || angka > 100) {
        tulisan = "Input di luar jangkauan (0-100).";
    } else if (angka == 0) {
        tulisan = "nol";
    } else if (angka == 100) {
        tulisan = "seratus";
    } else if (angka == 10) {
        tulisan = "sepuluh";
    } else if (angka == 11) {
        tulisan = "sebelas";
    } else if (angka < 10) {
        tulisan = satuan[angka];
    } else if (angka < 20) { 
        tulisan = satuan[angka % 10] + " belas";
    } else { 
        int puluhan = angka / 10;
        int sisa = angka % 10;
        tulisan = satuan[puluhan] + " puluh";
        if (sisa > 0) {
            tulisan += " " + satuan[sisa];
        }
    }

   cout << angka << " : " << tulisan <<endl;

    return 0;
}
```
#### Output:
<img width="471" height="134" alt="Image" src="https://github.com/user-attachments/assets/20119050-15af-423d-bc7e-195246a1d398" />

Program diatas fungsinya membaca input angka (0–100), lalu menampilkan output dalam bentuk kata.

#### Full code Screenshot:
<img width="925" height="1021" alt="Image" src="https://github.com/user-attachments/assets/8cc7abeb-e87e-415e-aaf1-3166498f63c0" />
### 3. [Soal]

```C++
#include <iostream>
using namespace std;

int main() {
    int angka;
   string tulisan = "";
   string satuan[] = {"", "satu", "dua", "tiga", "empat", "lima", "enam", "tujuh", "delapan", "sembilan"};

   cout << "Masukkan angka (0-100): ";
   cin >> angka;

    if (angka < 0 || angka > 100) {
        tulisan = "Input di luar jangkauan (0-100).";
    } else if (angka == 0) {
        tulisan = "nol";
    } else if (angka == 100) {
        tulisan = "seratus";
    } else if (angka == 10) {
        tulisan = "sepuluh";
    } else if (angka == 11) {
        tulisan = "sebelas";
    } else if (angka < 10) {
        tulisan = satuan[angka];
    } else if (angka < 20) { 
        tulisan = satuan[angka % 10] + " belas";
    } else { 
        int puluhan = angka / 10;
        int sisa = angka % 10;
        tulisan = satuan[puluhan] + " puluh";
        if (sisa > 0) {
            tulisan += " " + satuan[sisa];
        }
    }

   cout << angka << " : " << tulisan <<endl;

    return 0;
}
```
#### Output:
<img width="491" height="194" alt="Image" src="https://github.com/user-attachments/assets/2c58c4f8-6a75-44f4-a207-1ec7a6017f25" />

Program diatas menampilkan pola angka menurun dan menaik yang terpisah oleh tanda *, Sampai berbentuk segitiga terbalik.

#### Full code Screenshot:
<img width="527" height="984" alt="Image" src="https://github.com/user-attachments/assets/72f18e04-07e9-4deb-bd0f-ad6fa7318ea5" />

## Kesimpulan
Pembelajaran tentang materi input / output, if else dan juga percabangan operasi aritmatika.

## Referensi
[1] PEMROGRAMAN, ALGORITMA; FIRNANDA, MUHAMMAD ADITYA. LAPORAN PRAKTIKUM I. 2016.
