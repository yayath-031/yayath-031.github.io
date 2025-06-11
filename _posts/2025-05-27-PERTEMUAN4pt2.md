---
title: BREADTH-FIRST SEARCH (BFS)
date: 2025-05-27
categories: [DESAIN ANALISIS ALGORITMA, BFS, BACKTRACKING ALGORITHM]
tags: [daa, algorithm, backtracking, bfs]     # TAG names should always be lowercase
---

![Desktop View](https://i.ytimg.com/vi/oDqjPvD54Ss/maxresdefault.jpg){: width="500"}
_---_

WASSAP!, *Breadth-First Search* (BFS) adalah salah satu algoritma fundamental untuk menjelajahi atau mencari data pada struktur graf atau pohon. Metode ini bekerja dengan cara menelusuri simpul (node) berdasarkan tingkat atau level jaraknya dari titik awal. Secara sederhana, BFS akan mengunjungi semua simpul tetangga terdekat terlebih dahulu sebelum melanjutkan ke simpul yang lebih jauh. Karena pendekatannya yang menyebar ke segala arah secara merata, cara kerjanya sering diibaratkan seperti kita memeriksa seluruh ruangan di lantai satu sebuah gedung sebelum naik ke lantai berikutnya.

***

### Konsep Dasar dan Cara Kerja BFS

Konsep utama di balik BFS sangat sederhana dan sistematis.

* **Menggunakan Antrian (*Queue*)**: BFS memanfaatkan struktur data *queue* (antrian) untuk mengelola urutan simpul yang akan dikunjungi.
* **Penelusuran per Level**: Algoritma ini memulai dari simpul awal, mengunjungi semua tetangganya, lalu melanjutkan ke tetangga dari tetangga tersebut, dan seterusnya. Proses ini memastikan penelusuran terjadi lapis demi lapis, yang juga dikenal sebagai *level-order traversal*.

***

### Langkah-Langkah Algoritma

Proses pencarian menggunakan BFS mengikuti langkah-langkah berikut:
1.  **Tentukan Simpul Awal**: Pilih satu simpul sebagai titik awal (*start node*).
2.  **Masukkan ke Antrian**: Masukkan simpul awal tersebut ke dalam *queue*.
3.  **Proses Antrian**: Selama *queue* tidak kosong, lakukan langkah-langkah berikut:
    * Ambil simpul terdepan dari *queue* dan tandai sebagai simpul yang telah dikunjungi.
    * Periksa apakah simpul ini adalah tujuan (*goal node*). Jika ya, pencarian selesai.
    * Jika bukan tujuan, kunjungi semua tetangga dari simpul ini yang belum pernah dikunjungi.
    * Tandai semua tetangga tersebut sebagai "sudah dikunjungi" dan masukkan mereka ke dalam *queue*.
4.  **Ulangi**: Ulangi proses hingga tujuan ditemukan atau *queue* menjadi kosong, yang menandakan tidak ada jalur yang ditemukan.


![Desktop View](assets/images/POST/PERTEMUAN4pt2/Screenshot 2025-06-09 152344.png){: width="650"}
_---_


Berikut adalah simulasi cara kerja BFS pada sebuah graf dengan **S** sebagai *start node* dan **G** sebagai *goal node*.

| SIMPUL AKTIF | QUEUE | VISITED |
| :--- | :--- | :--- |
| **S** | S | S |
| **A** | A, B | SA |
| **B** | B, C, D | SAB |
| **C** | C, D, E, F | SABC |
| **D** | D, E, F | SABCD |
| **E** | E, F | SABCDE |
| **F** | F, H, G | SABCDEF |
| **H** | H, G | SABCDEFH |
| **G** | G | SABCDEFHG |

***

### Contoh Kode (C++)

Berikut adalah implementasi sederhana dari algoritma BFS menggunakan C++.

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <unordered_map>
#include <algorithm>

using namespace std;

// Inisialisasi graf dengan adjacency list
unordered_map<char, vector<char>> graf;
// Menyimpan simpul yang sudah dikunjungi
unordered_map<char, bool> sudahDikunjungi;
// Menyimpan jalur: simpul_sekarang -> simpul_sebelumnya (parent)
unordered_map<char, char> parent;

void bfs(char start, char goal) {
    queue<char> q;
    q.push(start);
    sudahDikunjungi[start] = true;
    parent[start] = '/0'; // Titik awal tidak punya parent

    while (!q.empty()) {
        char sekarang = q.front();
        q.pop();

        cout << "Kunjungi node: " << sekarang << endl;

        // Jika goal ditemukan, hentikan pencarian
        if (sekarang == goal) break;

        // Iterasi ke semua tetangga dari node 'sekarang'
        for (char tetangga : graf[sekarang]) {
            if (!sudahDikunjungi[tetangga]) {
                q.push(tetangga);
                sudahDikunjungi[tetangga] = true;
                parent[tetangga] = sekarang;
            }
        }
    }

    // Cetak jalur terpendek dari goal ke start
    cout << "/n=== HASIL ===" << endl;
    cout << "Start Node: " << start << endl;
    cout << "Goal Node: " << goal << endl;

    vector<char> jalur;
    char current = goal;
    while (current != '/0') {
        jalur.push_back(current);
        current = parent[current];
    }
    reverse(jalur.begin(), jalur.end()); // Balik urutan jalur

    cout << "Jalur Terpendek: ";
    for (size_t i = 0; i < jalur.size(); i++) {
        cout << jalur[i];
        if (i != jalur.size() - 1) cout << " -> ";
    }
    cout << endl;
}
```

***

### Aplikasi Nyata BFS

BFS sangat efektif dan banyak digunakan dalam berbagai aplikasi dunia nyata.

* **Pencarian Jalur dalam Labirin atau Game**: BFS digunakan untuk menemukan jalan terpendek dari titik awal ke tujuan. Contohnya adalah game Pac-Man yang menghitung rute terpendek untuk mengejar pemain.
* **Rekomendasi di Media Sosial**: Platform seperti Facebook dan LinkedIn menggunakan BFS untuk fitur "Orang yang Mungkin Anda Kenal". Algoritma ini bekerja dengan menelusuri teman langsung (level 1), lalu teman dari teman (level 2), dan seterusnya.
* **Pemetaan Jaringan Komputer**: BFS dapat memetakan semua perangkat (PC, server, router) dalam sebuah jaringan. Dimulai dari router utama, BFS akan menelusuri perangkat yang terhubung per level, seperti switch di level 1 dan PC di level 2.
* **Sistem Navigasi dan Transportasi**: Aplikasi seperti Google Maps, Grab, atau Gojek menggunakan BFS untuk menemukan rute terpendek, terutama jika semua jalur dianggap memiliki bobot yang sama (misalnya, mencari rute dengan jumlah persimpangan paling sedikit).

***

### Kelebihan dan Kekurangan

* **Kelebihan**: BFS menjamin penemuan solusi yang paling baik (optimal dan komplit), terutama untuk mencari jalur terpendek pada graf tak berbobot.
* **Kekurangan**: Membutuhkan memori dan waktu yang cukup banyak, terutama jika graf atau pohon sangat lebar.

***

### Kesimpulan

BFS adalah algoritma penelusuran graf yang menjelajahi simpul secara berlapis dari titik awal. Dengan bantuan struktur data *queue*, BFS memastikan semua simpul terdekat dijelajahi terlebih dahulu, menjadikannya metode yang ideal untuk mencari jalur terpendek pada graf tak berbobot. Berkat efektivitasnya, BFS banyak diterapkan dalam berbagai aplikasi modern, mulai dari game, peta digital, hingga analisis jaringan sosial.

![Desktop View](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTttgR1killt0xv2UYUV1Gkc9eU4_eSviJYmA&s){: width="350"}
_---_
