# Protected Routing

Sering kali kita memerlukan halaman yang diproteksi. Hanya user yang sudah login yang bisa masuk ke halaman tersebut.

Buat Halaman src/routes/AccessDenied.svelte

```markup
<script>
  import { Link } from "svelte-routing"
  import { PATH_URL } from "../helper/path"
</script>

<h1>No access 🤕</h1>
<h2>
  Go back to <Link to={PATH_URL.BASE}>Home page</Link>
</h2>
```

Buat file src/stores/token.js

```javascript
import { writable } from 'svelte/store';

export const token = writable(localStorage.getItem('token'));
```

Buat file src/ProtectedRoute.svelte

```javascript
<script>
  import { Route } from "svelte-routing"
  import AccessDenied from "./routes/AccessDenied.svelte"
  import { token } from "./stores/token.js"

  export let path
  export let component
  $: isAuthenticated = $token;
</script>

{#if isAuthenticated}
  <Route path={path} component={component} />
{:else}
  <Route path={path} component={AccessDenied} />
{/if}
```

Buat file src/routes/UserList.svelte

```javascript
<h1>List User</h1>
```

Ubah file src/App.svelte

```javascript
<script>
	import { Router, Route } from "svelte-routing"
	import About from "./routes/About.svelte"
	import Home from "./routes/Home.svelte"
	import { PATH_URL } from "./helper/path"
	import UserList from "./routes/UserList.svelte"
	import ProtectedRoute from "./ProtectedRoute.svelte"
</script>

<Router>
	<Route path={PATH_URL.BASE} component={Home}/>
	<Route path={PATH_URL.ABOUT} component={About}/>
	<ProtectedRoute path={PATH_URL.USER_LIST} component={UserList} />
</Router>
```

Buat file src/components/Navigation.svelte

```javascript
<script>
  import { Link, navigate } from "svelte-routing"
  import { token } from "../stores/token"
  import { PATH_URL } from "../helper/path"

  let isToken = false

  if (localStorage.getItem("token")) {
    isToken = true
  }


  $: isAuthenticated = $token;

  const login = () => {
    localStorage.setItem("token", "sudah-login")
    token.set(localStorage.getItem("token"))
    isToken = true
    navigate(PATH_URL.USER_LIST, { replace: true })
  }

  function logout () {
    localStorage.removeItem("token")
    token.set(token, localStorage.getItem("token"))
    isToken = false
    navigate(PATH_URL.BASE, { replace: true })
  }

</script>

<div>
  {#if isToken}
  <ul>
    <li><Link to={PATH_URL.USER_LIST}>List User</Link></li>
  </ul>
  <button on:click="{logout}">Logout</button>
  {:else}
  <ul>
    <li><Link to={PATH_URL.BASE}>Home</Link></li>
    <li><Link to={PATH_URL.ABOUT}>Tentang Kami</Link></li>
  </ul>
  <button on:click="{login}">Login</button>
  {/if}

</div>

```

Update file-file routes untuk menambahkan Navigation

{% code title="src/routes/About.svelte" %}
```javascript
<script>
  import Navigation from "../components/Navigation.svelte"
</script>
<Navigation/>
<h1>Tentang Kami</h1>
```
{% endcode %}

{% code title="src/routes/Home.svelte" %}
```javascript
<script>
  import { Images } from "../helper/images"
  import Navigation from "../components/Navigation.svelte"
</script>
<Navigation/>

<div id="container">
  <h1>Home</h1>
  <img src={Images.img_erp} alt="Gambar ERP"/>
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
{% endcode %}

{% code title="src/routes/UserList.svelte" %}
```javascript
<script>
  import Navigation from "../components/Navigation.svelte"
</script>
<Navigation/>

<h1>List User</h1>
```
{% endcode %}



