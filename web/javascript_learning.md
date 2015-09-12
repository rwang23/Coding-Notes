#Javascript Learning
```javascript


##Basic Idea

var o = new Object();
o.name ="john";
o.age=30;
o.salary=300;
for(var x in o){
	alert(x);//这个时候输出的是name age salary
	alert(o.x);//这个时候输出的是john 30 300
}

###Prototype
当写原型属性时，才在它自己内部产生实际的属性

组合原型和构造方法




***
###DOM：Document Object Model

##syntax



	array.length 得到数组变量数量

##Object
	Object.property
	Object.method()
	var xx = new Object;
	数组就是对象 Date也是对象

##DOM
	<p>这种就是 元素节点
	<p>里边的内容就是 文本节点
	<p>的style title等 就是属性节点

	document.getElementById("purchases")

	document.getElementById("myImage").src = "landscape.jpg";

	document.getElementById("p2").style.color = "blue";

	document.getElementById("myBtn").onclick = function(){displayDate()};

	`注意大小写，以及ID引入要加引号`
	object.getAttribute(attribute) attribute比如是title,href等
	object.setAttribute(attribute,value)
##Event
			document.getElementById("myBtn").addEventListener("click", displayDate);
	addEventListener(event, function, useCapture);

	The default useCapture is false, the bubbling
	In bubbling the inner most element's event is handled first
	In capturing the outer most element's event is handled

	element.removeEventListener("mousemove", myFunction);
###Event Example

	var x = document.getElementById("myBtn");

	if (x.addEventListener) {
    	x.addEventListener("click", myFunction);
	} else if (x.attachEvent) {
    	x.attachEvent("onclick", myFunction);
	} // for IE

	function myFunction() {
    	alert("Hello World!");
	}


###实现DOM
	function myFunction() {
    	var x = document.createElement("ADDRESS");
    	var t = document.createTextNode("Box 564, Disneyland, USA");
    	x.appendChild(t);
    	document.body.appendChild(x);
	}

	var myText = document.getElementById("intro").childNodes[0].nodeValue;
####DOM实现Example1
	<!DOCTYPE html>
	<html>
	<body>

	<div id="div1">
	<p id="p1">This is a paragraph.</p>
	<p id="p2">This is another paragraph.</p>
	</div>

	<script>
	var para = document.createElement("p");
	var node = document.createTextNode("This is new.");
	para.appendChild(node);
	var element = document.getElementById("div1");
	element.appendChild(para);
	//element.insertBefore(para,child);

	</script>

	</body>
	</html>
####DOM实现Example2
	<script>
	var parent = document.getElementById("div1");
	var child = document.getElementById("p1");
	parent.removeChild(child);
	//parent.replaceChild(para,child);
	</script>

###DOM操作函数
	document.getElementById()
	document.getElementsByTagName()
	document.getElementsByClassName()
	element.innerHTML=
	element.attribute=
	element.setAttribute(attribute,value)
	element.style.property

	document.createElement()
	document.removeChild()
	document.appendChild()
	document.replaceChild()
	document.write(text)

	document.getElementById(id).onclick=function(){code}

	document.anchors	Returns all <a> elements that have a name attribute
	document.body	Returns the <body> element
	document.cookie	Returns the document's cookie
	document.doctype	Returns the document's doctype
	document.forms	Returns all <form> elements
	document.images	Returns all <img> elements

	document.querySelectorAll("p.intro") 选择<p>下的intro class
***
##BOM
BOM Browser Object Model

	window.open() - open a new window
	window.close() - close the current window
	window.moveTo() -move the current window
	window.resizeTo() -resize the current window

	screen.width
	screen.height
	screen.availWidth
	screen.availHeight
	screen.colorDepth
	screen.pixelDepth

	window.location.href returns the href (URL) of the current page
	window.location.hostname returns the domain name of the web host
	window.location.pathname returns the path and filename of the current page
	window.location.protocol returns the web protocol used (http:// or https://)
	window.location.assign loads a new document
####Size
	var w = window.innerWidth
	|| document.documentElement.clientWidth //for IE	|| document.body.clientWidth; //another way for IE

	var h = window.innerHeight
	|| document.documentElement.clientHeight
	|| document.body.clientHeight;
####History
	function goBack() {
    window.history.back()
	}

	function goForward() {
    window.history.forward()//好像没用
}
***
##Cookie
	document.cookie="username=John Doe";
	document.cookie="username=John Doe; expires=Thu, 18 Dec 2013 12:00:00 UTC";
	document.cookie="username=John Doe; expires=Thu, 18 Dec 2013 12:00:00 UTC; path=/";
	var x = document.cookie;


***
##Datatype

	var cars = ["Saab", "Volvo", "BMW"];
	数组用的[]
	var person = {firstName:"John", lastName:"Doe", age:50, eyeColor:"blue"};
	Object用的 {}

	typeof variable得到数据类型
##Object
	var person = {
    	firstName:"John",
    	lastName:"Doe",
    	age:50,
    	eyeColor:"blue"
	};
	objectName.propertyName
	objectName[propertyName]
	objectName.methodName()

	objects cannot be compareds
	like: var x= new date();
		  var y= new date();
		  这俩不能比较

***
##Event
###Common Event Functions
	onchange:An HTML element has been changed
	onclick: The user clicks an HTML element
	onmouseover: The user moves the mouse over an HTML element
	onmouseout: The user moves the mouse away from an HTML element
	onkeydown: The user pushes a keyboard key
	onload: The browser has finished loading the page

	<button onclick='getElementById("demo").innerHTML=Date()'>The time is?</button>
	<button onclick="this.innerHTML=Date()">The time is?</button>

***


##Function
	setInterval("javascript function", milliseconds); //一直斤西瓜
	clearInterval() //中止setinterval
	setTimeout() 运行一次
	clearTimeout()
###Math
	Math.floor()
	Math.round()
	Math.ceil()
	Math.random()
	Math.min(x1,x2,x2)
	isNaN(x)
	parseFloat() Parses its argument and returns a floating point number
	parseInt() Parses its argument and returns an integer

	new Date(year, month, day, hours, minutes, seconds, milliseconds)
	The toUTCString() method converts a date to a UTC string (a date display standard).
	The toDateString() method converts a date to a more readable format:

###String
	The valueOf() method is the default behavior for an array. It returns an array as a string:
	For JavaScript arrays, valueOf() and toString() are equal.
	It behaves just like toString(), but you can specify the separator:

	The pop() method removes the last element from an array:
	The push() method returns the new array length.
	delete fruits[0];           // Changes the first element in fruits to undefined

      <script>
      words = fixNames("the", "DALLAS", "CowBoys")

      for (j = 0 ; j < words.length ; ++j)
        document.write(words[j] + "<br>")

      function fixNames()
      {
        var s = new Array()

        for (j = 0 ; j < fixNames.arguments.length ; ++j)
          s[j] = fixNames.arguments[j].charAt(0).toUpperCase() +
                 fixNames.arguments[j].substr(1).toLowerCase()

        return s
      }
    </script>







###Display
	Writing into an alert box, using window.alert().
	Writing into the HTML output using document.write().直接写在了屏幕上，替换了document
	Writing into an HTML element, using innerHTML.
	Writing into the browser console, using console.log().

***
##Error Handling
The `try` statement lets you test a block of code for errors.

The `catch` statement lets you handle the error.

The `throw` statement lets you create custom errors.

The `finally` statement lets you execute code, after try and catch, regardless of the result.

	try {
    	adddlert("Welcome guest!");
	}
	catch(err) {
    	document.getElementById("demo").innerHTML = err.message;
	}
###Error Example
	<!DOCTYPE html>
	<html>
	<body>

	<p>Please input a number between 5 and 10:</p>

	<input id="demo" type="text">
	<button type="button" onclick="myFunction()">Test Input</button>
	<p id="message"></p>

	<script>
	function myFunction() {
    	var message, x;
    	message = document.getElementById("message");
    	message.innerHTML = "";
    	x = document.getElementById("demo").value;
    	try {
        	if(x == "")  throw "empty";
        	if(isNaN(x)) throw "not a number";
        	x == Number(x);
        	if(x < 5)    throw "too low";
        	if(x > 10)   throw "too high";
    	}
    	catch(err) {
        	message.innerHTML = "Input is " + err;
    	}
    	finally {
        document.getElementById("demo").value = "";
    }
	}
	</script>
	</body>
	</html>
##Form Validation Example
	<!DOCTYPE html>
	<html>
	<body>

	<p>Enter a number and click OK:</p>

	<input id="id1" type="number" min="100" max="300">
	<button onclick="myFunction()">OK</button>
	<p>If the number is less than 100 or greater than 300, an error message will be displayed.</p>
	<p id="demo"></p>
	<script>
	function myFunction() {
    	var inpObj = document.getElementById("id1");
    	if (inpObj.checkValidity() == false) {
        	document.getElementById("demo").innerHTML = inpObj.validationMessage;
    	} else {
        	document.getElementById("demo").innerHTML = "Input OK";
    	}
	}
	</script>

	</body>
	</html>

***




