# <h1 align="center">Laporan Praktikum Modul 2 <br> Nama Modul</h1>
<p align="center">Hafis Akbar Anugrah - 103112400125</p>

## Dasar Teori
Modul ini membahas dasar-dasar penting dalam pemrograman C++, mencakup array, pointer, fungsi, dan prosedur. Array digunakan untuk menyimpan sekumpulan data bertipe sama yang dapat diakses melalui indeks, baik dalam bentuk satu dimensi maupun multidimensi. Pointer adalah variabel yang menyimpan alamat memori dari variabel lain, sehingga memungkinkan pengolahan data langsung di memori. Fungsi dan prosedur berperan untuk membagi program menjadi bagian-bagian kecil agar lebih terstruktur; fungsi mengembalikan nilai, sedangkan prosedur (fungsi bertipe void) tidak. Terdapat tiga metode pengiriman parameter, yaitu call by value (mengirim salinan nilai), call by pointer (menggunakan alamat memori dengan operator khusus), dan call by reference (menggunakan referensi dengan operator &), yang memungkinkan perubahan langsung pada variabel aslinya. Seluruh konsep ini menjadi landasan utama dalam pengelolaan memori dan penyusunan kode secara terstruktur di bahasa C++.

## Guide

## 01_ARRAY
```go
#include <iostream>
using namespace std;

int main() {

    int nilai[5] = {1, 2, 3, 4, 5};

    for ( int i = 0;  i < 5; i++)
    {
       
        cout << "elemen ke-" << i << "=" << nilai[i] << endl;
    }
    return 0;
}
```

## 02_ARRAY
```go
#include <iostream>
using namespace std;

int main() {
    int matrik[3][3] = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    for (int i = 0; i < 3; ++i) {
        for (int j = 0; j < 3; ++j) {
            cout << matrik[i][j] << " ";
        }
        cout << endl;
    }

    return 0;
}
```

## 03_POINTER
```go
#include <iostream>
using namespace std;

int main()
{
    int umur = 25;
    int *p_umur;

    p_umur = &umur;

    cout << "Nilai 'umur' : " << umur << endl;
    cout << "Alamat memori 'umur' : " << &umur << endl;
    cout << "Nilai 'p_umur' (alamat) : " << p_umur << endl;
    cout << "Nilai yang diakses 'p_umur' : " << *p_umur << endl;
    cout << "Alamat memori dari pointer 'p_umur' itu sendiri : " << &p_umur << endl;

    return 0;
}
```

## 04_ARRAY POINTER
```go
#include <iostream>
using namespace std;

int main()
{
    int data[5] = {10, 20, 30, 40, 50};
    int *p_data = data;

    cout << "Mengakses elemen array cara normal:" << endl;

    for (int i = 0; i < 5; ++i)
    {
        cout << "Nilai elemen ke-" << i << " : " << data[i] << endl;
    }

    cout << "Mengakses elemen array menggunakan pointer:" << endl;

    for (int i = 0; i < 5; ++i)
    {
        cout << "Nilai elemen ke-" << i << " : " << *(p_data + i) << endl;
    }

    return 0;
}
```

## 05_STRING POINTER
```go
#include <iostream>
using namespace std;

int main()
{
    char pesan_array[] = "Nasi Padang";
    char *pesan_pointer = "Ayam Bakar 23";

    cout << "String Array: " << pesan_array << endl;
    cout << "String Pointer: " << pesan_pointer << endl;

    // Mengubah karakter dalam array diperbolehkan
    pesan_array[0] = 'h';
    cout << "String Array setelah diubah: " << pesan_array << endl;

    // Pointer dapat diubah untuk menunjuk ke string lain
    pesan_pointer = "Sariman";
    cout << "String Pointer setelah menunjuk ke string lain: " << pesan_pointer << endl;

    return 0;
}
```

## 06_
```go

```

## 07_CALL BY POINTER
```go
#include <iostream>
using namespace std;

int main()
{
    int a = 10, b = 20;
    cout << "Sebelum ditukar: a = " << a << ", b = " << b << endl;
    tukar(&a, &b);
    cout << "Setelah ditukar: a = " << a << ", b = " << b << endl;
    return 0;
}

void tukar(int *px, int *py)
{
    int temp = *px;
    *px = *py;
    *py = temp;
}
```

## 08_CALL BY REFERENSI
```go
#include <iostream>
using namespace std;

int main()
{
    int a = 10, b = 20;
    cout << "Sebelum ditukar: a = " << a << ", b = " << b << endl;
    tukar(a, b);
    cout << "Setelah ditukar: a = " << a << ", b = " << b << endl;
    return 0;
}

void tukar(int &x, int &y)
{
    int temp = x;
    x = y;
    y = temp;
}
```

## Unguided

### soal 1
1. Buatlah sebuah program untuk melakukan transpose pada sebuah matriks persegi berukuran 3x3. Operasi transpose adalah mengubah baris menjadi kolom dan sebaliknya. Inisialisasi matriks awal di dalam kode, kemudian buat logika untuk melakukan transpose dan simpan hasilnya ke dalam matriks baru. Terakhir, tampilkan matriks awal dan matriks hasil transpose.

Contoh Output:

Matriks Awal:

1 2 3

4 5 6

7 8 9

Matriks Hasil Transpose:

1 4 7

2 5 8

3 6 9

### Soal 1

```go
#include <iostream>
using namespace std;

int main() {
    // Inisialisasi matriks awal 3x3
    int matriks[3][3] = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
    int transpose[3][3];
    
    // Menampilkan matriks awal
    cout << "Matriks Awal:" << endl;
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << matriks[i][j] << " ";
        }
        cout << endl;
    }
    
    // Melakukan operasi transpose
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            transpose[j][i] = matriks[i][j];
        }
    }
    
    // Menampilkan matriks hasil transpose
    cout << "\nMatriks Hasil Transpose:" << endl;
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << transpose[i][j] << " ";
        }
        cout << endl;
    }
    
    return 0;
}
```

> Output
> ![Screenshot bagian x](.png)

Penjelasan ttg kode kalian disini
Program ini menampilkan cara membuat matriks berukuran 3x3 dengan elemen bernilai 1 hingga 9, lalu menghasilkan matriks transpose dengan menukar posisi baris dan kolom menggunakan perulangan bersarang. Proses utama transposisi terdapat pada baris kode transpose[j][i] = matriks[i][j], di mana indeks i dan j saling ditukar. Dengan demikian, elemen yang semula berada di baris ke-i kolom ke-j akan berpindah ke baris ke-j kolom ke-i. Hasil akhirnya, matriks awal dengan baris 1-2-3, 4-5-6, 7-8-9 berubah menjadi matriks dengan kolom 1-4-7, 2-5-8, dan 3-6-9.


### Soal 2
2. Buatlah program yang menunjukkan penggunaan call by reference. Buat sebuah prosedur bernama kuadratkan yang menerima satu parameter integer secara referensi (&). Prosedur ini akan mengubah nilai asli variabel yang dilewatkan dengan nilai kuadratnya. Tampilkan nilai variabel di main() sebelum dan sesudah memanggil prosedur untuk membuktikan perubahannya. 

Contoh Output:

Nilai awal: 5
Nilai setelah dikuadratkan: 25
soal nomor 2A

```go
#include <iostream>
using namespace std;

// Prosedur dengan parameter referensi
void kuadratkan(int &angka) {
    angka = angka * angka; // Mengubah nilai asli variabel
}


int main() {
    int nilai = 5;
    
    // Menampilkan nilai sebelum diproses
    cout << "Nilai awal: " << nilai << endl;
    
    // Memanggil prosedur dengan passing by reference
    kuadratkan(nilai);
    
    // Menampilkan nilai setelah diproses
    cout << "Nilai setelah dikuadratkan: " << nilai << endl;
    
    return 0;
}
```

> Output
> ![Screenshot bagian x](.png)

penjelasan kode
Program ini memperlihatkan bagaimana perbedaan antara pengiriman parameter biasa dan menggunakan referensi. Saat symbol & ditambahkan pada parameter angka di fungsi kuadratkan, fungsi tersebut menerima alamat memori dari variable nilai, bukan hanya nilainya. Karena itu, Ketika perintah angka = angka * angka dijalankan di dalam fungsi, perubahan langsung mempengaruhi variable asli nilai di fungsi main. Hasilnya, nilai nilai yang awalnya 5 berubah menjadi 25 secara langsung, bukan hanya pada Salinan sementara.

## Referensi

1. [https://www.w3schools.com/cpp/exercise.asp?x=xrcise_function_reference1](https://www.w3schools.com/cpp/exercise.asp?x=xrcise_function_reference1)
2. [https://www.w3schools.com/cpp/cpp_function_param.asp](https://www.w3schools.com/cpp/cpp_function_param.asp)
