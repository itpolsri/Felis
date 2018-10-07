## How to USE

### Create your own config.json in your root project directory like this.
```
{
  "mysql" : {
    "dbh"       : "mysql:hostname = localhost; dbname=ProjectDB;",
    "user"      : "root",
    "password"  : ""
  }
}
```

### Get the Connection
```
require_once __DIR__ .'/vendor/autoload.php';

use Felis\Silvestris\Database as DB;

$db = DB::connect('mysql');
```

#### `Select Example 1`
```
$data = $db->select('users')->fetch(true)->get(); // select all fields from 'users' table
print_r($data);
```

#### `Select Example 2`
```
$data = $db->select('users', 'name')->fetch(true)->get(); // select 'name' field from 'users' table
print_r($data);
```

#### `Select Example 3`
```
$data = $db->select('users')->fetch(true)->toJson()->get(); // return JSON data
print_r($data);
```

#### `Select with where clauses Example`
```
$select = $db->select('users')->where([
  'name' => ['LIKE' => '%John%'],
  'job' => ['=' => 'Developer']
]);
$data = $select->fetch(true)->get();
print_r($data);
```

#### `Insert Example`
```
$insert = $db->insert('users', [
  'name' => 'Johny',
  'job' => 'Developer'
]);
var_dump($insert); //return true or false
```

#### `Update Example`
```
$update = $db->update('users', 'userid', 2, [
  'name' => 'Pretty',
  'job' => 'Sales'
]);
var_dump($update); //return true or false
```

#### `Update Example`
```
$delete = $db->delete('users', 'userid', 2);
var_dump($delete); //return true or false
```

#### `Query builder fetch() data Example`
```
$query = $db->query("SELECT * FROM users WHERE id = 1");
$data = $query->fetch()->get(); //use fetch() to return a data
print_r($data); //return data
```

#### `Query builder execute() Example`
```
$query = $db->query("DELETE * FROM users WHERE id = 1");
$exec = $query->execute(); //use execute() to execute a query
print_r($exec); return true or false
```


##### Silvestris Pagination documentation will come soon
