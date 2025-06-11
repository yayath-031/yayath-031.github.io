---
title: FRACTIONAL KNAPSACK
date: 2025-05-06
categories: [DESAIN ANALISIS ALGORITMA, GREEDY ALGORITHM]
tags: [daa, algorithm, greedy]     # TAG names should always be lowercase
---

![Desktop View](https://res.cloudinary.com/codecrucks/images/f_webp,q_auto/v1634623105/fractional-knapsack/fractional-knapsack.jpg?_i=AA){: width="500"}
_---_

Permasalahan **Knapsack** adalah masalah optimasi klasik dalam ilmu komputer dan riset operasi. Secara umum, ini melibatkan pemilihan item yang berbeda, masing-masing dengan berat dan nilai tertentu, untuk dimasukkan ke dalam "tas" (knapsack) dengan kapasitas berat terbatas, sedemikian rupa sehingga total nilai item yang dipilih dimaksimalkan. Ada beberapa varian dari masalah Knapsack, dan salah satunya adalah **Fractional Knapsack**.

### Definisi

**Fractional Knapsack** adalah varian dari masalah Knapsack di mana kita dapat mengambil **pecahan (fraksi)** dari suatu item, tidak hanya item secara keseluruhan. Ini berarti jika kita tidak bisa memasukkan seluruh item ke dalam knapsack karena kapasitas yang terbatas, kita bisa mengambil sebagian dari item tersebut untuk memaksimalkan nilai total.

---

### Karakteristik

* **Pecahan Item Diizinkan**: Ini adalah karakteristik utama yang membedakannya dari 0/1 Knapsack (di mana item harus diambil seluruhnya atau tidak sama sekali).
* **Setiap Item Memiliki Berat dan Nilai**: Setiap item *i* memiliki berat *w_i* dan nilai *v_i*.
* **Kapasitas Terbatas**: Knapsack memiliki kapasitas berat maksimum *W*.
* **Tujuan Optimasi**: Maksimalkan total nilai item yang dimasukkan ke dalam knapsack.

---

### Strategi Penyelesaian

Karena kita dapat mengambil pecahan item, masalah Fractional Knapsack dapat diselesaikan secara optimal menggunakan pendekatan **Greedy Algorithm**. Strategi ini didasarkan pada gagasan untuk selalu memilih apa yang tampak terbaik pada saat itu.

---

### Kompleksitas Waktu

Kompleksitas waktu untuk menyelesaikan Fractional Knapsack menggunakan algoritma greedy sebagian besar didominasi oleh langkah pengurutan. Jika ada *n* item:

* Mengurutkan item berdasarkan rasio nilai per berat membutuhkan waktu *O(n \log n)*.
* Iterasi melalui item yang sudah diurutkan membutuhkan waktu *O(n)*.

Oleh karena itu, **kompleksitas waktu keseluruhan adalah *O(n \log n)***.

---

### Pengaplikasiannya

Fractional Knapsack memiliki berbagai aplikasi di dunia nyata, antara lain:

* **Alokasi Sumber Daya**: Mengalokasikan sumber daya yang terbatas (misalnya, anggaran, waktu) ke berbagai proyek atau investasi untuk memaksimalkan keuntungan.
* **Manajemen Investasi**: Memilih portofolio investasi dengan memaksimalkan keuntungan berdasarkan modal yang tersedia dan nilai pengembalian per unit modal.
* **Pemuatan Truk/Kapal**: Memuat barang ke dalam kendaraan pengangkut dengan kapasitas terbatas untuk memaksimalkan nilai barang yang diangkut.
* **Penjadwalan Tugas**: Menjadwalkan tugas dengan durasi dan prioritas berbeda dalam rentang waktu tertentu.

---

### Algoritma Greedy

Algoritma greedy untuk Fractional Knapsack bekerja sebagai berikut:

1.  **Hitung Rasio Nilai per Berat**: Untuk setiap item, hitung rasio nilai per berat (*v_i / w_i*). Rasio ini menunjukkan seberapa "berharga" setiap unit berat dari suatu item.
2.  **Urutkan Item**: Urutkan semua item dalam urutan **menurun** berdasarkan rasio nilai per berat mereka. Item dengan rasio yang lebih tinggi dianggap lebih menguntungkan.
3.  **Iterasi dan Pilih Item**: Mulai dari item dengan rasio nilai per berat tertinggi:
    * Jika seluruh item dapat dimasukkan ke dalam knapsack (berat item *\le* sisa kapasitas knapsack), masukkan seluruh item tersebut, kurangi kapasitas knapsack, dan tambahkan nilai item ke total nilai.
    * Jika seluruh item tidak dapat dimasukkan (berat item *>* sisa kapasitas knapsack), ambil **pecahan** dari item tersebut yang sesuai dengan sisa kapasitas knapsack. Tambahkan nilai pecahan tersebut ke total nilai, dan kapasitas knapsack menjadi nol. Hentikan proses.



### Pseudocode

```
FUNCTION fractionalKnapsack(items, capacity):
    // items: sebuah list objek, di mana setiap objek memiliki properti 'weight' dan 'value'
    // capacity: kapasitas maksimum knapsack

    // 1. Hitung rasio nilai per berat untuk setiap item
    FOR EACH item IN items:
        item.ratio = item.value / item.weight

    // 2. Urutkan item dalam urutan menurun berdasarkan rasio nilai per berat
    SORT items IN DESCENDING ORDER BY item.ratio

    totalValue = 0.0
    currentCapacity = capacity

    // 3. Iterasi dan pilih item
    FOR EACH item IN items:
        IF currentCapacity == 0:
            BREAK // Knapsack sudah penuh

        IF item.weight <= currentCapacity:
            // Ambil seluruh item
            totalValue += item.value
            currentCapacity -= item.weight
        ELSE:
            // Ambil pecahan item
            fraction = currentCapacity / item.weight
            totalValue += fraction * item.value
            currentCapacity = 0 // Knapsack penuh
            BREAK // Tidak ada lagi ruang

    RETURN totalValue
```

### Beberapa Contoh Permasalahan serta Solusinya

#### Contoh 1:

Anda memiliki knapsack dengan kapasitas 15 kg. Anda memiliki item-item berikut:

| Item | Berat (kg) | Nilai (*) |
| :--- | :--------- | :-------- |
| A    | 7          | 21        |
| B    | 5          | 20        |
| C    | 3          | 12        |
| D    | 4          | 8         |

**Solusi:**

1.  **Hitung Rasio Nilai per Berat:**
    * Item A: *21 / 7 = 3*
    * Item B: *20 / 5 = 4*
    * Item C: *12 / 3 = 4*
    * Item D: *8 / 4 = 2*

2.  **Urutkan Item (Menurun berdasarkan rasio):**
    * Item B (rasio 4)
    * Item C (rasio 4)
    * Item A (rasio 3)
    * Item D (rasio 2)

    *Catatan: Jika rasio sama, urutan relatif tidak masalah, tetapi biasanya diurutkan berdasarkan berat atau indeks asli untuk konsistensi.*

3.  **Pilih Item:**
    * **Kapasitas Awal:** 15 kg
    * **Pilih Item B:** Berat 5 kg, Nilai 20.
        * Sisa kapasitas: *15 - 5 = 10* kg
        * Total nilai: *20
    * **Pilih Item C:** Berat 3 kg, Nilai 12.
        * Sisa kapasitas: *10 - 3 = 7* kg
        * Total nilai: *20 + 12 = 32
    * **Pilih Item A:** Berat 7 kg, Nilai 21.
        * Sisa kapasitas: *7 - 7 = 0* kg
        * Total nilai: *32 + 21 = 53

    Knapsack sudah penuh.

**Total Nilai Maksimum:** *53

---

#### Contoh 2:

Anda memiliki knapsack dengan kapasitas 10 kg. Item-item:

| Item | Berat (kg) | Nilai (*) |
| :--- | :--------- | :-------- |
| X    | 6          | 30        |
| Y    | 4          | 20        |
| Z    | 3          | 15        |

**Solusi:**

1.  **Hitung Rasio Nilai per Berat:**
    * Item X: *30 / 6 = 5*
    * Item Y: *20 / 4 = 5*
    * Item Z: *15 / 3 = 5*

2.  **Urutkan Item:** Karena semua rasio sama, urutan relatif tidak masalah. Mari kita asumsikan urutan X, Y, Z.

3.  **Pilih Item:**
    * **Kapasitas Awal:** 10 kg
    * **Pilih Item X:** Berat 6 kg, Nilai 30.
        * Sisa kapasitas: *10 - 6 = 4* kg
        * Total nilai: *30
    * **Pilih Item Y:** Berat 4 kg, Nilai 20.
        * Sisa kapasitas: *4 - 4 = 0* kg
        * Total nilai: *30 + 20 = 50

    Knapsack sudah penuh.

**Total Nilai Maksimum:** *50

---

### Implementasi Permasalahan pada C++

Berikut adalah contoh implementasi Fractional Knapsack menggunakan C++:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <iomanip> // Untuk output presisi floating point

// Struktur untuk merepresentasikan item
struct Item {
    int id;
    int weight;
    int value;
    double ratio; // Rasio nilai per berat

    // Constructor
    Item(int i, int w, int v) : id(i), weight(w), value(v) {
        ratio = static_cast<double>(value) / weight;
    }
};

// Fungsi perbandingan untuk mengurutkan item berdasarkan rasio secara menurun
bool compareItems(const Item& a, const Item& b) {
    return a.ratio > b.ratio;
}

// Fungsi untuk menyelesaikan masalah Fractional Knapsack
double fractionalKnapsack(int capacity, std::vector<Item>& items) {
    // Urutkan item berdasarkan rasio nilai per berat secara menurun
    std::sort(items.begin(), items.end(), compareItems);

    double totalValue = 0.0;
    int currentWeight = 0; // Berat saat ini di dalam knapsack

    std::cout << "Memilih item:" << std::endl;

    // Iterasi melalui item yang sudah diurutkan
    for (const auto& item : items) {
        if (currentWeight + item.weight <= capacity) {
            // Jika seluruh item dapat dimasukkan
            totalValue += item.value;
            currentWeight += item.weight;
            std::cout << "  - Mengambil seluruh Item " << item.id 
                      << " (Berat: " << item.weight << "kg, Nilai: *" << item.value << ")" << std::endl;
        } else {
            // Jika hanya sebagian item yang dapat dimasukkan
            int remainingCapacity = capacity - currentWeight;
            double fraction = static_cast<double>(remainingCapacity) / item.weight;
            totalValue += fraction * item.value;
            currentWeight += remainingCapacity; // Knapsack akan penuh
            
            std::cout << "  - Mengambil " << std::fixed << std::setprecision(2) << (fraction * 100) 
                      << "% dari Item " << item.id 
                      << " (Berat diambil: " << remainingCapacity << "kg, Nilai diambil: *" 
                      << std::fixed << std::setprecision(2) << (fraction * item.value) << ")" << std::endl;
            break; // Knapsack sudah penuh, hentikan
        }
    }
    std::cout << std::endl;
    return totalValue;
}

int main() {
    int capacity = 15; // Kapasitas knapsack
    std::vector<Item> items;

    // Menambahkan item ke vektor
    items.emplace_back(1, 7, 21); // Item A
    items.emplace_back(2, 5, 20); // Item B
    items.emplace_back(3, 3, 12); // Item C
    items.emplace_back(4, 4, 8);  // Item D

    std::cout << "Kapasitas Knapsack: " << capacity << "kg" << std::endl;
    std::cout << "Item yang tersedia:" << std::endl;
    for(const auto& item : items) {
        std::cout << "  Item " << item.id << ": Berat " << item.weight 
                  << "kg, Nilai *" << item.value 
                  << ", Rasio *" << std::fixed << std::setprecision(2) << item.ratio << "/kg" << std::endl;
    }
    std::cout << "---" << std::endl;

    double maxValue = fractionalKnapsack(capacity, items);

    std::cout << "Nilai Total Maksimum: *" << std::fixed << std::setprecision(2) << maxValue << std::endl;

    return 0;
}
```

**Output dari kode C++ di atas akan menjadi:**

```
Kapasitas Knapsack: 15kg
Item yang tersedia:
  Item 1: Berat 7kg, Nilai *21, Rasio *3.00/kg
  Item 2: Berat 5kg, Nilai *20, Rasio *4.00/kg
  Item 3: Berat 3kg, Nilai *12, Rasio *4.00/kg
  Item 4: Berat 4kg, Nilai *8, Rasio *2.00/kg
---
Memilih item:
  - Mengambil seluruh Item 2 (Berat: 5kg, Nilai: *20)
  - Mengambil seluruh Item 3 (Berat: 3kg, Nilai: *12)
  - Mengambil seluruh Item 1 (Berat: 7kg, Nilai: *21)

Nilai Total Maksimum: *53.00
```

### Kesimpulan

**Fractional Knapsack** adalah masalah optimasi yang dapat diselesaikan secara efisien menggunakan **algoritma greedy**. Kunci penyelesaiannya adalah mengurutkan item berdasarkan **rasio nilai per berat** dan memilih item-item dengan rasio tertinggi hingga knapsack penuh. Kemampuan untuk mengambil pecahan item membuatnya berbeda dan lebih sederhana untuk dipecahkan secara optimal dibandingkan dengan masalah 0/1 Knapsack yang memerlukan pemrograman dinamis. Efisiensinya, dengan kompleksitas waktu *O(n \log n)*, menjadikannya solusi praktis untuk berbagai skenario alokasi sumber daya.

![Desktop View](https://i.pinimg.com/564x/3f/55/43/3f554324815a6183498fb891d37b1a97.jpg){: width="200"}
_---_

