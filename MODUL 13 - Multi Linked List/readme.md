# <h1 align="center">Laporan Praktikum Multi Linked List</h1>
<p align="center">Panji Wahyu Nugroho</p>

## Dasar Teori

Multi Linked List adalah pengembangan dari struktur Linked List, 
di mana setiap node tidak hanya memiliki satu penunjuk (pointer) ke node berikutnya, tetapi lebih dari satu pointer.

## Guided 

### 1. [Multi Linked List]

```C++
#include <iostream>
using namespace std;

int main() {
    cout << "ini adalah file code guided praktikan" << endl;
    return 0;
}
```
Kode di atas digunakan contoh awal (code guided) pada kegiatan praktikum untuk memperkenalkan struktur dasar program C++.

## Unguided 

### 1. 

```C++
//multilist.h
#ifndef SLL_H
#define SLL_H
#include <iostream>
using namespace std;

struct Mahasiswa {
    string nama;
    string nim;
    char kelamin; 
    float ipk;
};

struct Node {
    Mahasiswa info;
    Node *next;
};

struct List {
    Node *first;
};

void createList(List &L);
Node* alokasi(Mahasiswa x);
void insertFirst(List &L, Node *p);
void insertLast(List &L, Node *p);
void insertAfter(Node *prec, Node *p);
void printInfo(List L);

#endif
//multilist.cpp
#include "multilist.h"

void createList(List &L) {
    L.first = NULL;
}

Node* alokasi(Mahasiswa x) {
    Node *p = new Node;
    p->info = x;
    p->next = NULL;
    return p;
}

void insertFirst(List &L, Node *p) {
    p->next = L.first;
    L.first = p;
}

void insertLast(List &L, Node *p) {
    if (L.first == NULL) {
        L.first = p;
    } else {
        Node *q = L.first;
        while (q->next != NULL) q = q->next;
        q->next = p;
    }
}

void insertAfter(Node *prec, Node *p) {
    p->next = prec->next;
    prec->next = p;
}

void printInfo(List L) {
    Node *p = L.first;

    while (p != NULL) {
        cout << "Nama : " << p->info.nama << endl;
        cout << "NIM  : " << p->info.nim << endl;
        cout << "L/P  : " << p->info.kelamin << endl;
        cout << "IPK  : " << p->info.ipk << endl << endl;
        p = p->next;
    }
}
//main.cpp
#include "multilist.h"

int main() {
    List L;
    createList(L);

    cout << "coba insert first, last, dan after" << endl;

    Mahasiswa m1 = {"Andi", "22001", 'L', 3.3};
    insertFirst(L, alokasi(m1));

    Mahasiswa m2 = {"Budi", "22002", 'L', 3.71};
    insertLast(L, alokasi(m2));

    Mahasiswa m3 = {"Citra", "22003", 'P', 3.5};
    insertLast(L, alokasi(m3));
    Mahasiswa m4 = {"Dewi", "22004", 'P', 4.0};
    Node *p = L.first;
    while (p->info.nama != "Citra") p = p->next;
    insertAfter(p, alokasi(m4));

    insertLast(L, alokasi({"Eko", "22005", 'L', 3.4}));
    insertLast(L, alokasi({"Farah", "22006", 'P', 3.45}));
    insertLast(L, alokasi({"Gilang", "22007", 'L', 3.75}));
    insertLast(L, alokasi({"Hana", "22008", 'P', 3.3}));

    printInfo(L);

    return 0;
}

```
#### Output:
<img width="369" height="965" alt="Image" src="https://github.com/user-attachments/assets/4bac7ea7-a259-47f1-ae38-3a88b1412b51" />

Program digunakan untuk mengimplementasikan struktur data Multi Linked List dalam pengelolaan data mahasiswa.

#### Full code Screenshot:
<img width="481" height="762" alt="Image" src="https://github.com/user-attachments/assets/1bd8c453-ecef-4c3a-85f5-ba81da9930ff" />
<img width="551" height="929" alt="Image" src="https://github.com/user-attachments/assets/845c1aeb-2350-4746-b00d-eb21e98d7822" />
<img width="574" height="627" alt="Image" src="https://github.com/user-attachments/assets/44209b3a-85f3-4639-b848-05e7acfd5d2e" />

## Kesimpulan

Berdasarkan program yang dibuat, dapat disimpulkan bahwa struktur data Multi Linked List efektif 
digunakan untuk mengelola data yang bersifat dinamis karena ukuran data tidak terbatas dan mudah dimodifikasi.

## Referensi
[1] Weiss, M. A. (2014). Data structures and algorithm analysis in C++ (4th ed.). Pearson.






















