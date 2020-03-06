Pastikan untuk mendownload dan menginstall aplikasi postman di https://www.postman.com

Pertama Buat file baru bernama kontak.php di dalam controllers lalu masukkan code dibawah

<?php

defined('BASEPATH') OR exit('No direct script access allowed');

require APPPATH . '/libraries/REST_Controller.php';
use Restserver\Libraries\REST_Controller;

class Kontak extends REST_Controller {

    function __construct($config = 'rest') {
        parent::__construct($config);
        $this->load->database();
    }

    function index_get() {
        $id = $this->get('id');
        if ($id == '') {
            $kontak = $this->db->get('telepon')->result();
        } else {
            $this->db->where('id', $id);
            $kontak = $this->db->get('telepon')->result();
        }
        $this->response($kontak, 200);
    }

    function index_post() {
        $data = array(
                    'id'           => $this->post('id'),
                    'nama'          => $this->post('nama'),
                    'nomor'    => $this->post('nomor'));
        $insert = $this->db->insert('telepon', $data);
        if ($insert) {
            $this->response($data, 200);
        } else {
            $this->response(array('status' => 'fail', 502));
        }
    }

    function index_put() {
        $id = $this->put('id');
        $data = array(
                    'id'       => $this->put('id'),
                    'nama'          => $this->put('nama'),
                    'nomor'    => $this->put('nomor'));
        $this->db->where('id', $id);
        $update = $this->db->update('telepon', $data);
        if ($update) {
            $this->response($data, 200);
        } else {
            $this->response(array('status' => 'fail', 502));
        }
    }

    function index_delete() {
        $id = $this->delete('id');
        $this->db->where('id', $id);
        $delete = $this->db->delete('telepon');
        if ($delete) {
            $this->response(array('status' => 'success'), 201);
        } else {
            $this->response(array('status' => 'fail', 502));
        }
    }

}
?>

setelah code diatas di save buka aplikasi postman dengan alamat http://127.0.0.1/rest_ci/index.php/kontak
Penggunaan postman terdapat 4 cara yaitu GET, POST, PUT, dan DELETE
GET
Untuk menguji kode yang telah dibuat buka Postman, Pilih metode GET, masukan http://127.0.0.1/Rest_ci/index.php/kontak pada address bar lalu klik "Send".(Yang berfungsi sebagai menampilkan semua data)
POST
Untuk mengujinya buka Postman, pilih metode POST, masukan http://127.0.0.1/Rest_ci/index.php/kontak pada address bar, klik "Body" pada menu dibawah address bar, pilih x-www-form-urlencoded, masukan key dan value yang diperlukan (id, nama, nomor), lalu klik "Send".(Yang berfungsi sebagai menambah data)
PUT
Untuk mengujinya buka Postman, pilih metode PUT, masukan http://127.0.0.1/Rest_ci/index.php/kontak pada address bar, klik "Body" pada menu dibawah address bar, pilih x-www-form-urlencoded, masukan key id dan value id yang akan diubah (88) diikuti key dan value selanjutnya, lalu klik "Send".(Yang berfungsi sebagai mengedit dan mengupdate data)
DELETE
Untuk mengujinya buka Postman, pilih metode DELETE, masukan http://127.0.0.1/rest_ci/index.php/kontak pada address bar, klik "Body" pada menu dibawah address bar, pilih x-www-form-urlencoded, masukan key id dan value id yang akan dihapus (88), lalu klik "Send".(Yang berfungsi sebagai menghapus data)
