# <h1 align="center">Laporan Praktikum Modul 4 <br> Singly Linked List (Bagian pertama)</h1>
<p align="center">Hafis Akbar Anugrah - 103112400125 </p>

## Dasar Teori

Singly Linked List adalah struktur data dinamis yang tersusun dari node-node saling terhubung melalui pointer. Tiap node berisi dua bagian: **data** dan **pointer next** yang menunjuk ke node berikutnya. Aksesnya hanya searah, dari **head** hingga node terakhir yang menunjuk ke **NULL**. Ukurannya fleksibel, bisa bertambah atau berkurang tanpa batas awal seperti array. Operasi dasarnya meliputi **insert**, **delete**, **traverse**, dan **update**. Keunggulannya adalah efisien dalam penyisipan dan penghapusan data, meski aksesnya harus dilakukan berurutan dari awal list.


## Guide

### linkedlist.cpp
```go
#include <iostream>
using namespace std;

// Struktur Node
struct Node {
    int data;
    Node* next;
};

// Pointer awal dan akhir
Node* head = nullptr;

// Fungsi untuk membuat node baru
Node* createNode(int data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->next = nullptr;
    return newNode;
}


void insertBelakang(int data) {
    Node* newNode = createNode(data);
    if (head == nullptr) {
        head = newNode;
    } else {
        Node* temp = head;
        while (temp->next != nullptr) {
            temp = temp->next;
        }
        temp->next = newNode;
    }
    cout << "Data " << data << " berhasil ditambahkan di belakang.\n";
}

void insertSetelah(int target, int dataBaru) {
    Node* temp = head;
    while (temp != nullptr && temp->data != target) {
        temp = temp->next;
    }

    if (temp == nullptr) {
        cout << "Data " << target << " tidak ditemukan!\n";
    } else {
        Node* newNode = createNode(dataBaru);
        newNode->next = temp->next;
        temp->next = newNode;
        cout << "Data " << dataBaru << " berhasil disisipkan setelah " << target << ".\n";
    }
}

// ========== DELETE FUNCTION ==========
void hapusNode(int data) {
    if (head == nullptr) {
        cout << "List kosong!\n";
        return;
    }

    Node* temp = head;
    Node* prev = nullptr;

    // Jika data di node pertama
    if (temp != nullptr && temp->data == data) {
        head = temp->next;
        delete temp;
        cout << "Data " << data << " berhasil dihapus.\n";
        return;
    }

    // Cari node yang akan dihapus
    while (temp != nullptr && temp->data != data) {
        prev = temp;
        temp = temp->next;
    }

    // Jika data tidak ditemukan
    if (temp == nullptr) {
        cout << "Data " << data << " tidak ditemukan!\n";
        return;
    }

    prev->next = temp->next;
    delete temp;
    cout << "Data " << data << " berhasil dihapus.\n";
}

// ========== UPDATE FUNCTION ==========
void updateNode(int dataLama, int dataBaru) {
    Node* temp = head;
    while (temp != nullptr && temp->data != dataLama) {
        temp = temp->next;
    }

    if (temp == nullptr) {
        cout << "Data " << dataLama << " tidak ditemukan!\n";
    } else {
        temp->data = dataBaru;
        cout << "Data " << dataLama << " berhasil diupdate menjadi " << dataBaru << ".\n";
    }
}


// ========== MAIN PROGRAM ==========
int main() {
    int pilihan, data, target, dataBaru;

    do {
        cout << "\n=== MENU SINGLE LINKED LIST ===\n";
        cout << "1. Insert Depan\n";
        cout << "2. Insert Belakang\n";
        cout << "3. Insert Setelah\n";
        cout << "4. Hapus Data\n";
        cout << "5. Update Data\n";
        cout << "6. Tampilkan List\n";
        cout << "0. Keluar\n";
        cout << "Pilih: ";
        cin >> pilihan;

        switch (pilihan) {
            case 1:
                cout << "Masukkan data: ";
                cin >> data;
                insertDepan(data);
                break;
            case 2:
                cout << "Masukkan data: ";
                cin >> data;
                insertBelakang(data);
                break;
            case 3:
                cout << "Masukkan data target: ";
                cin >> target;
                cout << "Masukkan data baru: ";
                cin >> dataBaru;
                insertSetelah(target, dataBaru);
                break;
            case 4:
                cout << "Masukkan data yang ingin dihapus: ";
                cin >> data;
                hapusNode(data);
                break;
            case 5:
                cout << "Masukkan data lama: ";
                cin >> data;
                cout << "Masukkan data baru: ";
                cin >> dataBaru;
                updateNode(data, dataBaru);
                break;
            case 6:
                tampilkanList();
                break;
            case 0:
                cout << "Program selesai.\n";
                break;
            default:
                cout << "Pilihan tidak valid!\n";
        }
    } while (pilihan != 0);

    return 0;
}
```
### Soal 1

buatlah single linked list untuk Antrian yang menyimpan data pembeli( nama dan pesanan). program memiliki beberapa menu seperti tambah antrian,  layani antrian(hapus), dan tampilkan antrian. \*antrian pertama harus yang pertama dilayani
```go
#include <iostream>
#include <string>
using namespace std;

struct Node {
    string nama;
    string pesanan;
    Node* next;
};

Node* head = nullptr;
Node* tail = nullptr;

bool kosong() {
    return head == nullptr;
}

void tambahAntrian(const string& nama, const string& pesanan) {
    Node* baru = new Node;
    baru->nama = nama;
    baru->pesanan = pesanan;
    baru->next = nullptr;

    if (kosong()) {
        head = tail = baru;
    } else {
        tail->next = baru;
        tail = baru;
    }

    cout << "\n✅ " << nama << " dengan pesanan '" << pesanan << "' telah ditambahkan ke antrian.\n";
}

void layaniAntrian() {
    if (kosong()) {
        cout << "\n⚠️  Antrian masih kosong!\n";
        return;
    }

    Node* hapus = head;
    cout << "\n👨‍🍳 Melayani pembeli: " << hapus->nama 
         << " (Pesanan: " << hapus->pesanan << ")\n";
    head = head->next;
    delete hapus;

    if (head == nullptr) tail = nullptr;
}

void tampilkanAntrian() {
    if (kosong()) {
        cout << "\n⚠️  Tidak ada antrian saat ini.\n";
        return;
    }

    cout << "\n===== DAFTAR ANTRIAN PEMBELI =====\n";
    Node* bantu = head;
    int nomor = 1;

    while (bantu != nullptr) {
        cout << nomor++ << ". " << bantu->nama 
             << " - Pesanan: " << bantu->pesanan << endl;
        bantu = bantu->next;
    }
    cout << "==================================\n";
}

int hitungAntrian() {
    Node* bantu = head;
    int count = 0;
    while (bantu != nullptr) {
        count++;
        bantu = bantu->next;
    }
    return count;
}

int main() {
    int pilihan;
    string nama, pesanan;

    do {
        cout << "\n=== MENU ANTRIAN PEMBELI ===\n";
        cout << "1. Tambah Antrian\n";
        cout << "2. Layani Antrian\n";
        cout << "3. Tampilkan Antrian\n";
        cout << "4. Keluar\n";
        cout << "Pilih menu: ";
        cin >> pilihan;
        cin.ignore();

        switch (pilihan) {
            case 1:
                cout << "\nMasukkan Nama Pembeli: ";
                getline(cin, nama);
                cout << "Masukkan Pesanan: ";
                getline(cin, pesanan);
                tambahAntrian(nama, pesanan);
                break;
            case 2:
                layaniAntrian();
                break;
            case 3:
                tampilkanAntrian();
                cout << "Jumlah antrian saat ini: " << hitungAntrian() << endl;
                break;
            case 4:
                cout << "\nTerima kasih, program selesai.\n";
                break;
            default:
                cout << "\nPilihan tidak valid! Coba lagi.\n";
        }
    } while (pilihan != 4);

    return 0;
}
```
> Output
> ![Screenshot bagian x](output/.png)

Program di atas merupakan implementasi **antrian pembeli** menggunakan **Singly Linked List** dalam bahasa C++. Setiap elemen antrian disimpan dalam node yang berisi nama pembeli dan pesanan. Program menyediakan beberapa fungsi utama, yaitu menambah antrian baru di bagian belakang (enqueue), melayani antrian dengan menghapus data dari bagian depan (dequeue), menampilkan seluruh antrian yang sedang menunggu, serta menghitung jumlah antrian yang ada. Proses antrian bersifat **FIFO (First In, First Out)**, artinya pembeli yang datang lebih dulu akan dilayani terlebih dahulu. Program ini berjalan secara interaktif melalui menu yang dapat dipilih pengguna hingga memilih keluar.

### Soal 2
buatlah program kode untuk membalik (reverse) singly linked list (1-2-3 menjadi 3-2-1) 

```go
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
};

Node* head = nullptr;

void tambahNode(int nilai) {
    Node* baru = new Node;
    baru->data = nilai;
    baru->next = nullptr;

    if (head == nullptr)
        head = baru;
    else {
        Node* bantu = head;
        while (bantu->next != nullptr)
            bantu = bantu->next;
        bantu->next = baru;
    }
}

void tampilList() {
    Node* bantu = head;
    while (bantu != nullptr) {
        cout << bantu->data;
        if (bantu->next != nullptr) cout << " -> ";
        bantu = bantu->next;
    }
    cout << endl;
}

void balikList() {
    Node* prev = nullptr;
    Node* curr = head;
    Node* next = nullptr;

    while (curr != nullptr) {
        next = curr->next;   
        curr->next = prev;   
        prev = curr;         
        curr = next;         
    }
    head = prev;
}

int main() {
    tambahNode(1);
    tambahNode(2);
    tambahNode(3);

    cout << "Linked List sebelum dibalik: ";
    tampilList();

    balikList();

    cout << "Linked List setelah dibalik: ";
    tampilList();

    return 0;
}

```

> Output
> ![Screenshot bagian x](Output/Output_no2.png)

Program di atas berfungsi untuk **membalik urutan data** pada **Singly Linked List**. Awalnya, program membuat list berisi data `1 → 2 → 3`. Fungsi `tambahNode()` digunakan untuk menambahkan node baru di akhir list, sedangkan `tampilList()` menampilkan isi list dari awal hingga akhir. Proses pembalikan dilakukan oleh fungsi `balikList()`, yang menggunakan tiga pointer: `prev`, `curr`, dan `next`. Pointer `curr` berjalan dari awal list hingga akhir, sambil membalik arah pointer `next` setiap node agar menunjuk ke node sebelumnya (`prev`). Setelah semua pointer dibalik, `head` diarahkan ke node terakhir (yang menjadi node pertama setelah dibalik). Hasil akhirnya, list yang semula `1 → 2 → 3` berubah menjadi `3 → 2 → 1`.

## Referensi
1. https://www.w3schools.com/dsa/dsa_theory_linkedlists.php
2. https://www.w3schools.com/dsa/dsa_algo_linkedlists_operations.php
3. https://www.w3schools.com/dsa/dsa_data_linkedlists_types.php
4. https://www.w3schools.com/dsa/dsa_theory_linkedlists_memory.php
5. https://www.w3schools.com/dsa/dsa_data_queues.php
