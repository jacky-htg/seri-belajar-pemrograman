# Asynchronous

Asynchronous adalah suatu proses yang dikerjakan secara bersamaan. Di javascript, umumnya suatu kode dikerjakana secara berurutan \(synchronous\), namun ada banyak yang dikerjakan secara asynchronous sepert event dan Ajax.

Keuntungan penggunaan aynchronous adalah proses menjadi lebih cepat, karena tidak harus menunggu suatu blok kode selessai dikerjakan. Jika javascript menemukan suatu proses yang lama, maka sambil menunggu proses itu selesai, javascript akan mengeksekusi kode selanjutnya.

Kelemahan asynchronous adalah adanya kemungkinan race condition jika ada suatu blok kode yang membutuhkan hasil dari proses lain, tenryata dieksekusi ketika proses lain tersebut belum memberikan hasil. Besar kemungkinan ketika bliok kode tersebut, datanya masih kosong.

Untuk mengatasi hal tersebut, dalam pemrograman asynchronous dioptimalkan penggunaan callback, async/await dan promise.

## Callback

Kita telah mempelajari callback sebelumnya. Dalam proses asynchronous, penggunaan callback sangat masif.  Sebagai contoh, kita akan menggunakan kode pemanggilan AJAX dengan teknik callback. Namun agar pemahaman lebih utuh, awalnya kita aklan mebuat contoh kode tanpa callback.

```markup
<h1>Callback Async - AJAX - List User</h1>
<main></main>
<script>
  let users = [];

  function displayUser() {
    const tables = [];
      tables.push(`
        <tr>
          <th>No</th>
          <th>Nama</th>
          <th>Umur</th>
        </tr>
      `); 
      let no = 1;
      for (user of users) {
        tables.push(`
          <tr>
            <td>${no}</td>
            <td>${user.name}</td>
            <td>${user.age}</td>
          </tr>
        `);
        no++;
      }

      const html = `
        <table>
          ${tables.join("")}
        </table>
      ` 
      const parent = document.getElementsByTagName("main")[0];
      parent.innerHTML = "";
      parent.insertAdjacentHTML("beforeend", html);
  }

  function list() {
    const xhttp = new XMLHttpRequest();
    xhttp.onload = function() {
      users = JSON.parse(this.responseText);
    };  
    xhttp.open("GET", "https://node-rest.rijalasepnugroho.com/users");
    xhttp.send();
  }

  list();
  displayUser();
  </script>
```

Pada kode di atas, kita memanggil list\(\); kemudian memangil displayUser\(\);. fungsi list\(\) berguna untuk mengupdate variabel users dengan data hasil call ajax. Sementara fungsi displayUser\(\) berguna untuk menampilkan data list user ke dalam tabel.

Harapannya akan tampil table list user dengan sleuruh data yang ada. Namun karena list\(\) membutuhkan waktu lebih lama, maka displayUser hanya menampilkan header table saja, karena ketika fungsi displayUser\(\) dijalankan, saat itu variabel users masih kosong.

Ide dasarnya adalah bagaimana caranya agar fungsi displayUser\(\) dipanggil setelah fungsi list\(\) selesai dieksekusi. Salah satu teknik yang digunakan adalah dengan callback, dimana funhsi displayUser\(\) akan dipanggil tepat setelah variabel users diupdate.

Kita akan perbaiki kode di atas dengan teknik callback. fungsi displayUser akan dilempar sebagai parameter fungsi list\(\), dan dipanggil tepat setelah variabel users diupdate.

```javascript
  function list(myCallback) {
    const xhttp = new XMLHttpRequest();
    xhttp.onload = function() {
      users = JSON.parse(this.responseText);
      myCallback();
    };  
    xhttp.open("GET", "https://node-rest.rijalasepnugroho.com/users");
    xhttp.send();
  }

  list(displayUser);
```

## Promise

Promise adalah suatu teknik handling asynchronous dengan memberi janji bahwa suatu kode akan dieksekusi dan hasilnya \(apakah akan berhasil atau tidak\)  akan diberi tahu kemudian. Cara untuk mengetahui hasil suatu promise adalah dengan mendengarkan/mengikuti/listen promise. 

Dengan teknik ini, akan ad dua buah kode, yaiti kode producer \(yang memberi janji\), dan kode konsumer \(yang mendengarkan hasil\).

Kode producer mengembalikan suatiu promise dengan dua callback, yaitu bila sukses akan menjalankan callback resolve\(\) sementara jika gagal akan mengembalikan callback reject\(\). Format producer promise adalah sebagai berikut :

```javascript
let myPromise = new Promise(function(myResolve, myReject) {
  // kode yang mungkin butuh waktu lama untuk eksekusi
  myResolve(); // when successful
  myReject();  // when error
});
```

Sementara kode untuk konsumer adalah dengan kata kunci then untuk handling jika hasilnya adalah sukses, dan catch jika hasilnya adalah error.

```javascript
myPromise
.then(result => console.log(result))
.catch(err => console.error(err));
```

Kita bisa melengkapi konsumer dengan kata kunci finally yang akan selalu dieksekusi baik sukses maupun error.

```javascript
myPromise
.then(result => console.log(result))
.catch(err => console.error(err))
.finally(console.log("seleseai"));
```

Sebagi contoh, kita akan mengubah penggunaan callback pada list user dengan promise. Karena pada contoh AJAX sebelumnya kita tidak menghandle error, saya akan mengenalkan event baru di xmlHttprequest yaitu onreadystatechange untuk menghandle event jika ajax sudah selesai. Juga ada suatu properti status untuk mengetahui status code dari response ajax.

```javascript
  function list() {
    return new Promise(function(resolve, reject){
      const xhttp = new XMLHttpRequest();
      xhttp.open("GET", "https://node-rest.rijalasepnugroho.com/users");
      xhttp.onreadystatechange = () => {
        if (xhttp.status !== 200) {
          reject(new Error("Error call list user"));
        } else {
          xhttp.onload = () => resolve(JSON.parse(xhttp.responseText));
        }
      };
      xhttp.send();
    });
  }

  list()
  .then(result => {
    users = result;
    displayUser();
  }).catch(err => console.error(err))
  .finally(console.log("selesai"));
```

## Promise.all\(\)

Ada kalanya kode yang dijanjikan bukan hanya satu, namun bisa banyak kode yang dijanjikan. Untuk konsumer, bisa dengan memanfaatkan fitur Promise.all\(\) untuk melisten seluruh kode yang dijanjikan.

```javascript
let promises = [];
promises.push(Promise.resolve("halo"));
promises.push(212);
promises.push(new Promise((res, rej) => {
    res(100);
}));

Promise.all(promises)
.then(result => console.log(result));
```

## async/await

Penulisan sintaks promise agak merepotkan, untunglah javascript menawarkan solusi async/await. kata kunci async yang diletakkan sebelum function membuat fungsi tersebut akan mengembalikan promise.

```javascript
async function salam () {
    return "Selamat Pagi";
}

// artinya sama dengan kode promise berikut
async function salam () {
    return Promise.resolve("Selamat Pagi");
}
 
```

Sementara sintaks await digunakan untuk menunggu promise selesai dieksekusi. Yang perlu diperhatikan adalah, async-await ini merupakan sintaks ES modern yang hanya bekerja dalam suatu module. Pastikan ketika menulis script, tambahkan informasi type=module.

```markup
<script type="module">
  // simple async-await
  async function salam() {
    return "Selamat Pagi";
  }

  const pagi = await salam();
  console.log(pagi);
  
  // async - promiseConsumer
  async function salam2() {
    return "Selamat Siang";
  }  
  
  salam2().then(result => console.log(result));
  
  // promiseProducer - await
  function salam3() {
    return new Promise(function(res, rej){
      res("Selamat Sore");
    });
  }
  
  const sore = await salam3();
  console.log(sore);
</script>
```

Dengan mengetahui konsep async dan await, kita bisa mengubah file list-user menjadi kode berikut:

```markup
<h1>Callback Async - AJAX - List User</h1>
<main></main>
<script type="module">
  let users = [];

  function displayUser() {
    const tables = [];
      tables.push(`
        <tr>
          <th>No</th>
          <th>Nama</th>
          <th>Umur</th>
        </tr>
      `); 
      let no = 1;
      for (const user of users) {
        tables.push(`
          <tr>
            <td>${no}</td>
            <td>${user.name}</td>
            <td>${user.age}</td>
          </tr>
        `);
        no++;
      }

      const html = `
        <table>
          ${tables.join("")}
        </table>
      ` 
      const parent = document.getElementsByTagName("main")[0];
      parent.innerHTML = "";
      parent.insertAdjacentHTML("beforeend", html);
  }

  function list() {
    return new Promise(function(resolve, reject){
      const xhttp = new XMLHttpRequest();
      xhttp.open("GET", "https://node-rest.rijalasepnugroho.com/users");
      xhttp.onreadystatechange = () => {
        if (xhttp.status !== 200) {
          reject(new Error("Error call list user"));
        } else {
          xhttp.onload = () => resolve(JSON.parse(xhttp.responseText));
        }
      };
      xhttp.send();
    });
  }

  users = await list();
  displayUser();
  </script>
```

