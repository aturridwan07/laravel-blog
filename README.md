
# Membuat Blog dengan Laravel


## Instalasi Laravel
Sebelum menggunakan Laravel, berikut langkah-langkah yang perlu anda lakukan:

1. Pertama-tama, anda harus meng-install aplikasi composer-nya terlebih dahulu dengan mengunjungi link berikut: https://getcomposer.org/download/

2. Download dan install aplikasi composer yang disebutkan pada langkah ke-1.

3. Setelah composer ter-install, periksa apakah instalasinya sudah benar dengan cara mengetikkan perintah “composer” di command prompt seperti yang ditunjukkan pada Gambar 1.
   
   ![gambar 1](https://socs.binus.ac.id/files/2017/09/dewi-5.jpg)
   
   Gambar 1

4. Buat sebuah direktori baru dimana saja pada sistem anda untuk proyek Laravel baru anda.

5. Setelah itu, masuk ke dalam command prompt dan pindahkan posisi inputan perintah ke direktori yang baru dibuat pada langkah ke-4 sebelumnya.

6. Ketik perintah berikut untuk meng-install Laravel pada sistem anda.


    ``` composer create-project laravel/laravel blog --prefer-dist ```


7. Setelah Laravel ter-install pada sistem, anda dapat memulainya dengan memasukkan perintah berikut pada command prompt dengan perintah berikut.
   
   ``` php artisan serve ```


## Template

Download Template berikut dari link [https://github.com/aturridwan07/template-admin-css-bootstrap/](https://github.com/aturridwan07/template-admin-css-bootstrap) yang dalam format .rar

 ![template](https://raw.githubusercontent.com/aturridwan07/template-admin-css-bootstrap/master/articles.PNG)

 Di dalam template.rar terdapat beberapa file dan folder yang dapat dipakai.

 ![list file](https://raw.githubusercontent.com/aturridwan07/template-admin-css-bootstrap/master/list-files.JPG)

 Cara pemakaian :
 1. Copy seluruh folder **assets** ke folder **public** di project laravel blog.
 2. Copy seluruh file html ke folder **resources -> views**.
 3. Ubah nama seluruh file dari ***.html** ke ***.blade.php**

## Buat Route
    Untuk membuat routing, buka file web.php di folder routes di blog.
    
### Buat Route untuk halaman login
``` php
    Route::get("/login",function(){
        return view("login");
    });
```
### Buat Route untuk halaman register
``` php
    Route::get("/register",function(){
        return view("register");
    });
```
## Buat Controller Articles

1. Ketik perintah berikut untuk membuat Controller dengan Resources.

    ``` php artisan make:controller ArticlesController -r ```
    
2. Kemudian cek di folder **blog -> app ->Http -> Contollers** akan terdapat satu file dengan nama **ArticlesController.php**

    ``` php
    <?php

    namespace App\Http\Controllers;

    use Illuminate\Http\Request;

    class ArticlesController extends Controller
    {
        /**
        * Display a listing of the resource.
        *
        * @return \Illuminate\Http\Response
        */
        public function index()
        {
            //
        }

        /**
        * Show the form for creating a new resource.
        *
        * @return \Illuminate\Http\Response
        */
        public function create()
        {
            //
        }

        /**
        * Store a newly created resource in storage.
        *
        * @param  \Illuminate\Http\Request  $request
        * @return \Illuminate\Http\Response
        */
        public function store(Request $request)
        {
            //
        }

        /**
        * Display the specified resource.
        *
        * @param  int  $id
        * @return \Illuminate\Http\Response
        */
        public function show($id)
        {
            //
        }

        /**
        * Show the form for editing the specified resource.
        *
        * @param  int  $id
        * @return \Illuminate\Http\Response
        */
        public function edit($id)
        {
            //
        }

        /**
        * Update the specified resource in storage.
        *
        * @param  \Illuminate\Http\Request  $request
        * @param  int  $id
        * @return \Illuminate\Http\Response
        */
        public function update(Request $request, $id)
        {
            //
        }

        /**
        * Remove the specified resource from storage.
        *
        * @param  int  $id
        * @return \Illuminate\Http\Response
        */
        public function destroy($id)
        {
            //
        }
    }

    ```

3. Dan tambahkan kode berikut ```return view("listArticle");``` ke dalam ```  public function index(){ .. } ``` :

    ``` php
    public function index()
    {
        return view("listArticle");
    }
    ```

4. Kemudian tambahkan ke file web.php di folder routes di blog, route controller ArticlesController :
   ``` php
    Route::get("list-article","ArticlesController@index");
    ```
5. Jalankan perintah :
   
   ``` php artisan serve ```

6. Dan ketikkan http://127.0.0.1:8000/list-article di browser kemudian ```enter```;


## Buat Model
    Model digunakan untuk menghubungkan ke database.  Yang akan kita gunakan adalah database MySQL yang telah diinstal berbarengan dengan XAMPP.

### Nyalakan server database MySQL
1. Buka XAMPP Control Panel
2. ```Start``` service MYSQL.

### Buat Database
1. buka http://localhost/phpmyadmin di browser.
2. kemudian buat sebuah database baru dengan cara klik di menu ```Databases``` dan ketikan nama database ``blog_db`` kemudian klik tombol ``create``

### Setting jalur ke database
    Untuk menset jalur aplikasi agar dapat terhubung ke database MySQL.
Berikut cara untuk mensetting jalur :
1. Di folder ```blog``` , buka file ```.env```
2. Cari baris kode :
    ``` env
    DB_CONNECTION=mysql
    DB_HOST=127.0.0.1
    DB_PORT=3306
    DB_DATABASE=homestead
    DB_USERNAME=homestead
    DB_PASSWORD=secret
    ```
3. Kemudian rubah menjadi :
   ```DB_CONNECTION=mysql
    DB_HOST=127.0.0.1
    DB_PORT=3306
    DB_DATABASE=blog_db
    DB_USERNAME=root
    DB_PASSWORD=
   ```

### Buat Model Article beserta Migration File
    Model Article digunakan untuk menempatkan code php yang akan digunakan untuk operasi ke tabel Article di database.  Dan Migration File nya akan digunakan untuk membuat struktur database dari laravel langsung tanpa membuatnya dalam SQL.  Hal ini memungkinkan untuk mengganti jenis database yang digunakan dengan mudah.
Ikuti langkah-langkah berikut :
1. Ketik perintah berikut untuk membuat Controller dengan Resources.

    ``` php artisan make:model Article --migration ```
