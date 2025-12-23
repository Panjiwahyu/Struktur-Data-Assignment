# <h1 align="center">Laporan Praktikum Graph</h1>
<p align="center">Panji Wahyu Nugroho</p>

## Dasar Teori

Graph merupakan struktur data non-linear yang terdiri dari sekumpulan simpul (vertex/node) dan sisi (edge) yang menghubungkan antar simpul. 
Graph digunakan untuk merepresentasikan hubungan antar objek, misalnya jaringan komputer, peta jalan, relasi sosial, atau alur proses.

## Guided 

### 1. [Graph]

```C++

```

## Unguided 

### 1. 

```C++
//graph.h
#ifndef GRAPH_H
#define GRAPH_H

#include <iostream>
using namespace std;

typedef char Info;
typedef struct Node *AdrNode;
typedef struct Edge *AdrEdge;

struct Edge {
    AdrNode tujuan;
    AdrEdge next;
};

struct Node {
    Info data;
    bool visited;
    AdrEdge edge;
    AdrNode next;
};

struct Graph {
    AdrNode head;
};

void initGraph(Graph &G);
void addNode(Graph &G, Info x);
void addEdge(AdrNode a, AdrNode b);
AdrNode searchNode(Graph G, Info x);
void showGraph(Graph G);
void DFS(Graph &G, AdrNode N);
void BFS(Graph &G, AdrNode N);
void resetVisited(Graph &G);

#endif

//graph.cpp
#include "graph.h"

void initGraph(Graph &G) {
    G.head = NULL;
}

AdrNode searchNode(Graph G, Info x) {
    for (AdrNode p = G.head; p != NULL; p = p->next)
        if (p->data == x) return p;
    return NULL;
}

void addNode(Graph &G, Info x) {
    AdrNode n = new Node{x, false, NULL, NULL};
    if (G.head == NULL) {
        G.head = n;
    } else {
        AdrNode p = G.head;
        while (p->next) p = p->next;
        p->next = n;
    }
}

void addEdge(AdrNode a, AdrNode b) {
    AdrEdge e1 = new Edge{b, a->edge};
    a->edge = e1;

    AdrEdge e2 = new Edge{a, b->edge};
    b->edge = e2;
}

void showGraph(Graph G) {
    for (AdrNode p = G.head; p != NULL; p = p->next) {
        cout << p->data << " -> ";
        for (AdrEdge e = p->edge; e != NULL; e = e->next)
            cout << e->tujuan->data << " ";
        cout << endl;
    }
}

void DFS(Graph &G, AdrNode N) {
    if (!N || N->visited) return;
    cout << N->data << " ";
    N->visited = true;

    for (AdrEdge e = N->edge; e != NULL; e = e->next)
        DFS(G, e->tujuan);
}

void BFS(Graph &G, AdrNode start) {
    AdrNode q[50];
    int front = 0, back = 0;

    start->visited = true;
    q[back++] = start;

    while (front < back) {
        AdrNode p = q[front++];
        cout << p->data << " ";

        for (AdrEdge e = p->edge; e != NULL; e = e->next) {
            if (!e->tujuan->visited) {
                e->tujuan->visited = true;
                q[back++] = e->tujuan;
            }
        }
    }
}

void resetVisited(Graph &G) {
    for (AdrNode p = G.head; p != NULL; p = p->next)
        p->visited = false;
}

//main.cpp
#include "graph.h"

int main() {
    Graph G;
    initGraph(G);

    char nodes[] = {'A','B','C','D','E','F','G','H'};
    for (char c : nodes) addNode(G, c);

    addEdge(searchNode(G,'A'), searchNode(G,'B'));
    addEdge(searchNode(G,'A'), searchNode(G,'C'));
    addEdge(searchNode(G,'B'), searchNode(G,'D'));
    addEdge(searchNode(G,'B'), searchNode(G,'E'));
    addEdge(searchNode(G,'C'), searchNode(G,'F'));
    addEdge(searchNode(G,'C'), searchNode(G,'G'));
    addEdge(searchNode(G,'D'), searchNode(G,'H'));
    addEdge(searchNode(G,'E'), searchNode(G,'H'));
    addEdge(searchNode(G,'F'), searchNode(G,'H'));
    addEdge(searchNode(G,'G'), searchNode(G,'H'));

    cout << "DFS : ";
    DFS(G, searchNode(G,'A'));

    resetVisited(G);

    cout << "\nBFS : ";
    BFS(G, searchNode(G,'A'));

    return 0;
}
```
#### Output:
<img width="491" height="125" alt="Image" src="https://github.com/user-attachments/assets/f8f2ba29-fcf5-44ba-becb-208c203047dd" />

Program digunakan untuk mengimplementasikan struktur data Graph (graf) menggunakan 
adjacency list serta melakukan penelusuran graf dengan algoritma Depth First Search (DFS) dan Breadth First Search (BFS).

#### Full code Screenshot:
<img width="497" height="932" alt="Image" src="https://github.com/user-attachments/assets/a3d36c87-e99a-49fa-ae15-1554dcb9e344" />
<img width="457" height="1032" alt="Image" src="https://github.com/user-attachments/assets/965b10fc-3a8b-4e89-83b3-ec6cd9ca6df0" />
<img width="596" height="747" alt="Image" src="https://github.com/user-attachments/assets/41ad4256-b1a2-4ec2-9f72-39d177c55a9b" />

## Kesimpulan

Struktur data graph dapat direpresentasikan secara efektif menggunakan linked list (adjacency list),
Algoritma DFS cocok untuk penelusuran graf secara mendalam hingga ke cabang terdalam terlebih dahulu.

## Referensi
[1] Goodrich, M. T., Tamassia, R., & Goldwasser, M. H. (2014). Data Structures and Algorithms in C++ (2nd ed.). Wiley.























