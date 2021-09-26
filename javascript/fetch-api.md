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

Buat file list-user.html

```markup
<h1>AJAX - List User</h1>
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

Kita akan membuat perubahan pada halaman Ajax dengan logik seperti berikut

1. Pada file list-user.html tambahkan button "Tambah User" yang jika diklik akan redirect ke halaman add-user.html
2. Buat halaman add-user.html yang berisi form.
3. Form dicegah untuk submit karena akan dihandle lewat ajax. `document.getElementById("form").addEventListener("submit", function(event){       event.preventDefault();  })`
4. Buat fungsi add\(\) untuk memangil ajax POST /users
5. Pada callback AJAX, dibuat pengecekan, jika response berhasil dan menghasilkan id, maka akan redirect kembali ke halaman list.

Ubah file list-user.html untuk menambahkan tombol "Tambah User". 

```markup
<h1>AJAX - List User</h1>
<button onclick="location.href='./add-user.html'">Tambah User</button>
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
    xhttp.open("GET", "https://api.anter.rijalasepnugroho.com/users");
    xhttp.send();
  }

  list();
  </script>

```

Buat file add-user.html

```markup
<h1>AJAX - Add user</h1>
<form id="form">
  <div>
    <label for="email">Email</label>
    <input type="email" onchange="changeUser('email', this.value)" name="email" placeholder="email" required/>
  </div>

  <div>
    <label for="password">Password</label>
    <input type="password" onchange="changeUser('password', this.value)" name="password" placeholder="password" required/>
  </div>

  <div>
    <label for="name">Nama</label>
    <input type="name" onchange="changeUser('name', this.value)" name="text" placeholder="nama" required/>
  </div>

  <div>
    <label for="age">Umur</label>
    <input type="number" onchange="changeUser('age', this.value)" name="age" placeholder="umur" required/>
  </div>

  <button onclick="add()">Tambah User</button>
</form>

<script>
  document.getElementById("form").addEventListener("submit", function(event){
    event.preventDefault();
  });

  const curUser = {};

  function changeUser(field, value) {
    curUser[field] = value;
  }

  function add() {
    var xhttp = new XMLHttpRequest();
    xhttp.open("POST", "https://api.anter.rijalasepnugroho.com/users", true);
    xhttp.onload = function() {
      const newUser = JSON.parse(this.responseText);
      if (newUser.id > 0) {
        location.href = "./list-user.html";
      } 
    }
    xhttp.setRequestHeader("Content-type", "application/json");
    xhttp.send(JSON.stringify(curUser));
  }
  </script>
```

### Single page using modal

kadang kita ingin menjadikan halaman list dan add dalam satu halaman saja. Solusinya adalah membuat form tambah user dalam bentuk modal. Logic pembuatan single page adalah sebagia berikut :

1. Tambahkan modal form add-user dalam file list-user.html dalam keadaan hide.
2. Jika ada klik "Tambah User" maka tampilkan modal form add-user.
3. Setelah submit form tambah user maka modal kembali dihide dan load ulang fungsi list\(\) untuk melakukan pembaruan data.

Berikut file list-user.html

```markup
<style>
  #modal{
    display: none;
    background-color: #808080aa;
    position: fixed;
    height: 100%;
    width: 100%;
    top: 0;
    left: 0;
    z-index:99;
  }

  #form-container {
    width:100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  form {
    width: 38%;
    background-color: white;
    border: 1px solid black;
    padding: 1%;
  }

  form div {
    padding: 2%;
  }

  form label {
    display: inline-block;
    width: 20%; 
  }

  form input {
    width: 77%;
  }

  #closeBtn {
    position: relative;
    left: calc(100% - 30px); 
    top:0;
  }
</style>

<h1>AJAX - List User</h1>
<div id="modal">
  <div id="form-container">
    <form id="form">
      <button id="closeBtn" onclick="closeModal()">X</button>
      <div>
        <label for="email">Email</label>
        <input type="email" onchange="changeUser('email', this.value)" name="email" placeholder="email" required/>
      </div>
    
      <div>
        <label for="password">Password</label>
        <input type="password" onchange="changeUser('password', this.value)" name="password" placeholder="password" required/>
      </div>
    
      <div>
        <label for="name">Nama</label>
        <input type="name" onchange="changeUser('name', this.value)" name="text" placeholder="nama" required/>
      </div>
    
      <div>
        <label for="age">Umur</label>
        <input type="number" onchange="changeUser('age', this.value)" name="age" placeholder="umur" required/>
      </div>
    
      <button onclick="add()">Tambah User</button>
    </form>
  </div>
</div>
<button onclick="openModal()">Tambah User</button>
<main></main>
<script>
  document.getElementById("form").addEventListener("submit", function(event){
    event.preventDefault();
  });

  const curUser = {};

  function changeUser(field, value) {
    curUser[field] = value;
  }

  function add() {
    var xhttp = new XMLHttpRequest();
    xhttp.open("POST", "https://api.anter.rijalasepnugroho.com/users", true);
    xhttp.onload = function() {
      const newUser = JSON.parse(this.responseText);
      if (newUser.id > 0) {
        closeModal();
        list();
      } 
    }
    xhttp.setRequestHeader("Content-type", "application/json");
    xhttp.send(JSON.stringify(curUser));
  }

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
    xhttp.open("GET", "https://api.anter.rijalasepnugroho.com/users");
    xhttp.send();
  }

  function openModal(){
    document.getElementById("modal").style.display = 'block';
  }

  function closeModal(){
    document.getElementById("modal").style.display = 'none';
  }

  list();
  </script>
```

