# Perulangan

Perulangan dapat mengeksekusi blok kode beberapa kali. Ini berguna jika Anda ingin menjalankan kode yang sama berulang-ulang, setiap kali dengan nilai yang berbeda.

### for

```markup
<h1>Perulangan</h1>

<script>
  for (let index = 1; index <= 10; index++) {
    console.log("Aku baca buku halaman ", index);
  }
</script>
```

### for in

```markup
<h1>Perulangan</h1>

<script>
  var pages = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
  for (const index in pages) {
    console.log("Aku baca buku halaman ", pages[index]);
  }
</script>
```

### for of

```markup
<h1>Perulangan</h1>

<script>
  var pages = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
  for (const element of pages) {
    console.log("Aku baca buku halaman ", element);
  }
</script>
```

### foreach

```markup
<h1>Perulangan</h1>

<script>
  var pages = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
  pages.forEach((element, index) => {
    console.log("Aku baca buku halaman ", element);
  });
</script>
```

### while

```markup
<h1>Perulangan</h1>

<script>
  var page = 1;
  while (page >= 1 && page <= 10) {
    console.log("Aku baca buku halaman ", page);
    page++;
  }
</script>
```

