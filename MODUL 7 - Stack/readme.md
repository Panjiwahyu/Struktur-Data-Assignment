# <h1 align="center">Laporan Praktikum Stack</h1>
<p align="center">Panji Wahyu Nugroho</p>

## Dasar Teori

Stack merupakan salah satu struktur data linear yang bekerja dengan prinsip LIFO (Last In First Out), 
yaitu elemen yang terakhir dimasukkan ke dalam stack akan menjadi elemen pertama yang dikeluarkan.

## Guided 

### 1. [Stack]

```C++
//Stack.h
#ifndef STACK_TABLE
#define STACK_TABLE

#include <iostream>
using namespace std;

//ubah kapasitas sesuai kebutuhan
const int MAX = 10;

struct stackTable{
    int data[MAX];
    int top; // -1 = kosong

};

bool isEmpty(stackTable s);
bool isFull(stackTable s);
void createStack(stackTable &s);

void push(stackTable &s, int angka);
void pop(stackTable &s);
void update(stackTable &s, int posisi);
void view(stackTable s);
void searchData(stackTable s, int data);

#endif

//Stack.cpp
#include "stack.h"
#include <iostream>

using namespace std;

bool isEmpty(stackTable s) {
    return s.top == -1;
}

bool isFull(stackTable s){
    return s.top == MAX -1;
}

void createStack(stackTable &s) {
    s.top = -1;
}

void push(stackTable &s, int angka){
    if(isFull(s)){
        cout << "Stack Penuh!" << endl;
    } else {
        s.top++;
        s.data[s.top] = angka;
        cout << "Data " << angka << " berhasil ditambahkan kedalam stack!" << endl;
    }
}

void pop(stackTable &s){
    if(isEmpty(s)){
        cout << "Stack kosong!" << endl;
    } else {
        int val = s.data[s.top];
        s.top--;
        cout << "Data " << val << " Berhasil dihapus dari stack!" << endl;
    }
}

void update(stackTable &s, int posisi){
    if(isEmpty(s)){
        cout << "Stack kosong!" << endl;
        return;
    }
    if(posisi <= 0){
        cout << "Posisi tidak valid!" << endl;
        return;
    }

    //index = top - (posisi -1)
    int idx = s.top - (posisi -1);
    if(idx < 0 || idx > s.top){
        cout << "Posisi " << posisi << " Tidak valid!" << endl;
        return;
    }

    cout << "Update data posisi ke-" << posisi << endl;
    cout << "Masukkan angka: ";
    cin >> s.data[idx];
    cout << "Data berhasil diupdate!" << endl;
    cout << endl;
}

void view(stackTable s){
    if(isEmpty(s)){
        cout << "Stack Kosong!" << endl;
    } else {
        for(int i = s.top; i >= 0; --i){
            cout << s.data[i] << " ";
        }
    }
    cout << endl;
}

void searchData(stackTable s, int data){
    if(isEmpty(s)){
        cout << "Stack Kosong!" << endl;
        return;
    }
    cout << "Mencari data" << data << "..." << endl;
    int posisi = 1;
    bool found = false;

    for(int i = s.top; i >= 0; --i){
        if(s.data[i] == data){
            cout << "Data " << data << " ditemukan pada posisi ke-" << posisi << endl;
            cout << endl;
            found = true;
            break;
        }
        posisi++;
    }

    if(!found){
        cout << "Data " << data << " tidak ditemukan didalam stack!" << endl;
        cout << endl;
    }
}

//main.c
#include "stack.h"
#include <iostream>

using namespace std;

int main(){
    stackTable s;
    createStack(s);

    push(s, 1);
    push(s, 2);
    push(s, 3);
    push(s, 4);
    push(s, 5);
    cout << endl;

    cout << "--- Stack setelah push ---" << endl;
    view(s);
    cout << endl;

    pop(s);
    pop(s);
    cout << endl;

    cout << "--- Stack setelah pop 2 kali ---" << endl;
    view(s);
    cout << endl;

    //Posisi dihitung dari TOP(1-based)
    update(s, 2);
    update(s, 1);
    update(s, 4);
    cout << endl;

    cout << "--- Stack setelah update ---" << endl;
    view(s);
    cout << endl;

    searchData(s, 4);
    searchData(s, 9);

    return 0;
}
```
Kode di atas digunakan untuk mengimplementasikan struktur data Stack berbasis array (stack statis) beserta operasi-operasi dasarnya.

## Unguided 

### 1. 

```C++
//stack.h
#ifndef STACK_H
#define STACK_H

const int MAX = 20;

struct Stack {
    int data[MAX];
    int top;
};

void createStack(Stack &S);
void push(Stack &S, int x);
int pop(Stack &S);
void printInfo(Stack S);
void balikStack(Stack &S);
void getInputStream(Stack &S);

#endif

//stack.cpp
#include <iostream>
#include "stack.h"
using namespace std;

void createStack(Stack &S) {
    S.top = -1;
}

void push(Stack &S, int x) {
    if (S.top < MAX - 1) {
        S.top++;
        S.data[S.top] = x;
    }
}

int pop(Stack &S) {
    if (S.top >= 0) {
        int value = S.data[S.top];
        S.top--;
        return value;
    }
    return -1;
}

void printInfo(Stack S) {
    cout << "[TOP] ";
    for (int i = S.top; i >= 0; i--) {
        cout << S.data[i] << " ";
    }
    cout << endl;
}

void balikStack(Stack &S) {
    Stack temp;
    createStack(temp);

    while (S.top >= 0) {
        push(temp, pop(S));
    }

    S = temp;
}

void getInputStream(Stack &S) {
    string input = "4729601"; 
    cout << input << endl;

    for (char ch : input) {
        push(S, ch - '0');
    }
}

//main.cpp
#include <iostream>
#include "stack.h"
using namespace std;

int main() {
    cout << "Hello Word" << endl;  

    Stack S;
    createStack(S);

    getInputStream(S);  
    printInfo(S);

    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);

    return 0;
}

```
#### Output:
<img width="490" height="192" alt="Image" src="https://github.com/user-attachments/assets/7900d189-427c-4255-ba9a-961269c42e06" />

Program di atas digunakan untuk mengimplementasikan dan mendemonstrasikan struktur data Stack berbasis array dengan 
beberapa operasi dasar termasuk pembalikan isi stack (reverse stack).

#### Full code Screenshot:
<img width="403" height="508" alt="Image" src="https://github.com/user-attachments/assets/7e7b87de-69d1-45af-8ee6-1f5d270d53d1" />
<img width="313" height="892" alt="Image" src="https://github.com/user-attachments/assets/ad2cd84e-ca6d-42ad-b9f1-d7dbcedb4647" />
<img width="448" height="532" alt="Image" src="https://github.com/user-attachments/assets/4304be51-5391-42df-a495-a5b861db5f3d" />

## Kesimpulan

Berdasarkan implementasi program, dapat disimpulkan bahwa struktur data stack berbasis 
array mampu menyimpan dan memanipulasi data secara efektif menggunakan prinsip LIFO.

## Referensi
[1] Cormen, T. H., Leiserson, C. E., Rivest, R. L., & Stein, C. (2022). Introduction to algorithms (4th ed.). MIT Press.




















