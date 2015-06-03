#JQuery Learning
	$(document).ready(function(){
    	$("p").click(function(){
        	$(this).hide();
    	});
	});

The $(document).ready() method allows us to execute a function when the document is fully loaded.
##Basic Syntax
	$(this).hide() - hides the current element.
	$("p").hide() - hides all <p> elements.
	$(".test").hide() - hides all elements with class="test".
	$("#test").hide() - hides the element with id="test".
##DOM Events
	click
	dbclick
	mouseenter
	mouseleave
	hover
	keypress
	keydown
	keyup
	submit
	change
	focus
	blur
	load 
	resize
	scroll
	unload
	
	$("input").focus(function(){
    	$(this).css("background-color", "#cccccc");
	});
	
	$("p").on("click", function(){
    	$(this).hide();
	});
##Effects
###Hide/Show
	$("#hide").click(function(){
    	$("p").hide();
	});

	$("#show").click(function(){
    	$("p").show();
	});
###Fade/Slide/animate/
	fadeIn()
	fadeOut()
	fadeToggle()
	fadeTo()		
	
	slideDown() //css中 display:none
	slideUp()
	slideToggle()
	stop()
	
	$(selector).animate({params},speed,callback);
	
	$("button").click(function(){
    	$("div").animate({
        	height: 'toggle'
    	});
	}); 
###Chain
	$("#p1").css("color", "red").slideUp(2000).slideDown(2000);
###JQery HTML
####Get Content
	$("#btn1").click(function(){
    	alert("Text: " + $("#test").text());
	});
	$("#btn2").click(function(){
    	alert("HTML: " + $("#test").html());
	});
####Set Content
	$("#btn1").click(function(){
    	$("#test1").text("Hello world!");
	});
	$("#btn2").click(function(){
    	$("#test2").html("<b>Hello world!</b>");
	});
	$("#btn3").click(function(){
    	$("#test3").val("Dolly Duck");
	});
####Add Content
	$("p").append("Some appended text.");
	$("p").prepend("Some prepended text.");
	$("p").append(txt1, txt2, txt3);         // Append the new elements 
	The jQuery after() method inserts content AFTER the selected HTML elements.
	The jQuery before() method inserts content BEFORE the selected HTML elements.
	$("img").after("Some text after");
	$("img").before("Some text before");
####Remove Content	
	$("#div1").remove();
	$("#div1").empty();
	$("p").remove(".test");
####CSS Class
	$("button").click(function(){
    	$("h1, h2, p").addClass("blue");
    	$("div").addClass("important");
	});	
	
	$("button").click(function(){
    	$("h1, h2, p").removeClass("blue");
	});
	
	$("button").click(function(){
   		$("h1, h2, p").toggleClass("blue");
	});
	
	$("p").css("background-color", "yellow");
	$("p").css({"background-color": "yellow", "font-size": "200%"});
	
	$("#div1").innerWidth()
	$("#div1").outerWidth()
###jQuery Traversing
	 $("span").parent().css({"background-color": "yellow", "font-size": "200%"});
	 $("div").children();
	 $("h2").siblings();
	 $("div p").first();
	 
	 $(document).ready(function(){
    	$("span").parentsUntil("div");
	}); //returns all ancestor elements between two given arguments.
###jQuery Ajax
	 $("#div1").load("demo_test.txt");
	 $("#div1").load("demo_test.txt #p1");
	 
	 $("button").click(function(){
     $("#div1").load("demo_test.txt", 		function(responseTxt, statusTxt, xhr){
        if(statusTxt == "success")
            alert("External content loaded successfully!");
        if(statusTxt == "error")
            alert("Error: " + xhr.status + ": " + xhr.statusText);
    });
	});
####GET POST
	$("button").click(function(){
    $.get("demo_test.asp", function(data, status){
        alert("Data: " + data + "\nStatus: " + status);
    });
	});
	
	$("button").click(function(){
    $.post("demo_test_post.asp",
    {
        name: "Donald Duck",
        city: "Duckburg"
    },
    function(data, status){
        alert("Data: " + data + "\nStatus: " + status);
    });
	});

	
	
	
	