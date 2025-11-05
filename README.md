# <h1 align="center">Laporan Praktikum Struktur Data<br> Modul 7 STACK </h1>
<p align="center">Osha Alfida Valyana / 103112430202</p>

## Dasar Teori

stack adalah struktur data yang digunakan untuk menyimpan sekumpulan objek. Item individu dapat ditambahkan dan disimpan di dalam stack menggunakan operasi push. Objek dapat diambil menggunakan operasi pop, yang menghapus item dari stack.

## Guided

### Soal 1

```cpp
#include <iostream>
using namespace std;

struct Node
{
    int data;
    Node *next;
};

bool isEmpty(Node *top)
{
    return top == nullptr;
}
void push (Node *&top, int data)
{
    Node *newNode = new Node();
    newNode-> data = data;
    newNode-> next = top;
    top = newNode;
}

int pop(Node *&top)
{
    if (isEmpty(top))
    {
        cout << "Stack Kosong, tidak bisa pop!" << endl;
        return 0;
    }
    int poppedData = top-> data;
    Node *temp = top;
    top = top-> next;

    delete temp;
    return poppedData;
}

void show(Node *top)
{
    if (isEmpty(top))
{
    cout << "Stack Kosong." << endl;
    return;
}
cout << "TOP ->";
Node *temp = top;

while (temp != nullptr)
{
    cout << temp-> data << " ->";
    temp = temp-> next;
}
cout << "NULL" << endl;
}

int main()
{
    Node *stack = nullptr;

    push (stack, 10);
    push (stack, 20);
    push (stack, 30);

    cout << "Menampilkan isi stack: " << endl;
    show(stack);

    cout << "Pop: " << pop(stack) << endl;

    cout << "Menampilkan sisa stack: " << endl;
    show(stack);

    return 0;
}
```
 ⁠
 
Output
⁠![Output guided](https://github.com/chafdv/Modul-7/blob/main/output/guidedm7.png)

Program ini membuat **stack** dengan **struct dan pointer**. Fungsi push menambah data ke atas stack, pop menghapus data teratas, dan show menampilkan isi stack. Program menunjukkan prinsip LIFO (Last In, First Out), di mana data terakhir yang dimasukkan akan keluar terlebih dahulu.


---

## Unguided

### Soal 1

Buatlah ADT Stack menggunakan ARRAY sebagai berikut di dalam file “stack.h” dan Buatlah implementasi ADT Stack menggunakan Array pada file “stack.cpp” dan “main.cpp”

```cpp
#ifndef STACK_H
#define STACK_H

#define MAX 20
using namespace std;

typedef int infotype;

struct Stack {
    infotype info[MAX];
    int top;
};

void createStack(Stack &S);
void push(Stack &S, infotype x);
infotype pop(Stack &S);
void printInfo(Stack S);
void balikStack(Stack &S);
void pushAscending(Stack &S, infotype x);

#endif
```

 ⁠
 ⁠
Output
	⁠![Output Soal 1](https://github.com/chafdv/Modul-7/blob/main/output/unguidedm7.png)

Pada unguided 1 menunjukkan cara kerja dasar stack dengan operasi push dan pop. Data dimasukkan ke stack, beberapa dihapus, lalu ditampilkan hasil akhirnya sebelum dan sesudah dibalik.

---

### Soal 2

Tambahkan prosedur pushAscending( in/out S : Stack, in x : integer)

```cpp
#include <iostream>
#include "stack.h"
using namespace std;

void createStack(Stack &S) {
    S.top = -1;
}

void push(Stack &S, infotype x) {
    if (S.top < MAX - 1) {
        S.top++;
        S.info[S.top] = x;
    }
}

infotype pop(Stack &S) {
    if (S.top >= 0) {
        infotype x = S.info[S.top];
        S.top--;
        return x;
    }
    return -1;
}

void printInfo(Stack S) {
    cout << "[TOP] ";
    for (int i = S.top; i >= 0; i--) {
        cout << S.info[i] << " ";
    }
    cout << endl;
}

void balikStack(Stack &S) {
    Stack temp;
    createStack(temp);
    while (S.top != -1) {
        push(temp, pop(S));
    }
    S = temp;
}

void pushAscending(Stack &S, infotype x) {
    Stack temp;
    createStack(temp);
    while (S.top != -1 && S.info[S.top] > x) {
        push(temp, pop(S));
    }
    push(S, x);
    while (temp.top != -1) {
        push(S, pop(temp));
    }
}
```

 ⁠

Output 
	⁠![Output Soal 2](https://github.com/chafdv/Modul-7/blob/main/output/unguidedm7.png)

Pada unguided 2 menambahkan data ke stack secara berurutan naik (ascending) menggunakan fungsi tambahan agar nilai selalu tersusun dari kecil ke besar, lalu hasilnya dibalik.

---

### Soal 3

Tambahkan prosedur getInputStream( in/out S : Stack ). Prosedur akan terus membaca dan menerima input user dan memasukkan setiap input ke dalam stack hingga user menekan tombol enter. Contoh: gunakan cin.get() untuk mendapatkan inputan user.

```cpp
#include <iostream>
#include "stack.h"
using namespace std;

int main() {
    cout << "Hello world!" << endl;

    Stack S;
    createStack(S);

    push(S, 3);
    push(S, 4);
    push(S, 8);
    pop(S);
    push(S, 2);
    push(S, 3);
    pop(S);
    push(S, 9);
    printInfo(S);
    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);
    cout << endl;

    createStack(S);
    pushAscending(S, 3);
    pushAscending(S, 4);
    pushAscending(S, 8);
    pushAscending(S, 2);
    pushAscending(S, 3);
    pushAscending(S, 9);
    printInfo(S);
    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);
    cout << endl;

    createStack(S);
    push(S, 1);
    push(S, 0);
    push(S, 6);
    push(S, 9);
    push(S, 2);
    push(S, 7);
    push(S, 4);
    printInfo(S);
    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);

    return 0;
}
```
 ⁠
 
Output 
	⁠![Output Soal 3]([https://github.com/chafdv/Modul-7/blob/main/output/unguidedm7.png)

Pada unguided 3 menampilkan contoh stack dengan data tetap (tanpa inputan), kemudian dibalik urutannya untuk menunjukkan proses pembalikan isi stack secara otomatis.

## Referensi

1.⁠ (https://techterms.com/definition/stack) [diakses 4-11-2025]
