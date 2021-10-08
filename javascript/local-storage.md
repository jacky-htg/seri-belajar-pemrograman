# Local Storage

Ada banyak cara untuk menyimpan data ke dalam storage di browser. Kita bisa mengeceknya melalui developer tool dan klik tab Application. Di sebelah kiri terdapat menu, lihat menu Storage, ada banyak pilihan di sana meliputi : Local Storage, Session Storage, IndexedDB, Web SQL, Cookies dan Trust Tokens.

Kali ini kita akan memanfaatkan local storage untuk menyimpan data token yang didapatkan setelah berhasil login. 

Untuk menyimpan data menggunakan perintah `localStorage.setItem("nama-key", "value-yang-hendak-disimpan")`. Sementara untuk membaca data menggunakan perintah `localStorage.getItem("nama-key")`. Untuk menghapus local storage berdasarkan key, gunakan perintah `localStorage.removeItem("nama-key")`.

```javascript
// Store
localStorage.setItem("token", "akxakcnacnadkasaksnaksasaksnasnaks");
// Retrieve
console.log(localStorage.getItem("token"));
// Remove
localStorage.removeItem("token");
```

Praktek-kan ke dalam kode login yang pernah dibuat. Buat file login.html

```markup
<main>
  <h1>Login</h1>
  <form id="form">
    <div>
      <label for="email">Email</label>
      <input type="email" onchange="changeUser('email', this.value)" name="email" placeholder="email" required/>
    </div>
  
    <div>
      <label for="password">Password</label>
      <input type="password" onchange="changeUser('password', this.value)" name="password" placeholder="password" required/>
    </div>
  
    <button onclick="login()">Login</button>
  </form>
</main>

<script>
  document.getElementById("form").addEventListener("submit", function(event){
    event.preventDefault();
  });

  const curUser = {};

  function changeUser(field, value) {
    curUser[field] = value;
  }

  function login() {
    var xhttp = new XMLHttpRequest();
    xhttp.open("POST", "https://node-rest.rijalasepnugroho.com/login", true);
    xhttp.onload = function() {
      const loginResponse = JSON.parse(this.responseText);
      if (loginResponse.token) {
        localStorage.setItem("token", loginResponse.token);
        location.href = "./list-user.html";
      } 
    }
    xhttp.setRequestHeader("Content-type", "application/json");
    xhttp.send(JSON.stringify(curUser));
  }
  </script>
```

Jika login berhasil maka di dalam local storage akan tersimpan Key = token dan Value = alabama-token.

Agar lebih riil, maka di dalam halaman yang harus login terlebih dahulu, dilakukan pengecekan apakah sudah login atau belum, jika belum diredirct ke halaman login.

```javascript
  if (!localStorage.getItem("token")) {
    location.href = "./login.html";
  }
```

Penganganan logout juga diperlukan. Tambahkan button logout yang jika diklik akan mengahapus local storage dan redirect ke halamn login.

```markup
<button onclick="localStorage.removeItem('token'); location.href='./login.html'">Logout</button>
```



