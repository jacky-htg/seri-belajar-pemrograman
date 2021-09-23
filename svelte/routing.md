# Routing

### Routing

Kita akan mengimplementasikan routing di svelte dengan memanfaatkan library svelte-routing 

Ubah file src/main.js

```javascript
import App from './App.svelte';

const app = new App({
	target: document.body
});

export default app;
```

Buat file src/helper/path.js agart mudah mengelola path aplikasi.

```javascript
export const PATH_URL = {
  BASE: "/",
  ABOUT: "/tentang-kami"
}
```

Buat file src/routes/About.svelte

```markup
<h1>Tentang Kami</h1>
```

Buat file src/routes/Home.svelte

```markup
<h1>Home</h1>
```

Ubah file src/App.svelte

```markup
<script>
	import { Router, Route } from 'svelte-routing'
	import About from "./routes/About.svelte"
	import Home from "./routes/Home.svelte"
	import { PATH_URL } from "./helper/path"
</script>

<Router>
	<Route path={PATH_URL.BASE} component={Home}/>
	<Route path={PATH_URL.ABOUT} component={About}/>
</Router>
```

Script di atas mengimport svelte-routing, maka kita perlu install library ini dengan menjalankan `npm install svelte-routing`

Ubah file package.json -&gt; scripts -&gt; start dengan menambahkan --single

```markup
{
  "name": "svelte-app",
  "version": "1.0.0",
  "private": true,
  "scripts": {
    "build": "rollup -c",
    "dev": "rollup -c -w",
    "start": "sirv public --no-clear --single"
  },
  "devDependencies": {
    "@rollup/plugin-commonjs": "^17.0.0",
    "@rollup/plugin-node-resolve": "^11.0.0",
    "rollup": "^2.3.4",
    "rollup-plugin-css-only": "^3.1.0",
    "rollup-plugin-livereload": "^2.0.0",
    "rollup-plugin-svelte": "^7.0.0",
    "rollup-plugin-terser": "^7.0.0",
    "svelte": "^3.0.0"
  },
  "dependencies": {
    "sirv-cli": "^1.0.0",
    "svelte-routing": "^1.6.0"
  }
}

```

Kemudian jalankan ulang `npm run dev`

Sekarang kita sudah punya routing, yaitu /  yang mengharah ke fiule src/routes/Home.svelte dan /tentang-kami yang mengarah ke fiel src/routes/About.svelte

### Gambar

Ada kalanya kita perlu menampilkan gambar sebagai informasi maupun sebagai pemanis halaman. Kita akan mempraktekkan penggunaan gambar \(maupun asset lainnya\) di svelte. Pertama buat folder images di folder public. dan copy-kan gambar yang hendak digunakan ke folder tersebut. Untuk keperluan ini,  saya telah  menyimpan gambar di public/image/erp.png.

 Untuk memudahkan mengelola path gambar, kita akan membuat file helper, src/helper/images.js

```javascript
export const Images = {
  img_erp: './images/erp.png'
}
```

Sekarang kita ubah file src/routes/Home.svelte 

```javascript
<script>
  import { Images } from "../helper/images";
</script>

<div id="container">
  <h1>Home</h1>
  <img src={Images.img_erp} alt="Gambar ERP">
</div>

<style>
  #container {
    width:100%;
  }

  img {
    width:50%;
  }
</style>
```



