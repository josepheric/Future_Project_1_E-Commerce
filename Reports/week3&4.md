

# Laporan Minggu 3&4

    23 Februari - 9 Maret 2021
## Membuat DataWarehouse 
### Star Schema  
Berikut Star Schema / desain data warehouse: (**Outdated**)

**![](https://lh6.googleusercontent.com/yF9PlaofIOV-VnWhPOFuJMab_XyRLSb9dKMbXoMl8HtIGu_s8ivu4UlrBUrbynC4kSbqpVxVb5Fpg8Wb1H3E485OslKpyl1eypP--zfXSdO-yF9XZBUYf0Etc00zElFTyFsskpLu)**

Catatan: pada fact tables, order_date_sk, order_approved_date_sk, ship_date_sk, pickup_limit_date_sk, pickup_date_sk, estimated_delivery_date_sk, delivered_date_sk akan menggunakan date_sk pada dates dimension.  

Revisi StarSchema (**Current StarSchema**):   
**![](https://lh6.googleusercontent.com/rBFr87xnrVXpacWPt2fS35SMjda5s9dLbPyqsYSB-_bKUCXNKnnOGmezGS5zxO-V5sHHH-6Um1SYWiRAl5uKYGtACXoRHuSRsqzVoQwLZiM14J7B7D7fJYh-0w-4kS6pFmxlIaOW)**  

 - Review dimension dihilangkan karena fact table yang dibuat hanya
   tentang sales / penjualan saja.   
   
 - Date Dimension diperlengkap



### Proses ETL
Pertama-tama dibuat sebuah schema baru bernama datawarehouse pada database yang sebelumnya sudah ada. Database sebelumnya berada di schema public.    
**![](https://lh4.googleusercontent.com/GKHmzydhr0cvnOmJvr-r5rI8bb4bcnW38_TV2G48-hREGIk8H-BuUrBUiCREcoMH3QlGLnedm24OVwdpP7-qg-KIetO-hFXU7kEjqVTCJZIpt9GzWHXmn54-zPMjOw0IjP9_aFuc)**    
#### Date Dimension
Selanjutnya saya membuat date dimension terlebih dahulu. Disini saya membuat date dimension menggunakan bantuan Microsoft Excel.   
**![](https://lh5.googleusercontent.com/wsArn7jCO2_TGF4pC5mi-i8ne2Sz3gHYVIxqXkhZI_JXMC5pswqmGBdYLE-5CAC4OBsqnicBEd4rgwifWL7jKPotfT-MrQUs8yWlKE26-POM5tfTdNfJoSfk8kPGOC_A87jZnJQu)**  
Saya membuat DateDimension dari tahun 2016 - 2021 agar dapat mengcakup seluruh tanggal yang nantinya digunakan,    

### Product, Seller, & User Dimension
Ketiga dimensi diatas saya buat dengan mengambil data dari tabel-tabel yang ada di schema public. Pada ketiga dimension ini, terdapat Surrogate Key (SK) masing-masing. Script postgreSQL lengkap dapat dilihat disini:  

### Sales Fact Table
Saya membuat fact tabel sesuai dengan desain dari starSchema, lalu memasukkan data dari tabel-tabel yang ada di schema public beserta key (SK) dari tiap-tiap dimension. Script postgreSQL lengkap dapat dilihat disini:  

Berikut Screenshot dari tabel salesfact:
**![](https://lh5.googleusercontent.com/tgklFKgApO97F_3cIyVE_QXCAQWcUpJQOBlcjRl0QjvQP_gvAz1R0oUg6Mp5VIl825lNx64URu0agwpP8l31trXkUfvv36N2GOKz4Qd4doUDRPJVJoeXCk5Qit8E7jlmst2yb8eb)**  



