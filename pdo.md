## PDO

PHP 数据对象, 为PHP访问数据库定义了一个轻量级的一致接口. 

利用 PDO 扩展自身并不能实现任何数据库功能；必须使用一个 具体数据库的 PDO 驱动 来访问数据库服务。

PDO 提供了一个 数据访问 抽象层，这意味着，不管使用哪种数据库，都可以用相同的函数（方法）来查询和获取数据。

- oo
- 轻量级
- 一致接口

PDO 驱动

CUBRID (PDO)
MS SQL Server (PDO)
Firebird (PDO)
IBM (PDO)
Informix (PDO)
MySQL (PDO)
Oracle (PDO)
ODBC and DB2 (PDO)
PostgreSQL (PDO)
SQLite (PDO)
4D (PDO)

```
<?php

try {

    //create connection
    $dbh = new PDO('mysql:host=localhost;dbname=test', $user, $pass);
    
    /*持久连接
    $dbh = new PDO('mysql:host=localhost;dbname=test', $user, $pass, array(
        PDO::ATTR_PERSISTENT => true
    ));    
    */
    
    //crud    
    foreach($dbh->query('SELECT * from FOO') as $row) {
        //query return an PDOStatement object, see the doc to learn more about it to get the result
        print_r($row);
    }
    
    //prepare
    $sql = 'SELECT name, colour, calories
    FROM fruit
    WHERE calories < :calories AND colour = :colour';
    $sth = $dbh->prepare($sql, array(PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY));
    $sth->execute(array(':calories' => 150, ':colour' => 'red'));
    $red = $sth->fetchAll();
    $sth->execute(array(':calories' => 175, ':colour' => 'yellow'));
    $yellow = $sth->fetchAll();
    
    //事务
    try {  
      $dbh->beginTransaction();
      //exec is like query, but it dose not return an PDOStatement object, instead, it return the number of affacted rows
      $dbh->exec("insert into staff (id, first, last) values (23, 'Joe', 'Bloggs')");
      $dbh->exec("insert into salarychange (id, amount, changedate) 
          values (23, 50000, NOW())");
      $dbh->commit();
      
    } catch (Exception $e) {
      $dbh->rollBack();
      echo "Failed: " . $e->getMessage();
    }
 
    //close connection
    $dbh = null;
    
    //error handling with error code
    echo $dbh->errorCode();
    echo $dbh->errorInfo();
    
    
} catch (PDOException $e) {
    //error handling with exception
    print "Error!: " . $e->getMessage() . "<br/>";
    die();
}

?>
```

## mysql

推荐使用PDO_MySQL或mysqli来访问mysql。mysql扩展已在 PHP 5.5.0被弃用。

mysqli指：MySQL Improved。

PDO_MySQL或mysqli两者的主要区别：

mysqli支持：Procedural Interface(指过程化风格），API supports non-blocking, asynchronous queries with mysqlnd
不支持：API supports client-side Prepared Statements。
PDO_MySQL相反。

The mysqli, PDO_MySQL PHP extensions are lightweight wrappers on top of a C client library.
The extensions can either use the mysqlnd library or the libmysqlclient library. Choosing a library is a compile time decision.
mysqlnd library比libmysqlclient library功能丰富，建议使用。

mysqlnd -  MySQL Native Driver

The MySQL database extensions MySQL extension, mysqli and PDO MYSQL all communicate with the MySQL server. In the past, this was done by the extension using the services provided by the MySQL Client Library. The extensions were compiled against the MySQL Client Library in order to use its client-server protocol.

With MySQL Native Driver there is now an alternative, as the MySQL database extensions can be compiled to use MySQL Native Driver instead of the MySQL Client Library.

MySQL Native Driver is written in C as a PHP extension.

mysqlnd是被PDO_MySQL或mysqli使用来连接mysqlserver，其实现也是一个php扩展。



```php
<?php

//错误处理
mysqli_report(MYSQLI_REPORT_STRICT); 

try{
    //连接
    $mysqli = new mysqli('localhost', 'my_user', 'my_password', 'my_db');
} catch (mysqli_sql_exception $e) { 
    throw $e; //异常处理
} 

//持久连接
//需要打开一个持久化连接时，你必须在 连接时在主机名前增加p:

//错误处理
if ($mysqli->connect_error) {
    die('Connect Error (' . $mysqli->connect_errno . ') '
            . $mysqli->connect_error);
}

//crud
if ($result = $mysqli->query("SELECT Name FROM City LIMIT 10")) {
    printf("Select returned %d rows.\n", $result->num_rows);

    /* free result set */
    $result->close();
}

//Executes one or multiple queries which are concatenated by a semicolon.
$query  = "SELECT CURRENT_USER();";
$query .= "SELECT Name FROM City ORDER BY ID LIMIT 20, 5";


if ($mysqli->multi_query($query)) {
    do {
        /* store first result set */
        if ($result = $mysqli->store_result()) {
            while ($row = $result->fetch_row()) {
                printf("%s\n", $row[0]);
            }
            $result->free();
        }
        /* print divider */
        if ($mysqli->more_results()) {
            printf("-----------------\n");
        }
    } while ($mysqli->next_result());
}

//prepare
$city = "Amersfoort";
if ($stmt = $mysqli->prepare("SELECT District FROM City WHERE Name=?")) {

    /* bind parameters for markers */
    $stmt->bind_param("s", $city);

    /* execute query */
    $stmt->execute();

    /* bind result variables */
    $stmt->bind_result($district);

    /* fetch value */
    $stmt->fetch();

    printf("%s is in district %s\n", $city, $district);

    /* close statement */
    $stmt->close();
}

//事务
$mysqli->begin_transaction(MYSQLI_TRANS_START_READ_ONLY);

$mysqli->query("SELECT first_name, last_name FROM actor");
$mysqli->query("SELECT last_name FROM actor");
$mysqli->commit();

$mysqli->close();

echo 'Success... ' . $mysqli->host_info . "\n";

//关闭连接
$mysqli->close();

?>

```

