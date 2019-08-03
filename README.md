# UAS Pemrosesan Data Tersebar

Aplikasi Pembelian dan Penjualan dengan menggunakan database Oracle, Mengguanakan Interface di Mobile Apps (Android). Komunikasi data antar Aplikasi menggunakan *RESTful Service* di oracle.

### Database

Aplikasi ini memiliki 5 table, yaitu :

1. [Customer](#table-customer)
2. [Barang](#table-barang)
3. [Penjualan](#table-penjualan)
4. [Pembelian](#table-pembelian)
5. [Supplier](#table-supplier)

#### Table Customer
![Table Customer!](./GMBR/table-customer.JPG "Table Customer")

#### Table Barang
![Table Customer!](./GMBR/table-barang.JPG "Table Barang")

#### Table Penjualan
![Table Customer!](./GMBR/table-penjualan.JPG "Table Pembelian")

#### Table Pembelian
![Table Customer!](./GMBR/t-pembelian.JPG "Table Pembelian")

#### Table Supplier
![Table Customer!](./GMBR/table-supplier.JPG "Table Pembelian")

### *RESTful Services*

![Resful!](./GMBR/resfull-1.jpg "Daftar Restful 1")

![Resful!](./GMBR/resfull-2.jpg "Daftar Restful 2")

PUT dan DELETE menggunakan {id} untuk mengidentifikasi data yang akan dieksekusi.  
Metode HTTP yang digunakan dalam aplikasi ini adalah:

| Method | Deskripsi|
| ------ | ------ |
| **GET** | menyediakan hanya akses baca pada _resource_ |
| **POST** | digunakan untuk menciptakan _resource_ baru |
| **PUT** | digunakan untuk memperbarui _resource_ yang ada atau membuat _resource_ baru |
| **DELETE** | digunakan untuk menghapus _resource_ |

*Resource Handler* & *Query* dapat dilihat pada gambar dibawah ini.

#### *RESTful Service* pada Barang

- **GET Barang**  
![GET](./GMBR/resfull-barang-get.JPG)

- **POST Barang**  
![POST](./GMBR/resfull-barang-post.JPG)

- **PUT Barang**  
![PUT](./GMBR/resfull-barang-put.JPG)

- **DELETE Barang**  
![DELETE](./GMBR/resfull-barang-delete.JPG)

#### *RESTful Service* pada Customer

- **GET Customer**  
![GET](./GMBR/resfull-customer-get.JPG)

- **POST Customer**  
![POST](./GMBR/resfull-customer-post.JPG)

- **PUT Customer**  
![PUT](./GMBR/resfull-customer-put.JPG)

- **DELETE Customer**  
![DELETE](./GMBR/resfull-customer-delete.JPG)

#### *RESTful Service* pada Penjualan

- **GET Penjualan**  
![GET](./GMBR/resfull-pembelian-get.JPG)

- **POST Penjualan**  
![POST](./GMBR/resfull-pembelian-post.JPG)

#### *RESTful Service* pada Pembelian

- **GET Pembelian**  
![GET](./GMBR/resfull-penjualan-post.JPG)

- **POST Pembelian**  
![POST](./GMBR/resfull-penjualan-post.JPG)

#### *RESTful Service* pada Supplier

- **GET Supplier**  
![GET](./GMBR/resfull-supplier-get.JPG)

- **POST Supplier**  
![POST](./GMBR/resfull-supplier-post.JPG)

- **PUT Supplier**  
![PUT](./GMBR/resfull-supplier-put.JPG)

- **DELETE Supplier**  
![DELETE](./GMBR/resfull-supplier-delete.JPG)

### CodeIgniter

[Script](./oracle-uas/application/libraries/Api.php) dibawah ini merupakan script php yang digunakan untuk mengakses *RESTful Services* dari Oracle menggunakan library [Goutte](https://github.com/FriendsOfPHP/Goutte).

```php
use GuzzleHttp\Client;

defined('BASEPATH') or exit('No direct script access allowed');

class Api
{
    private $client;

    public function __construct()
    {
        // base url yang digunakan untuk mengakses RESTful API
        $this->client = new Client(['base_uri' => 'http://192.168.43.75:8888/apex/obe/']);
    }

    public function request($method, $uri, $data = [])
    {
        // data di convert menjadi data JSON
        $options['json'] = $data;

        // jika metode HTTP nya adalah DELETE maka response yang diberikan adalah status code nya
        if ($method == 'delete') {
            $request = $this->client->request($method, $uri);
            return $request->getStatusCode();
        }

        $request = $this->client->request($method, $uri, $options);

        // response yang diberikan berupa content nya
        return $request->getBody()->getContents();
    }
}
```
#### Tampilan Web

- Barang
![List Barang](./GMBR/barang.JPG)

- Customer
![List Customer](./GMBR/customer.JPG)

- Penjualan
![List Penjualan](./GMBR/transaksi-penjualan.JPG)

- Pembelian
![List Pembelian](./GMBR/transaksi-pembelian.JPG)

- Supplier
![List Supplier](./GMBR/supplier.JPG)

#### Tampilan Mobile Apps

- **Android Studio**
![Android Studio](./GMBR/gambar-android.JPG)

- **Tampilan Android**  
![Tampilan Android](./GMBR/android-tampilan.JPG)
