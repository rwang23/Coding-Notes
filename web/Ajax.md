#Ajax Learning
***
AJAX is about updating parts of a web page, without reloading the whole page.


###Basic Loading XML
	function loadXMLDoc()
	{
  	var xmlhttp;
  	if (window.XMLHttpRequest)
  	{// code for IE7+, Firefox, Chrome, Opera, Safari
    	xmlhttp=new XMLHttpRequest();
  	}
  	else
  	{// code for IE6, IE5
    	xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
  	}
  	xmlhttp.onreadystatechange=function()
  	{
    	if (xmlhttp.readyState==4 && xmlhttp.status==200)
    	{
      		document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
    }
  	}
  	xmlhttp.open("GET","ajax_info.txt",true);
  	xmlhttp.send();
	}

Holds the readyState of the XMLHttpRequest. Changes from 0 to 4: 

* 0: request not initialized 
* 1: server connection established
* 2: request received 
* 3: processing request
* 4: request finished and response is ready
* status 200: "OK" 404: Page not found



###Create an XMLHttp
	variable=new XMLHttpRequest();
	Old versions of Internet Explorer (IE5 and IE6) uses an ActiveX Object:
	variable=new ActiveXObject("Microsoft.XMLHTTP");
###Send Request To a Server
	xmlhttp.open("GET","ajax_info.txt",true);
	open(method,url,async)
	
	xmlhttp.send();
	send(string)
###Get??Post
	GET is simpler and faster than POST, and can be used in most cases.
	
	However, always use POST requests when:
	- A cached file is not an option (update a file or database on the server)
	- Sending a large amount of data to the server (POST has no size limitations)
	-Sending user input (which can contain unknown characters), POST is more robust and secure than GET
###Get Request
	xmlhttp.open("GET","demo_get.asp",true);
	xmlhttp.send();
	
	In the example above, you may get a cached result.
	To avoid this, add a unique ID to the URL:
	xmlhttp.open("GET","demo_get.asp?t=" + Math.random(),true);
	xmlhttp.send();
	
	If you want to send information with the GET method, add the information to the URL:

	xmlhttp.open("GET","demo_get2.asp?fname=Henry&lname=Ford",true);
	xmlhttp.send();
###Post Request
	xmlhttp.open("POST","demo_post.asp",true);
	xmlhttp.send();	
	
	xmlhttp.open("POST","ajax_test.asp",true);
	xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded");
	xmlhttp.send("fname=Henry&lname=Ford");