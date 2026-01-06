# lab10web
Ahmad Ibnu Abdillah <br>
TI.24.A.5
# kode
```
<?php
$config = [
    'host' => 'localhost',
    'username' => 'root',
    'password' => '',
    'db_name' => 'latihan1'
];
?>
```
```
<?php
class Database {
    protected $host;
    protected $user;
    protected $password;
    protected $db_name;
    protected $conn;

    public function __construct() {
        $this->getConfig();
        $this->conn = new mysqli($this->host, $this->user, $this->password, $this->db_name);
        
        if ($this->conn->connect_error) {
            die("Connection failed: " . $this->conn->connect_error);
        }
    }

    private function getConfig() {
        // Memanggil file config.php yang berisi array $config
        include_once("config.php");
        $this->host = $config['host'];
        $this->user = $config['username'];
        $this->password = $config['password'];
        $this->db_name = $config['db_name'];
    }

    public function query($sql) {
        return $this->conn->query($sql);
    }

    public function get($table, $where=null) {
        if ($where) {
            $where = " WHERE " . $where;
        }
        $sql = "SELECT * FROM " . $table . $where;
        $result = $this->conn->query($sql);
        return $result->fetch_assoc();
    }

    public function insert($table, $data) {
        if (is_array($data)) {
            foreach($data as $key => $val) {
                $column[] = $key;
                $value[] = "'{$val}'";
            }
            $columns = implode(",", $column);
            $values = implode(",", $value);
        }
        $sql = "INSERT INTO " . $table . " (" . $columns . ") VALUES (" . $values . ")";
        $result = $this->conn->query($sql);
        return ($result == true) ? true : false;
    }

    public function update($table, $data, $where) {
        $update_value = array(); 
        if (is_array($data)) {
            foreach($data as $key => $val) {
                $update_value[] = "$key='{$val}'";
            }
            $update_value = implode(",", $update_value);
        }
        $sql = "UPDATE " . $table . " SET " . $update_value . " WHERE " . $where;
        $result = $this->conn->query($sql);
        return ($result == true) ? true : false;
    }

    public function delete($table, $filter) {
        $sql = "DELETE FROM " . $table . " " . $filter;
        $result = $this->conn->query($sql);
        return ($result == true) ? true : false;
    }
}
?>
```
```
<?php
class Form {
    private $fields = array();
    private $action;
    private $submit = "Submit Form";
    private $jumField = 0;

    public function __construct($action, $submit) {
        $this->action = $action;
        $this->submit = $submit;
    }

    public function displayForm() {
        echo "<form action='".$this->action."' method='POST'>";
        echo '<table width="100%" border="0">';
        for ($j=0; $j<count($this->fields); $j++) {
            echo "<tr><td align='right'>".$this->fields[$j]['label']."</td>";
            echo "<td><input type='text' name='".$this->fields[$j]['name']."'></td></tr>";
        }
        echo "<tr><td colspan='2'>";
        echo "<input type='submit' value='".$this->submit."'></td></tr>";
        echo "</table></form>";
    }

    public function addField($name, $label) {
        $this->fields[$this->jumField]['name'] = $name;
        $this->fields[$this->jumField]['label'] = $label;
        $this->jumField++;
    }
}
?>
```
```
<?php
include "form.php";
echo "<html><head><title>Mahasiswa</title></head><body>";
$form = new Form("", "Input Form");
$form->addField("txtnim", "Nim");
$form->addField("txtnama", "Nama");
$form->addField("txtalamat", "Alamat");
echo "<h3>Silahkan isi form berikut ini:</h3>";
$form->displayForm();
echo "</body></html>";
?>
```
![img](https://github.com/AhmadIbnuAbdillah/img10/blob/2c3ee1273c68a9dd0bdd724aa0a783b9886230a5/Screenshot%202026-01-06%20203959.png)
```
<?php
/**
* Program sederhana pendefinisian class dan pemanggilan class.
**/
class Mobil
{
 private $warna;
 private $merk;
 private $harga;
 public function __construct()
 {
 $this->warna = "Biru";
 $this->merk = "BMW";
 $this->harga = "10000000";
 }
 public function gantiWarna ($warnaBaru)
 {
 $this->warna = $warnaBaru;
 }
 public function tampilWarna ()
 {
 echo "Warna mobilnya : " . $this->warna;
 }
}
// membuat objek mobil
$a = new Mobil();
$b = new Mobil();
// memanggil objek
echo "<b>Mobil pertama</b><br>";
$a->tampilWarna();
echo "<br>Mobil pertama ganti warna<br>";
$a->gantiWarna("Merah");
$a->tampilWarna();
// memanggil objek
echo "<br><b>Mobil kedua</b><br>";
$b->gantiWarna("Hijau");
$b->tampilWarna();
?>

```
![img](https://github.com/AhmadIbnuAbdillah/img10/blob/2c3ee1273c68a9dd0bdd724aa0a783b9886230a5/Screenshot%202026-01-06%20204007.png) <br>
INI ADALAH TEST BAHWA DATABASE.PHP DAN CONFIG.PHP SUDAH BERHASIL <br>
![img](https://github.com/AhmadIbnuAbdillah/img10/blob/2c3ee1273c68a9dd0bdd724aa0a783b9886230a5/Screenshot%202026-01-06%20204016.png)
