# String

Untuk menulis string digunakan tanda petik dua \("\) atau tanda petik satu \('\).

```javascript
console.log('Selamat pagi dunia!');
console.log("Selamat pagi dunia!"); 
```

Meski kita bebas menggunakan tanda petik dua maupun tanda petik satu, pastikan Anda hanya mengunakan salah satunya saja. Ini demi konsistensi dan kemudahan maintenance kode. 

Untuk menulis string yang mengandung quote/tenda petik, bisa menggunakan tanda petik yang berbeda dengan yang hendak dicetak atau menggunakan prefix backslash.

```javascript
console.log('Matahari tersenyum menyapa, "Selamat pagi dunia!"');
console.log("Matahari tersenyum menyapa, \"Selamat pagi dunia!\"");
```

## Properti 

### length

Untuk mendapatkan panjang suatu string, gunakan properti length

```javascript
let salam = "Apa Kabar";
console.log("Selamat pagi dunia!".length);
console.log(salam.length);
```

## Method

Ada banyak method yang dimiliki oleh string, kita ahnaya akan membahas sebagian yang menurut saya pribadi sering digunakan.

### Mengambil potongan string : slice dan substring/substr

Ada dua cara untuk mengambil potongan string, bisa melalui slice\(\), dan substring\(\).

```javascript
Syntax: string.slice(start, stop);
Syntax: string.substring(start, stop);
```

#### Slice

Digunakan untuk mengambil bagian dari string yang diberikan. Caranya dengan melempar index awal dan index akhir dari slice/potongan string yang diinginkan.  Indek yang diberikan bisa bernilai positif maupun negatif. Jika positif, indek dihitung dari kiri string. JIka negatif, indek dihitung dari kanan string.

```javascript
let salam = "Selamat pagi dunia!";
console.log(salam.slice(0, 7));
console.log(salam.slice(8, 12));
console.log(salam.slice(13, -1));
console.log(salam.slice(-6, -1));
console.log(salam.slice(0, salam.length));

console.log(salam.slice(0));
console.log(salam.slice(0, 1000));
```

#### substring/substr

substring dan substr adalah dua method yang sama persis, kita bosa meilih salah satunya saja. Method ini juga digunakan untuk mengambil suatu potongan string berdasarkan indek string. Berbeda dengan slice, substring tidak bisa mempunyai indek negatif.

```javascript
let salam = "Selamat pagi dunia!";
console.log(salam.substring(0));
console.log(salam.substring(0, 1000));

console.log(salam.substring(0, salam.length));
console.log(salam.substring(12, 8));
console.log(salam.substring(12, "asal"));
```

**Kesamaan apa yang mereka miliki:**

1. Jika `start` sama dengan `stop`: mengembalikan string kosong
2. Jika `stop` dihilangkan: ekstrak karakter ke akhir string
3. Jika salah satu argumen lebih besar dari panjang string, panjang string akan digunakan sebagai gantinya.

**Perbedaan**[`substring()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/substring)**:**

1. Jika `start > stop`, maka `substring` akan menukar 2 argumen tersebut.
2. Jika salah satu argumen negatif atau `NaN`, itu diperlakukan seolah-olah `0`.

**Perbedaan**[`slice()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/slice)**:**

1. Jika `start > stop`, `slice()` akan mengembalikan string kosong. \(`""`\)
2. Jika `start` negatif: set char dari akhir string, persis seperti `substr()` di Firefox. Perilaku ini diamati di Firefox dan IE.
3. Jika `stop` negatif: set berhenti ke: `string.length – Math.abs(stop)` \(nilai asli\), kecuali dibatasi pada 0 \(dengan demikian, `Math.max(0, string.length + stop)`\) sebagaimana dicakup dalam [spesifikasi ECMA](https://www.ecma-international.org/ecma-262/9.0/index.html#sec-string.prototype.slice) .

### Mengambil karakter berdasarkan indek: charAt

charAt digunakan untuk mengambil suatu karakter sebuah string berdasarkan indek yang dilempar. Karena yang dilempar adalah indek dan dimulai dari index ke nol, maka indek terakhir adalah panjang suatu string dikurangi 1. 

charAt memiliki sifat :

* Jika indek tidak ditemukan, akan dikembalikan string kosong. 
* Jika diberi indek negatif makan akan dikembalikan string kosong.
* Jika diberi indeks Nan maka akan dikembalikan character pada indek ke nol.  

```javascript
let salam = "Selamat pagi dunia!";
console.log(salam.charAt(0));
console.log(salam.charAt(5));
console.log(salam.charAt(salam.length));
console.log(salam.charAt(salam.length - 1));
console.log(salam.charAt(-1));
console.log(salam.charAt("asal"));
```

### Mengubah huruf besar/kecil : toUpperCase dan toLowerCase

Untuk mengubah suatu string menjadi huruf besar maupun huruf kecil, digunakan metho toUppercase dan toLoweCase.

```javascript
let salam = "Selamat pagi dunia!";
console.log(salam.toUpperCase());
console.log(salam.toLocaleLowerCase());
console.log(salam.charAt(0).toUpperCase()+salam.slice(1).toLocaleLowerCase());
```

### Menggabungkan dua string : concat

Untuk menggabungkan dua buah string atau lebih, kita bisa memilih menggunakan operator plus \(+\) maupun method concat.

```javascript
let sapa = "Halo";
let name = "Jacky";
console.log(sapa + " " + name);
console.log(sapa.concat(" ").concat(name));
```

### Menghilangkan spasi berlebih : trim

```javascript
let salam = "    Selamat      pagi dunia!        ";
console.log(salam.trim());
console.log(salam.trimStart());
console.log(salam.trimEnd());
```

Mengubah string .menjadi array : split

```javascript
let salam = "Selamat pagi dunia!";
console.log(salam.split(" "));
```

### Template using backtick

Kadang kita memerlukan template string, misalnya saat hendak memasukkan variabel ke dalam format string. Javascript menyediakan template string dengan backtick \(\`\).

```javascript
let name = "Jacky";
console.log(`Selamat pagi ${name}. Bagaimana keadaanmu di sana? Semoga ${name} dalam keadaan sehat dan bahagia.`);
```



