SOAL 1

//MAIN.CPP
#include <iostream>
#include "SLLInventory.h"
using namespace std;

int main() {
    List L;
    createList(L);

    product p1 = {"Pulpen", "A001", 20, 2500, 0};
    product p2 = {"Buku Tulis", "A002", 15, 5000, 10};
    product p3 = {"Penghapus", "A003", 30, 1500, 0};

    insertLast(L, p1);
    insertLast(L, p2);
    insertLast(L, p3);

    cout << "\n=== LIST AWAL ===\n";
    viewList(L);

    node* del;
    deleteFirst(L, del);
    deallocate(del);

    cout << "\n=== LIST SETELAH deleteFirst ===\n";
    viewList(L);

    product updateData = {"Stabilo", "A010", 40, 9000, 5};
    updateAtPosition(L, 2, updateData);

    cout << "\n=== LIST SETELAH UPDATE POSISI KE 2 ===\n";
    viewList(L);

    cout << "\n=== SEARCH HargaAkhir 2000 - 7000 ===\n";
    searchByFinalPriceRange(L, 2000, 7000);

    cout << "\n=== PRODUK DENGAN HARGA AKHIR MAKSIMUM ===\n";
    MaxHargaAkhir(L);

    return 0;
}

//SLLINVENTORY.CPP
#include "SLLInventory.h"

bool isEmpty(List L) {
    return L.head == nullptr;
}

void createList(List &L) {
    L.head = nullptr;
}

node* allocate(product P) {
    node* N = new node;
    N->info = P;
    N->next = nullptr;
    return N;
}

void deallocate(node* &P) {
    delete P;
    P = nullptr;
}

void insertFirst(List &L, product P) {
    node* N = allocate(P);
    N->next = L.head;
    L.head = N;
}

void insertLast(List &L, product P) {
    node* N = allocate(P);
    if (isEmpty(L)) {
        L.head = N;
    } else {
        node* Q = L.head;
        while (Q->next != nullptr) {
            Q = Q->next;
        }
        Q->next = N;
    }
}

void insertAfter(List &L, node* Q, product P) {
    if (Q != nullptr) {
        node* N = allocate(P);
        N->next = Q->next;
        Q->next = N;
    }
}

void deleteFirst(List &L, node* &P) {
    if (!isEmpty(L)) {
        P = L.head;
        L.head = P->next;
        P->next = nullptr;
    } else {
        P = nullptr;
    }
}

void deleteLast(List &L, node* &P) {
    if (isEmpty(L)) {
        P = nullptr;
    } else if (L.head->next == nullptr) {
        P = L.head;
        L.head = nullptr;
    } else {
        node* Q = L.head;
        while (Q->next->next != nullptr) {
            Q = Q->next;
        }
        P = Q->next;
        Q->next = nullptr;
    }
}

void delelteAfter(List &L, node* Q, node* &P) {
    if (Q != nullptr && Q->next != nullptr) {
        P = Q->next;
        Q->next = P->next;
        P->next = nullptr;
    } else {
        P = nullptr;
    }
}

void updateAtPosition(List &L, int posisi, product dataBaru) {
    node* Q = L.head;
    int i = 1;
    while (Q != nullptr && i < posisi) {
        Q = Q->next;
        i++;
    }
    if (Q != nullptr) {
        Q->info = dataBaru;
    }
}

float hargaAkhir(product p) {
    float diskon = p.hargaSatuan * (p.diskonPersen / 100.0f);
    return (p.hargaSatuan - diskon) * p.jumlah;
}

void viewList(List L) {
    node* P = L.head;
    int i = 1;
    while (P != nullptr) {
        cout << i++ << ". " 
             << P->info.Nama << " | SKU: " << P->info.SKU
             << " | Jumlah: " << P->info.jumlah
             << " | Harga Akhir: " << hargaAkhir(P->info)
             << endl;
        P = P->next;
    }
}

void searchByFinalPriceRange(List L, float minp, float maxp) {
    node* P = L.head;
    while (P != nullptr) {
        float h = hargaAkhir(P->info);
        if (h >= minp && h <= maxp) {
            cout << P->info.Nama 
                 << " | Harga Akhir: " << h << endl;
        }
        P = P->next;
    }
}

void MaxHargaAkhir(List L) {
    if (isEmpty(L)) {
        cout << "List kosong\n";
        return;
    }
    node* P = L.head;
    node* maxNode = P;
    while (P != nullptr) {
        if (hargaAkhir(P->info) > hargaAkhir(maxNode->info)) {
            maxNode = P;
        }
        P = P->next;
    }
    cout << "Produk dengan harga akhir tertinggi:\n";
    cout << maxNode->info.Nama 
         << " | Harga Akhir: " << hargaAkhir(maxNode->info) << endl;
}

//SLLINVENTORY.H
    #ifndef SLLINVENTORY_H
    #define SLLINVENTORY_H
    #include <iostream>
    using namespace std;

    struct product {
        string Nama;
        string SKU;
        int jumlah;
        float hargaSatuan;
        float diskonPersen;
    };

    struct node {
        product info;
        node* next;
    };

    struct List {
        node* head;
    };

    bool isEmpty(List L);
    void createList(List &L);
    node* allocate(product P);
    void deallocate(node* &P);
    void insertFirst(List &L, product P);
    void insertLast(List &L, product P);
    void insertAfter(List &L, node* Q, product P);
    void deleteFirst(List &L, node* &P);
    void deleteLast(List &L, node* &P);
    void delelteAfter(List &L, node* Q, node* &P);
    void updateAtPosition(List &L, int posisi, product dataBaru);
    void viewList(List L);
    float hargaAkhir(product p);
    void searchByFinalPriceRange(List l, float minp, float maxp);
    void MaxHargaAkhir(List L);

    #endif  

    //OUTPUT
    <img width="488" height="366" alt="image" src="https://github.com/user-attachments/assets/2451aa8a-53fd-4d58-8853-0be6b5818cff" />

    SOAL 2
    

