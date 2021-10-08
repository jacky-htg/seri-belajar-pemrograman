# Error Handling

Dalam membuat aplikasi, error pasti akan terjadi dan harus kita handle. Error bisa disebabkan oleh banyak hal, sintaks kode yang salah, input user yang salah, dan lain-lain.

### try - catch

Penangan error dilakukan dengan sintaks try - catch, artinya kita akan mencoba untuk mengeksekusi suatu kode, namun jika ada error kita akan menagkapnya.

```javascript
try {
  alart("selamat pagi");
} catch (err) {
  console.error("terjadi error : ", err);
}
```

### throw error

error bisa dibuat secara kustom melalui perintah throw.

```javascript
try {
  const angka = prompt("masukkan angka untuk dibagi");
  switch (true) {
    case angka == 0:
      throw "tidak bisa membagi dengan nol";
      break;
    case angka < 0 :
      console.log("membagi dengan angka negatif");
      break;
    case angka > 0 :
      console.log("membagi dengan angka positif");  
      break;
  }
} catch (err) {
  console.error("terjadi error : ", err);
}
```

### finally

finally adalah suatu blok yang selalu dieksekusi dalam sebuah rangkaian try-catch-finally

```javascript
try {
  const angka = prompt("masukkan angka untuk dibagi");
  switch (true) {
    case angka == 0:
      throw "tidak bisa membagi dengan nol";
      break;
    case angka < 0 :
      console.log("membagi dengan angka negatif");
      break;
    case angka > 0 :
      console.log("membagi dengan angka positif");  
      break;
    default:
      console.log("anda tidak memasukkan angka");
      break;
  }
} catch (err) {
  console.error("terjadi error : ", err);
} finally {
  console.log("selesai");
}
```

