# tugas-kelompok-
# Nama Kelompok : 
Ni Putu Indahning Sasmita (2501010104)
Maria Indriani Lelu (2501010335)

# 1. Pendahuluan
1.1 Latar Belakang
Peningkatan jumlah kendaraan bermotor seringkali tidak sebanding dengan ketersediaan lahan parkir yang memadai. Pengelolaan parkir secara manual menggunakan pencatatan kertas rentan terhadap kesalahan manusia (human error), kehilangan data, dan potensi kebocoran pendapatan. Oleh karena itu, diperlukan sistem digital sederhana yang dapat mencatat waktu secara otomatis dan menghitung tarif dengan akurat untuk meningkatkan efisiensi operasional.

1.2 Rumusan Masalah
Bagaimana cara mencatat waktu masuk dan keluar kendaraan secara otomatis?
Bagaimana logika perhitungan tarif parkir berdasarkan durasi waktu yang tepat?
Bagaimana cara mengelola data kendaraan yang sedang berada di dalam area parkir?

1.3 Tujuan
Membangun aplikasi parkir yang dapat melakukan pencatatan data kendaraan (plat nomor).
Mengotomatisasi perhitungan biaya parkir berdasarkan selisih waktu masuk dan keluar.
Menyediakan laporan sederhana mengenai status kendaraan yang terparkir.

# 2. Landasan Teori
Manajemen Data: Menggunakan struktur data Dictionary pada Python untuk menyimpan pasangan kunci (plat nomor) dan nilai (waktu masuk) guna akses data yang cepat (O(1) time complexity).
Pemrosesan Waktu: Menggunakan library datetime untuk manipulasi data waktu (objek timestamp).
Logika Tarif: Menerapkan pembulatan ke atas (metode ceiling) di mana setiap bagian dari satu jam yang dilewati akan dihitung sebagai satu jam penuh.

# 3. Desain dan Implementasi Sistem
3.1 Alur Kerja (Flowchart)
Input: User memasukkan plat nomor kendaraan.
Proses Masuk: Sistem memeriksa apakah plat sudah ada. Jika belum, catat datetime.now().
Proses Keluar: Sistem mencari plat di database, menghitung selisih waktu, dan menentukan biaya.
Output: Menampilkan struk parkir atau total biaya.

# 3.2 Pseudocode
Plaintext
ALGORITMA Sistem_Parkir
VAR
    daftar_parkir: DICTIONARY OF <string, datetime>
    TARIF_PER_JAM: INTEGER = 3000

PROSEDUR Masuk(plat_nomor)
    JIKA plat_nomor ADA DI daftar_parkir MAKA
        TAMPILKAN "Kendaraan sudah ada"
    SELAIN ITU
        daftar_parkir[plat_nomor] = WAKTU_SEKARANG
        TAMPILKAN "Kendaraan masuk"
    AKHIR JIKA
END PROSEDUR
PROSEDUR Keluar(plat_nomor)
    JIKA plat_nomor TIDAK ADA MAKA
        TAMPILKAN "Data tidak ditemukan"
    SELAIN ITU
        waktu_masuk = daftar_parkir[plat_nomor]
        durasi = WAKTU_SEKARANG - waktu_masuk
        total_jam = CEIL(durasi_dalam_detik / 3600)
        total_bayar = total_jam * TARIF_PER_JAM
        HAPUS daftar_parkir[plat_nomor]
        TAMPILKAN total_bayar
    AKHIR JIKA
END PROSEDUR

# 4. Implementasi Program (Python)
Berikut adalah kode yang sudah disempurnakan dengan menu interaktif:
Python
import datetime
import math
class SistemParkir:
    def __init__(self):
        self.data_parkir = {}
        self.tarif_per_jam = 3000
    def masuk(self, plat):
        if plat in self.data_parkir:
            print(f"\n[!] Kendaraan {plat} sudah terdaftar di dalam.")
        else:
            self.data_parkir[plat] = datetime.datetime.now()
            print(f"\n[OK] Kendaraan {plat} berhasil masuk pada {self.data_parkir[plat].strftime('%H:%M:%S')}")
    def keluar(self, plat):
        if plat not in self.data_parkir:
            print(f"\n[!] Plat {plat} tidak ditemukan.")
            return
        waktu_masuk = self.data_parkir.pop(plat)
        waktu_keluar = datetime.datetime.now()      
        selisih = waktu_keluar - waktu_masuk
        detik = selisih.total_seconds()
        # Logika: Minimal bayar 1 jam, selebihnya pembulatan ke atas
        jam = math.ceil(detik / 3600) if detik > 0 else 1
        total_bayar = jam * self.tarif_per_jam
        print("\n" + "="*25)
        print("      STRUK PARKIR      ")
        print("="*25)
        print(f"Plat Nomor  : {plat}")
        print(f"Jam Masuk   : {waktu_masuk.strftime('%H:%M:%S')}")
        print(f"Jam Keluar  : {waktu_keluar.strftime('%H:%M:%S')}")
        print(f"Durasi      : {jam} Jam")
        print(f"Total Bayar : Rp{total_bayar:,}")
        print("="*25)

# Fungsi Utama (Main Menu)
def main():
    app = SistemParkir()
    while True:
        print("\n--- MENU PARKIR SEDERHANA ---")
        print("1. Kendaraan Masuk")
        print("2. Kendaraan Keluar")
        print("3. Lihat Kendaraan Terparkir")
        print("4. Keluar Aplikasi")
        pilihan = input("Pilih menu (1-4): ")
        if pilihan == '1':
            plat = input("Masukkan Plat Nomor: ").upper()
            app.masuk(plat)
        elif pilihan == '2':
            plat = input("Masukkan Plat Nomor: ").upper()
            app.keluar(plat)
        elif pilihan == '3':
            print("\nDaftar Kendaraan di Dalam:")
            for p in app.data_parkir: print(f"- {p}")
        elif pilihan == '4':
            break
        else:
            print("Pilihan tidak valid.")
if __name__ == "__main__":
    main()

# 5. Kesimpulan
Sistem ini berhasil mengimplementasikan fungsi dasar pengelolaan parkir dengan memanfaatkan struktur data yang efisien dan modul waktu pada Python. Meskipun sederhana, sistem ini memiliki pondasi yang kuat untuk dikembangkan lebih lanjut, seperti penambahan kategori kendaraan (mobil/motor) atau integrasi dengan database fisik.
