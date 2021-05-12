

# Laporan Minggu 9&10

    7 - 21 April 2021
## Memperbaiki Data Warehouse 
Setelah mengikuti mentoring dengan para mentor teknikal, saya menyadari ada berberapa kesalahan dari Data Warehouse saya.

### Mempebaiki Duplikat User Dimension
Solusi: User Dimension saya rank berdasarkan zipcode dan partisi berdasarkan username. Alamat yang disimpan adalah alamat dengan zip code terbesar. Duplikat username lainnya akan didelete pada Data Warehouse ini.  
**![](https://lh4.googleusercontent.com/IEGHjtCifHHgrwpf0aQZCtAcveuFuax5whdmRvSR2dBwxHxotL2QaEYKlZWrRmSxJe7ScR3On1wvl7YdaJtp2fUNiaVv946Yepp24uxoqBOx803CfwlH8xDS5mOfGLQ6rSrFb7-3)**  


### Menambahkan Review pada Data Warehouse
Saya mencoba membuat dimensi review menggunakan scd type 2. Saya berhasil menandai feedback terbaru. Namun saya belum berhasil memasukkkan end-date dari dimensi ini.   
**![](https://lh6.googleusercontent.com/BuRVVoq_GKkQLbJnAVMXWsUE12Cs96mjA8AXScmcsTh5QwIiVSwB8yTBFx30YM97LrWhIhSQr7jbXCiVIfS0C_uaLdO7PJ_2BJL9tbu-0KT4OgTpL9GBNtBazbiF-M-Rrm5Z1rkw)**  
