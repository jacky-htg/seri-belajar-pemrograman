# Notification

Notification mutlak diperlukan ketika kita bertransaksi dengan data, apakah transaksi kita sukses atau gagal. Untuk membuat notification cukup sederhana, dengan memanfaatkan css modal dan fungsi setTimeout().

Modal

 Buat modal notification dengan html dan css seperti berikut

```html
<style>
  #notification{
    display: none;
    position: fixed;
    height: 100%;
    width: 100%;
    top: 0;
    left: 0;
    z-index:99;
  }

  #notification div#notif-container{
    width:100%;
    height: 100%;
    display: flex;
    justify-content: center;
    margin-top: 20px;
  }

  #notification div#notif-container div#notif-content {
    width: 50%;
    height: 40px;
    padding: 1%;
  }

  .notif-success {
    background-color: green;
    color: white;
  }

  .notif-warning {
    background-color: yellow;
    color: black;
  }

  .notif-error {
    background-color: red;
    color: white;
  }

  .notif-info {
    background-color: grey;
    color: white;
  }
  
</style>

<div id="notification">
  <div id="notif-container">
    <div id="notif-content"></div>
  </div>
</div>
```

SetTimeout

SetTimeout adalah fungsi javascript yang digunakan untuk memberi jeda eksekusi suatu callback (blok fungsi). Idenya adalah : 

1. Tampilkan modal notification
2. dengan fungsi setTimeout(), setlah beerapa mili second, modal notification kembali disembunyikan.
3. Redirect ke halaman yang diinginkan.

```javascript
function showNotification(message, type, redirect="") {
    let notifClass = "info";
    if (type === "error" || type === "warning" || type == "success") {
      notifClass = type;
    }

    const notifDiv = document.getElementById("notif-content");
    notifDiv.innerHTML = message;
    notifDiv.classList.add("notif-"+type);
    document.getElementById("notification").style.display = "block";
    
    setTimeout(function(){
      document.getElementById("notification").style.display = "none";
      notifDiv.classList.remove("notif-"+type);
      notifDiv.innerHTML = ""; 
      if (redirect) {
        location.href=redirect;
      }
    }, 3000); 
  }
```

Selanjutnya kita akan memodifikasi file login.html agar mempunyai notification. Fungsi listening event onload dimodifikasi agar jika sukses akan menampilkan notifikasi sukses, dan jika gagal login akan menampilkan notifikasi error login. 

```javascript
function login() {
    var xhttp = new XMLHttpRequest();
    xhttp.open("POST", "https://node-rest.rijalasepnugroho.com/login", true);
    xhttp.onload = function() {
      const loginResponse = JSON.parse(this.responseText);
      if (loginResponse.token) {
        localStorage.setItem("token", loginResponse.token);
        showNotification("Login success", "success", "./list-user.html");
      } else {
        showNotification("Login failed", "error");
      }
    }
    xhttp.setRequestHeader("Content-type", "application/json");
    xhttp.send(JSON.stringify(curUser));
  }
```

Berikut adalah kode lengkap file login.html

```html
<style>
  #notification{
    display: none;
    position: fixed;
    height: 100%;
    width: 100%;
    top: 0;
    left: 0;
    z-index:99;
  }

  #notification div#notif-container{
    width:100%;
    height: 100%;
    display: flex;
    justify-content: center;
    margin-top: 20px;
  }

  #notification div#notif-container div#notif-content {
    width: 50%;
    height: 40px;
    padding: 1%;
  }

  .notif-success {
    background-color: green;
    color: white;
  }

  .notif-warning {
    background-color: yellow;
    color: black;
  }

  .notif-error {
    background-color: red;
    color: white;
  }

  .notif-info {
    background-color: grey;
    color: white;
  }
  
</style>

<div id="notification">
  <div id="notif-container">
    <div id="notif-content"></div>
  </div>
</div>

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
        showNotification("Login success", "success", "./list-user.html");
      } else {
        showNotification("Login failed", "error");
      }
    }
    xhttp.setRequestHeader("Content-type", "application/json");
    xhttp.send(JSON.stringify(curUser));
  }

  function showNotification(message, type, redirect="") {
    let notifClass = "info";
    if (type === "error" || type === "warning" || type == "success") {
      notifClass = type;
    }

    const notifDiv = document.getElementById("notif-content");
    notifDiv.innerHTML = message;
    notifDiv.classList.add("notif-"+type);
    document.getElementById("notification").style.display = "block";
    
    setTimeout(function(){
      document.getElementById("notification").style.display = "none";
      notifDiv.classList.remove("notif-"+type);
      notifDiv.innerHTML = ""; 
      if (redirect) {
        location.href=redirect;
      }
    }, 3000);
    
  }
  </script>
```

