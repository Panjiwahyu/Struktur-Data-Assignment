# <h1 align="center">Laporan Praktikum Singly Linked List (Bagian Pertama)</h1>
<p align="center">Panji Wahyu Nugroho</p>

## Dasar Teori

berfokus pada definisi, karakteristik, dan operasi dasar dari struktur data ini, yang sangat penting sebagai fondasi komputasi dinamis.

## Guided 

### 1. [Singly Linked List (Bagian Pertama)]

```C++
1. list.h
#include "list.h"

#include<iostream>
using namespace std;

int main(){
    linkedlist List;
    address nodeA, nodeB, nodeC, nodeD, nodeE = Nil;
    createList(List);

    dataMahasiswa mhs;

    nodeA = alokasi("Dhimas", "2311102151", 20);
    nodeB = alokasi("Arvin", "2211110014", 21);
    nodeC = alokasi("Rizal", "2311110029", 20);
    nodeD = alokasi("Satrio", "2211102173", 21);
    nodeE = alokasi("Joshua", "2311102133", 21);

    insertFirst(List, nodeA);
    insertLast(List, nodeB);
    insertAfter(List, nodeC, nodeA);
    insertAfter(List, nodeD, nodeC);
    insertLast(List, nodeE);

    cout << "--- ISI LIST SETELAH DILAKUKAN INSERT ---" << endl;
    printList(List);

    return 0;
}

2. list.cpp
#include "list.h"
#include <iostream>
using namespace std;

//I.S = Initial State / kondisi awal
//F.S = Final State / kondisi akhir

//fungsi untuk cek apakah list kosong atau tidak
bool isEmpty(linkedlist List) {
    if(List.first == Nil){
        return true; 
    } else {
        return false;
    }
}

//pembuatan linked list kosong
void createList(linkedlist &List) {
    /* I.S. sembarang
       F.S. terbentuk list kosong */
    List.first = Nil;
}

//pembuatan node baru dengan menerapkan manajemen memori
address alokasi(string nama, string nim, int umur) { 
    /* I.S. sembarang
       F.S. mengembalikan alamat node baru dengan isidata = sesuai parameter dan next = Nil */
    address nodeBaru = new node; 
    nodeBaru->isidata.nama = nama;
    nodeBaru->isidata.nim = nim; 
    nodeBaru->isidata.umur = umur;
    nodeBaru->next = Nil;
    return nodeBaru;
}

//penghapusan node dengan menerapkan manajemen memori
void dealokasi(address &node) {
    /* I.S. P terdefinisi
       F.S. memori yang digunakan node dikembalikan ke sistem */
    node->next = Nil;
    delete node;
}

//prosedur-prosedur untuk insert / menambahkan node baru kedalam list
void insertFirst(linkedlist &List, address nodeBaru) {
    /* I.S. sembarang, P sudah dialokasikan
       F.S. menempatkan elemen list (node) pada awal list */
    nodeBaru->next = List.first; 
    List.first = nodeBaru;
}

void insertAfter(linkedlist &List, address nodeBaru, address Prev) {
    /* I.S. sembarang, nodeBaru dan Prev alamat salah satu elemen list (node)
       F.S. menempatkan elemen (node) sesudah elemen node Prev */
    if (Prev != Nil) {
        nodeBaru->next = Prev->next;
        Prev->next = nodeBaru;
    } else {
        cout << "Node sebelumnya tidak valid!" << endl;
    }
}

void insertLast(linkedlist &List, address nodeBaru) {
    /* I.S. sembarang, nodeBaru sudah dialokasikan
       F.S. menempatkan elemen nodeBaru pada akhir list */
    if (isEmpty(List)) {
        List.first = nodeBaru;
    } else {
        address nodeBantu = List.first;
        while (nodeBantu->next != Nil) {
            nodeBantu = nodeBantu->next;
        }
        nodeBantu->next = nodeBaru;
    }
}

//prosedur-prosedur untuk delete / menghapus node yang ada didalam list
void delFirst(linkedlist &List){
    /* I.S. list tidak kosong
    F.S. node pertama di list terhapus*/
    address nodeHapus;
    if (isEmpty(List) == false) {
        nodeHapus = List.first;
        List.first = List.first->next;
        nodeHapus->next = Nil;
        dealokasi(nodeHapus);
    } else {
        cout << "List kosong!" << endl;
    }
}

void delLast(linkedlist &List){
    /* I.S. list tidak kosong
    F.S. node terakhir di list terhapus */
    address nodeHapus, nodePrev;
    if(isEmpty(List) == false){
        nodeHapus = List.first;
        if(nodeHapus->next == Nil){
            List.first->next = Nil;
            dealokasi(nodeHapus);
        } else { 
            while(nodeHapus->next != Nil){
                nodePrev = nodeHapus; 
                nodeHapus = nodeHapus->next;
            }
            nodePrev->next = Nil; 
            dealokasi(nodeHapus);
        }
    } else {
        cout << "list kosong" << endl;
    }
}

void delAfter(linkedlist &List, address nodeHapus, address nodePrev){
    /* I.S. list tidak kosng, Prev alamat salah satu elemen list
    F.S. nodeBantu adalah alamat dari Prev→next, menghapus Prev→next dari list */
    if(isEmpty(List) == true){
        cout << "List kosong!" << endl;
    } else { //jika list tidak kosong
        if (nodePrev != Nil && nodePrev->next != Nil) { 
            nodeHapus = nodePrev->next;       
            nodePrev->next = nodeHapus->next;  
            nodeHapus->next = Nil;         
            dealokasi(nodeHapus);
        } else {
            cout << "Node sebelumnya (prev) tidak valid!" << endl;
        }
    }
}

//prosedur untuk menampilkan isi list
void printList(linkedlist List) {
    /* I.S. list mungkin kosong
       F.S. jika list tidak kosong menampilkan semua info yang ada pada list */
    if (isEmpty(List)) {
        cout << "List kosong." << endl;
    } else {
        address nodeBantu = List.first;
        while (nodeBantu != Nil) { 
            cout << "Nama : " << nodeBantu->isidata.nama << ", NIM : " << nodeBantu->isidata.nim << ", Usia : " << nodeBantu->isidata.umur << endl;
            nodeBantu = nodeBantu->next;
        }
    }
}

//function untuk menampilkan jumlah node didalam list
int nbList(linkedlist List) {
    /* I.S. list sudah ada
       F.S. menampilkan jumlah node didalam list*/
    int count = 0;
    address nodeBantu = List.first;
    while (nodeBantu != Nil) {
        count++;
        nodeBantu = nodeBantu->next; 
    }
    return count;
}

//prosedur untuk menghapus list (menghapus semua node didalam list)
void deleteList(linkedlist &List){
    /* I.S. list sudah ada
       F.S. menghapus semua node didalam list*/
    address nodeBantu, nodeHapus;
    nodeBantu = List.first;
    while(nodeBantu != Nil){
        nodeHapus = nodeBantu;
        nodeBantu = nodeBantu->next;
        dealokasi(nodeHapus); 
    }
    List.first = Nil; 
    cout << "List sudah terhapus!" << endl;
}

3. main.cpp
#include "list.h"

#include<iostream>
using namespace std;

int main(){
    linkedlist List;
    address nodeA, nodeB, nodeC, nodeD, nodeE = Nil;
    createList(List);

    dataMahasiswa mhs;

    nodeA = alokasi("Dhimas", "2311102151", 20);
    nodeB = alokasi("Arvin", "2211110014", 21);
    nodeC = alokasi("Rizal", "2311110029", 20);
    nodeD = alokasi("Satrio", "2211102173", 21);
    nodeE = alokasi("Joshua", "2311102133", 21);

    insertFirst(List, nodeA);
    insertLast(List, nodeB);
    insertAfter(List, nodeC, nodeA);
    insertAfter(List, nodeD, nodeC);
    insertLast(List, nodeE);

    cout << "--- ISI LIST SETELAH DILAKUKAN INSERT ---" << endl;
    printList(List);

    return 0;
}
```
Kode di atas digunakan untuk membuat, mengelola, dan menampilkan data mahasiswa menggunakan struktur data linked list (singly linked list) dalam bahasa C++.

## Unguided 

### 1. 

```C++
//Singlylist.h
#ifndef SINGLYLIST_H
#define SINGLYLIST_H

#include <cstdlib>

typedef int infotype;
typedef struct Elmlist *address;

typedef struct Elmlist {
    infotype info;
    address next;
} Elmlist;

typedef struct {
    address First;
} List;

void CreateList(List *L);

address alokasi(infotype x);

void printInfo(List L);

void insertFirst(List *L, address P);

#endif

//Singlylist.cpp
#include "Singlylist.h"
#include <iostream>

using namespace std;

void CreateList(List *L) {
    L->First = NULL;
}

address alokasi(infotype x) {
    address P = (address)malloc(sizeof(Elmlist));
    if (P != NULL) {
        P->info = x;
        P->next = NULL;
    }
    return P;
}

void printInfo(List L) {
    address P = L.First;
    while (P != NULL) {
        cout << P->info << " ";
        P = P->next;
    }
    cout << endl;
}

void insertFirst(List *L, address P) {
    P->next = L->First;
    L->First = P;
}

//main.cpp
#include "Singlylist.h"
#include <iostream>

using namespace std;

int main() {
    List L;
    address P1, P2, P3, P4, P5; 

    P1 = P2 = P3 = P4 = P5 = NULL;
    CreateList(&L);
 
    P1 = alokasi(2);
    insertFirst(&L, P1);

    P2 = alokasi(0);
    insertFirst(&L, P2);

    P3 = alokasi(8);
    insertFirst(&L, P3);

    P4 = alokasi(12);
    insertFirst(&L, P4);

    P5 = alokasi(9);
    insertFirst(&L, P5);
    
    cout << "\nOutput yang diharapkan: " << endl;
    cout << "9 12 8 0 2" << endl;

    return 0;
}
```
#### Output:
<img width="482" height="113" alt="Image" src="https://github.com/user-attachments/assets/596ff539-d65b-4b53-a495-a2dff95ba647" />

Program di atas digunakan untuk mengimplementasikan dan menguji pembentukan struktur dataSinglylist dengan urutan elemen.

#### Full code Screenshot:
<img width="371" height="545" alt="Image" src="https://github.com/user-attachments/assets/ef107699-48ac-48d9-b2ba-735f9e5ac6ef" />
<img width="471" height="639" alt="Image" src="https://github.com/user-attachments/assets/c896a44c-4733-47db-b4d0-e3bfaf92ce43" />
<img width="468" height="662" alt="Image" src="https://github.com/user-attachments/assets/cf00fcd2-72b0-45ae-9c38-935d73f8bac7" />

### 2.

```C++
//Singlylist.h
#ifndef SINGLYLIST_H
#define SINGLYLIST_H

#include <cstdlib>

typedef int infotype;
typedef struct Elmlist *address;

typedef struct Elmlist {
    infotype info;
    address next;
} Elmlist;

typedef struct {
    address First;
} List;

void CreateList(List *L);
address alokasi(infotype x);
void dealokasi(address P); 
void printInfo(List L);
int nbList(List L);

void insertFirst(List *L, address P);

void deleteFirst(List *L, address *Pdel);
void deleteLast(List *L, address *Pdel);
void deleteAfter(List *L, address *Pdel, address Prec);
void deleteList(List *L);

#endif

//Singlylist.cpp
#include "Singlylist.h"
#include <iostream>

using namespace std;

void CreateList(List *L) {
    L->First = NULL;
}

address alokasi(infotype x) {
    address P = (address)malloc(sizeof(Elmlist));
    if (P != NULL) {
        P->info = x;
        P->next = NULL;
    }
    return P;
}

void dealokasi(address P) {
    if (P != NULL) {
        free(P);
    }
}

void printInfo(List L) {
    address P = L.First;
    while (P != NULL) {
        cout << P->info << " ";
        P = P->next;
    }
    cout << endl;
}

int nbList(List L) {
    int count = 0;
    address P = L.First;
    while (P != NULL) {
        count++;
        P = P->next;
    }
    return count;
}

void insertFirst(List *L, address P) {
    P->next = L->First;
    L->First = P;
}

void deleteFirst(List *L, address *Pdel) {
    *Pdel = NULL;
    if (L->First != NULL) {
        *Pdel = L->First;
        L->First = L->First->next;
        (*Pdel)->next = NULL; 
    }
}

void deleteLast(List *L, address *Pdel) {
    *Pdel = NULL;
    if (L->First == NULL) return; 

    address P = L->First;
    address Prec = NULL;

    if (P->next == NULL) {
        *Pdel = P;
        L->First = NULL;
    } else {
        while (P->next != NULL) {
            Prec = P;
            P = P->next;
        }
        *Pdel = P;
        Prec->next = NULL;
    }
}

void deleteAfter(List *L, address *Pdel, address Prec) {
    *Pdel = NULL;
    if (Prec != NULL && Prec->next != NULL) {
        *Pdel = Prec->next; 
        Prec->next = (*Pdel)->next; 
        (*Pdel)->next = NULL;
    }
}

void deleteList(List *L) {
    address P;
    while (L->First != NULL) {
        deleteFirst(L, &P);
        dealokasi(P);
    }
}

//main.cpp
#include "Singlylist.h"
#include <iostream>

using namespace std;

int main() {
    List L;
    address P1, P2, P3, P4, P5; 
    address Pdel; 
    
    P1 = P2 = P3 = P4 = P5 = NULL;
    CreateList(&L);

    P1 = alokasi(2); insertFirst(&L, P1); 
    P2 = alokasi(0); insertFirst(&L, P2); 
    P3 = alokasi(8); insertFirst(&L, P3); 
    P4 = alokasi(12); insertFirst(&L, P4); 
    P5 = alokasi(9); insertFirst(&L, P5); 
    
    deleteFirst(&L, &Pdel);
    dealokasi(Pdel); 

    deleteLast(&L, &Pdel);
    dealokasi(Pdel);

    address Prec_for_8 = L.First;
    if (Prec_for_8 != NULL) {
        deleteAfter(&L, &Pdel, Prec_for_8);
        dealokasi(Pdel);
    }

    printInfo(L);
    cout << "Jumlah node : " << nbList(L) << endl;

    cout << "\n- List Berhasil Terhapus -" << endl;
    deleteList(&L);
    cout << "Jumlah node : " << nbList(L) << endl;

    return 0;
}
```
#### Output:
<img width="493" height="129" alt="Image" src="https://github.com/user-attachments/assets/75d59b22-ac82-4d7e-ac43-0e69d78f42e3" />

Program diatas fungsinya untuk mengimplementasikan dan menguji operasi dasar dari struktur data ADT.

#### Full code Screenshot:
<img width="519" height="649" alt="Image" src="https://github.com/user-attachments/assets/5cb6beef-1510-4534-b24d-10bff3add595" />
<img width="468" height="961" alt="Image" src="https://github.com/user-attachments/assets/7f145506-4520-475f-8a71-84b8ae159af1" />
<img width="501" height="909" alt="Image" src="https://github.com/user-attachments/assets/a75eba00-0bb6-44d6-bc73-ea4b6176117a" />
<img width="473" height="819" alt="Image" src="https://github.com/user-attachments/assets/8e98c893-fbe6-477d-9416-cb448d63c877" />

## Kesimpulan

Kesimpulan nya adalah bahwa program ini berhasil mengimplementasikan ADT (Abstract Data Type) Singly Linked List dan menguji fungsionalitas CRUD (Create, Read, Update, Delete) untuk struktur data tersebut.

## Referensi
[1] Cormen, T. H., Leiserson, C. E., Rivest, R. L., & Stein, C. (2022). Introduction to algorithms (4th ed.). MIT Press.














