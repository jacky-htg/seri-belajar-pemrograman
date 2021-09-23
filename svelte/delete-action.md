# Delete Action

Untuk menghandle penghapusan data, cukup dengan mengupdate fungsi onDelete pada file src/routes/UserList.svelte

```javascript
<script>
  import { onMount } from "svelte"
  import { Link } from "svelte-routing"
  import Navigation from "../components/Navigation.svelte"
  import { HOST_URL } from '../env'
  import { PATH_URL } from "../helper/path"
  import { notifications } from '../helper/toast'
  import { navigate } from "svelte-routing"

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
    navigate("/admin/users/"+id, { replace: true })
  }

  const deleteUser = async(id) => {
    var oReq = new XMLHttpRequest()
    oReq.open("DELETE", HOST_URL+ "/users/"+id)
    oReq.send()
  };

  const onDelete = async (event) => {
    let id = event.target.dataset.id
    if (confirm("Yakin hendak menghapus?#"+id)) {
      try {
        await deleteUser(id)
        document.getElementById("tr-"+id).remove()
      } catch(e) {
        notifications.danger(e.message)
      }
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
  <tr id="tr-{user.id}">
    <td>{user.id}</td>
    <td>{user.email}</td>
    <td>{user.name}</td>
    <td>{user.age}</td>
    <td><button data-id="{user.id}" on:click="{onEdit}">Edit</button> <button data-id="{user.id}" on:click="{onView}">View</button> <button data-id="{user.id}" on:click="{onDelete}">Delete</button></td>
  </tr>
  {/each}
</table>

```



