# Halaman List

Dengan semakin seringnya kita menggunakan url, ada baiknya untuk menyimpan url dalam sebuah env.

Buat file src/env.js

```javascript
export const HOST_URL = 'http://localhost:3000';
export const APP_ENV = 'development';
```

Ubah file src/routes/UserList.svelte

```javascript
<script>
  import { onMount } from "svelte"
  import { Link } from "svelte-routing"
  import Navigation from "../components/Navigation.svelte"
  import { HOST_URL } from '../env'
  import { PATH_URL } from "../helper/path";
  import { notifications } from '../helper/toast'

  let isLoadingTable = false
  let users = []
 
  function reqListener () {
    users = JSON.parse(this.responseText)
  }

  const fetchData = async() => {
    var oReq = new XMLHttpRequest()
    oReq.addEventListener("load", reqListener)
    oReq.open("GET", HOST_URL+ "/users")
    oReq.send()
  };

  onMount(async () => {
		try {
			isLoadingTable = true
			await fetchData()
			isLoadingTable = false
    } catch(e) {
			isLoading = false;
      notifications.danger(e.message)
    }
	})

  const onEdit = (event) => {
    let id = event.target.dataset.id
    console.log("edit", id)
  }

  const onView = (event) => {
    let id = event.target.dataset.id
    console.log("view", id)
  }

  const onDelete = (event) => {
    let id = event.target.dataset.id
    if (confirm("Yakin hendak menghapus?#"+id)) {
      console.log("delete", id)
    }
  }
</script>
<Navigation/>

<h1>List User</h1>

<Link to={PATH_URL.USER_CREATE}>Tambah User</Link>
<table>
  <tr>
    <th>ID</th>
    <th>Email</th>
    <th>Nama</th>
    <th>Umur</th>
    <th></th>
  </tr>

  {#each users as user}
  <tr>
    <td>{user.id}</td>
    <td>{user.email}</td>
    <td>{user.name}</td>
    <td>{user.age}</td>
    <td><button data-id="{user.id}" on:click="{onEdit}">Edit</button> <button data-id="{user.id}" on:click="{onView}">View</button> <button data-id="{user.id}" on:click="{onDelete}">Delete</button></td>
  </tr>
  {/each}
</table>
```

