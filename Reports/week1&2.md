
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

**Issue** :   
Saya menemukan kesulitan untuk menetukan cardinality dari table user dan table order. Table order dan table user dihubungkan oleh keberadaan user_name. Namun user_name pada table user sendiri dapat berupa duplikat:    
**![](https://lh5.googleusercontent.com/9qU8MT-Bqc9-mSx_pLWNzu_k4jy8WAcvdmuRbW_rDXDnP4rJ-mp8wM3k-rOrmhuqGo8qv8tB-YYb_SnBVEdMO_6obuq16nmmsI-Elgv1r2es9FAVIudoUi380c6-QP_fneQZzWAI)**  
dan bahkan user_name yang sama, dapat memiliki zip code, city, dan state yang berbeda:  
**![](https://lh3.googleusercontent.com/bMPKDRFN2MsxEtYjiAdoqJ-6qcStfeUN7EBNlhx6c5C77NbhEfyHKs4ZQUkHgolRYGJ5ZeX1fadvA5ixv5DNu2Lyq7Z68nWvI50zPoQShQ75lISHiDKeNz08SumAJcypSYzumGQF)**   
Setelah eksplorasi data lebih lanjut, tampaknya table user ini dibuat dari setiap kali suatu user membuat order. Yang berarti, setiap kali ada 1 order baru (order_id baru), maka akan muncul 1 user pada table user. Hal ini dibuktikan dari jumlah user_name yang sama pada table order maupun table user.  
**![](https://lh6.googleusercontent.com/5BFRQ-ZQeyv8IRnUQX30c8EmGFXXVmng9d2DHdf0F9Qm8MNkpn-QkgLcYhRk2I68WgAXPtg-bqqMU8tc_t4e2sYwqYg-qo5JaozDI91v3JHULtNWsY3L3GkP2fgBlJze0HeyRYLY)** **![](https://lh6.googleusercontent.com/A9nkkeI0RdpWWbSSIfC_AjFEcGTJrX222pSpxX1EuZ1kN--Qr5f3qWYP4OogQCzfCgU1_s9YXvDWb4fGwzOvW93cyQXyWSkD5Tg037pMhO7kZ9d4-HsgpTYkgA6GzFPSm5YWNCw0)**  
Permasalahan muncul bila ada user_id yang sama, dan melakukan order dengan 2 atau lebih alamat berbeda.  
**![](https://lh3.googleusercontent.com/bMPKDRFN2MsxEtYjiAdoqJ-6qcStfeUN7EBNlhx6c5C77NbhEfyHKs4ZQUkHgolRYGJ5ZeX1fadvA5ixv5DNu2Lyq7Z68nWvI50zPoQShQ75lISHiDKeNz08SumAJcypSYzumGQF)**    
**Kita tidak dapat memetakan order_id mana, memiliki alamat yang mana pada case user_name yang sama. (In Progress)** 
