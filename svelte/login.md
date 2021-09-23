# Login

Saat ini login masih dihardcode di component Navigation, seharusnya halaman login diakses melalui form login. Sebagai contoh, kita akan membuat form login di halaman home. Selain form login kita juga akan membutuhkan toast notification, dan fetch api.

### Toast

buat file src/helper/toast.js

```javascript
import { writable, derived } from "svelte/store"

const TIMEOUT = 2000

function createNotificationStore (timeout) {
    const _notifications = writable([])

    function send (message, type = "default", timeout) {
        _notifications.update(state => {
            return [...state, { id: id(), type, message, timeout }]
        })
    }

    let timers = []

    const notifications = derived(_notifications, ($_notifications, set) => {
        set($_notifications)
        if ($_notifications.length > 0) {
            const timer = setTimeout(() => {
                _notifications.update(state => {
                    state.shift()
                    return state
                })
            }, $_notifications[0].timeout)
            return () => {
                clearTimeout(timer)
            }
        }
    })
    const { subscribe } = notifications

    return {
        subscribe,
        send,
		    default: (msg, timeout = TIMEOUT) => send(msg, "default", timeout),
        danger: (msg, timeout = TIMEOUT) => send(msg, "danger", timeout),
        warning: (msg, timeout = TIMEOUT) => send(msg, "warning", timeout),
        info: (msg, timeout = TIMEOUT) => send(msg, "info", timeout),
        success: (msg, timeout = TIMEOUT) => send(msg, "success", timeout),
    }
}

function id() {
    return '_' + Math.random().toString(36).substr(2, 9);
};

export const notifications = createNotificationStore()
```

Buat file src/components/Toast.svelte

```javascript
<script>
  import { flip } from "svelte/animate";
  import { fly } from "svelte/transition";
  import { notifications } from "../helper/toast.js";

  export let themes = {
      danger: "#E26D69",
      success: "#84C991",
      warning: "#f0ad4e",
      info: "#5bc0de",
      default: "#aaaaaa",
  };
</script>

<div class="notifications">
  {#each $notifications as notification (notification.id)}
      <div
          animate:flip
          class="toast"
          style="background: {themes[notification.type]};"
          transition:fly={{ y: 30 }}
      >
          <div class="content">{notification.message}</div>
          {#if notification.icon}<i class={notification.icon} />{/if}
      </div>
  {/each}
</div>

<style>
  .notifications {
    position: fixed;
    top: 10px;
    left: 0;
    right: 0;
    margin: 0 auto;
    padding: 0;
    z-index: 9999;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
    pointer-events: none;
  }

  .toast {
    flex: 0 0 auto;
    margin-bottom: 10px;
    border-radius: 4px;
  }

  .content {
    padding: 16px 40px;
    display: block;
    color: white;
    font-weight: 500;
  }
</style>

```

Pasang component Toast di file src/App.svelte

```javascript
<script>
	import { Router, Route } from "svelte-routing"
	import About from "./routes/About.svelte"
	import Home from "./routes/Home.svelte"
	import { PATH_URL } from "./helper/path"
	import UserList from "./routes/UserList.svelte"
	import ProtectedRoute from "./ProtectedRoute.svelte"
	import Toast from "./components/Toast.svelte"
</script>

<Router>
	<Route path={PATH_URL.BASE} component={Home}/>
	<Route path={PATH_URL.ABOUT} component={About}/>
	<ProtectedRoute path={PATH_URL.USER_LIST} component={UserList} />
</Router>
<Toast/>
```

### Form Login

Buat komponen Input pada file src/components/Input.svelte

```javascript
<script>
  export let label
  export let value
</script>

<div>
  <label for={label}>{label}</label>
  <input bind:value id={label} name={label} {...$$restProps} />
</div>

```

Buat komponen Button pada file src/components/Button.svelte

```javascript
<script>
  import Loader from './Loader.svelte';
  export let bgColor = "#00FF00AA"
  export let bgHoverColor = "#00FF0088"
  export let size = "medium";
  export let className = "";
  export let isLoading = false;

  const getPaddingSize = (size) => {
    switch (size) {
      case "small":
        return "py-1 px-4"
      default:
        return "py-2 px-8"
    }
  }

  const getTextSize = (size) => {
    switch (size) {
      case "small":
        return "text-sm"
      default:
        return "text-lg"
    }
  }

  const getLoaderSize = (size) => {
    switch (size) {
      case "small":
        return "20"
      default:
        return "40"
    }
  }
  let padding = getPaddingSize(size);
  let text = getTextSize(size);
  let loaderSize = getLoaderSize(size);
  
</script>

<button
  disabled={isLoading}
  on:click
  class={`flex align-center justify-center text-white ${bgColor} border-0 ${padding} focus:outline-none hover:${bgHoverColor} rounded ${text} ${className}`}>
  {#if isLoading}
    <div class="relative">
      <div class="invisible"><slot /></div>
      <div class="loader-container">
        <Loader size={loaderSize}/>
      </div>
    </div>
  {:else}
    <slot />
  {/if}
</button>

<style>
  .loader-container {
    display: flex;
    justify-content: center;
    position: absolute;
    left: 0px;
    right: 0px;
    top: 0px;
    bottom: 0px;
    margin: auto;
    height: fit-content;
  }
</style>
```

Pada button dibuat suatu loader, ide-nya ketika button diklik, maka akan muncul loader selama sekian detik \(sekitar 1,5 detik\). Untuk buat file src/components/Loader/svelte

```javascript
<script>
  export const durationUnitRegex = /[a-zA-Z]/;
  export const range = (size, startAt = 0) =>
  [...Array(size).keys()].map(i => i + startAt);
  export let color = "#ffffff";
  export let unit = "px";
  export let duration = "1.5s";
  export let size = "60";
  let durationUnit = duration.match(durationUnitRegex)[0];
  let durationNum = duration.replace(durationUnitRegex, "");
</script>

<style>
  .wrapper {
    position: relative;
    display: flex;
    justify-content: center;
    align-items: center;
    width: var(--size);
    height: calc(var(--size) / 2.5);
    margin-top: calc(var(--size) / 5);
  }
  .circle {
    position: absolute;
    top: 0px;
    width: calc(var(--size) / 5);
    height: calc(var(--size) / 5);
    border-radius: 999px;
    background-color: var(--color);
    animation: motion var(--duration) cubic-bezier(0.895, 0.03, 0.685, 0.22)
      infinite;
  }
  @keyframes motion {
    0% {
      opacity: 1;
    }
    50% {
      opacity: 0;
    }
    100% {
      opacity: 1;
    }
  }
</style>

<div
  class="wrapper"
  style="--size: {size}{unit}; --color: {color}; --duration: {duration}">
  {#each range(3, 0) as version}
    <div
      class="circle"
      style="animation-delay: {version * (+durationNum / 10)}{durationUnit}; left: {version * (+size / 3 + +size / 15) + unit};" />
  {/each}
</div>

```

Update halaman src/routes/Home.svelte untuk menambahkan form login

```javascript
<script>
  import { Images } from "../helper/images"
  import Button from "../components/Button.svelte"
  import Input from "../components/Input.svelte"
  import { notifications } from '../helper/toast'
  import { PATH_URL } from "../helper/path"
  import { token } from "../stores/token"
  import { navigate } from "svelte-routing"

  const state = {
    username: "",
    password: ""
  }
  
  let isLoading = false;
  let isToken = false;

  if (localStorage.getItem("token")) {
    isToken = true
  }

  const handleInput = (e) => {
    const { value, name } = e.target
    state[name] = value
  }

  const loginCall = async (username, password) => {
    
    if (username === "rijal.asep.nugroho@gmail.com" && password === "1234") {
      return {
        Token: "sudah-login"
      }
    }

    return {}
  }

  const login = async () => {
    try {
      isLoading = true
      const user = await loginCall(state.username, state.password)
      
      if (!user.Token) {
        throw({message: "please suplay valid username and password"})
      }
      
      localStorage.setItem("token", user.Token)
      token.set(localStorage.getItem('token'));
      isLoading = false;
      isToken = true

      navigate(PATH_URL.USER_LIST, { replace: false })
    } catch(e) {
      isLoading = false;
      notifications.danger(e.message)
    }
  };

  let widthDiv = 50;
  if (isToken) {
    widthDiv = 100;
  }
 
</script>

<div id="container" style="background-image:url({Images.img_erp});">
  <div id="welcome-div" style="flex:{widthDiv}%;">
    <h1>Selamat datang di svelte skeleton</h1>
    <a href="{PATH_URL.ABOUT}">About Us</a>
  </div>
  {#if !isToken}
  <div id="loginDiv" style="flex: {widthDiv}%;">
    <form on:submit|preventDefault={login}>
      <Input label="Username" name="username" on:input={handleInput} bind:value={state.username} placeholder="username" type="text" required/>
      <Input label="Password" name="password" on:input={handleInput} bind:value={state.password} placeholder="password" type="password" required/>
      <Button isLoading={isLoading}>Login</Button>
    </form>
  </div>
  {/if}
 </div>

<style>
  #container {
    width:100vw;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  #welcome-div, #loginDiv {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-flow: wrap column;
  }

  a {
    color: wheat;
  }
</style>
```

Karena fungsi login sdh diambil alih di halaman Home, maka komponen Navigation kita update untuk menghapus kode tentang login.

```javascript
<script>
  import { Link, navigate } from "svelte-routing"
  import { token } from "../stores/token"
  import { PATH_URL } from "../helper/path"
  
  let isToken = false

  if (localStorage.getItem("token")) {
    isToken = true
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
  <Link to="{PATH_URL.BASE}">Login</Link>
  {/if}

</div>

```

### Call API

Saat ini, fungsi loginCall\(\) pada halaman Home masih dihardcode. Pada aplikasi sesungguhnya fungsi ini memanggil api dari backend melalui Ajax.

Ubah file src/routes/Home.svelte 

```javascript
<script>
  import { Images } from "../helper/images"
  import Button from "../components/Button.svelte"
  import Input from "../components/Input.svelte"
  import { notifications } from '../helper/toast'
  import { PATH_URL } from "../helper/path"
  import { token } from "../stores/token"
  import { navigate } from "svelte-routing"

  const state = {
    username: "",
    password: ""
  }

  const user = {token: ""}
  
  let isLoading = false;
  let isToken = false;

  if (localStorage.getItem("token")) {
    isToken = true
  }

  const handleInput = (e) => {
    const { value, name } = e.target
    state[name] = value
  }

  function reqListener() {
    user.token = JSON.parse(this.responseText).token;
  }

  const loginCall = async (username, password) => {
    const url = "http://localhost:3000/login";
    const data = {
      email:username, 
      password:password
    }

    var xmlHttp = new XMLHttpRequest();
    xmlHttp.addEventListener("load", reqListener);
    xmlHttp.open("POST", url, false); // false for synchronous request
    xmlHttp.setRequestHeader("Content-type", "application/json");
    xmlHttp.send(JSON.stringify(data));
    
  }

  const login = async () => {
    try {
      isLoading = true
      await loginCall(state.username, state.password)
      
      if (!user.token) {
        throw({message: "please suplay valid username and password"})
      }
      
      localStorage.setItem("token", user.Token)
      token.set(localStorage.getItem('token'));
      isLoading = false;
      isToken = true

      navigate(PATH_URL.USER_LIST, { replace: false })
    } catch(e) {
      isLoading = false;
      notifications.danger(e.message)
    }
  };

  let widthDiv = 50;
  if (isToken) {
    widthDiv = 100;
  }
 
</script>

<div id="container" style="background-image:url({Images.img_erp});">
  <div id="welcome-div" style="flex:{widthDiv}%;">
    <h1>Selamat datang di svelte skeleton</h1>
    <a href="{PATH_URL.ABOUT}">About Us</a>
  </div>
  {#if !isToken}
  <div id="loginDiv" style="flex: {widthDiv}%;">
    <form on:submit|preventDefault={login}>
      <Input label="Username" name="username" on:input={handleInput} bind:value={state.username} placeholder="username" type="text" required/>
      <Input label="Password" name="password" on:input={handleInput} bind:value={state.password} placeholder="password" type="password" required/>
      <Button isLoading={isLoading}>Login</Button>
    </form>
  </div>
  {/if}
 </div>

<style>
  #container {
    width:100vw;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  #welcome-div, #loginDiv {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-flow: wrap column;
  }

  a {
    color: wheat;
  }
</style>
```

