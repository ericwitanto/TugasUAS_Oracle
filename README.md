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
![Table Customer!](./GMBR/table-customer.jpg "Table Customer")

#### Table Barang
![Table Customer!](./GMBR/table-barang.jpg "Table Barang")

#### Table Penjualan
![Table Customer!](./GMBR/table-penjualan.jpg "Table Pembelian")

#### Table Pembelian
![Table Customer!](./GMBR/t-pembelian.jpg "Table Pembelian")

#### Table Supplier
![Table Customer!](./GMBR/table-supplier.jpg "Table Pembelian")

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
![GET](./GMBR/resfull-barang-get.jpg)

- **POST Barang**  
![POST](./GMBR/resfull-barang-post.jpg)

- **PUT Barang**  
![PUT](./GMBR/resfull-barang-put.jpg)

- **DELETE Barang**  
![DELETE](./GMBR/resfull-barang-delete.jpg)

#### *RESTful Service* pada Customer

- **GET Customer**  
![GET](./GMBR/resfull-customer-get.jpg)

- **POST Customer**  
![POST](./GMBR/resfull-customer-post.jpg)

- **PUT Customer**  
![PUT](./GMBR/resfull-customer-put.jpg)

- **DELETE Customer**  
![DELETE](./GMBR/resfull-customer-delete.jpg)

#### *RESTful Service* pada Penjualan

- **GET Penjualan**  
![GET](./GMBR/resfull-pembelian-get.jpg)

- **POST Penjualan**  
![POST](./GMBR/resfull-pembelian-post.jpg)

#### *RESTful Service* pada Pembelian

- **GET Pembelian**  
![GET](./GMBR/resfull-penjualan-post.jpg)

- **POST Pembelian**  
![POST](./GMBR/resfull-penjualan-post.jpg)

#### *RESTful Service* pada Supplier

- **GET Supplier**  
![GET](./GMBR/resfull-supplier-get.jpg)

- **POST Supplier**  
![POST](./GMBR/resfull-supplier-post.jpg)

- **PUT Supplier**  
![PUT](./GMBR/resfull-supplier-put.jpg)

- **DELETE Supplier**  
![DELETE](./GMBR/resfull-supplier-delete.jpg)

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
![List Barang](./GMBR/barang.jpg)

- Customer
![List Customer](./GMBR/customer.jpg)

- Penjualan
![List Penjualan](./GMBR/transaksi-penjualan.jpg)

- Pembelian
![List Pembelian](./GMBR/transaksi-pembelian.jpg)

- Supplier
![List Supplier](./GMBR/supplier.jpg)

#### Tampilan Mobile Apps

