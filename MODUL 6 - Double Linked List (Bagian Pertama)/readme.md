# <h1 align="center">Laporan Praktikum DoubleLinked List (Bagian Pertama)</h1>
<p align="center">Panji Wahyu Nugroho</p>

## Dasar Teori

Doubly Linked List adalah struktur data linear yang terdiri dari kumpulan node,
di mana setiap node memiliki tiga komponen utama, yaitu data, pointer ke node berikutnya (next), dan pointer ke node sebelumnya (prev)

## Guided 

### 1. [Double Linked List (Bagian Pertama)]

```C++
#include <iostream>
#define Nil NULL
using namespace std;

typedef int infotype; // Definisikan tipe data infotype sebagai integer untuk menyimpan informasi elemen
typedef struct elmlist *address; // Definisikan tipe address sebagai pointer ke struct elmlist

struct elmlist {
    infotype info; // Deklarasikan field info untuk menyimpan data elemen
    address next;
    address prev;
};

struct List { 
    address first; 
    address last; 
}; 

void insertFirst(List &L, address P) { 
    P->next = L.first; // Set pointer next dari P ke elemen pertama saat ini
    P->prev = Nil; // Set pointer prev dari P ke Nil karena menjadi elemen pertama
    if (L.first != Nil) L.first->prev = P; // Jika list tidak kosong, set prev elemen pertama lama ke P
    else L.last = P; // Jika list kosong, set last juga ke P
    L.first = P; // Update first list menjadi P
} 

void insertLast(List &L, address P) { 
    P->prev = L.last; // Set pointer prev dari P ke elemen terakhir saat ini
    P->next = Nil; // Set pointer next dari P ke Nil karena menjadi elemen terakhir
    if (L.last != Nil) L.last->next = P; // Jika list tidak kosong, set next elemen terakhir lama ke P
    else L.first = P; // Jika list kosong, set first juga ke P
    L.last = P; // Update last list menjadi P
} 

void insertAfter(List &L, address P, address R) { // Definisikan fungsi insertAfter untuk menyisipkan elemen setelah R
    P->next = R->next; // Set pointer next dari P ke elemen setelah R
    P->prev = R; // Set pointer prev dari P ke R
    if (R->next != Nil) R->next->prev = P; // Jika ada elemen setelah R, set prev elemen tersebut ke P
    else L.last = P; // Jika R adalah terakhir, update last menjadi P
    R->next = P; // Set next dari R ke P
}

address alokasi(infotype x) { // Definisikan fungsi alokasi untuk membuat elemen baru
    address P = new elmlist; // Alokasikan memori baru untuk elemen
    P->info = x; // Set info elemen dengan nilai x
    P->next = Nil; // Set next elemen ke Nil
    P->prev = Nil; // Set prev elemen ke Nil
    return P; 
} 

void printInfo(List L) { // Definisikan fungsi printInfo untuk mencetak isi list
    address P = L.first; // Set P ke elemen pertama list
    while (P != Nil) { // Loop selama P tidak Nil
        cout << P->info << " "; // Cetak info dari P 
        P = P->next; // Pindah ke elemen berikutnya
    } 
    cout << endl; 
}

int main() { 
    List L; 
    L.first = Nil; 
    L.last = Nil;
    address P1 = alokasi(1); 
    insertFirst(L, P1); 
    address P2 = alokasi(2); 
    insertLast(L, P2); 
    address P3 = alokasi(3); 
    insertAfter(L, P3, P1); 
    printInfo(L); 
    return 0; 
}
```
Kode di atas digunakan untuk implementasi Double Linked List (punya next dan prev) lengkap dengan operasi dasar.

## Unguided 

### 1. 

```C++
//Doublelinglist.h
#ifndef DOUBLYLIST_H
#define DOUBLYLIST_H

#include <iostream>
#include <string>
using namespace std;

struct Kendaraan {
    string nopol;
    string warna;
    int tahun;
};

typedef struct Node* address;

struct Node {
    Kendaraan data;
    address next;
    address prev;
};

struct List {
    address first;
    address last;
};

void createList(List &L);
address newNode(Kendaraan x);
void printList(List L);
void insertLast(List &L, address P);
address find(List L, string nopol);

void deleteByNopol(List &L, string nopol);

#endif

//Doublelinglist.cpp
#include "DoublyList.h"
using namespace std;

void createList(List &L) {
    L.first = NULL;
    L.last = NULL;
}

address newNode(Kendaraan x) {
    address P = new Node;
    P->data = x;
    P->next = NULL;
    P->prev = NULL;
    return P;
}

void printList(List L) {
    cout << "DATA LIST 1\n\n";
    address P = L.last;
    while (P != NULL) {
        cout << "no polisi : " << P->data.nopol << endl;
        cout << "warna     : " << P->data.warna << endl;
        cout << "tahun     : " << P->data.tahun << endl;
        if (P->prev != NULL) cout << endl;
        P = P->prev;
    }
}

void insertLast(List &L, address P) {
    if (L.first == NULL) {
        L.first = L.last = P;
    } else {
        L.last->next = P;
        P->prev = L.last;
        L.last = P;
    }
}

address find(List L, string nopol) {
    address P = L.first;
    while (P != NULL) {
        if (P->data.nopol == nopol) return P;
        P = P->next;
    }
    return NULL;
}

void deleteByNopol(List &L, string nopol) {
    address P = find(L, nopol);
    if (P == NULL) {
        cout << "Data tidak ditemukan\n";
        return;
    }

    if (P == L.first && P == L.last) {
        L.first = L.last = NULL;
    } 
    else if (P == L.first) {
        L.first = P->next;
        L.first->prev = NULL;
    } 
    else if (P == L.last) {
        L.last = P->prev;
        L.last->next = NULL;
    } 
    else {
        P->prev->next = P->next;
        P->next->prev = P->prev;
    }

    cout << "Data dengan nomor polisi " << nopol << " berhasil dihapus.\n\n";
    delete P;
}

//main.c
#include <iostream>
#include "DoublyList.h"
using namespace std;

int main() {
    List L;
    createList(L);

    Kendaraan x;
    string nopol;

    cout << "masukkan nomor polisi: ";
    cin >> x.nopol;
    cout << "masukkan warna kendaraan: ";
    cin >> x.warna;
    cout << "masukkan tahun kendaraan: ";
    cin >> x.tahun;
    insertLast(L, newNode(x));
    cout << endl;

    cout << "masukkan nomor polisi: ";
    cin >> x.nopol;
    cout << "masukkan warna kendaraan: ";
    cin >> x.warna;
    cout << "masukkan tahun kendaraan: ";
    cin >> x.tahun;
    insertLast(L, newNode(x));
    cout << endl;

    cout << "masukkan nomor polisi: ";
    cin >> nopol;
    if (find(L, nopol) != NULL) {
        cout << "nomor polisi sudah terdaftar\n\n";
    }

    cout << "masukkan nomor polisi: ";
    cin >> x.nopol;
    cout << "masukkan warna kendaraan: ";
    cin >> x.warna;
    cout << "masukkan tahun kendaraan: ";
    cin >> x.tahun;
    insertLast(L, newNode(x));
    cout << endl;

    printList(L);
    cout << endl;

    cout << "Masukkan Nomor Polisi yang dicari  : ";
    cin >> nopol;

    address P = find(L, nopol);
    if (P != NULL) {
        cout << "\nNomor Polisi : " << P->data.nopol << endl;
        cout << "Warna        : " << P->data.warna << endl;
        cout << "Tahun        : " << P->data.tahun << endl;
    }
    cout << endl;

    cout << "Masukkan Nomor Polisi yang akan dihapus  : ";
    cin >> nopol;
    deleteByNopol(L, nopol);

    printList(L);

    return 0;
}
```
#### Output:
<img width="398" height="786" alt="Image" src="https://github.com/user-attachments/assets/3ea7dc0d-12c7-42e4-a35e-a7475b6dd339" />
<img width="456" height="401" alt="Image" src="https://github.com/user-attachments/assets/70deaa68-726f-4ccc-be72-acaed24c83e6" />

Program di atas digunakan untuk mengelola data kendaraan menggunakan Doubly Linked List, jadi setiap data kendaraan bisa ditelusuri.

#### Full code Screenshot:

<img width="488" height="909" alt="Image" src="https://github.com/user-attachments/assets/fca865f9-ff11-4f28-b790-75e860a86f6f" />
<img width="441" height="783" alt="Image" src="https://github.com/user-attachments/assets/6e31bb00-6bd9-4293-9672-5011cf539294" />
<img width="532" height="437" alt="Image" src="https://github.com/user-attachments/assets/82ad540e-2ba2-4618-8c66-18d9d7ff9f19" />
<img width="477" height="975" alt="Image" src="https://github.com/user-attachments/assets/e037f9ec-4c15-40c6-b7b3-bd503d5af800" />

## Kesimpulan

Berdasarkan hasil implementasi dan pengujian program, dapat disimpulkan bahwa struktur data Doubly Linked List 
mampu mengelola data kendaraan secara dinamis dengan baik. Program berhasil melakukan operasi penambahan data, pencarian berdasarkan nomor polisi, 
penampilan data, serta penghapusan data pada posisi awal, tengah, maupun akhir list.

## Referensi
[1] Cormen, T. H., Leiserson, C. E., Rivest, R. L., & Stein, C. (2022). Introduction to algorithms (4th ed.). MIT Press.

















