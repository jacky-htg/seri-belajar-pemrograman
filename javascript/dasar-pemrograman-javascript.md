# Dasar Pemrograman Javascript

Dasar pemrograman javascript meliputi pengaksesan DOM HTML,  variable, konstanta dan tipe data.

### DOM HTML

Dokumen HTML bisa diakses melalui DOM \(_Document Object Model\)._ Ketika sebuah halaman HTML diload oleh browser, maka browser akan menciptakan sebuah dokumen. Dokumen ini dimodelkan dalam bentuk objek yang berisi kumpulan data/atribut dan fungsi, yang bisa dimanfaatkan \(dipanggil\) saat kita membuat kode-kode javascript.

Contoh fungsi dalam document adalah document.write\(\) yang berguna untuk menulis di dalam document. Contoh properti/atribut document adalah document.body \(untuk mengakses body HTML\) dan document.title  \(untuk mengakses title HTML\). 

{% tabs %}
{% tab title="JavaScript" %}
{% code title="index.js" %}
```javascript
document.write("Halo Selamat Pagi ");
document.body.style.backgroundColor = "pink";
```
{% endcode %}
{% endtab %}

{% tab title="HTML" %}
{% code title="index.html" %}
```markup
<!DOCTYPE html>
<html>
  <head>
    <title>Indonesia Pagi</title>
    <script src="index.js"></script>
  </head>
  <body>
    Indonesia
  </body>
</html>
```
{% endcode %}
{% endtab %}
{% endtabs %}

Ketika script di atas dijalankan maka akan menulis isi dari body HTMl dengan tulisan "Halo Selamat Pagi ", kemudian mengakses properti style backgroundColor dari body dan menggantinya dengan nilai "pink" sehingga tampilan browser akan meanmpilkan tulisan "Halo Selamat Pagi Indonesia" dengan background browser berwarna pink. 

Fungsi-fungsi lain yang sering digunakan untuk mengakses sebuah element dalam HTML adalah:

* document.getElementById\(\)
* document.getElementsByName\(\)
* document.getElementsByTagName\(\)
* document.getElementsByClassName\(\)
* document.querySelector\(\)
* document.querySelectorAll\(\)

```markup
<p id="main-p">Selamat Pagi</p>
<p>Selamat Siang</p>
<p>Selamat Sore</p>
<p class="malam">Selamat Malam</p>
<p class="malam">Selamat Tidur</p>
<input name="kota" type="text" value="Jakarta"/>
<script>
    document.getElementById("main-p").style.color = "gold";
    document.getElementsByTagName("p")[2].innerText = "Selamat Senja";
    document.getElementsByName("kota")[0].value = "Surabaya";
    document.querySelector("p.malam").innerText = "good night";
    console.log("queryALL", document.querySelectorAll("p.malam, p#main-p"));
</script>
```

Dari kode di atas kita juga mengenal beberapa properti/atribut dari sebuah objek, meliputi: element.style untuk mengakses style dari objek, element.InnerText atau element.innerHTML untuk mengakses text/html dari sebuah object. Document juga mempunyai atribut seperti document.body, document.style dll.

### Variabel dan Konstanta

Variabel adalah kontainer untuk menyimpan data, dimana isi dari data tersebut bisa diubah-ubah. Semua nama variable harus bersifat unik dan menjadi identitas dari variable tersebut \(identifier\). Penamaan variabel \(dan konstanta\) harus mengikuti kaidah : 

* Nama dapat berisi huruf, angka, garis bawah, dan tanda dolar. 
* Nama harus diawali dengan huruf 
* Nama peka huruf besar/kecil \(y dan Y adalah variabel yang berbeda\) 
* Kata-kata yang dicadangkan \(seperti kata kunci JavaScript\) tidak dapat digunakan sebagai nama

Ada dua cara untuk membuat variabel, yaitu dengan var dan let. var adalah cara penggunaan untuk deklarasi variabel global, dimana ruang liangkup hidup-nya di seluruh kode. Sementara let adalah cara deklarasi variable lokal dimana ruang lingkup-nya aganya ada di dalam blok kode dimana variabel tersebut dideklarasikan.

Sementara kontanta adalah suatu kontainer untuk menyimpan data yang tidak dapat diubah. Untuk membuat konstanta digunakan kata kunci const.

{% code title="variable.html" %}
```markup
<h1>variabel dan Konstanta</h1>

<script>
  var salam = "Selamat Pagi";
  console.log("salam di luar blok: ", salam);

  const ekspresi = "senyum";
  console.log("ekspresi di luar blok: ", ekspresi);
    
  {
    // cek apakah salam hidup dalam blok ini
    console.log("salam di dalam blok: ", salam);

    // cek apakah ekspresi hidup di blok ini
    console.log("ekspresi di dalam blok: ", ekspresi);
    
    ekspresi = "tertawa";
    console.log("ekspresi di dalam blok: ", ekspresi);

    salam = "Selamat siang";
    console.log("salam di dalam blok: ", salam);
    
    let sapa = "Halo....";
    console.log("sapa di dalam blok: ", sapa);

    sapa = "Apa Kabar";
    console.log("sapa di dalam blok: ", sapa);

    const jawab = "baik";
    console.log("jawab di dalam blok: ", jawab);
    
  }

  console.log("salam di akhir dan luar blok: ", salam);
  console.log("sapa di akhir dan luar blok: ", sapa);
  console.log("ekspresi di akhir dan luar blok: ", ekspresi);
  console.log("jawab di akhir dan luar blok: ", jawab);
    
</script>
```
{% endcode %}

 ketika kode di atas dijalankan maka akan error `variabel.html:17 Uncaught TypeError: Assignment to constant variable. at variabel.html:17` Ini disebabkan ada upaya untuk mengganti nilai dari sebuah konstanta.   
  
Jika kita komen kode pada baris 17 agar tidak dieksekusi, kemudian kita jalankan kembali kode di atas, maka error akan berpindah pada baris 35  `variabel.html:35 Uncaught ReferenceError: sapa is not defined at variabel.html:35`Ini disebabkan baris 35 menggunakan variabel '_sapa'_ yang tidak dikenal, karena variabel '_sapa'_ hanya hidup di dalam blok saja.  
  
Perhatikan juga baris 37 dimana ada upaya menggunakan konstanta '_jawab'_, kode ini akan menyebabkan error karena konstanta '_jawab'_ hanya dikenal di dalam blok saja.   

### Tipe Data

Ada beberapa tipe data dalam pemrograman javascript

* undefined suatu tipe data yang belum didefinisikan isinya. Jika membuat suatu variable tanpa pernah mengisi data di dalamnya, maka tipe data varibel tersebut adalah undefined. 
* null  sebenarnya null merupakan object, namun sengaja saya pisahkan tersendiri agar mendapat perhatian yang lebih. null adalah suatu keadaan dimana suatu varibel dideklarasikan kemudian diberi nilai null. Jika menjalankan typeof , maka tipe data-nya adalah object. 
* String \(teks\)
* Integer atau Number \(bilangan bulat\)
* Float \(bilangan Pecahan\) : sebenarnya juga merupakan tipe data number.
* Boolean : hanya berisi dua kemungkinan nilai, yaitu : true atau false.
* Object : bisa berupa null, json object, maupun array object. Object merupakan satu-satunya tipe data yang bukan primitif, melainkan tipe data turunan.

```markup
<h1>Tipe Data</h1>

<script>
  let variabelUndefined;
  let variableNull = null;
  let variabelBoolean = true;
  let variabelString = "Apa Kabar?";
  let variabelNumber = 12345;
  let variabelFloat = 3.14;
  let variabelObjectArray = [1, 2, 3, 4, 5];
  let variabelObjectJson = {
    nama: "Naruto",
    umur: 12,
    alamat: "Desa Konoha"
  }
  
  console.log("variabelUndefined", typeof(variabelUndefined));
  console.log("variableNull", typeof(variableNull));
  console.log("variabelBoolean", typeof(variabelBoolean));
  console.log("variabelString", typeof(variabelString));
  console.log("variabelNumber", typeof(variabelNumber));
  console.log("variabelFloat", typeof(variabelFloat));
  console.log("variabelObjectArray", typeof(variabelObjectArray));
  console.log("variabelObjectJson", typeof(variabelObjectJson));
  
</script>
```

Di dalam javascript, perubahan tipe data berlangusng secara dinamis ketika sebuah nilai diassign ke variabel. Bisa jadi dalam state tertentu tipe data variable adalah string, di state berikutnya bisa berubah menjadi number. Perhatikan contoh berikut :

```markup
<h1>Tipe Data Dinamis</h1>

<script>
  let a = 100;
  console.log("a: ", a, " | ", typeof(a));

  a = a + 50;
  console.log("a: ", a, " | ", typeof(a));

  a = a + "50";
  console.log("a: ", a, " | ", typeof(a));

  a = a + " hari";
  console.log("a: ", a, " | ", typeof(a));
</script>
```

