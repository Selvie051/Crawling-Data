###### Selvie Akmalia

###### 160411100051

###### Penambangan dan Pencarian Web - Dosen Pngampu Bapak Mula'ab, S.si, M.kom

###### Teknik Informatika Universitas Trunojoyo Madura

Berikut ini, saya akan membahas tutorial mengambil data (crawl) dari sebuah Website dan disimpan ke database. Sebelumnya, disini saya menggunakan bahasa pemrograman  Python 3.6. Bagi kalian yang belum mempunyai Python, kalian bisa mendownload di internet lalu menginstallnya di laptop masing - masing. 

Dibawah ini adalah tahapan - tahapan untuk mengcrawl data :

- Pertama - tama download Python di internet (kalian bisa memilih ingin mendownload versi berapa), saya memilih mendownload versi 3.6

- Setelah Python terdownload, waktunya menginstall di laptop kalian masing - masing

- Sebelum menjalankan Python, anda perlu menginstall library request dan beautifulsoup dengan cara :

  - Membuka command prompt di laptop anda 

  - Ketikkan kode berikut :

    ```
    pip install bs4
    ```

    pip install bs4 digunakan untuk menginstall beautifulsoup. 

    ```
    pip install requests
    ```

    pip install request digunakan untuk menginstall requests

    Mengapa kita harus menginstall beautifulsoup dan requests ?

    Kita perlu menginstall beautifulsoup untuk mengubah objek file ke beautifulsoup, sedangkan requests untuk mengambil data dari internet

- Setelah requests dan beautifulsoup telah terinstall, kalian bisa membuka Python yang telah terinstall

- Ketikkan code dibawah ini :

  ```
  import requests
  from bs4 import BeautifulSoup
  import sqlite3
  ```

  Code diatas digunakan untuk mengambil semua library yang telah terinstall

- Setelah mengimport seluruh library yang dibutuhkan, maka langkah selanjutnya adalah mengkoneksikan database ke file .db yang telah dibuat sebelumnya, codenya seperti dibawah ini :

  ```
  conn = sqlite3.connect('test.db')
  ```

- Melakukan pengecekan jika terdapat nama tabel yang sama, tabel yang telah saya buat namanya adalah "Berita", jadi jika terdapat tabel yang namanya juga "Berita"maka otomatis akan dihapus, codenya seperti dibawah ini :

  ```
  conn.execute('drop table if exists Berita')
  ```

- Membuat tabel dengan nama sesuai keinginan, tabel disini saya beri nama "Berita" dengan field "Judul" dan "Isi". Codenya seperti dibawah ini :

  ```
  conn.execute('''CREATE TABLE Berita
           (Judul TEXT NOT NULL,
           Isi TEXT NOT NULL);''')
  ```

- Membuat variabel yang isinya adalah link URL dari website yang ingin kita ambil datanya. Codenya seperti dibawah ini :

  ```
  src = "https://www.anehdidunia.com/"
  ```

  Link URL yang saya ambil adalah www.anehdidunia.com

- Setelah itu kita melakukan konversi pada link URL diatas dan mengubahnya ke objek beautifulsoup. Codenya seperti dibawah ini :

  ```
  page = requests.get(src)
  soup = BeautifulSoup(page.content, 'html.parser')
  ```

- FIeld yang telah kita buat tadi yaitu "Judul" dan "Isi" akan mengambil data berdasarkan class yang terdapat pada Website yang kita ambil. Untuk mengetahui class tersebut, kita cukup memblok teks yang akan kita crawl lalu klik kanan, setelah itu klik "Inspect" maka akan muncul class yang ingin kita ambil. Codenya seperti dibawah ini :

  ```
  judul = soup.findAll(class_='post-title entry-title')
  isi = soup.findAll(class_='snippets')
  ```

- Dengan menggunakan perulangan for, kita akan membuat variabel baru yang bernama a dan b kemudian mendeklarasikan ke tipe data "string" dengan deklarasi "%s" dan "%s". Codenya seperti dibawah ini :

  ```
  for i in range(len(judul)):
      a = judul[i].getText()
      b = isi[i].getText()
      
      conn.execute('INSERT INTO Berita(Judul, Isi) VALUES ("%s", "%s")' %(a, b));
  ```

- Membuat variabel yang isinya akan menampilkan seluruh isi yang terdapat pada tabel yang bernama "Berita". Codenya seperti dibawah ini :

  ```
  cursor = conn.execute("SELECT * from Berita")
  ```

- Menampilkan baris yang telah diambil pada tabel "Berita". Codenya seperti dibawah ini :

  ```
  for row in cursor:
      print(row)
  ```

  





