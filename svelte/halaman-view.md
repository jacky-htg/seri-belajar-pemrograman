# Halaman View

Update file src/helper/path.js

```javascript
export const PATH_URL = {
  BASE: "/",
  ABOUT: "/tentang-kami",
  USER_LIST: "/admin/users",
  USER_CREATE: "/admin/users/add",
  USER_VIEW: "/admin/users/:id"
}
```

Buat file src/routes/UserView.svelte

```javascript
<script>
  import { onMount } from "svelte"
  import Navigation from "../components/Navigation.svelte"
  import { HOST_URL } from "../env"
  import { notifications } from "../helper/toast"
  import Input from "../components/Input.svelte"
  
  export let id

  let isLoading = false
  let user = {}
 
  function reqListener () {
    user = JSON.parse(this.responseText)
  }

  const fetchData = async() => {
    var oReq = new XMLHttpRequest()
    oReq.addEventListener("load", reqListener)
    oReq.open("GET", HOST_URL+ "/users/"+id)
    oReq.send()
  };

  onMount(async () => {
		try {
			isLoading = true
			await fetchData()
			isLoading = false
    } catch(e) {
			isLoading = false;
      notifications.danger(e.message)
    }
	})
  
</script>

<Navigation />
<main>
  <h1>View User</h1>
  <Input label="Email" name="email" value={user.email} disabled />
  <Input label="Name" name="name" value={user.name} disabled />
  <Input label="Age" name="age" value={user.age} disabled />
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
	import UserView from "./routes/UserView.svelte"
</script>

<Router>
	<Route path={PATH_URL.BASE} component={Home}/>
	<Route path={PATH_URL.ABOUT} component={About}/>
	<ProtectedRoute path={PATH_URL.USER_LIST} component={UserList} />
	<ProtectedRoute path={PATH_URL.USER_CREATE} component={UserAdd} />
	<ProtectedRoute path={PATH_URL.USER_VIEW} component={UserView} let:params>
		<UserView id="{params.id}"/>
	</ProtectedRoute>
</Router>
<Toast/>
```

Pada file src/routes/UserList.svelte ubah fungsi onView

```javascript
  const onView = (event) => {
    let id = event.target.dataset.id
    navigate("/admin/users/"+id, { replace: true })
  }
```

