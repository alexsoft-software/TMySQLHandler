# TMySQLHandler - MySQL Wrapper for ASCOOS Framework

TMySQLHandler is a MySQL database handler designed to **simulate legacy MySQL functions** while utilizing modern **MySQLi** functionality within the **ASCOOS Framework**.

## 🔧 Requirements
- PHP `>= 8.2`
- MariaDB `>= 11.x`
- ASCOOS Framework `>= 25.0.0.x`

## 🛠️ Installation
1. Clone the repository:
   ```sh
   git clone https://github.com/alexsoft-software/TMySQLHandler.git
   ```
2. Include the library in your project:
   ```php
   require_once '/path/to/mysql.php';
   ```

## Class Usage Example
```php
<?php

require_once '/path/to/mysql.php';

use ASCOOS\FRAMEWORK\Extras\DB\MySQL\TMySQLHandler;

// Class Properties
$properties = [
    'db' => [
        'mysqli' => [
            'host' => 'localhost',
            'user' => 'root',
            'pass' => 'password',
            'dbname' => 'test_db',
            'prefix' => '',
            'persistency' => false
        ]
    ],
    'logs' => [
        'useLogger' => false
    ],
];

// Initialize Class
$db =& TMySQLHandler::getInstance($properties);

// MySQL Query
$query = "SELECT * FROM #__snippets LIMIT ?";
$params = [5];
$result = $db->query($query, $params);

if ($result instanceof mysqli_result) {
    while ($row = $result->fetch_assoc()) {
        echo "<p>Snippets: " . $row['title'] . "</p>" . PHP_EOL;
    }
}

$db->close();


/*
Output Results
----------------
Snippets: Interactive BootLib Button with Rotation and Effects
Snippets: jAscoos on Event
Snippets: jAscoos add Event
Snippets: Orange
Snippets: jAscoos Attr method
*/
?>
```

## 🚀 Helper Functions Usage Example
```php
require_once '/path/to/mysql.php';

use function ASCOOS\FRAMEWORK\Extras\DB\MySQL\{
    mysql_connect, mysql_query, mysql_close
};

$db = mysql_connect('localhost', 'root', 'password', 'test_db');

$query = "SELECT * FROM #__snippets";
$result = mysql_query($db, $query);

if ($result instanceof mysqli_result) {
    while ($row = $result->fetch_assoc()) {
        echo "<p>Snippets: " . $row['title'] . "</p>" . PHP_EOL;
    }
}

mysql_close($db);
```

## 📌 Available Methods

### **Core Methods (`TMySQLHandler`)**
| Method | Return     | Description     |
|--------|------------|-----------------|
| `__construct(array $properties = [])` | void  | Constructor to initialize the class.   |
| `&getInstance(array $properties = [])` | TMySQLHandler  | Get the singleton instance of TMySQLHandler.   |
| `affected_rows()` | int  | Get the number of affected rows in the last query.   |
| `backup_database($database, $file)` | bool /  mysqli_result   | Create a backup of the specified database and save to a file.      |
| `begin_transaction(int $flags = 0, ?string $name = null)` | bool   | Begin a transaction.      |
| `client_encoding()` | string   |  Get the name of the current character set.     |
| `close()` | void   | Close the database connection.      |
| `commit_transaction()` | bool   | Commit the current transaction.      |
| `connect(?string $host = null, ? string $username = null, ?string $password = null, ?string $database = null, ?int $port = null, ?string $socket = null)` | mysqli   | Establish a connection to a MySQL database.      |
| `create_db(string $database)` | bool / mysqli_result   | Create a new MySQL database.      |
| `data_seek(mysqli_result $result, int $offset)` | bool   | Move the internal result pointer to a specified row.      |
| `db_name(mysqli_result $result, int $row)` | string / false   | Retrieve a database name from the result of mysql_list_dbs.      |
| `db_query(string $database, string $query)` | mysqli_result / false   | Select a database and execute a query on it.      |
| `drop_db(string $database)` | bool   | Drop (delete) a MySQL database.      |
| `errno()` | int   | Get the numerical value of the last error from MySQL.      |
| `error()` | string   | Get the error message from the last MySQL operation.      |
| `escape_string(string $string)` | string   | Escape special characters in a string for use in a query.      |
| `fetch_array(mysqli_result $result, int $result_type = MYSQLI_BOTH)` | array / null / false   | Fetch a result row as an associative array, a numeric array, or both.      |
| `fetch_assoc(mysqli_result $result)` | array /null / false   | Fetch a result row as an associative array.      |
| `fetch_field(mysqli_result $result)` | bool / object   | Get column information from a result and return it as an object.      |
| `fetch_lengths(mysqli_result $result)` | array / null   | Get the length of each output in the current result row.      |
| `fetch_object(mysqli_result $result)` | bool / object / null   | Fetch a result row as an object.      |
| `fetch_row(mysqli_result $result)` | array / bool / null   | Fetch a result row as a numeric array.      |
| `field_flags(mysqli_result $result, int $field_offset)` | string / null   | Get the flags associated with the specified field in a result.      |
| `field_len(mysqli_result $result, int $field_offset)` | int / null   | Get the length of the specified field in a result.      |
| `field_name(mysqli_result $result, int $field_offset)` | string / null   | Get the name of the specified field in a result.      |
| `field_seek(mysqli_result $result, int $field_offset)` | bool   | Set the result pointer to a specified field offset.      |
| `field_table(mysqli_result $result, int $field_offset)` | string / null   | Get the table name associated with the specified field in a result.      |

### **Helper Functions**
| Method | Return     | Description     |
|--------|------------|-----------------|
| `mysql_connect(?string $host, ?string $user, ?string $password, ?string $database, ?int $port = null, ?string $socket = null)`| TMySQLHandler   | Establishes connection using `TMySQLHandler::getInstance()`. |
| `mysql_query(TMySQLHandler $db, string $query, array $params = [])` | mysqli_result / bool   | Executes an SQL query using `query()`. |
| `mysql_list_dbs(TMySQLHandler $db)` | mysqli_result | Retrieves available databases. |
| `mysql_fetch_assoc(mysqli_result $result)` | array / null | Fetches a row as an associative array. |
| `mysql_close(TMySQLHandler $db)` | void | Closes the database connection. |

## 🤝 Contributing
We welcome contributions! Feel free to fork the repository, make your changes, and submit a pull request.

## 📜 License
This project is licensed under the AGL-F License - see the [LICENSE file](LICENSE_AGL-F.md) for details.

---

This text is a living document and will be updated as the TMySQLHandler class evolves.
