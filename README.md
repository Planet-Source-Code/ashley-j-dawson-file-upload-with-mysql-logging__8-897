<div align="center">

## File upload with MySQL logging


</div>

### Description

This code lets you browse your local drives for files to upload. You then enter a title for the file. The code uploads the file to a directory on your server and logs the file name and title on a MySQL Database.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Ashley J Dawson](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/ashley-j-dawson.md)
**Level**          |Beginner
**User Rating**    |4.0 (20 globes from 5 users)
**Compatibility**  |PHP 3\.0, PHP 4\.0
**Category**       |[Files](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/files__8-2.md)
**World**          |[PHP](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/php.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/ashley-j-dawson-file-upload-with-mysql-logging__8-897/archive/master.zip)

### API Declarations

Copyrighted 2003 retryx.com web design. All rights reserved.


### Source Code

```
<html>
<head>
<title>Upload and log Files To Server</title>
</head>
<body>
<!-- Retryx.com web design. All code copyright 2003 by retryx design.  -->
<!-- All right reserved. For more info please e-mail: info@retryx.com  -->
<!-- Requires PHP and MySQL on host server.        -->
<!-- PHP code to upload files to a directory on your host server and  -->
<!-- log the file name and title in a MySQL database.      -->
<!-- MySQL requires a table with the following fields:      -->
<!-- field: id   type: INT not_null, auto_increment, primary -->
<!-- field: title  type: TEXT not_null        -->
<!-- field: filename type: TEXT not_null        -->
<!-- PHP code start -->
<?
//***********************************
//***********************************
//Upload directory path (absolute)
$uploadpath = "/full/directory/path/to/upload/file";
//***********************************
//***********************************
//Define Functions
function upload($filename, $filename_name, $uploadpath, $title){
	//***********************************
	//***********************************
	//MySQL Information
	//Database name
	$dbname  = "databaseName";
	//MySQL Login information
	$dbhost  = "localhost";
	$dbusername = "username";
	$dbpassword = "password";
 //Database table name
 $dbtable = "tableName";
	//***********************************
	//***********************************
	//** Edit nothing below this point (except form function, for it's style!) **
 copy($filename,$uploadpath."/".$filename_name);
	$database = mysql_connect($dbhost, $dbusername, $dbpassword) or die ("ERROR Cant connect to MySQL");
	mysql_select_db($dbname, $database) or die("ERROR Cant connect to database");
	$query = "INSERT INTO " . $dbtable . " (id, title, filename) VALUES (NULL,'$title','$filename_name')";
 mysql_query($query);
	mysql_close($database);
	echo "$title";
	echo "<p>Has been Uploaded!</p>";
	//Change "index.php" to whatever you call this page
	echo "<a href=\"index.php\">Upload another file?</a>";
	}
//*******************************************************
//Form function, change the style of this if you need to!
function form(){?>
<form name= "form1"form method="post"action="<?=$_SERVER['PHP_SELF']?>"enctype="multipart/form-data">
 <p>
 <input type="file" name="filename"></p><p>
 <input type="text" name="title">
 	<strong>Title</strong></p><p>
 <input name="Submit" type="submit" id="Submit" value="Upload">
 <input type="hidden" name="formaction" value="uploadNow">
	<input name="reset" type="reset" id="reset" value="Clear">
</p>
</form><? }
//*******************************************************
//End Functions
switch ($formaction){
	default:
		form();
		break;
	case "uploadNow":
		if ($filename=="none") {
			echo("*** No information given! ***");}
		else{
			upload($filename, $filename_name, $uploadpath, $title);
	 		break;}
	break;
}
//End of upload script
?>
<!-- PHP code End -->
</body>
</html>
```

