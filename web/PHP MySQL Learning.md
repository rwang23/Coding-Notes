#PHP MySQL Learning
***
###Easy Example 
	<?php // query.php
  	require_once 'login.php';
  	$conn = new mysqli($hn, $un, $pw, $db);
  	if ($conn->connect_error) die($conn->connect_error);

  	$query  = "SELECT * FROM classics";
  	$result = $conn->query($query);
  	if (!$result) die($conn->error);

  	$rows = $result->num_rows;

  	for ($j = 0 ; $j < $rows ; ++$j)
  	{
    	$result->data_seek($j);
    	echo 'Author: '   . $result->fetch_assoc()['author']   . '<br>';
    	$result->data_seek($j);
    	echo 'Title: '    . $result->fetch_assoc()['title']    . '<br>';
    	$result->data_seek($j);
    	echo 'Category: ' . $result->fetch_assoc()['category'] . '<br>';
    	$result->data_seek($j);
    	echo 'Year: '     . $result->fetch_assoc()['year']     . '<br>';
    	$result->data_seek($j);
    	echo 'ISBN: '     . $result->fetch_assoc()['isbn']     . '<br><br>';
    	
  	}
  
  	/////////* 也可以用更简洁的方式
    for ($j = 0 ; $j < $rows ; ++$j)
  	{
    $result->data_seek($j);
    $row = $result->fetch_array(MYSQLI_ASSOC);

    echo 'Author: '   . $row['author']   . '<br>';
    echo 'Title: '    . $row['title']    . '<br>';
    echo 'Category: ' . $row['category'] . '<br>';
    echo 'Year: '     . $row['year']     . '<br>';
    echo 'ISBN: '     . $row['isbn']     . '<br><br>';
  	}
	*///////
  	$result->close();
  	$conn->close();
	?>
	//fetch_array(MYSQLI_NUM) 通过$row[0] $row[1]访问
	//fetch_array(MYSQLI_ASSOC) 通过$row['author']访问
	//fetch_array(MYSQLI_BOTH) 通过两者访问
    
####Read row in mysql
	<?php
    function readDataForwards($dbh) {
      $sql = 'SELECT hand, won, bet FROM mynumbers ORDER BY BET';
      try {
        $stmt = $dbh->prepare($sql, array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL));
        $stmt->execute();
        while ($row = $stmt->fetch(PDO::FETCH_NUM, PDO::FETCH_ORI_NEXT)) {
          $data = $row[0] . "\t" . $row[1] . "\t" . $row[2] . "\n";
          print $data;
        }
        $stmt = null;
      }
      catch (PDOException $e) {
        print $e->getMessage();
      }
    }
    function readDataBackwards($dbh) {
      $sql = 'SELECT hand, won, bet FROM mynumbers ORDER BY bet';
      try {
        $stmt = $dbh->prepare($sql, array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL));
        $stmt->execute();
        $row = $stmt->fetch(PDO::FETCH_NUM, PDO::FETCH_ORI_LAST);
        do {
          $data = $row[0] . "\t" . $row[1] . "\t" . $row[2] . "\n";
          print $data;
        } while ($row = $stmt->fetch(PDO::FETCH_NUM, PDO::FETCH_ORI_PRIOR));
        $stmt = null;
      }
      catch (PDOException $e) {
        print $e->getMessage();
      }
    }

    print "Reading forwards:\n";
    readDataForwards($conn);

    print "Reading backwards:\n";
    readDataBackwards($conn);
    ?>
####SQL Safety Example
	<?php
  	require_once 'login.php';
  	$conn = new mysqli($hn, $un, $pw, $db);
  	if ($conn->connect_error) die($conn->connect_error);

  	$user  = mysql_entities_fix_string($conn, $_POST['user']);
 	$pass  = mysql_entities_fix_string($conn, $_POST['pass']);
  	$query = "SELECT * FROM users WHERE user='$user' AND pass='$pass'";

  	// Etc...
  	function mysql_entities_fix_string($conn, $string)
  	{
    	return htmlentities(mysql_fix_string($conn, $string));
  	}    

  	function mysql_fix_string($conn, $string)
  	{	
    	if (get_magic_quotes_gpc()) $string = stripslashes($string);
    	return $conn->real_escape_string($string);
  	}
	?>
####Notice
	//Use 
	<?php
  	function sanitizeString($var)
  	{
    	if (get_magic_quotes_gpc())
      	$var = stripslashes($var);
    	$var = strip_tags($var);
    	$var = htmlentities($var);
    	return $var;
  	}

  	function sanitizeMySQL($connection, $var)
  	{
    	$var = $connection->real_escape_string($var);
    	$var = sanitizeString($var);
    	return $var;
  	}
  	$var = sanitizeString($_POST['user_input']);
  	$var = sanitizeMySQL($connection, $_POST['user_input']);
	?>

	//instread of 
	$variable = $_POST['user_input'];

***
	<?php
	$servername = "localhost";
	$database = "publications";
	$username = "username";
	$password = "password";

	// Create connection
	$conn = new mysqli($servername, $username, $password,$database);

	// Check connection
	if ($conn->connect_error) {
    	die("Connection failed: " . $conn->connect_error);
	} 
	echo "Connected successfully";
	
	// Create database
	$sql = "CREATE DATABASE myDB";
	
	if ($conn->query($sql) === TRUE) {
    	echo "Database created successfully";
	} else {
    	echo "Error creating database: " . $conn->error;
	}
	
	$sql = "CREATE TABLE MyGuests (
	id INT(6) UNSIGNED AUTO_INCREMENT PRIMARY KEY,
	firstname VARCHAR(30) NOT NULL,
	lastname VARCHAR(30) NOT NULL,
	email VARCHAR(50),
	reg_date TIMESTAMP	
	)";
	
	if ($conn->query($sql) === TRUE) {
    	echo "Database created successfully";
	} else {
    	echo "Error creating database: " . $conn->error;
	}
	
	$sql = "INSERT INTO MyGuests (firstname, lastname, email)
	VALUES ('John', 'Doe', 'john@example.com')";
***	
		// prepare and bind
	$stmt = $conn->prepare("INSERT INTO MyGuests (firstname, lastname, email) VALUES (?, ?, ?)");
	$stmt->bind_param("sss", $firstname, $lastname, $email);

	// set parameters and execute
	$firstname = "John";
	$lastname = "Doe";
	$email = "john@example.com";
	$stmt->execute();

	$firstname = "Mary";
	$lastname = "Moe";
	$email = "mary@example.com";
	$stmt->execute();
	
	
	$stmt->close();
	$conn->close();
	?>
***
	$sql = "SELECT id, firstname, lastname FROM MyGuests";
	$result = $conn->query($sql);

	if ($result->num_rows > 0) {
    	// output data of each row
    	while($row = $result->fetch_assoc()) {
        echo "id: " . $row["id"]. " - Name: " . $row["firstname"]. " " . $row["lastname"]. "<br>";
    	}
	} else {
    	echo "0 results";
		}
	$conn->close();	
***
	$sql = "SELECT * FROM Orders LIMIT 30";
	$sql = "SELECT * FROM Orders LIMIT 10 OFFSET 15";
	$sql = "SELECT * FROM Orders LIMIT 15, 10";
***
#Tricks
###real_escape_string	
	$city = "'s Hertogenbosch";

	/* this query will fail, cause we didn't escape $city */
	if (!$mysqli->query("INSERT into myCity (Name) VALUES ('$city')")) {
    printf("Error: %s\n", $mysqli->sqlstate);
	}

	$city = $mysqli->real_escape_string($city);

	/* this query with escaped $city will work */
	if ($mysqli->query("INSERT into myCity (Name) VALUES ('$city')")) {
    printf("%d Row inserted.\n", $mysqli->affected_rows);
###for prepared Query
	$stmt->bind_param("s",$video_id);
	$stmt->bind_param("s",$_COOKIE['email']);

	 Binds variables to a prepared statement as parameters
	
   	mysqli_stmt_store_result($stmt);
   	Transfers a result set from a prepared statement    
   	
   	$stmt->execute();
   	Executes a prepared Query
   	
   	$stmt->bind_result($video_name);
   	Binds variables to a prepared statement for result storage
   	

	 while ($stmt -> fetch()) {}   	
	 Fetch results from a prepared statement into the bound variables
   	
	mysqli_stmt_free_result($stmt);   	
	Frees stored result memory for the given statement 
	
	$stmt->close();
	Closes a prepared statement

	
##Functions
	$check_count = $stmt->num_rows;
	Return the number of rows in statements result set

   	
   	
   	
   	
