#PHP Learning
***
check_function to see if the function exists

	<?php
  		if (function_exists("array_combine"))
  		{
    		echo "Function exists";
  		}
		else {
    		echo "Function does not exist - better write our own";
  		}
	?>
##Syntax
Basic Syntax
	
	<php echo "Hello World"; 
		 echo $variable;	
		 echo <<<_END
		 _END; 
		 // no comment after _END and it must be fisrt in the line, also between END, dont need to be add escape
	?>
include
	include "library.php";
	include_once "library.php";
	require_once "library.php"; //must have this file or fail	
Variable
	
	$variable =1;
	$string = "PHP Learning";
	$team = array("Bill","Alice","Mary");
	$team2 = array(array("Bill","Alice","Mary"),
				   array("John","Snow","Sawer")
	);
	echo $team2[0][0];
	
	echo "You have to buy".$string."books";
	
	$info = 'Preface variables with a $ like this: $variable'; //single quotation, just string
	$info = "Preface variables with a $ like this: $variable"; //double quoatation, will get variable
	
	$text = 'My spelling\'s still atroshus';
	
	define("ROOT_LOCATION", "/usr/local/www/");
	
	global $user;
	
    // you don’t want any other parts of your code to have access to, but you would also like to keep its value for the next time the function is called
    //can not be initialized with the expression
	function test() //static variable 
  	{
    	static $count = 0;
    	echo $count;
    	$count++;
	}

superglobal and security

	$_SERVER $_GET $_POST $_FILES $_COOKIE $_SESSION

	$_REQUEST $_ENV

	
	$came_from = htmlentities($_SERVER['HTTP_REFERER']);
##Array
####assign
  	  $p1 = array("Copier", "Inkjet", "Laser", "Photo");
	  $p2 = array('copier' => "Copier & Multipurpose",
              'inkjet' => "Inkjet Printer",
              'laser'  => "Laser Printer",
              'photo'  => "Photographic Paper");

####foreach

	$paper = array("Copier", "Inkjet", "Laser", "Photo");
  	$j = 0;
  	foreach($paper as $item)
  	{
    	echo "$j: $item<br>";
		++$j; }      

	
  	foreach($paper as $item => $description)
    echo "$item: $description<br>";	
	或者可以用
	while (list($item, $description) = each($paper))
    echo "$item: $description<br>";

   	多维数组
   	 foreach($products as $section => $items)
    	foreach($items as $key => $value)
      		echo "$section:\t$key\t($value)<br>";
	使用foreach之后还想再使用，就必须使用
	reset($paper); 
	用end可以使foreach pointer移到最后一个
	end($paper);
      		
####Function
	is_array();
	count();
	sort();
	shuffle();
	explode();
	$temp = explode(' ', "This is a sentence with seven words");//将temp转化成了array，每个元素由空格隔开
	extract($_GET)//will automatedly create variable $q to store
	extract($_GET, EXTR_PREFIX_ALL, 'fromget');//这样会得到$fromget_q
	compact();//将多个variable放在一起组成array
####example for compact and explode
	  $j       = 23;
  	  $temp    = "Hello";
      $address = "1 Old Street";
      $age     = 61;
      print_r(compact(explode(' ', 'j temp address age')));	
		将会得到
	Array (
      [j] => 23
      [temp] => Hello
      [address] => 1 Old Street
      [age] => 61
)

      
      		
            	
##Objects and Class
####syntax
	$object1 = new User();
	$object2 = new User();
	$object->name     = "Joe";
  	$object->password = "mypass";
  	$object1 = $object2; // this is not assignment, but making $object1 have the "Joe" and "mypass" value
  	$object1 = clone  $object2;

	class User {
    	public $name, $password;
    	function save_user()
    	{
      		echo "Save User code goes here";
    	}
	}

####Method Scope

	public, outside can access. public can be writen into var

	protected, can be referenced only by the object’s class methods and those of any subclasses.

	private, can be referenced only by methods within the same class—not by subclasses. 	
####static method
	User::pwd_string();//have no access to property
	class User {
    	static function pwd_string()
    	{
      	echo "Please enter your password";
    	}
	}    
####inherit
	class user{}
	class subscriber extends user{}
	parent::test();
	parent::__construct();	
	
##Function
function function_name(){};
####String Function
	sutstr() 提取string
	strrev() return reversed order of character
	str_repeat() repeat twice
	strtoupper() to upper	
	strytolower()
	ucfirst()  fisrt character to upper
####Math Function
	abs()	
####Normal Function
	printf("There are d% ", 3);	
	printf("The result is: $%.2f", 123.42 / 12);//.2f return 2 digit of precision
####Time function
	echo time();
	echo mktime(0,0,0,1,1,2000);
	//hour minute second month day year
	date($format,$timestamp);//refer to manual
    echo "The date is ".date("l F jS Y",time());
	checkdate($month, $day, $year); //check whether the date is valid
####File function
	  $fh = fopen("testfile.txt", 'w') or die("Failed to create file");
	  $line = fgets($fh);
	  $text = fread($fh, 3);//the third line
	  fwrite($fh, $text) or die("Could not write to file");
	  copy('testfile.txt', 'testfile2.txt') or die("Could not copy file");
	  rename('testfile2.txt', 'testfile2.new')
	  file_get_contents("testfile.txt");
  	  fclose($fh);	
  	  unlink('testfile2.new')

  	  

  	    $fh   = fopen("testfile.txt", 'r+') or die("Failed to open file");
  		$text = fgets($fh);
  		fseek($fh, 0, SEEK_END);
  		fwrite($fh, "$text") or die("Could not write to file");
  		fclose($fh);

####Uploading File

	$name = $_FILES['filename']['name'];
    move_uploaded_file($_FILES['filename']['tmp_name'], $name);
    echo "Uploaded image '$name'<br><img src='$name'>";

    $_FILES['file']['tmp_name']//The name of the temporary file stored on the server

    $_FILES['file']['name']//The name of the uploaded file (e.g., smiley.jpg)   		

    $_FILES['file']['type']//The content type of the file (e.g., image/jpeg)

    $_FILES['file']['size']//The file’s size in bytes

    $_FILES['file']['error'//The error code resulting from the file upload

    $name = preg_replace("/[^A-Za-z0-9.]/", "", $name);

    $name = strtolower(ereg_replace("[^A-Za-z0-9.]", "", $name));

  		
##Cookies
####Cookies Function
	setcookie(name, value, expire, path, domain, secure, httponly);
    setcookie('username', 'Hannah', time() + 60 * 60 * 24 * 7, '/');
    if (isset($_COOKIE['username'])) $username = $_COOKIE['username'];
   	setcookie('username', 'Hannah', time() - 2592000, '/');//delete the cookie by set the time in the past
####PHP Authentication
	<?php
      $username = 'admin';
      $password = 'letmein';

      if (isset($_SERVER['PHP_AUTH_USER']) &&
          isset($_SERVER['PHP_AUTH_PW']))
      {
        if ($_SERVER['PHP_AUTH_USER'] == $username &&
            $_SERVER['PHP_AUTH_PW']   == $password)
              echo "You are now logged in";
        else die("Invalid username / password combination");
      }
      else
      {
        header('WWW-Authenticate: Basic realm="Restricted Section"');
        header('HTTP/1.0 401 Unauthorized');
        die ("Please enter your username and password");
      }
    ?>
####Storing username and password
	$token = hash('ripemd128', 'mypassword');/basic
    $token = hash('ripemd128', 'hqb%$tmypasswordcg*l');//more safer, ass we add some special string in password
##Session
	$_SESSION['variable'] = $value;
    $variable = $_SESSION['variable'];
    session_destroy();
    ini_set('session.gc_maxlifetime', 60 * 60 * 24);
####Session Regenerate
    session_start();
      if (!isset($_SESSION['initiated']))
      {
        session_regenerate_id();
        $_SESSION['initiated'] = 1;
      }
      if (!isset($_SESSION['count'])) $_SESSION['count'] = 0;
      else ++$_SESSION['count'];
      echo $_SESSION['count'];

	
	