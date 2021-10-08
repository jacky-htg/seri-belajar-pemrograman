# JSON

### JSON object

JSON merupakan singkatan dari **J**ava**S**cript **O**bject **N**otation. Untuk membuat JSON On=bject harus memenhi kriteria:

* Data dalam pasangan nama dan nilai.
* Data dipisahkan dengan koma.
* Object dibuat dengan kururung kurawal {}
* Array dibuat dengan kurung persegi \[\] 

JSON object bisa dideklarasikan dengan berbagai cara :

```javascript
const ninja1 = {
    nama: "Naruto",
    umur: 12,
    alamat: "Desa Konoha",
    jurus: ["kage bunshin", "rasengan"]
}
console.log(ninja1);

const ninja2 = {}
ninja2.nama = "Naruto";
ninja2.umur = 12;
ninja2.alamat = "Desa Konoha";
ninja2.jurus = ["kage bunshin", "rasengan"];
console.log(ninja2);

const ninja3 = new Object();
ninja3.nama = "Naruto";
ninja3.umur = 12;
ninja3.alamat = "Desa Konoha";
ninja3.jurus = ["kage bunshin", "rasengan"];
console.log(ninja3);

// kita bisa mengakses langsung properti object
console.log(ninja3.nama);
console.log(ninja3["nama"]);
```

### JSON stringify

Digunakan untuk mengubah json object menjadi string

```javascript
const ninja1 = {
  nama: "Naruto",
  umur: 12,
  alamat: "Desa Konoha",
  jurus: ["kage bunshin", "rasengan"]
}
console.log(ninja1);
console.log(JSON.stringify(ninja1));
```

### JSON parse

Digunakan untuk mengubah string menjadi JSON Object

```javascript
ninjaStr = '{"nama":"Naruto","umur":12,"alamat":"Desa Konoha","jurus":["kage bunshin","rasengan"]}';
console.log(JSON.parse(ninjaStr));
```

### delete 

Digunakan untuk menghapus properti dari sebuah object. Sementara untuk menambah properti jauh lebih simple, sama seperti waktu deklarasi object, langsung menambah properti yang diinginkan.

```javascript
const ninja1 = {
  nama: "Naruto",
  umur: 12,
  alamat: "Desa Konoha",
  jurus: ["kage bunshin", "rasengan"]
};
console.log(ninja1);
delete ninja1.umur;
delete ninja1["alamat"];
console.log(ninja1);
```

