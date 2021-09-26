# AJAX

AJAX = **A**synchronous **J**avaScript **A**nd **X**ML. Merupakan kombinasi dari `XMLHttpRequest` dan JavaScript DOM. XMLHttpRequest digunakan untuk memanggil API, semanatar javascript DOM digunakan untuk mengolah dan menampilkan data hasil dari pemanggilan API.

Ajax dibagi menjadi tiga tahapan :

1. Membuat objek XMLHttpRequest `const xhttp = new XMLHttpRequest();` 
2. Membuat callback.  `xhttp.onload = function() {      // lakukan manipulasi DOM ketika sudah mendapat response  }`
3. Mengirim request. `xhttp.open("http method: GET|POST|PUT|DELETE", "url");  xhttp.send();`

Untuk persiapan dan bahan pembelajaran, saya sudah sediakan CRUD Rest API untuk digunakan, yaitu :  
- GET /users  
- POST /users  
- GET /users/:id  
- PUT /users/:id  
- DELETE /users/:id  
Url bisa diakses melalui :  https://api.anter.rijalasepnugroho.com

### List

```markup
<h1>AJAX</h1>
<main></main>
<script>

  function list() {
    const xhttp = new XMLHttpRequest();
    xhttp.onload = function() {
      const tables = [];
      tables.push(`
        <tr>
          <th>No</th>
          <th>Nama</th>
          <th>Umur</th>
        </tr>
      `); 
      users = JSON.parse(this.responseText);
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
    };  
    xhttp.open("GET", "http://localhost:3000/users");
    xhttp.send();
  }

  list();
  </script>
```

### Insert

Saat insert, method yang gunakan adalah "POST" dan saat send\(\) kita mengirim data berupa string json.  
  
`xhttp.open("POST", "http://localhost:3000/users", true);  
xhttp.send(JSON.stringify(user));`

Kita akan membuat perubahan pada halaman Ajax denga logik seperti berikut

1. Pada html tambahkan button "Tambah User" yang jika diklik memanggil fungsi add\(\).
2. Buat fungsi makeRandomName\(\) untuk membuat nama user secara random.
3. Buat fungsi add\(\) untuk memangil ajax POST /users
4. Pada callback AJAX, dibuat pengecekan, jika response berhasil dan menghasilkan id, maka akan load ulang fungsi list\(\) agar memperbarui data.

```markup
<h1>AJAX</h1>
<button onclick="add()">Tambah User</button>
<main></main>
<script>

  function list() {
    const xhttp = new XMLHttpRequest();
    xhttp.onload = function() {
      const tables = [];
      tables.push(`
        <tr>
          <th>No</th>
          <th>Nama</th>
          <th>Umur</th>
        </tr>
      `); 
      users = JSON.parse(this.responseText);
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
    };  
    xhttp.open("GET", "http://localhost:3000/users");
    xhttp.send();
  }

  function add() {
    const name = makeRandomName(8);
    const user = {
      email : `${name}@gmail.com`,
      password: "1234",
      name: name,
      age: Math.floor(Math.random() * 20)
    };

    console.log(JSON.stringify(user));
    var xhttp = new XMLHttpRequest();
    xhttp.open("POST", "http://localhost:3000/users", true);
    xhttp.onload = function() {
      const newUser = JSON.parse(this.responseText);
      if (newUser.id > 0) {
        list();
      } 
    }
    xhttp.setRequestHeader("Content-type", "application/json");
    xhttp.send(JSON.stringify(user));
  }

  function makeRandomName(length) {
    var result           = '';
    var characters       = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789';
    var charactersLength = characters.length;
    for ( var i = 0; i < length; i++ ) {
      result += characters.charAt(Math.floor(Math.random() * charactersLength));
   }
   return result;
  }

  list();
  </script>
```

