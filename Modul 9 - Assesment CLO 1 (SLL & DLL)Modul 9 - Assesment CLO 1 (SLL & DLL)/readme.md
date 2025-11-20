```C++
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
    ```C
    //DLLPLAYLIST.CPP
    #include "DLLPlaylist.h"

Song createSong(std::string title, std::string artist, int duration, int playCount, float rating) {
    return {title, artist, duration, playCount, rating};
}

void createList(List& L) {
    L.head = nullptr;
    L.tail = nullptr;
}

bool isEmpty(List L) {
    return L.head == nullptr;
}

address allocate(Song S) {
    address P = new Node;
    P->info = S;
    P->prev = nullptr;
    P->next = nullptr;
    return P;
}

void deallocate(address& P) {
    delete P;
    P = nullptr;
}

void insertFirst(List& L, Song S) {
    address P = allocate(S);
    if (isEmpty(L)) {
        L.head = L.tail = P;
    } else {
        P->next = L.head;
        L.head->prev = P;
        L.head = P;
    }
}

void insertLast(List& L, Song S) {
    address P = allocate(S);
    if (isEmpty(L)) {
        L.head = L.tail = P;
    } else {
        P->prev = L.tail;
        L.tail->next = P;
        L.tail = P;
    }
}

void insertBefore(List& L, address Q, Song S) {
    if (Q == nullptr) return;

    if (Q == L.head) {
        insertFirst(L, S);
    } else {
        address P = allocate(S);
        P->next = Q;
        P->prev = Q->prev;
        Q->prev->next = P;
        Q->prev = P;
    }
}

void insertAfter(List& L, address Q, Song S) {
    if (Q == nullptr) return;

    if (Q == L.tail) {
        insertLast(L, S);
    } else {
        address P = allocate(S);
        P->prev = Q;
        P->next = Q->next;
        Q->next->prev = P;
        Q->next = P;
    }
}

void deleteFirst(List& L, Song& S) {
    if (isEmpty(L)) return;

    address P = L.head;
    S = P->info;
    
    if (L.head == L.tail) {
        L.head = L.tail = nullptr;
    } else {
        L.head = P->next;
        L.head->prev = nullptr;
    }
    P->next = nullptr; 
    deallocate(P);
}

void deleteLast(List& L, Song& S) {
    if (isEmpty(L)) return;

    address P = L.tail;
    S = P->info;

    if (L.head == L.tail) {
        L.head = L.tail = nullptr;
    } else {
        L.tail = P->prev;
        L.tail->next = nullptr;
    }
    P->prev = nullptr;
    deallocate(P);
}

void deleteBefore(List& L, address Q, Song& S) {
    if (Q == nullptr || Q == L.head) return; 

    address P = Q->prev;
    if (P == L.head) {
        deleteFirst(L, S);
    } else {
        S = P->info;
        P->prev->next = Q;
        Q->prev = P->prev;
        P->prev = nullptr;
        P->next = nullptr; 
        deallocate(P);
    }
}

void deleteAfter(List& L, address Q, Song& S) {
    if (Q == nullptr || Q == L.tail) return; 

    address P = Q->next;
    if (P == L.tail) {
        deleteLast(L, S);
    } else {
        S = P->info;
        Q->next = P->next;
        P->next->prev = Q;
        P->prev = nullptr;
        P->next = nullptr;
        deallocate(P);
    }
}

address search(List L, std::string title, std::string artist) {
    address P = L.head;
    while (P != nullptr) {
        if (P->info.Title == title && P->info.Artist == artist) {
            return P;
        }
        P = P->next;
    }
    return nullptr;
}

address searchNodeByPosition(List L, int posisi) {
    if (posisi <= 0) return nullptr;
    
    address P = L.head;
    int counter = 1;
    while (P != nullptr && counter < posisi) {
        P = P->next;
        counter++;
    }
    return P;
}

void updateAtPosition(List& L, int posisi, Song S) {
    address P = searchNodeByPosition(L, posisi);
    if (P != nullptr) {
        P->info = S;
    } else {
        std::cout << "\n[!] Gagal Update: Posisi " << posisi << " tidak valid." << std::endl;
    }
}

void updateBefore(List& L, address Q, Song S) {
    if (Q == nullptr || Q == L.head) {
        std::cout << "\n[!] Gagal UpdateBefore: Q nullptr atau Q adalah Head." << std::endl;
        return;
    }

    address P = Q->prev;
    P->info = S;
    std::cout << "\n[*] Berhasil Update data lagu sebelum node posisi Q (" << Q->info.Title << ")." << std::endl;
}

float calculatePopularityScore(Song S) {
    return (0.8 * S.PlayCount) + (20.0 * S.Rating);
}

void viewList(List L) {
    std::cout << "\n\n=== Isi Playlist ===" << std::endl;
    if (isEmpty(L)) {
        std::cout << "[Kosong]" << std::endl;
        return;
    }

    address P = L.head;
    int posisi = 1;

    std::cout << std::left << std::setw(6) << "Pos"
              << std::setw(25) << "Title"
              << std::setw(15) << "Artist"
              << std::setw(10) << "Score"
              << std::endl;
    std::cout << std::string(56, '-') << std::endl;

    while (P != nullptr) {
        float score = calculatePopularityScore(P->info);
        std::cout << std::left << std::setw(6) << posisi
                  << std::setw(25) << P->info.Title
                  << std::setw(15) << P->info.Artist
                  << std::setw(10) << std::fixed << std::setprecision(2) << score
                  << std::endl;
        P = P->next;
        posisi++;
    }
    std::cout << "====================" << std::endl;
}

void searchByPopularityRange(List L, float minScore, float maxScore) {
    std::cout << "\n\n=== Hasil Search (Score " << std::fixed << std::setprecision(2) << minScore << " - " << maxScore << ") ===" << std::endl;
    if (isEmpty(L)) {
        std::cout << "[Playlist Kosong]" << std::endl;
        return;
    }

    address P = L.head;
    int posisi = 1;
    bool found = false;

    std::cout << std::left << std::setw(6) << "Pos"
              << std::setw(25) << "Title"
              << std::setw(15) << "Artist"
              << std::setw(10) << "Score"
              << std::endl;
    std::cout << std::string(56, '-') << std::endl;

    while (P != nullptr) {
        float score = calculatePopularityScore(P->info);
        if (score >= minScore && score <= maxScore) {
            std::cout << std::left << std::setw(6) << posisi
                      << std::setw(25) << P->info.Title
                      << std::setw(15) << P->info.Artist
                      << std::setw(10) << std::fixed << std::setprecision(2) << score
                      << std::endl;
            found = true;
        }
        P = P->next;
        posisi++;
    }

    if (!found) {
        std::cout << "[Tidak ada lagu dalam rentang skor tersebut]" << std::endl;
    }
    std::cout << "=======================================================" << std::endl;
}

//DLLPLAYLIST.H
#ifndef DLLPLAYLIST_H
#define DLLPLAYLIST_H

#include <iostream>
#include <string>
#include <iomanip>

typedef struct {
    std::string Title;
    std::string Artist;
    int DurationSec;
    int PlayCount;
    float Rating;
} Song;

Song createSong(std::string title, std::string artist, int duration, int playCount, float rating);

typedef struct Node* address;

typedef struct Node {
    Song info;
    address prev;
    address next;
} Node;

typedef struct {
    address head;
    address tail;
} List;

void createList(List& L);
bool isEmpty(List L);
address allocate(Song S);
void deallocate(address& P);

void insertFirst(List& L, Song S);
void insertLast(List& L, Song S);
void insertBefore(List& L, address Q, Song S);
void insertAfter(List& L, address Q, Song S);

void deleteFirst(List& L, Song& S);
void deleteLast(List& L, Song& S);
void deleteBefore(List& L, address Q, Song& S);
void deleteAfter(List& L, address Q, Song& S);

address search(List L, std::string title, std::string artist);
address searchNodeByPosition(List L, int posisi);

void updateAtPosition(List& L, int posisi, Song S);
void updateBefore(List& L, address Q, Song S);

float calculatePopularityScore(Song S);
void viewList(List L);
void searchByPopularityRange(List L, float minScore, float maxScore);

#endif

//MAIN.CPP
#include "DLLPlaylist.h"

int main() {
    List L;
    Song tempSong;

    Song lagu1 = createSong("Senja di Kota", "Nona Band", 210, 150, 4.2);
    Song lagu2 = createSong("Langkahmu", "Delta", 185, 320, 4.8);
    Song lagu3 = createSong("Hujan Pagi", "Arka", 240, 90, 3.9);

    Song updateSong = createSong("Pelita", "Luna", 200, 260, 4.5);
    Song insertSong = createSong("Senandung", "Mira", 175, 120, 4.0);
    Song updateBeforeSong = createSong("Rindu", "Rana", 190, 100, 4.1);

    std::cout << "1. Membuat list kosong (createList)..." << std::endl;
    createList(L);
    viewList(L);

    std::cout << "\n2. Masukkan 3 lagu menggunakan insertLast..." << std::endl;
    insertLast(L, lagu1);
    insertLast(L, lagu2);
    insertLast(L, lagu3);

    std::cout << "\n3. Tampilkan list setelah 3x insertLast." << std::endl;
    viewList(L);

    std::cout << "\n4. Lakukan deleteLast sebanyak 1x..." << std::endl;
    deleteLast(L, tempSong);
    std::cout << "[*] Lagu yang dihapus: " << tempSong.Title << " oleh " << tempSong.Artist << std::endl;

    std::cout << "\n   Tampilkan list setelah deleteLast." << std::endl;
    viewList(L);

    std::cout << "\n5. Update node pada posisi ke-2 (Lagu 'Langkahmu')..." << std::endl;
    updateAtPosition(L, 2, updateSong);
    std::cout << "[*] Node posisi 2 diupdate menjadi: " << updateSong.Title << std::endl;

    std::cout << "\n6. Tampilkan list setelah update." << std::endl;
    viewList(L);

    address Q_posisi2 = searchNodeByPosition(L, 2);
    if (Q_posisi2 == nullptr) return 1;

    std::cout << "\n7. Operasi BEFORE (menggunakan Q = node posisi ke-2: " << Q_posisi2->info.Title << ")" << std::endl;

    std::cout << "\na. insertBefore lagu 'Senandung' sebelum node posisi 2 ('Pelita')." << std::endl;
    insertBefore(L, Q_posisi2, insertSong);

    std::cout << "\n   Tampilkan list setelah insertBefore." << std::endl;
    viewList(L);

    std::cout << "\nb. updateBefore pada node posisi 2 (update node sebelum 'Pelita' menjadi 'Rindu')." << std::endl;
    updateBefore(L, Q_posisi2, updateBeforeSong);

    std::cout << "\n   Tampilkan list setelah updateBefore." << std::endl;
    viewList(L);

    address Q_posisi3 = searchNodeByPosition(L, 3);
    if (Q_posisi3 != nullptr) {
        std::cout << "\nc. deleteBefore pada node posisi 3 ('Pelita'). Menghapus node posisi 2 ('Rindu')." << std::endl;
        deleteBefore(L, Q_posisi3, tempSong);
        std::cout << "[*] Lagu yang dihapus: " << tempSong.Title << " oleh " << tempSong.Artist << std::endl;
    }

    std::cout << "\n   Tampilkan list setelah deleteBefore." << std::endl;
    viewList(L);
    
    float min = 150.0;
    float max = 300.0;
    std::cout << "\n8. Searching berdasarkan PopularityScore (min=" << min << ", max=" << max << ")" << std::endl;
    searchByPopularityRange(L, min, max);

    return 0;
}

//OUTPUT
<img width="472" height="865" alt="image" src="https://github.com/user-attachments/assets/333bca10-4eba-4e10-8ddc-3e99bc1365eb" />
<img width="671" height="956" alt="image" src="https://github.com/user-attachments/assets/f916125e-06ac-43b3-b3d6-82828345ba99" />

SOAL 3

//MAIN.CPP
#include "StackMahasiswa.h"

int main() {
    StackMHS S;
    Mahasiswa tempMHS;

    Mahasiswa mhs1 = createMahasiswa("Venti", "11111", 75.7, 82.1, 65.5);
    Mahasiswa mhs2 = createMahasiswa("Xiao", "22222", 87.4, 88.9, 81.9);
    Mahasiswa mhs3 = createMahasiswa("Kazuha", "33333", 92.3, 88.8, 82.4);
    Mahasiswa mhs4 = createMahasiswa("Wanderer", "44444", 95.5, 85.5, 90.5);
    Mahasiswa mhs5 = createMahasiswa("Lynette", "55555", 77.7, 65.4, 79.9);
    Mahasiswa mhs6 = createMahasiswa("Chasca", "66666", 99.9, 93.6, 87.3);

    Mahasiswa updateMHS = createMahasiswa("Heizou", "77777", 99.9, 88.8, 77.7);

    std::cout << "1) Membuat Stack Kosong..." << std::endl;
    createStack(S);

    std::cout << "\n2) Melakukan Push 6 data Mahasiswa..." << std::endl;
    Push(S, mhs1);
    Push(S, mhs2);
    Push(S, mhs3);
    Push(S, mhs4);
    Push(S, mhs5);
    Push(S, mhs6);

    std::cout << "\n3) Tampilkan Stack setelah input 6 data." << std::endl;
    View(S);

    std::cout << "\n4) Melakukan Pop sebanyak 1x..." << std::endl;
    Pop(S, tempMHS);
    std::cout << "[*] Data yang di Pop: " << tempMHS.Nama << " (NIM: " << tempMHS.NIM << ")" << std::endl;

    std::cout << "\n5) Tampilkan Stack setelah Pop 1x." << std::endl;
    View(S);

    std::cout << "\n6) Update data pada posisi ke-3 (Posisi 3 saat ini adalah Kazuha)..." << std::endl;
    Update(S, 3, updateMHS);

    std::cout << "\n7) Tampilkan Stack setelah Update." << std::endl;
    View(S);

    float min = 85.5;
    float max = 95.5;
    std::cout << "\n8) Searching data mahasiswa dengan Nilai Akhir dalam rentang " << min << " - " << max << std::endl;
    SearchNilaiAkhir(S, min, max);

    std::cout << "\n=== Bagian B: Menampilkan Nilai Akhir Maksimum ===" << std::endl;
    MaxNilaiAkhir(S);

    return 0;
}
//STACKMAHASISWA.CPP
#include "StackMahasiswa.h"

float hitungNilaiAkhir(Mahasiswa M) {
    return (0.20 * M.NilaiTugas) + (0.40 * M.NilaiUTS) + (0.40 * M.NilaiUAS);
}

Mahasiswa createMahasiswa(std::string nama, std::string nim, float tugas, float uts, float uas) {
    return {nama, nim, tugas, uts, uas};
}

bool isEmpty(StackMHS S) {
    return S.Top == -1;
}

bool isFull(StackMHS S) {
    return S.Top == MAX - 1;
}

void createStack(StackMHS& S) {
    S.Top = -1;
}

void Push(StackMHS& S, Mahasiswa M) {
    if (isFull(S)) {
        std::cout << "[!] Stack Penuh. Push Gagal." << std::endl;
        return;
    }
    S.Top++;
    S.dataMahasiswa[S.Top] = M;
}

void Pop(StackMHS& S, Mahasiswa& M) {
    if (isEmpty(S)) {
        std::cout << "[!] Stack Kosong. Pop Gagal." << std::endl;
        return;
    }
    M = S.dataMahasiswa[S.Top];
    S.Top--;
}

void Update(StackMHS& S, int posisi, Mahasiswa M) {
    if (posisi < 1 || posisi > S.Top + 1) {
        std::cout << "[!] Posisi Update tidak valid." << std::endl;
        return;
    }
    
    int index = (S.Top + 1) - posisi;
    S.dataMahasiswa[index] = M;
    std::cout << "[*] Data posisi ke-" << posisi << " berhasil diupdate." << std::endl;
}

void View(StackMHS S) {
    std::cout << "\n=== Isi Stack Mahasiswa ===" << std::endl;
    if (isEmpty(S)) {
        std::cout << "[Stack Kosong]" << std::endl;
        return;
    }

    std::cout << "Pos | Nama | NIM | Tugas | UTS | UAS | Akhir" << std::endl;
    std::cout << "-----------------------------------------------" << std::endl;

    for (int i = S.Top; i >= 0; i--) {
        float nilaiAkhir = hitungNilaiAkhir(S.dataMahasiswa[i]);
        int posisi = (S.Top + 1) - i;
        std::cout << posisi << " | "
                  << S.dataMahasiswa[i].Nama << " | "
                  << S.dataMahasiswa[i].NIM << " | "
                  << S.dataMahasiswa[i].NilaiTugas << " | "
                  << S.dataMahasiswa[i].NilaiUTS << " | "
                  << S.dataMahasiswa[i].NilaiUAS << " | "
                  << nilaiAkhir
                  << std::endl;
    }
    std::cout << "===========================" << std::endl;
}

void SearchNilaiAkhir(StackMHS S, float NilaiAkhirMin, float NilaiAkhirMax) {
    std::cout << "\n=== Hasil Search (Akhir: " << NilaiAkhirMin << " - " << NilaiAkhirMax << ") ===" << std::endl;
    if (isEmpty(S)) {
        std::cout << "[Stack Kosong]" << std::endl;
        return;
    }

    bool found = false;
    std::cout << "Pos | Nama | NIM | Nilai Akhir" << std::endl;
    std::cout << "--------------------------------" << std::endl;

    for (int i = S.Top; i >= 0; i--) {
        float nilaiAkhir = hitungNilaiAkhir(S.dataMahasiswa[i]);
        if (nilaiAkhir >= NilaiAkhirMin && nilaiAkhir <= NilaiAkhirMax) {
            int posisi = (S.Top + 1) - i;
            std::cout << posisi << " | "
                      << S.dataMahasiswa[i].Nama << " | "
                      << S.dataMahasiswa[i].NIM << " | "
                      << nilaiAkhir
                      << std::endl;
            found = true;
        }
    }

    if (!found) {
        std::cout << "[Tidak ada data dalam rentang nilai akhir tersebut]" << std::endl;
    }
    std::cout << "=================================================" << std::endl;
}

void MaxNilaiAkhir(StackMHS S) {
    if (isEmpty(S)) {
        std::cout << "\n[!] Stack Kosong. Tidak dapat mencari nilai maksimum." << std::endl;
        return;
    }

    float maxNilai = -1.0;
    int maxIndex = -1;

    for (int i = 0; i <= S.Top; i++) {
        float nilaiAkhir = hitungNilaiAkhir(S.dataMahasiswa[i]);
        if (nilaiAkhir > maxNilai) {
            maxNilai = nilaiAkhir;
            maxIndex = i;
        }
    }

    int posisi = (S.Top + 1) - maxIndex;
    Mahasiswa M = S.dataMahasiswa[maxIndex];

    std::cout << "\n=== Mahasiswa dengan Nilai Akhir Terbesar ===" << std::endl;
    std::cout << "Nama           : " << M.Nama << std::endl;
    std::cout << "NIM            : " << M.NIM << std::endl;
    std::cout << "Nilai Akhir    : " << maxNilai << std::endl;
    std::cout << "Posisi di Stack: " << posisi << std::endl;
    std::cout << "==============================================" << std::endl;
}
//STACKMAHASISWA.H
#ifndef STACKMAHASISWA_H
#define STACKMAHASISWA_H

#include <iostream>
#include <string>

const int MAX = 6;

typedef struct {
    std::string Nama;
    std::string NIM;
    float NilaiTugas;
    float NilaiUTS;
    float NilaiUAS;
} Mahasiswa;

Mahasiswa createMahasiswa(std::string nama, std::string nim, float tugas, float uts, float uas);

typedef struct {
    Mahasiswa dataMahasiswa[MAX];
    int Top;
} StackMHS;

bool isEmpty(StackMHS S);
bool isFull(StackMHS S);
void createStack(StackMHS& S);
void Push(StackMHS& S, Mahasiswa M);
void Pop(StackMHS& S, Mahasiswa& M);
void Update(StackMHS& S, int posisi, Mahasiswa M);
void View(StackMHS S);
void SearchNilaiAkhir(StackMHS S, float NilaiAkhirMin, float NilaiAkhirMax);
void MaxNilaiAkhir(StackMHS S);

#endif
//OUTPUT
<img width="561" height="647" alt="image" src="https://github.com/user-attachments/assets/6fbaf6b8-c105-41ba-9ba3-0f4fae0366ab" />
<img width="588" height="573" alt="image" src="https://github.com/user-attachments/assets/4466a076-4daf-4041-806d-e030393a479f" />

SOAL 4
//MAIN.CPP
#include "QueuePengiriman.h"

void inputDataPaket(QueueEkspedisi& Q) {
    std::cout << "\nInput 5 data paket (EnQueue):" << std::endl;

    Paket p1 = createPaket("123456", "Hutao", 14, "Sumeru");
    Paket p2 = createPaket("234567", "Ayaka", 10, "Fontaine");
    Paket p3 = createPaket("345678", "Bennet", 7, "Natlan");
    Paket p4 = createPaket("456789", "Furina", 16, "Liyue");
    Paket p5 = createPaket("567890", "Nefer", 6, "Inazuma");

    enQueue(Q, p1);
    enQueue(Q, p2);
    enQueue(Q, p3);
    enQueue(Q, p4);
    enQueue(Q, p5);
    
    std::cout << "5 Paket berhasil di-EnQueue." << std::endl;
}

int main() {
    QueueEkspedisi Q;
    Paket tempPaket;
    int pilihan;

    std::cout << "1) Membuat Queue Kosong (createQueue)..." << std::endl;
    createQueue(Q);

    do {
        std::cout << "\nKomaniya Ekspress" << std::endl;
        std::cout << "1. Input Data Paket" << std::endl;
        std::cout << "2. Proses Data Paket (Dequeue)" << std::endl;
        std::cout << "3. Tampilkan queue paket" << std::endl;
        std::cout << "4. Hitung Total Biaya Pengiriman" << std::endl;
        std::cout << "5. Keluar" << std::endl;
        std::cout << "Pilihan anda: ";
        std::cin >> pilihan;

        switch (pilihan) {
            case 1:
                inputDataPaket(Q);
                break;
            case 2:
                std::cout << "\n5) Lakukan deQueue sebanyak 1x..." << std::endl;
                deQueue(Q, tempPaket);
                std::cout << "Paket yang diproses (DeQueue): Resi " << tempPaket.KodeResi << " dari " << tempPaket.NamaPengirim << std::endl;
                
                std::cout << "\n6) Tampilkan queue setelah DeQueue 1x." << std::endl;
                viewQueue(Q);
                break;
            case 3:
                std::cout << "\n4) Tampilkan queue yang sudah diinput data paket." << std::endl;
                viewQueue(Q);
                break;
            case 4:
                {
                    int totalBiaya = TotalBiayaPengiriman(Q);
                    std::cout << "\nTotal Biaya Pengiriman semua paket di antrian: Rp " << totalBiaya << std::endl;
                }
                break;
            case 5:
                std::cout << "Keluar dari program." << std::endl;
                break;
            default:
                std::cout << "Pilihan tidak valid." << std::endl;
        }
    } while (pilihan != 5);

    return 0;
}
//QUEUEPENGIRIMAN.CPP
#include "QueuePengiriman.h"

Paket createPaket(std::string resi, std::string pengirim, int berat, std::string tujuan) {
    return {resi, pengirim, berat, tujuan};
}

bool isEmpty(QueueEkspedisi Q) {
    return Q.Tail == -1;
}

bool isFull(QueueEkspedisi Q) {
    return Q.Tail == MAX - 1;
}

void createQueue(QueueEkspedisi& Q) {
    Q.Head = 0;
    Q.Tail = -1;
}

void enQueue(QueueEkspedisi& Q, Paket P) {
    if (isFull(Q)) {
        std::cout << "Antrian Penuh. EnQueue gagal." << std::endl;
        return;
    }
    Q.Tail++;
    Q.dataPaket[Q.Tail] = P;
}

void deQueue(QueueEkspedisi& Q, Paket& P) {
    if (isEmpty(Q)) {
        std::cout << "Antrian Kosong. DeQueue gagal." << std::endl;
        return;
    }

    P = Q.dataPaket[Q.Head];

    for (int i = Q.Head; i < Q.Tail; i++) {
        Q.dataPaket[i] = Q.dataPaket[i + 1];
    }
    
    Q.Tail--;

    if (Q.Tail == -1) {
        Q.Head = 0;
    }
}

void viewQueue(QueueEkspedisi Q) {
    std::cout << "\nIsi Antrian Paket (Komaniya Ekspress)" << std::endl;
    if (isEmpty(Q)) {
        std::cout << "[Antrian Kosong]" << std::endl;
        return;
    }

    std::cout << "Indeks | Resi | Pengirim | Berat(kg) | Tujuan" << std::endl;
    std::cout << "0 | Head (Keluar)" << std::endl;

    for (int i = Q.Head; i <= Q.Tail; i++) {
        std::cout << i << " | "
                  << Q.dataPaket[i].KodeResi << " | "
                  << Q.dataPaket[i].NamaPengirim << " | "
                  << Q.dataPaket[i].BeratBarang << " | "
                  << Q.dataPaket[i].Tujuan;
        
        if (i == Q.Tail) {
            std::cout << " | Tail (Masuk)";
        }
        std::cout << std::endl;
    }
}

int TotalBiayaPengiriman(QueueEkspedisi Q) {
    if (isEmpty(Q)) {
        return 0;
    }

    int totalBerat = 0;
    for (int i = Q.Head; i <= Q.Tail; i++) {
        totalBerat += Q.dataPaket[i].BeratBarang;
    }

    return totalBerat * BIAYA_PER_KG;
}
//QUEUEPENGIRIMAN.H
#ifndef QUEUEPENGIRIMAN_H
#define QUEUEPENGIRIMAN_H

#include <iostream>
#include <string>

const int MAX = 5;
const int BIAYA_PER_KG = 8250;

typedef struct {
    std::string KodeResi;
    std::string NamaPengirim;
    int BeratBarang;
    std::string Tujuan;
} Paket;

typedef struct {
    Paket dataPaket[MAX];
    int Head;
    int Tail;
} QueueEkspedisi;

Paket createPaket(std::string resi, std::string pengirim, int berat, std::string tujuan);

bool isEmpty(QueueEkspedisi Q);
bool isFull(QueueEkspedisi Q);
void createQueue(QueueEkspedisi& Q);
void enQueue(QueueEkspedisi& Q, Paket P);
void deQueue(QueueEkspedisi& Q, Paket& P);
void viewQueue(QueueEkspedisi Q);
int TotalBiayaPengiriman(QueueEkspedisi Q);

#endif
//OUTPUT
<img width="454" height="797" alt="image" src="https://github.com/user-attachments/assets/93613294-82b6-40ae-857f-2a72fdf014da" />
<img width="463" height="527" alt="image" src="https://github.com/user-attachments/assets/89b81e8f-340f-4d95-8778-402fb160e185" />

```
    


