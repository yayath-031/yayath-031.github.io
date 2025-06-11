---
title: DEPTH-FIRST SEARCH (DFS)
date: 2025-05-27
categories: [DESAIN ANALISIS ALGORITMA, DFS, BACKTRACKING ALGORITHM]
tags: [daa, algorithm, backtracking, dfs]     # TAG names should always be lowercase
---

![Desktop View](https://cdn.educba.com/academy/wp-content/uploads/2020/03/Depth-First-Search.jpg){: width="450"}
_---_

OLAA! COMO ESTAS?, *Depth-First Search* (DFS) atau Pencarian Mendalam Pertama adalah salah satu algoritma fundamental yang digunakan untuk menelusuri atau mencari data dalam struktur data pohon (*tree*) dan graf. Berbeda dengan saudaranya, *Breadth-First Search* (BFS), yang menjelajah lapis demi lapis, DFS memilih untuk menggali "sedalam" mungkin pada satu cabang sebelum kembali untuk menjelajahi cabang lain yang belum dikunjungi.

***

### Definisi Depth-First Search (DFS)

*Depth-First Search* (DFS) adalah algoritma pencarian atau penelusuran pada struktur data graf atau pohon yang bekerja dengan menjelajahi satu cabang sedalam mungkin sebelum mundur (*backtrack*) dan melanjutkan ke cabang berikutnya.

***

### Prinsip Utama dan Langkah-Langkah

Prinsip utama DFS adalah penggunaan struktur data **Tumpukan (*Stack*)** yang mengikuti metode **LIFO (Last-In, First-Out)**.

Algoritma DFS bekerja melalui langkah-langkah berikut:
1.  Masukkan simpul (node) akar ke dalam *stack*.
2.  Ambil satu simpul dari bagian teratas *stack*, lalu periksa apakah simpul tersebut merupakan solusi yang dicari.
    * Jika ya, pencarian selesai dan hasilnya dikembalikan.
    * Jika bukan, masukkan seluruh node anak (tetangga yang belum dikunjungi) dari simpul tersebut ke dalam *stack*.
3.  Jika *stack* tidak kosong, ulangi proses pencarian dari langkah ke-2.
4.  Jika *stack* kosong dan setiap simpul sudah diperiksa, maka pencarian berakhir.

***

### Contoh Kasus dan Ilustrasi

Jika penelusuran DFS dilakukan dari **simpul awal 1**, ada beberapa kemungkinan urutan kunjungan yang bisa dihasilkan, tergantung pada urutan simpul anak dimasukkan ke dalam *stack*.

**Kemungkinan Urutan Kunjungan dari Simpul 1:**
* `1 -> 2 -> 4 -> 5 -> 6 -> 7 -> 8 -> 9 -> 10`
* `1 -> 2 -> 5 -> 6 -> 7 -> 8 -> 9 -> 10 -> 4`
* `1 -> 2 -> 5 -> 6 -> 9 -> 10 -> 7 -> 8 -> 4`

Jika penelusuran dilakukan dari **simpul awal 1** dengan **tujuan akhir di simpul 10**, salah satu kemungkinan jalur yang ditemukan adalah `1, 2, 4, 6, 9, 10`.

***

<table>
  <tr>
    <td><img src="assets/images/POST/PERTEMUAN4pt3/Screenshot 2025-06-09 160547.png" alt="Gambar 1" width="400"></td>
    <td><img src="assets/images/POST/PERTEMUAN4pt3/Screenshot 2025-06-09 160534.png" alt="Gambar 2" width="400"></td>
  </tr>
</table>

### Implementasi Kode (C++)

Berikut adalah contoh implementasi DFS dalam bahasa C++.

```cpp
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

// Fungsi untuk menjalankan algoritma DFS
void DFS(int start, vector<vector<int>>& graph, vector<bool>& visited)
{
    stack<int> s;
    s.push(start);

    while (!s.empty()) {
        int node = s.top();
        s.pop();

        // Jika node belum dikunjungi
        if (!visited[node])
        {
            cout << node << " "; 
            visited[node] = true; 
        }

        // Masukkan semua tetangga yang belum dikunjungi ke stack
        for (int neighbor : graph[node]) {
            if (!visited[neighbor]) {
                s.push(neighbor);
            }
        }
    }
}

int main() {
    int n = 6;
    vector<vector<int>> graph(n);
    
    // Mendefinisikan hubungan antar node
    graph[0].push_back(1); 
    graph[0].push_back(2); 
    graph[1].push_back(0); 
    graph[1].push_back(3); 
    graph[1].push_back(4); 
    graph[2].push_back(0); 
    graph[2].push_back(5); 
    graph[3].push_back(1); 
    graph[4].push_back(1); 
    graph[5].push_back(2); 

    // Vektor untuk melacak node yang sudah dikunjungi
    vector<bool> visited(n, false);

    // Memulai penelusuran DFS dari node 1
    cout << "DFS traversal starting from node 1: ";
    DFS(1, graph, visited);
    cout << endl;

    return 0;
}
```

***

### Kelebihan dan Kekurangan

Sama seperti algoritma lainnya, DFS memiliki kelebihan dan kekurangan.

**Kelebihan 👍:**
* Penggunaan memori lebih efisien.
* Mudah diimplementasikan.
* Sangat cocok untuk menemukan solusi pada kedalaman maksimal.
* Menjadi dasar bagi banyak algoritma penting.

**Kekurangan 👎:**
* Tidak menjamin penemuan solusi terbaik atau terpendek.
* Bisa terjebak dalam *infinite loop* jika diimplementasikan pada graf siklik tanpa penanganan node yang sudah dikunjungi.
* Kurang efisien jika diterapkan pada graf yang sangat luas tetapi dangkal.
* Tidak cocok untuk semua jenis masalah pencarian.

***

### Kesimpulan

*Depth-First Search* (DFS) adalah algoritma penelusuran yang menjelajahi simpul sedalam mungkin pada satu cabang sebelum melakukan *backtracking* untuk melanjutkan ke simpul lainnya. Proses penelusuran ini dilakukan dengan bantuan struktur data *stack* yang bekerja berdasarkan prinsip LIFO (*Last-In, First-Out*). Penelusuran dimulai dari simpul akar, lalu terus menyusuri anak-anak simpul hingga mencapai simpul terdalam, sebelum kembali untuk menjelajahi cabang lain yang belum dikunjungi. DFS sangat cocok digunakan untuk pencarian solusi yang berada di kedalaman maksimal dan dapat menghasilkan jalur penelusuran yang berbeda-beda tergantung urutan pemrosesan simpulnya.

---

![Desktop View](https://i.pinimg.com/736x/72/5c/e4/725ce4ffc8bfc9772f8d677ba387ebb2.jpg){: width="300"}
_----_

---