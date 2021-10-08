# Array

Array adalah koleksi atau kumpulan dari banyak nilai.

```javascript
const arStr = ["senin", "selasa", "rabu", "kamis", "jumat"];
console.log(arStr);

const arInt = [1, 2, 3, 4, 5];
console.log(arInt);

const arMix = ["senin", 100, "rabu", 200, "jumat"];
console.log(arMix);

const arMixWithObj = ["senin", 100, "rabu", 200, "jumat", ["Rambutan", "Durian", "Salak"], {name: "jacky", age: 12}];
console.log(arMixWithObj);
```

cara deklarasi array bisa seperti di atas. Namun bisa juga dengan menggunakan objek Array dan memanggilnya dengan kata kunci new, atau dengan mengakses indek array tersebut.

```javascript
const ar = ["senin", "selasa", "rabu", "kamis", "jumat"];
console.log(ar);

const arIndex = [];
arIndex[0] = "senin";
arIndex[1] = "selasa";
arIndex[2] = "rabu";
arIndex[3] = "kamis";
arIndex[4] = "jumat";
console.log(arIndex);

const arObj = new Array("senin", "selasa", "rabu", "kamis", "jumat");
console.log(arObj);
```

Object Array juga punya method penting untuk mengecek apakah suatu variabel array atau bukan.

```javascript
const ar = ["senin", "selasa", "rabu", "kamis", "jumat"];
console.log(Array.isArray(ar));
console.log(Array.isArray(["Rambutan", "Durian", "Salak"]));
console.log(Array.isArray({name: "jacky", age: 12}));
console.log(Array.isArray("Apa kabar"));
console.log(Array.isArray(2021));
```

Untuk mengakses array bisa langsung menunjuk indek-nya

```javascript
const ar = ["senin", "selasa", "rabu", "kamis", "jumat"];
console.log(ar[3]);
```

Array juga mempunya properti dan method

## Properti

### length

Untuk mendapatkan panjang suatu array, gunakan properti length

```javascript
const ar = ["senin", "selasa", "rabu", "kamis", "jumat"];
console.log(ar.length);
```

## Method

Array mempunyai banyak method, kita akan membahas sebagian yang sering digunakan.

### Menambah dan mengurangi anggota sebuah array

#### push

Untuk menambahkan elemen baru ke dalam array. Anggota terbaru akan diletakkan di indek paling terakhir.

```javascript
const ar = ["senin", "selasa", "rabu", "kamis", "jumat"];
ar.push("sabtu");
ar.push("minggu");
console.log(ar);
```

#### Pop

Pop adalah suatu method untuk mendapatkan anggota terahir dari sebuah array sekaligus mengeluarkan \(menghapus\) anggota tersebut dari array. Pop merupakan method standard dari struktur data stack \(tumpukan\). Dimana pop digunakan untuk mengambil dari tumpukan paling atas.

```javascript
const ar = ["senin", "selasa", "rabu", "kamis", "jumat"];
ar.push("sabtu");
ar.push("minggu");
console.log(ar);

console.log(ar.pop())
console.log(ar.pop())

console.log(ar);
```

#### shift

shift mirip dengan pop, digunakan untuk mengambil tumpukan paling bawah. shift akan menampilkan nilai dari indek pertama sebauh array sekaligus mengeluarkan \(menghapus\) value tersebut dari array.

```javascript
const ar = ["senin", "selasa", "rabu", "kamis", "jumat"];
console.log(ar.shift());
console.log(ar);
```

#### unshift

unshift mirip dengan push, digunakan untuk menambahkan anggota baru ke dalam sebuah array, namun anggota baru ini akan ditambahkan di indek paling awal.

```javascript
const ar = ["senin", "selasa", "rabu", "kamis", "jumat"];
ar.unshift("minggu");
ar.unshift("sabtu");
console.log(ar);
```

### Memanipulasi isi/nilai sebuah array

#### delete

delete digunakan untuk menghapus value dari sebuah indek. delete tidak menhilangkan keanggotaan, melainkan hanya menghapus nilai saya.

```javascript
const ar = ["senin", "selasa", "rabu", "kamis", "jumat"];
delete ar[3];
console.log(ar);
ar[3] = "kamis";
console.log(ar);
  
```

### Membuat potongan sebuah array

slice digunakan untuk memotong sebuah array. slice mempunyai sifat:

* Membuat array baru tanpa menghapus array sumber.
* Mempunyai 2 argumen, argumen pertama adalah indek awal, argumen kedua adalah indek akhir.
* Slice memotong mulai dari indek awal sampai sebelum indek akhir. Artinya potongan array tidak termasuk indek terakhir. 
* Jika hanya ada 1 argumen maka dianggap argumen kedua adalah panjang array.
* Jika argumen negatif, maka itu sama dengan panjang array dikurangi argumen \(atau dihitung dari array terakhir\).

```javascript
const days = ["senin", "selasa", "rabu", "kamis", "jumat", "sabtu", "minggu"];
const weekdays = days.slice(0, 5);
const weekend = days.slice(5, 7);
const weekendsOneArg = days.slice(5);
const weekendUsingLengthMinus = days.slice(days.length-2);
const weekendUsingMinus = days.slice(-2);
console.log("days", days);
console.log("weekdays", weekdays);
console.log("weekend", weekend);
console.log("weekendsOneArg", weekendsOneArg);
console.log("weekendUsingLengthMinus", weekendUsingLengthMinus);
console.log("weekendUsingMinus", weekendUsingMinus);
```

### Menggabungkan dua buah array : concat\(\)

Berlawanan dengan slice, concat adalah untuk menambah anggota baru.

```javascript
const weekdays = ["senin", "selasa", "rabu", "kamis", "jumat"];
const weekend = ["sabtu", "minggu"];
const days = weekdays.concat(weekend);
console.log(days);

let myFruits = ["Rambutan", "Durian", "Salak"];
myFruits = myFruits.concat(
    ["Kesemek", "Apel", "Jeruk"], 
    ["Jambu", "Pepaya", "Mangga"], 
    "Nanas", 
    ["Kelengkeng"]
);
myFruits = myFruits.concat("Nangka");
console.log(myFruits);
```

### Mengurutkan array : sort

Untuk mengurutkan array dari terkecil ke terbesar.

```javascript
const myFruits = ["Rambutan", "Durian", "Salak"];
myFruits.sort();
console.log(myFruits);

const myNumber = [400, 314, 256, 512];
myNumber.sort();
console.log(myNumber);

const myMix = ["Rambutan", 374, "Duku", 845, "Kedondong", 543];
myMix.sort();
console.log(myMix);

const myMixObj = [null, "Rambutan", ["senin", "selasa"], 374, ["sabtu", "minggu"], "Duku", 845, {name: "jeruk"}, "Kedondong", 543, {name: "anggur"}];
myMixObj.sort();
console.log(myMixObj);
```

### Membalik susunan array : reverse

```javascript
const days = ["senin", "selasa", "rabu", "kamis", "jumat", "sabtu", "minggu"];
days.reverse();
console.log(days);
```

### Mengubah array menjadi string

Untuk mengubah array ke string, kita bisa menggunakan fungsi toString\(\) maupun join\(\). Jika menggunakan toString\(\) maka array akan menjadi string dengan separator koma \(,\). Jika menginginkan separator lain, gunakan fungsi join\(\) dengan melempar separator yang diinginkan.

```javascript
const days = ["senin", "selasa", "rabu", "kamis", "jumat", "sabtu", "minggu"];
console.log(days.toString());
console.log(days.join(" "));
```

### Perulangan pada array

Method-method array yang melakukan iterasi antara lain foreach\(\), map\(\) dan filter\(\) 

#### forEach 

forEach melakukan iterasi dengan setiap iterasi-nya memanggil fungsi \(callback\).

```javascript
const myNums = [1, 2, 3, 4, 5];
const square = (value, index, arr) => console.log(value * value);
myNums.forEach(square);
```

#### map

Mirip seperti forEach,  map juga melakukan iterasi pada sebuah array.  Bedanya forEach murni melakukan iterasi. Sementara map selain melakukan iterasi, dia juga  menciptakan array baru. Map tidak merubah array aslinya. 

```javascript
const myNums = [1, 2, 3, 4, 5];
const square = num => num * num;
console.log(myNums.map(square));
```

#### filter

filter digunakan jika kita ingin memfilter array lama, dengan memilih beberapa anggota array yang memenuhi kriteria yang diinginkan. Hasil filter akan disimpan dalam sebuah array baru dan tidak merubah array yang asli.

```javascript
const myNums = [1, 2, 3, 4, 5];
const even = num => num%2 === 0
const odd = num => num%2 !== 0
const bigSquare = num => num * num > 10;
console.log("filter genap", myNums.filter(even));
console.log("filter ganji", myNums.filter(odd));
console.log("filter big square", myNums.filter(bigSquare));
```

## Struktur data terkait array

Struktur data adalah cara penyimpanan, penyusunan dan pengaturan data di dalam media penyimpanan komputer sehingga data tersebut dapat digunakan secara efisien

Ada beberapa struktur data terkait array, pada kesempatan ini saya akan mengenalkan tiga struktur data yang sering digunakan :

1. **Stack** Stack adalah struktur data tumpukan, dimana menggunakan prinsip LIFO \(Last In First Out\) 
2. **Queue** Queue adalah struktur data antrian, dimana menggunakan prinsip FIFI \(First In First Out\)
3. **Set** Set adalah data struktur dimana setiap nilai anggotanya adalah unique \(tidak ada anggota yang kembar\)



