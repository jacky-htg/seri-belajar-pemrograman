# Param Url

Seringkali kita membutuhkan suatu nilai yang dilempar sebagai parameter url. Perhatikan url berikut :  http://localhost/users?id=101\&name=jhon

url di atas mempunyai dua parameter, yaitu parameter id dengan nilai 101, dan paremeter name dengan nilai jhon.

Untuk mengambil paremeter url, javascript sudah menyediakan object yang dibutuhkan, yaitu object location. Object location ini sudah sering kita gunakan sebagai redirect, yaitu dengan mengganti properti href dari object location tersebut. 

```javascript
console.log(location);
console.log(location.search);
```

Perhatikan location.search yang didapatkan yaitu ?id=101\&name=jhon, yang mempunyai pola diawali dengan '?' dan setiap parameter diseparator dengan '&'. Masing-masing parameter merupakan pasangan key dan value yang dipisahkan dengan '='. 

Dengan pola ini kita bisa mengubah paremeter url menjadi object json.

```javascript
function convertSearchToObj(){
    const paramUrl = {};
    location.search.substr(1).split("&").forEach((param) => {
      const pair = param.split("=");
      paramUrl[pair[0]] = pair[1];
    });
    return paramUrl;
  }

  const paramUrl = convertSearchToObj();
  console.log(paramUrl);
  if (paramUrl.id) {
    console.log(paramUrl.id);
  }
```
