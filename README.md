# tugas_project_besar

```s
NAMA    : ALIYAH ASMARANI
```

# INPUT
```
<?php
$berkas = "data.json";
$dataJson = file_get_contents($berkas);
$pesananPelangganAll = json_decode($dataJson, true);

if (isset($_POST['pesan'])) {
  $namaPelanggan = $_POST['nama'];
  $menuMochi = $_POST['menu'];
  $alamatPelanggan = $_POST['alamat'];

  $pesananPelanggan = [
    'nama' => $namaPelanggan,
    'menu' => $menuMochi,
    'alamat' => $alamatPelanggan
  ];

  if (is_array($pesananPelangganAll)) {
    $pesananPelangganAll[] = $pesananPelanggan;
  } else {
    $pesananPelangganAll = [$pesananPelanggan];
  }

  $dataJson = json_encode($pesananPelangganAll, JSON_PRETTY_PRINT);
  file_put_contents($berkas, $dataJson);

  // Mengurutkan Daftar Maskapai sesuai Abjad dari yang terkecil
  usort($pesananPelangganAll, function ($a, $b) {
    return $a['nama'] <=> $b['nama'];
  });

  $dataJson = json_encode($pesananPelangganAll, JSON_PRETTY_PRINT);
  file_put_contents($berkas, $dataJson);
}
?>
```
> $pesananPelangganAll : Data ini akan disimpan dalam variabel $pesananPelangganAll dan digunakan untuk menampilkan daftar pesanan pelanggan.
>
> if (isset($_POST['pesan'])) { ... }: Ini adalah blok kondisional yang mengecek apakah tombol "Pesan" pada formulir diklik. Jika ya, maka blok kode di dalamnya akan dieksekusi untuk memproses data pesanan yang diinput oleh pengguna.
>
> if (is_array($pesananPelangganAll)) { ... } else { ... }: Blok kondisional ini memeriksa apakah $pesananPelangganAll sudah berisi array pesanan pelanggan sebelumnya. Jika ya, maka data pesanan yang baru diinput akan ditambahkan ke dalam array tersebut. Jika belum, maka array baru akan dibentuk.
>
> usort($pesananPelangganAll, function ($a, $b) { ... });: Mengurutkan array $pesananPelangganAll berdasarkan nilai 'nama' dalam setiap elemennya menggunakan usort(). Fungsi komparasi di dalamnya akan membandingkan nilai 'nama' antara dua elemen array untuk menentukan urutan pengurutan.
>

```
<!doctype html>
<html>
  <head>
    <title>Mo'mochiah</title>
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <div class="wrapper">
      <div class="nav">
        <div class="logo">
          <a href="#">
            <p>Mo'Mochiah</p>
          </a>
        </div>
        <ul>
          <li>HOME</li>
          <li>MENU</li>
          <li>PEMESANAN</li>
        </ul>
      </div>
<div class="body">
        <div class="container px-5">
        <form method="POST">
          <td>
            <!-- Masukkan data nama -->
            <label for="nama">Nama:</label>
            <input type="text" id="nama" name="nama" required>
          </td>
          
          <td>
            <!-- Masukkan data menu -->
            <label for="menu">Menu:</label>
            <select id="menu" name="menu" required>
              <option value="">Pilih Menu</option>
              <option value="Daifuku Mochi">Daifuku Mochi</option>
              <option value="Mochi Strawberry">Mochi Strawberry</option>
              <option value="Mochi Isi Kacang">Mochi Isi Kacang</option>
            </select>
          </td>
          
          <td>
            <!-- Masukkan data alamat -->
            <label for="alamat">Alamat:</label>
            <input type="text" id="alamat" name="alamat" required>
          </td>
          <input type="submit" value="Pesan" name="pesan">
        </form>

        <!-- Menampilkan Daftar Pemesanan Pelanggan -->
        <h1 class= "text-center py-5">Data Pesanan Pelanggan</h1>
      <table border="1" style="width: 800px;">
        <thead>
          <th>No</th>
          <th>Nama</th>
          <th>Menu</th>
          <th>Alamat</th>
          </tr>
        </thead>
        <tbody>
          <?php
          $no = 1;
          foreach ($pesananPelangganAll as $pesanan) {
            echo "<tr>";
            echo "<td>" . $no . "</td>";
            echo "<td>" . $pesanan['nama'] . "</td>";
            echo "<td>" . $pesanan['menu'] . "</td>";
            echo "<td>" . $pesanan['alamat'] . "</td>";
            echo "</tr>";
            $no++;
          }
          ?>
        </tbody>
      </table>

        </div>
      </div>
    </div>

    <!-- Menampilkan Daftar Pemesanan Pelanggan
        <h1 class= "text-center py-5">Data Pesanan Pelanggan</h1>
      <table border="1" style="width: 800px;">
        <thead>
          <th>No</th>
          <th>Nama</th>
          <th>Menu</th>
          <th>Alamat</th>
          </tr>
        </thead>
        <tbody>
          <?php
          $no = 1;
          foreach ($pesananPelangganAll as $pesanan) {
            echo "<tr>";
            echo "<td>" . $no . "</td>";
            echo "<td>" . $pesanan['nama'] . "</td>";
            echo "<td>" . $pesanan['menu'] . "</td>";
            echo "<td>" . $pesanan['alamat'] . "</td>";
            echo "</tr>";
            $no++;
          }
          ?>
        </tbody> -->
      </table>
  </body>
</html>
```

# OUTPUT
![image](https://github.com/R4N104/tugas_project_besar/assets/138820515/353023dc-9820-40a4-922a-9fb65e28cf44)
