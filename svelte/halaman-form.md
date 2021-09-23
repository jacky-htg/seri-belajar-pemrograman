# Halaman Form

Update file src/helper/path.js 

```javascript
export const PATH_URL = {
  BASE: "/",
  ABOUT: "/tentang-kami",
  USER_LIST: "/admin/users",
  USER_CREATE: "/admin/users/add"
}
```

Buat file src/routes/UserAdd.svelte

```javascript
<script>
  import Navigation from "../components/Navigation.svelte"
  import Input from "../components/Input.svelte"
  import Button from "../components/Button.svelte" 
  import { notifications } from '../helper/toast'
  import { PATH_URL } from "../helper/path"
  import { navigate } from "svelte-routing"
  import { HOST_URL } from '../env'

  const state = {
    email: "",
    password: "",
    name: "",
    age: "" 
  }
  let isLoading = false

  const handleInput = (e) => {
    const { value, name } = e.target
    state[name] = value
  }

  const createUser = async () => {
    const url = HOST_URL + "/users"
    var xmlHttp = new XMLHttpRequest()
    xmlHttp.open("POST", url, true)
    xmlHttp.setRequestHeader("Content-type", "application/json")
    xmlHttp.send(JSON.stringify(state))
    
  }

  const onCreate = async () => {
    try {
      isLoading = true
      await createUser()
      isLoading = false

      navigate(PATH_URL.USER_LIST, { replace: true })
    } catch(e) {
      isLoading = false;
      notifications.danger(e.message)
    }
  };


</script>
<Navigation/>

<h1>Tambah User</h1>
<main>
  <form on:submit|preventDefault={onCreate}>
    <Input label="Email" name="email" on:input={handleInput} bind:value={state.email} placeholder="username" type="email" required/>
    <Input label="Password" name="password" on:input={handleInput} bind:value={state.password} placeholder="password" type="password" required/>
    <Input label="Name" name="name" on:input={handleInput} bind:value={state.name} placeholder="name" type="text" required/>
    <Input label="Age" name="age" on:input={handleInput} bind:value={state.age} placeholder="age" type="number" required/>
    <Button isLoading={isLoading}>Login</Button>
  </form>
</main>
```

Update file src/App.svelte

```javascript
<script>
	import { Router, Route } from "svelte-routing"
	import About from "./routes/About.svelte"
	import Home from "./routes/Home.svelte"
	import { PATH_URL } from "./helper/path"
	import UserList from "./routes/UserList.svelte"
	import ProtectedRoute from "./ProtectedRoute.svelte"
	import Toast from "./components/Toast.svelte"
	import UserAdd from "./routes/UserAdd.svelte"
</script>

<Router>
	<Route path={PATH_URL.BASE} component={Home}/>
	<Route path={PATH_URL.ABOUT} component={About}/>
	<ProtectedRoute path={PATH_URL.USER_LIST} component={UserList} />
	<ProtectedRoute path={PATH_URL.USER_CREATE} component={UserAdd} />
</Router>
<Toast/>
```



