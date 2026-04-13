# tugas-kelompok-
LAPORAN SISTEM PARKIR SEDERHANA
1. Pendahuluan

Perkembangan teknologi informasi mendorong berbagai sistem manual untuk beralih menjadi sistem terkomputerisasi, termasuk dalam pengelolaan parkir. Sistem parkir yang masih dilakukan secara manual seringkali menimbulkan berbagai permasalahan, seperti ketidakteraturan antrian kendaraan, kesulitan dalam memantau kapasitas parkir, serta kurang efisien dalam proses keluar masuk kendaraan.

Untuk mengatasi permasalahan tersebut, diperlukan suatu sistem yang mampu mengelola antrian kendaraan secara terstruktur. Salah satu solusi yang dapat digunakan adalah dengan menerapkan konsep struktur data, khususnya queue (antrian) dengan metode FIFO (First In First Out).

Pada penelitian ini, dirancang sebuah sistem parkir sederhana menggunakan linked list sebagai struktur penyimpanan data. Dengan sistem ini, kendaraan yang pertama masuk akan menjadi kendaraan pertama yang keluar, sehingga proses parkir menjadi lebih teratur dan efisien.

2. Isi (Pembahasan)
2.1 Rumusan Masalah
Bagaimana penerapan struktur data queue dalam sistem parkir sederhana?
Bagaimana sistem mengelola antrian kendaraan masuk dan keluar?
Bagaimana implementasi linked list dalam sistem parkir?
2.2 Landasan Teori

Struktur data merupakan cara untuk menyimpan dan mengorganisir data agar dapat digunakan secara efisien. Salah satu struktur data yang sering digunakan dalam kehidupan sehari-hari adalah queue, yaitu struktur data yang menerapkan prinsip FIFO (First In First Out), di mana data yang pertama masuk akan menjadi data yang pertama keluar.

Queue banyak digunakan dalam berbagai sistem, seperti antrian layanan pelanggan, sistem printer, dan sistem parkir. Dalam implementasinya, queue dapat menggunakan array maupun linked list. Namun, linked list memiliki keunggulan dalam hal fleksibilitas ukuran karena tidak memiliki batasan kapasitas tetap seperti array.

Linked list adalah struktur data yang terdiri dari kumpulan node, di mana setiap node berisi data dan referensi ke node berikutnya. Dengan menggunakan linked list, proses penambahan dan penghapusan data dapat dilakukan secara dinamis tanpa perlu menggeser elemen seperti pada array.

2.3 Desain Sistem
Alur Sistem:

Input → Proses → Output

Input: nomor plat kendaraan
Proses: tambah/hapus data (enqueue & dequeue)
Output: daftar kendaraan parkir

2.4 Implementasi Sistem 
# Node Linked List
class Node:
    def _init_(self, plat):
        self.plat = plat
        self.next = None

# Queue Parkir
class Parkir:
    def _init_(self, kapasitas):
        self.front = None
        self.rear = None
        self.kapasitas = kapasitas
        self.jumlah = 0

    # Kendaraan masuk (Enqueue)
    def masuk(self, plat):
        if self.jumlah >= self.kapasitas:
            print("Parkir penuh!")
            return
        
        new_node = Node(plat)

        if self.rear is None:
            self.front = self.rear = new_node
        else:
            self.rear.next = new_node
            self.rear = new_node

        self.jumlah += 1
        print(f"Kendaraan {plat} masuk")

    # Kendaraan keluar (Dequeue)
    def keluar(self):
        if self.front is None:
            print("Parkir kosong!")
            return
        
        keluar = self.front
        self.front = self.front.next

        if self.front is None:
            self.rear = None

        self.jumlah -= 1
        print(f"Kendaraan {keluar.plat} keluar")

    # Lihat kendaraan depan
    def peek(self):
        if self.front is None:
            print("Parkir kosong!")
        else:
            print(f"Kendaraan terdepan: {self.front.plat}")

    # Tampilkan semua
    def display(self):
        if self.front is None:
            print("Parkir kosong!")
            return
        
        current = self.front
        print("Daftar kendaraan:")
        while current:
            print(current.plat)
            current = current.next


# Program utama
parkir = Parkir(5)

while True:
    print("\n1. Masuk")
    print("2. Keluar")
    print("3. Peek")
    print("4. Tampilkan")
    print("5. Keluar Program")

    pilih = input("Pilih: ")

    if pilih == "1":
        plat = input("Plat nomor: ")
        parkir.masuk(plat)
    elif pilih == "2":
        parkir.keluar()
    elif pilih == "3":
        parkir.peek()
    elif pilih == "4":
        parkir.display()
    elif pilih == "5":
        break
    else:
        print("Pilihan salah!")

3. Kesimpulan

Berdasarkan hasil perancangan dan implementasi sistem parkir sederhana, dapat disimpulkan bahwa penggunaan struktur data queue dengan metode FIFO mampu mengelola antrian kendaraan secara teratur dan sistematis.

Implementasi menggunakan linked list memberikan fleksibilitas dalam pengelolaan data karena tidak memiliki batasan ukuran tetap, sehingga lebih efisien dibandingkan array dalam kasus tertentu.

Sistem yang dibangun telah mampu menjalankan fungsi utama, yaitu menambahkan kendaraan, mengeluarkan kendaraan, menampilkan data, serta melihat kendaraan terdepan. Dengan demikian, sistem parkir sederhana ini telah berhasil memenuhi tujuan dan sesuai dengan konsep teori struktur data
