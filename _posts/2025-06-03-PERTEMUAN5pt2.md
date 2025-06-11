---
title: DIJKSTRA's ALGORITHM
date: 2025-05-27
categories: [DESAIN ANALISIS ALGORITMA, DIJKSTRA's ALGORITHM]
tags: [daa, algorithm, backtracking, dijkstra]     # TAG names should always be lowercase
---

Pernahkah klen bertanya-tanya? bagaimana aplikasi peta seperti Google Maps dapat menemukan rute tercepat ke tujuan Anda di antara ribuan kemungkinan jalan? Jawabannya terletak pada algoritma pencarian jalur yang cerdas. Salah satu yang paling fundamental dan terkenal adalah **Algoritma Dijkstra**.

### Apa itu Algoritma Dijkstra?

**Algoritma Dijkstra** adalah sebuah metode yang digunakan untuk mencari jalur terpendek antara dua titik dalam sebuah graf. Graf ini bisa berupa jaringan yang terdiri dari simpul (titik) dan sisi (hubungan antar titik) dengan bobot tertentu pada sisi-sisinya. Algoritma ini membantu kita menentukan jalur terpendek dari titik awal ke titik tujuan.

-----

### Cara Kerja Algoritma Dijkstra

Algoritma ini bekerja dengan langkah-langkah sistematis sebagai berikut:

1.  Buat sebuah tabel dengan kolom sebagai tempat nilai atau jarak dari simpul, dan baris sebagai posisi simpul.
2.  Pilih simpul awal dan simpul tujuan, dengan syarat keduanya harus terhubung secara langsung.
3.  Hitung jarak untuk beberapa simpul tujuan yang telah dipilih.
4.  Setelah semua simpul diuji, pilih jarak yang terpendek.
5.  Simpul yang dipilih akan menjadi acuan untuk tahap selanjutnya, dan proses diulangi hingga semua simpul telah diuji.

-----

### Contoh Permasalahan

Carilah nilai dan lintasan terpendek dari simpul **A** ke simpul **F** pada graf berikut.

Berdasarkan perhitungan, ditemukan bahwa **lintasan terpendek adalah ABEF atau ABDF dengan total nilai 4**.

-----

### Implementasi Kode (C++)

Berikut adalah contoh implementasi standar dari Algoritma Dijkstra dalam C++ yang menggunakan *priority queue* untuk efisiensi.


{% raw %}
```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <limits>
#include <map>

using namespace std;

const int INF = numeric_limits<int>::max();

void dijkstra(const map<char, vector<pair<char, int>>>& graph, char start_node) {
    map<char, int> dist;
    for (auto const& [node, neighbors] : graph) {
        dist[node] = INF;
    }
    dist[start_node] = 0;

    // Priority queue untuk menyimpan pasangan {jarak, simpul}
    // Diurutkan berdasarkan jarak terkecil
    priority_queue<pair<int, char>, vector<pair<int, char>>, greater<pair<int, char>>> pq;
    pq.push({0, start_node});

    while (!pq.empty()) {
        int d = pq.top().first;
        char u = pq.top().second;
        pq.pop();

        // Jika jarak yang tersimpan lebih kecil, lewati
        if (d > dist[u]) {
            continue;
        }

        // Iterasi melalui tetangga dari simpul u
        if (graph.count(u)) {
            for (auto const& edge : graph.at(u)) {
                char v = edge.first;
                int weight = edge.second;

                // Jika ditemukan jalur yang lebih pendek ke v melalui u
                if (dist[u] + weight < dist[v]) {
                    dist[v] = dist[u] + weight;
                    pq.push({dist[v], v});
                }
            }
        }
    }

    // Cetak jarak terpendek dari simpul awal
    cout << "Jarak terpendek dari simpul " << start_node << ":" << endl;
    for (auto const& [node, distance] : dist) {
        if (distance == INF) {
            cout << "  ke " << node << " = Tak terhingga" << endl;
        } else {
            cout << "  ke " << node << " = " << distance << endl;
        }
    }
}

int main() {
    map<char, vector<pair<char, int>>> graph;
    graph['A'] = {{'B', 1}, {'C', 5}};
    graph['B'] = {{'D', 2}, {'E', 1}, {'C', 2}};
    graph['C'] = {{'E', 2}};
    graph['D'] = {{'F', 1}};
    graph['E'] = {{'D', 3}, {'F', 2}};
    graph['F'] = {};

    // Menjalankan algoritma dari simpul 'A'
    dijkstra(graph, 'A');

    return 0;
}
```
{% endraw %}


-----

### Contoh Penggunaan

  * **Navigasi Jalan**: Saat kita ingin mencari rute terpendek dari rumah ke sekolah, Algoritma Dijkstra akan membantu menentukan jalan mana yang lebih pendek dengan mempertimbangkan semua jalan yang ada.
  * **Pengiriman Barang**: Sebuah perusahaan ekspedisi yang ingin mengirim paket dari gudang ke beberapa pelanggan dapat menggunakan Algoritma Dijkstra untuk menentukan rute pengiriman yang paling efisien agar paket sampai lebih cepat dan tidak boros bensin atau tenaga.

-----

### Kelebihan dan Kekurangan

#### Kelebihan 👍

  * **Menjamin Jalur Terpendek**: Dijkstra selalu menemukan solusi yang optimal (jalur terpendek) selama semua bobot sisi bernilai positif.
  * **Efisien untuk Banyak Aplikasi**: Algoritma ini sangat cocok untuk graf yang padat dan sering digunakan dalam aplikasi nyata seperti GPS dan *routing* jaringan.
  * **Dapat Menyelesaikan Banyak Tujuan Sekaligus**: Dengan sekali eksekusi dari satu titik awal, algoritma ini bisa memberikan informasi jarak terpendek ke semua titik lainnya.

#### Kekurangan 👎

  * **Tidak Bekerja dengan Bobot Negatif**: Algoritma ini tidak dapat digunakan jika ada sisi dengan bobot negatif.
  * **Kurang Efisien untuk Graf Besar yang Jarang Terhubung**: Pada graf yang sangat besar dan *sparse* (jarang terhubung), kinerjanya bisa menjadi lambat jika tidak dioptimalkan dengan struktur data *priority queue*.
  * **Perhitungan Bisa Terlalu Luas**: Jika hanya mencari jalur dari A ke B, Dijkstra tetap menghitung jarak ke semua titik lain, yang terkadang tidak efisien. Untuk kasus seperti ini, algoritma lain seperti A\* (A-Star) bisa lebih baik.

-----

### Kesimpulan

Algoritma Dijkstra merupakan salah satu algoritma pencarian jalur terpendek yang paling efisien dan banyak digunakan dalam teori graf. Algoritma ini bekerja dengan cara mencari jalur terpendek dari satu simpul sumber ke semua simpul lainnya dalam graf berbobot non-negatif. Melalui pendekatan *greedy*, Dijkstra memastikan bahwa setiap langkahnya mendekatkan solusi menuju hasil optimal. Keunggulan utama algoritma ini terletak pada keakuratannya dan efisiensinya, terutama jika dikombinasikan dengan struktur data seperti *priority queue* atau *min-heap*. Dalam implementasi praktis, algoritma Dijkstra sangat berguna dalam berbagai bidang seperti jaringan komputer, sistem navigasi, dan pemodelan transportasi.