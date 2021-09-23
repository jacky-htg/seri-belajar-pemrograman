# Pengenalan Node JS

Node JS memungkinkan javascript untuk bekerja di sisi server.

### Installasi NodeJS

Installasi NodeJS bisa dilakukan dengan mendownload melalui halaman [https://nodejs.org/en/download/](https://nodejs.org/en/download/) dan pilih versi LTS. Ikuti langkah-langkah yang disampaikan ketika melakukan instalasi. 

Untuk mengecek apakah installasi berhasil dengan baik, ketik perintah berikut :  
`node -v`  
`npm -v`   
npm adalah node package manager untuk mengelola paket-paket library di javascript. 

### Get Started

{% code title="index.js" %}
```javascript
var http = require('http');

http.createServer(function (req, res) {
  res.writeHead(200, {'Content-Type': 'text/html'});
  res.end('Selamat Pagi!');
}).listen(8080);
```
{% endcode %}

Jalankan dengan perintah `node index.js`

Kemudian buka browser localhost:8080

