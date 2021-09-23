# Fungsi

Fungsi diperlukan agar suatu kode tidak ditulis berulang-ulang, cukup dibuat sekali dalam satu fungsi, dan bisa dipanggil berkali-kali kapan pun dibutuhkan.

### Deklarasi Fungsi 

Dekalrasi fungsi terdiri dari kata kunci function, nama fungsi beserta argumen yang diperlukan

```text
function namaFungsi(argumen1, argumen2) {
    // blok kode
}
```

Contoh penggunaan fungsi

```javascript
function cetakSalam() {
    console.log("Selamat Pagi");
}

function cetak(salam) {
    console.log(salam);
}

function sapa(salam, nama) {
    console.log(salam, nama);
}

cetakSalam();
cetak("Selamat Pagi");
sapa("Selamat Pagi", "Beruang");
```

### Fungsi dengan return

Fungsi bisa menghasilkan kembalian berupa data hasil dari eksekusi fungsi tersebut.

```javascript
function isPrimeNumber(n) {
    if (n < 2) {
      return false;
    }
    for (let i = 2; i < n; i++) {
      if (n%i == 0) {
        return false;
      }
    }

    return true;
  }
  
  // Mencetak bilangan prima antara 1 - 100
  for (let i = 1; i<=100; i++) {
    if (isPrimeNumber(i)) {
      console.log(i);
    }
  }
  
  // mencetak N bilangan prima pertama 
  const bilangan = prompt("masukkan bilangan");
  let iterator = 1;
  let jumlah = 1;
  while (jumlah <= bilangan) {
    if (isPrimeNumber(iterator)) {
      console.log(`${jumlah} --> ${iterator}`);
      jumlah++;
    }

    iterator++;
  }
  
  
  function GetStudent(id){
    if (id === 1) {
      return {
        name: "Amalia",
        age: 14 
      } 
    }
    
    return {}
  }
  
  let amalia = GetStudent(1);
  let kosong = GertStudent(2);
  
  console.log("amalia : ", amalia);
  console.log("kosong : ", kosong);
  
```

### Fungsi Anonim

Fungsi anonim adalah suatu fungsi yang dideklarasikan tanpa nama

```javascript
let weekDays = ["Senin", "Selasa", "Rabu", "Kamis", "Jumat"];

weekDays.forEach(function (value, index) { 
    console.log(index, value); 
});
```

Fungsi anonim juga bisa disimpan dalam sebuah variabel

```javascript
const salam = function(str) {
    console.log("fungsi anonim di variabel", str);
};

salam("Halo");
```

### Arrow Function

```javascript
const salam = str => console.log("arrow function", str);
const sapa = (salam, nama) => console.log("arrow function", salam, nama);
const multiLine = () => {
    console.log("line 1");
    console.log("line 2");
}
const withReturn = () => "halo";
const withReturnMultiLine = () => {
    let str = "halo";
    return str;
}

salam("selamat pagi");
sapa("selamat pagi", "beruang");
multiLine();
const halo = withReturn();
console.log(halo);

const haloAgain = withReturnMultiLine();
console.log(haloAgain);
```

### Callback Function

Ketika sebuah fungsi dijadikan paramter fungsi lain, itulah yang disebut dengan callback.  Kita akan mengubah anonim function pada contoh foreach weekdays menjadi callback.

```javascript
function cetak(value, index) { 
    console.log(index, value); 
}

let weekDays = ["Senin", "Selasa", "Rabu", "Kamis", "Jumat"];

weekDays.forEach(cetak);
```

Contoh lain

```javascript
function cetak(data) {
    console.log(data);
}

function hitung(angka1, angka2, myCallback){
    let jumlah = angka1 + angka2;
    myCallback(jumlah);
}

hitung(4, 5, cetak);

function ask(question, no, yes) {
    if (confirm(question)) {
        yes();
    } else {
        no();
    }
}

function agree() {
    console.log("Ya, Saya setuju!");
}

function disagree() {
    console.log("Tidak, saya tidak setuju!");
}

ask("Apakah Anda Setuju?", disagree, agree);
```

