#HTML Skills
```html
***
###For Form
####autocomplete
	<form action='myform.php' method='post' autocomplete='on'>
		<input type='text' name='username'>
		<input type='password' name='password' autocomplete='off'>
	</form>
####autofocus
	<input type='text' name='query' autofocus='autofocus'>
####required attribute
	<input type='text' name='creditcard' required='required'>
####Override
	<form action='url1.php' method='post'>
		<input type='text' name='field'>
		<input type='submit' formaction='url2.php'>
	</form>
####min max step
	<input type='time' name='alarm' value='07:00' min='05:00' max='09:00'>
	<input type='time' name='meeting' value='12:00' min='09:00' max='16:00' step='3600'>
####color input
	 <input type='color' name='color'>


