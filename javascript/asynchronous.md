# Asynchronous

Asynchronous adalah suatu proses yang dikerjakan secara bersamaan. Di javascript, umunya suatu kode dikerjakana secara berurutan \(synchronous\), namun ada banyak yang dikerjakan secara asynchronous sepert event dan Ajax.

Keuntungan penggunaan aynchronous adalah proses menjadi lebih cepat, karena tidak harus menunggu suatu blok kode selessai dikerjakan. Jika javascript menemukan suatu proses yang lama, maka sambil menunggu proses itu selesai, javascript akan mengeksekusi kode selanjutnya.

Kelemahan asynchronous adalah adanya kemungkinan race condition jika ada suatu blok kode yang membutuhkan hasil dari proses lain, tenryata dieksekusi ketika proses lain tersebut belum memberikan hasil. Besar kemungkinan ketika bliok kode tersebut, datanya masih kosong.

Untuk mengatasi hal tersebut, dalam pemrograman asynchronous dioptimalkan penggunaan callback, async/await dan promise.

Callback

Kita telah mempelajari callback sebelumnya. Dalam proses asynchronous, penggunaan callback sangat masif.  



