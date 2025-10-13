# <h1 align="center">Laporan Praktikum Modul 3 <br> Abstract Data Type
</h1>
<p align="center">Hafis Akbar Anugrah - 103112400125</p>

## Dasar Teori
Abstract Data Type (ADT) adalah konsep dalam pemrograman yang mendefinisikan suatu tipe data beserta kumpulan operasi dasar yang dapat dilakukan terhadapnya, tanpa memperlihatkan detail implementasi di dalamnya. Fokus utama ADT terletak pada “apa yang dilakukan” oleh operasi, bukan “bagaimana cara melakukannya”, sehingga terdapat pemisahan jelas antara spesifikasi perilaku dan implementasi aktual. Dalam penerapannya, ADT umumnya dibagi menjadi dua bagian utama: file header (.h) yang memuat deklarasi tipe data serta prototipe fungsi/prosedur, dan file implementasi (.cpp) yang berisi kode lengkap dari setiap operasi yang didefinisikan. Dengan pendekatan ini, pengguna dapat menggunakan tipe data melalui antarmuka yang telah ditentukan tanpa perlu memahami detail internalnya. Hal ini mendukung prinsip modularitas, abstraksi, dan kemudahan pemeliharaan dalam pengembangan perangkat lunak.
## Guide

## Menghitung rata rata mahasiswa.h
```go
#ifndef MAHASISWA_H_INCLUDED
#define MAHASISWA_H_INCLUDED

struct mahasiswa
{
    char nim[10];
    int nilai1, nilai2;
};

void inputMhs(mahasiswa &m);
float rata2(mahasiswa m);

#endif

```

## Mahasiswa.cpp
```go
#include "mahasiswa.h"
#include <iostream>
using namespace std;

void inputMhs(mahasiswa &m)
{
    cout << "input nama = ";
    cin >> (m) .nim;
    cout << "input nilai = ";
    cin >> (m) .nilai1;
    cout << "input niali2 = ";
    cin >> m .nilai2;

}
float rata2(mahasiswa m)
{
    return float(m.nilai1 + m.nilai2) / 2;

```

## main.cpp
```go
#include <iostream>
#include "mahasiswa.h"
using namespace std;

int main(){
    mahasiswa mhs;
    inputMhs(mhs);
    cout << "rata rata = " << rata2(mhs);
    return 0;
}

```


## Unguide

### Soal 1

Buat program yang dapat menyimpan data mahasiswa (max. 10) ke dalam sebuah array
dengan field nama, nim, uts, uas, tugas, dan nilai akhir. Nilai akhir diperoleh dari FUNGSI
dengan rumus 0.3*uts+0.4*uas+0.3*tugas.
```go
#include <iostream>
#include <string>
#include <iomanip>
#include <limits>
using namespace std;

struct Mahasiswa {
    string nama;
    string nim;
    float uts;
    float uas;
    float tugas;
    float nilaiAkhir;
};

float hitungNilaiAkhir(float uts, float uas, float tugas) {
    return 0.3f * uts + 0.4f * uas + 0.3f * tugas;
}

int main() {
    Mahasiswa mhs[10];
    int n = 0;
    while (true) {
        cout << "\n1. Tambah data\n2. Tampilkan data\n3. Keluar\nPilih menu: ";
        int pilihan;
        if (!(cin >> pilihan)) {
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
            cout << "Input tidak valid.\n";
            continue;
        }

        if (pilihan == 1) {
            if (n >= 10) {
                cout << "Data penuh (maks 10 mahasiswa).\n";
                continue;
            }
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
            cout << "Nama   : ";
            getline(cin, mhs[n].nama);
            cout << "NIM    : ";
            getline(cin, mhs[n].nim);
            cout << "Nilai UTS  : ";
            while (!(cin >> mhs[n].uts)) {
                cin.clear();
                cin.ignore(numeric_limits<streamsize>::max(), '\n');
                cout << "Masukkan angka untuk UTS: ";
            }
            cout << "Nilai UAS  : ";
            while (!(cin >> mhs[n].uas)) {
                cin.clear();
                cin.ignore(numeric_limits<streamsize>::max(), '\n');
                cout << "Masukkan angka untuk UAS: ";
            }
            cout << "Nilai Tugas: ";
            while (!(cin >> mhs[n].tugas)) {
                cin.clear();
                cin.ignore(numeric_limits<streamsize>::max(), '\n');
                cout << "Masukkan angka untuk Tugas: ";
            }
            mhs[n].nilaiAkhir = hitungNilaiAkhir(mhs[n].uts, mhs[n].uas, mhs[n].tugas);
            n++;
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
            cout << "Data berhasil ditambah.\n";
        } else if (pilihan == 2) {
            if (n == 0) {
                cout << "Belum ada data.\n";
                continue;
            }
            cout << "\nDaftar Nilai Mahasiswa\n";
            cout << left << setw(4) << "No" << setw(25) << "Nama" << setw(12) << "NIM" << setw(10) << "NilaiAkhir" << '\n';
            cout << string(55, '-') << '\n';
            cout << fixed << setprecision(2);
            for (int i = 0; i < n; ++i) {
                cout << left << setw(4) << (i + 1)
                     << setw(25) << mhs[i].nama
                     << setw(12) << mhs[i].nim
                     << setw(10) << mhs[i].nilaiAkhir << '\n';
            }
        } else if (pilihan == 3) {
            cout << "Keluar.\n";
            break;
        } else {
            cout << "Pilihan tidak tersedia.\n";
        }
    }
    return 0;
}
```

> Output
> ![Screenshot bagian x](Output/Output_no1.png)

## Referensi

1. [https://www.w3schools.com/cpp/exercise.asp?x=xrcise_function_reference1](https://www.w3schools.com/cpp/exercise.asp?x=xrcise_function_reference1)
2. [https://www.w3schools.com/cpp/cpp_function_param.asp](https://www.w3schools.com/cpp/cpp_function_param.asp)
