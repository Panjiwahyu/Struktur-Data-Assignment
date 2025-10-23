# <h1 align="center">Laporan Praktikum Singly Linked List (Bagian Pertama)</h1>
<p align="center">Panji Wahyu Nugroho</p>

## Dasar Teori


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
Kode di atas digunakan untuk menginput dan menghitung rata-rata nilai mahasiswa menggunakan Abstract Data Type (ADT).

## Unguided 

### 1. 

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
<img width="429" height="515" alt="Image" src="https://github.com/user-attachments/assets/5ed94911-3d15-43d7-a745-14b66512424b" />

Program di atas digunakan untuk menyimpan dan menghitung data nilai mahasiswa (maksimal 10 orang).

#### Full code Screenshot:
<img width="509" height="814" alt="Image" src="https://github.com/user-attachments/assets/e0c776ee-bd6e-4250-b348-d0b3dbaba50b" />

### 2.

```C++
//pelajaran.h
#ifndef PELAJARAN_H
#define PELAJARAN_H
#include <string>
using namespace std;

struct pelajaran {
    string namaMapel;
    string kodeMapel;
};

pelajaran create_pelajaran(string nama, string kode);
void tampil_pelajaran(pelajaran pel);

#endif

//pelajaran.cpp
#include <iostream>
#include "pelajaran.h"
using namespace std;

pelajaran create_pelajaran(string nama, string kode) {
    pelajaran p;
    p.namaMapel = nama;
    p.kodeMapel = kode;
    return p;
}

void tampil_pelajaran(pelajaran pel) {
    cout << "nama pelajaran : " << pel.namaMapel << endl;
    cout << "nilai : " << pel.kodeMapel << endl;
}

//Main.cpp
#include <iostream>
#include "pelajaran.h"
using namespace std;

int main() {
    string namaPel = "Struktur Data";
    string kodePel = "STD";

    pelajaran pel = create_pelajaran(namaPel, kodePel);
    tampil_pelajaran(pel);

    return 0;
}
```
#### Output:
<img width="301" height="169" alt="Image" src="https://github.com/user-attachments/assets/fa4e429c-be0d-458d-97f4-12e40f7339a3" />

Program diatas fungsinya untuk membuat dan menampilkan data mata pelajaran menggunakan konsep ADT.

#### Full code Screenshot:
<img width="594" height="373" alt="Image" src="https://github.com/user-attachments/assets/4e941211-4bae-485b-8976-e1005bcdba39" />
<img width="627" height="393" alt="Image" src="https://github.com/user-attachments/assets/3a281009-8918-4282-94f4-e8d83e777905" />
<img width="604" height="341" alt="Image" src="https://github.com/user-attachments/assets/499d1d2f-6316-45d1-b8f3-8ee34e22f708" />

### 3.
```C++
#include <iostream>
using namespace std;

void tampil(int A[3][3]) {
    for (int i=0;i<3;i++){
        for (int j=0;j<3;j++)
            cout << A[i][j] << "\t";
        cout << endl;
    }
}

void tukarArray(int A[3][3], int B[3][3], int i, int j) {
    int temp = A[i][j];
    A[i][j] = B[i][j];
    B[i][j] = temp;
}

void tukarPointer(int *p1, int *p2) {
    int temp = *p1;
    *p1 = *p2;
    *p2 = temp;
}

int main() {
    int A[3][3]={{1,2,3},{4,5,6},{7,8,9}};
    int B[3][3]={{9,8,7},{6,5,4},{3,2,1}};
    int x=10, y=20, *p1=&x, *p2=&y;

    cout << "Array A awal:\n"; tampil(A);
    cout << "\nArray B awal:\n"; tampil(B);

    tukarArray(A,B,1,1);
    cout << "\nSetelah tukar elemen [1][1]:\n";
    cout << "Array A:\n"; tampil(A);
    cout << "Array B:\n"; tampil(B);

    cout << "\nSebelum tukar pointer: x="<<x<<", y="<<y<<endl;
    tukarPointer(p1,p2);
    cout << "Setelah tukar pointer: x="<<x<<", y="<<y<<endl;
}
```
#### Output:
<img width="489" height="533" alt="Image" src="https://github.com/user-attachments/assets/ec6eede5-fb39-486b-a4ba-b1b5613fc081" />

Program diatas kita diminta untuk membuat program.
Buatlah program dengan ketentuan : 

    - 2 buah array 2D integer berukuran 3x3 dan 2 buah pointer integer 
    
    - fungsi/prosedur yang menampilkan isi sebuah array integer 2D 
    
    - fungsi/prosedur yang akan menukarkan isi dari 2 array integer 2D pada posisi tertentu 
    
    - fungsi/prosedur yang akan menukarkan isi dari variabel yang ditunjuk oleh 2 buah pointer.

#### Full code Screenshot:
<img width="566" height="824" alt="Image" src="https://github.com/user-attachments/assets/02eed818-faf1-4963-8d17-f844404e1d72" />

## Kesimpulan
Ketiga program mengajarkan dasar dasar penting C++ 

— mulai dari penggunaan array, fungsi, struct (ADT), hingga pointer sebagai fondasi logika pemrograman dan pengelolaan data secara efisien.

## Referensi
[1] Schildt, H. (2014). C++: The Complete Reference (4th ed.). McGraw-Hill Education.

[2] Stroustrup, B. (2013). The C++ Programming Language (4th ed.). Addison-Wesley.













