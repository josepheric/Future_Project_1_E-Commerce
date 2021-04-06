# Laporan Minggu 5&6

    9 - 23 Maret 2021
## Kesalahan Pada Data Warehouse 
Setelah mengikuti mentoring dengan para mentor teknikal, saya menyadari ada berberapa kesalahan dari Data Warehouse saya.
### User Dimension
Masih ada user_name yang duplikat (memiliki username dan alamat yang sama persis). Ada juga user_name yang memiliki 2 alamat atau lebih ( 1 user_name terdapat berberapa alamat).
DIkarenakan tidak adanya data **waktu** user mengganti alamat, kita tidak dapat mengetahui pesanan mana, dikirimkan ke alamat mana (untuk kasus user_name memiliki lebih dari 1 alamat).   

Solusi: saya akan memilih salah satu alamat untuk setiap satu user_name yang memiliki banyak alamat, dan menghapus alamat lainnya.  


### Tidak Ada Data Review pada Data Warehouse
Pada Data Warehouse saya, masih belum ada data review. Sedangkan data warehouse wajib memiliki seluruh data dari semua file csv yang telah diberikan.  

Solusi: membuat dimension review dengan prinsip Slowly Changing Dimension agar dapat menampung review user yang dapat berubah dengan jalannya waktu.    

## Yang dilakukan selama minggu 5 & 6
Dikarenakan kesibukan kuliah, saya masih belum dapat mengimplementasikan solusi untuk permasalahan pada data warehouse saya. Saya masih mempelajari konsep slowly changing dimension untuk penerapan Review Dimension
