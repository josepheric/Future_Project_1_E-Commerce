

# Laporan Minggu 1&2

    9-23 Februari 2021

## Membuat Relational Database
Pada Dataset Terdapat 7 table yaitu:

 - Feedback
 - Order
 - Order Item
 - Products
 - Payment
 - User
 - Seller  

Ke 7 tables itu berupa file csv. Maka pertama-tama, 7 tables itu diimport menjadi tables pada database postgresql. Hal ini dapat dilakukan menggunakan fitur import dari DBeaver.  
**![](https://lh3.googleusercontent.com/dEwJ8fV6p-jG01xy72fYjWwzGHu9VeJHsmDaluBUXwjDeNbSbKYku-50Tbp94awi6igSqTzxiOZ0RMx3LbYwvz_jbr2vJ-DXS1pEamuS4C3laqZvippKM09kul8LUbpyWTE_Q-sm)**  
Setelah itu, ditentukan cardinality antar table sebagai berikut:
|  Table 1 | Key | Table 2  | Cardinality (T1 to T2)  |
|--|---|---|---|
| feedback |  order_id | order  | Many to 1  |
|  order_item | order_id  | order  | Many to 1  |
|  order_item | product_id  | product  | Many to 1   |
| payment  | order_id  |  order | Many to 1  |
|  user | user_name  | order  | **TBD**  |   

Berikut berberapa hal yang saya temukan dari mengeksplorasi tabel-tabel diatas: 
 - 1 order bisa banyak feedback : feedback bisa diupdate oleh user berkali-kali  
 **![](https://lh4.googleusercontent.com/YIgNXEF27oQRM_aeWFq739NLPuPItNj7bKPWhuE5hn8vex7LD7MLsdgcQVzlXjeS7UBmo3xkjCealpxTTVIJ94ZPv5JQZUBvg_vfA0ZwpIJ1MaKVfkvmWwvw9SuyUzzk4oSdXdyT)**  
 - Pada 1 order id, bisa terdapat banyak product (banyak product id)
 **![](https://lh4.googleusercontent.com/Mla-EI-29M6RagJMyziXEqieKyKhP8DWpmLoEMmnBpSv333Hn8msBPfcKTqroYojQCp0R8fuOldU1S_PEU2b22FNcFgZdD3JVNGUePnw90Pg9cfjKiJVonhzlHaYMiX1tjXLqfJn)      ![](https://lh3.googleusercontent.com/y9rXDbU3bLN-DoIxREFDIoXbv7UHCzIYLo4dsCfvNkIXTYItnAuvo2MugR0gJsIzLJA6gN5O7rT-rQL7jO_EpW8ga1ZePS5K6i45fUKokppWfUxpXxmCRdzEP4p64CsK2zdiwa1x)**     
- Pada 1 order id, bisa terdapt 1 product yang dibeli dalam jumlah banyak  
 **![](https://lh6.googleusercontent.com/xAIG878h_4_hWmiDzQ5qxW5avPQEEVP7-feZL_NAHzHrNxVvYdpAIWHMRcSwZsz9Z3FU-InhQY7yQPrMGScKgMfEo1Fc_GPukskAacSmxffHvPDo02WR7nuhhXLbgxD_wSpqpP2P)**  
- Pada 1 order id, dapat berbagai produk dari berbagai macam seller: 
 **![](https://lh6.googleusercontent.com/aGb-OqV9RO3WNOps_JRsygzHLBbCuv2l6_5ccQcjgiCPk1G4vOvhbOv8UnYQ80R_XSb10b3pnlVcw0mZW9MhPzoDbtiMI1URTPRbs-kO7CZB3YEurDc3oIyxr46q0_ArsGK-86mj)**  

Selain itu, saya juga menemukan berberapa issue dari tabel-tabel diatas: 

### Issue 1 :   
Saya menemukan kesulitan untuk menetukan cardinality dari table user dan table order. Table order dan table user dihubungkan oleh keberadaan user_name. Namun user_name pada table user sendiri dapat berupa duplikat:    
**![](https://lh5.googleusercontent.com/9qU8MT-Bqc9-mSx_pLWNzu_k4jy8WAcvdmuRbW_rDXDnP4rJ-mp8wM3k-rOrmhuqGo8qv8tB-YYb_SnBVEdMO_6obuq16nmmsI-Elgv1r2es9FAVIudoUi380c6-QP_fneQZzWAI)**  
dan bahkan user_name yang sama, dapat memiliki zip code, city, dan state yang berbeda:  
**![](https://lh3.googleusercontent.com/bMPKDRFN2MsxEtYjiAdoqJ-6qcStfeUN7EBNlhx6c5C77NbhEfyHKs4ZQUkHgolRYGJ5ZeX1fadvA5ixv5DNu2Lyq7Z68nWvI50zPoQShQ75lISHiDKeNz08SumAJcypSYzumGQF)**   
Setelah eksplorasi data lebih lanjut, tampaknya table user ini dibuat dari setiap kali suatu user membuat order. Yang berarti, setiap kali ada 1 order baru (order_id baru), maka akan muncul 1 user pada table user. Hal ini dibuktikan dari jumlah user_name yang sama pada table order maupun table user.  
**![](https://lh6.googleusercontent.com/5BFRQ-ZQeyv8IRnUQX30c8EmGFXXVmng9d2DHdf0F9Qm8MNkpn-QkgLcYhRk2I68WgAXPtg-bqqMU8tc_t4e2sYwqYg-qo5JaozDI91v3JHULtNWsY3L3GkP2fgBlJze0HeyRYLY)** **![](https://lh6.googleusercontent.com/A9nkkeI0RdpWWbSSIfC_AjFEcGTJrX222pSpxX1EuZ1kN--Qr5f3qWYP4OogQCzfCgU1_s9YXvDWb4fGwzOvW93cyQXyWSkD5Tg037pMhO7kZ9d4-HsgpTYkgA6GzFPSm5YWNCw0)**  
Permasalahan muncul bila ada user_id yang sama, dan melakukan order dengan 2 atau lebih alamat berbeda.  
**![](https://lh3.googleusercontent.com/bMPKDRFN2MsxEtYjiAdoqJ-6qcStfeUN7EBNlhx6c5C77NbhEfyHKs4ZQUkHgolRYGJ5ZeX1fadvA5ixv5DNu2Lyq7Z68nWvI50zPoQShQ75lISHiDKeNz08SumAJcypSYzumGQF)**    
**Kita tidak dapat memetakan order_id mana, memiliki alamat yang mana pada case user_name yang sama. (In Progress)**   
Dikarenakan desain database tidak diperbolehkan untuk mengubah struktur tabel, saya belum menemukan solusi agar user_name bisa menjadi uniqe (agar dapat digunakan sebagai primary key).  

### Issue 2:
Saya menemukan bahwa 1 feedback_id bisa dipake untuk banyak order_id :  
**![](https://lh4.googleusercontent.com/2bQIFjumr8hMCzYqzpQnhIrD8ADsgnH_IDghAlPKqR9fg_xNAD_z5QAK3pAUmd-6SIRiYE6di2i5NqHb-QcBt8mNDAoHSrCAf3GzhMBOx9tL8_5UnDACMJBc6uCl4Gr68Lf_n9ci)**  
Hal ini merupakan suatu anomali, dikarenakan feedback_id untuk setiap order seharunya uniqe (berdasarkan proses bisnis yang ada).  
Solusi: feedback id akan dibuat uniqe saat sudah masuk ke data warehouse.  

## Membuat Data Warehouse
Proses pembuatan  desain Data Warehouse:   
- Identifikasi Proses Bisnis: proses bisnis standard e-commerce, dimana user dapat membeli suatu produk dari suatu seller, serta dapat memberikan review atas produk itu. Berikut berberapa pertanyaan bisnis yang nantinya diharapkan dapat dijawab oleh data warehouse: 
	-    List sales by product groups, ordered by order_date?
    
		-   What type of payment options is most common?
    
	-   What is the purchase history for repeated users?
    
	-   What types of products do repeat customers most often purchase?
    
	-   What is the average time from ordering date to shipping date? Does this vary by product?
    
	-   What are the Top 5 products sold based on the time of year and location?
    
	-   What are the top 5 products sold by product category and customer location?
    
	-   What are the top categories of products sold based on time of year and location?
    
	-   What are the top 5 sellers with most sales for each month / year?
    
	-   What are the top 5 sellers by seller’s city / state?
    
	-   What is the relation between feedback score and sales amount?
    
	-   What are the sales for each month ordered by highest sales?
- Mendefinisikan Grain: dari proses bisnis dan business question yang kiranya nanti digunakan, saya mendefinisikan grain sebagai berikut:  
*sebuah produk (line item) yang dipesan oleh seorang customer pada suatu hari dan dijual oleh seorang seller yang dibayar dengan suatu metode tertentu beserta feedbacknya.* Grain ini akan berada pada level daily (harian).
-  Mendefinisikan Dimension:
	1.  Product dimension
	2.  Customer dimension
	3.  Seller dimension
	4.  Date dimension  
	5.  Payment dimension
	6.  Feedback dimension
- Mendefinisikan Measures / pengukuran: 
	1.  Sales Ammount: harga produk terjual
	2. Shipping Cost: biaya ongkos kirim

### Star Schema
**On Going**: akan dikerjakan pada minggu selanjutnya.
