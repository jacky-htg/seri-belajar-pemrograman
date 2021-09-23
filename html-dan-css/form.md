# Form

Form merupakan alat utama untuk interaksi antara user dengan aplikasi web. Form memungkinkan user untuk memasukkan data, yang kemudian diteruskan untuk diproses/disimpan di server.

HTML form terdiri dari input, textarea, dan select. Namun pada prakteknya tak pernah lepas dari label dan button.  Untuk membuat form biasanya dengan membuat tag form yang diisi dengan dengan elemen-elemen HTML form yang diperlukan.

### Form 

Form merupakan tag untuk mengawali pembuatan form.   
&lt;form&gt;Content&lt;/form&gt;

### Label 

Label merupakan tag untuk membuat label.   
&lt;label for="username"&gt;Content&lt;/label&gt;

### Input

Input merupakan tag generic untuk memasukkan data ke dalam form. Ada berbagai macam tipe yang didukung oleh input. 

```markup
<style>
  label {
    width:120px;
    display: inline-block;
  }

  div {
    padding: 2px;
  }

  form {
    width: 100%;
  }

  input {
    width: 235px;
  }

  .radio-input, .radio-label, .checkbox-input, .checkbox-label {
    width:auto;
  }
</style>

<form>
  <div>
    <label for="text-input">Text</label>
    <input id="text-input" type="text" placeholder="nama"/>
  </div>

  <div>
    <label for="email-input">Email</label>
    <input id="email-input" type="email" placeholder="email"/>
  </div>

  <div>
    <label for="url-input">Url</label>
    <input id="url-input" type="url" value="https://www.rijalasepnugroho.com"/>
  </div>

  <div>
    <label for="tel-input">Tel</label>
    <input id="tel-input" type="tel"/>
  </div>

  <div>
    <label for="number-input">Angka</label>
    <input id="number-input" type="number"/>
  </div>

  <div>
    <label for="password-input">Password</label>
    <input id="password-input" type="password"/>
  </div>

  <div>
    <label for="search-input">Search</label>
    <input id="search-input" type="search"/>
  </div>

  <div>
    <label for="date-input">Tanggal</label>
    <input id="date-input" type="date"/>
  </div>

  <div>
    <label for="datetime-local-input">Datetime Local</label>
    <input id="datetime-local-input" type="datetime-local"/>
  </div>

  <div>
    <label for="month-input">Bulan</label>
    <input id="month-input" type="month"/>
  </div>

  <div>
    <label for="time-input">Jam</label>
    <input id="time-input" type="time"/>
  </div>

  <div>
    <label for="week-input">Week</label>
    <input id="week-input" type="week"/>
  </div>

  <div>
    <label for="color-input">Warna</label>
    <input id="color-input" type="color"/>
  </div>

  <div>
    <label for="file-input">File</label>
    <input id="file-input" type="file"/>
  </div>

  <input id="hidden-input" type="hidden"/>

  <div>
    <label for="range-input">Range</label>
    <input id="range-input" type="range"/>
  </div>

  <div>
    <label>Radio</label>
    <input class="radio-input" id="l-radio-input" name="jenis-kelamin" value="L" type="radio"/>
    <label class="radio-label" for="l-radio-input">Laki-Laki</label>
    <input class="radio-input" id="p-radio-input" name="jenis-kelamin" value="P" type="radio"/>
    <label class="radio-label" for="p-radio-input">Perempuan</label>  
  </div>

  <div>
    <label>Checkbox</label>
    <input class="checkbox-input" id="m-checkbox-input" name="pelajaran[]" value="matematika" type="checkbox"/>
    <label class="checkbox-label" for="m-checkbox-input">Matematika</label>
    <input class="checkbox-input" id="k-checkbox-input" name="pelajaran[]" value="komputer" type="checkbox"/>
    <label class="checkbox-label" for="k-checkbox-input">Komputer</label>
    <input class="checkbox-input" id="b-checkbox-input" name="pelajaran[]" value="bahasa" type="checkbox"/>
    <label class="checkbox-label" for="b-checkbox-input">Bahasa</label> 
  </div>
</form>
```

### Textarea

Textarea  merupakan tag untuk membuat suatu teks dengan panjang tak terbatas. 

```markup
<textarea style="width:50%; height:30vw;">
Form merupakan alat utama untuk interaksi antara user dengan aplikasi web. Form memungkinkan user untuk memasukkan data, yang kemudian diteruskan untuk diproses/disimpan di server.
  
HTML form terdiri dari input, textarea, select, radio dan checkbox. Namun pada prakteknya tak pernah lepas dari label dan button.  Untuk membuat form biasanya dengan membuat tag form yang diisi dengan dengan element-element HTML Form yang diperlukan.
</textarea>
```

### Select

Untuk input yang mempunyai beberapa opsi untuk dipilih, HTML form menyediakan tag select. Select hanya memilih satu dari sekian banyak opsi. Jika ingin memilih lebih dari satu opsi, tambahkan atribut multiple. 

```markup
<style>
  select {
    width: 235px;
  }
</style>
<select multiple>
  <option disabled selected>Pilih Mata Pelajaran yang disukai</option>
  <optgroup label="IPA">
    <option>Matematika</option>
    <option>Fisika</option>
    <option>Biologi</option>
    <option>Kimia</option>
  </optgroup>

  <optgroup label="IPS">
    <option>Sosiologi</option>
    <option>Geografi</option>
    <option>Sejarah</option>
    <option>Akuntansi</option>
  </optgroup>

  <optgroup label="Umum">
    <option>Bahasa Indonesia</option>
    <option>Bahasa Inggris</option>
    <option>Komputer</option>
  </optgroup>
</select>
```

### Button

Button adalah input untuk membuat tombol. Ada tiga tipe button: button, reset dan submit. Tipe button hanya menampilkan tampilan tombol tanpa ada fungsi apapun. Reset menampilkan tombol yang jika diklik akan me-reset _value_ dari form. Tipe submit menampilkan tombol yang jika diklik akan mengirimkan hasil dari pengisian form.

```markup
<form>
<div>
    <label>Radio</label>
    <input class="radio-input" id="l-radio-input" name="jenis-kelamin" value="L" type="radio"/>
    <label class="radio-label" for="l-radio-input">Laki-Laki</label>
    <input class="radio-input" id="p-radio-input" name="jenis-kelamin" value="P" type="radio"/>
    <label class="radio-label" for="p-radio-input">Perempuan</label>  
  </div>

  <div>
    <label>Checkbox</label>
    <input class="checkbox-input" id="m-checkbox-input" name="pelajaran[]" value="matematika" type="checkbox"/>
    <label class="checkbox-label" for="m-checkbox-input">Matematika</label>
    <input class="checkbox-input" id="k-checkbox-input" name="pelajaran[]" value="komputer" type="checkbox"/>
    <label class="checkbox-label" for="k-checkbox-input">Komputer</label>
    <input class="checkbox-input" id="b-checkbox-input" name="pelajaran[]" value="bahasa" type="checkbox"/>
    <label class="checkbox-label" for="b-checkbox-input">Bahasa</label> 
  </div>

  <button type="button">Klik Button</button>
  <button type="reset">Klik Reset</button>
  <button type="submit">Klik Submit</button>
</form>
```

Dengan berakhirnya materi tentang form, berakhir pula materi tentang HTML dan CSS. Sampai di sini, siswa diharapkan sudah mampu melakukan design web, baik melayout halaman web secara umum maupun membuat form.  Untuk memastikan hal tersebut, bab berikutnya adalah praktikum.

