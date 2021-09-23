# Seleksi Kondisi

Seleksi kondisi digunakan untuk melakukan tindakan yang berbeda berdasarkan kondisi yang berbeda. Kode akan dieksekusi jika syarat yang diminta terpenuhi.

### if

```markup
<h1>If</h1>

<script>
  let cuaca = prompt("apa cuaca hari ini ?", "cerah");

  if (cuaca === "cerah") {
    console.log("cuaca", cuaca, ", saya pergi bermain di luar rumah");
  }
</script>
```

### if else

```markup
<h1>If Else</h1>

<script>
  let cuaca = prompt("apa cuaca hari ini ?", "cerah");

  if (cuaca === "cerah") {
    console.log("cuaca", cuaca, ", saya pergi bermain di luar rumah");
  } else {
    console.log("cuaca", cuaca, ", saya baca buku di ruang tamu");
  }
</script>
```

### nested if else 

```markup
<h1>Nested If Else</h1>

<script>
  let cuaca = prompt("apa cuaca hari ini ?", "cerah");

  if (cuaca === "cerah") {
    console.log("cuaca", cuaca, ", saya pergi bermain di luar rumah");
  } else if (cuaca === "berawan") {
    console.log("cuaca", cuaca, ", saya baca buku di teras");
  } else {
    console.log("cuaca", cuaca, ", saya baca buku di ruang tamu");
  }
</script>
```

### switch

Jika nested if else terkalu banyak, itu tandanya anda membutuhkan switch.

```markup
<h1>Switch</h1>

<script>
  let cuaca = prompt("apa cuaca hari ini ?", "cerah");

  switch (cuaca) {
    case "cerah":
      console.log("cuaca", cuaca, ", saya pergi bermain di luar rumah");
      break
    case "berawan":
      console.log("cuaca", cuaca, ", saya baca buku di teras");
      break
    default:
      console.log("cuaca", cuaca, ", saya baca buku di ruang tamu");
  }
</script>
```

