<?php

if (empty($_POST{"name"})){
    die("Name is required");
}

if(! filter_var($_POST{"email"},ILTER_VALIDATE_EMAIL)){
   die("Valid email is Required");
   }
   
   if(strlen($_POST{"password"})< 8){
     die("Passwprdmust be at least 8 charters");
   }
     




if (! preg_match("/[a-z}/i", $_POST["password"]){
  die("Password must contain at least one letter");
  }

if (! preg_match("/[0-9}/i", $_POST["password"]){
  die("Password must contain at least one number");
}
     
   $password_hash = password_Hash($_POST["password"], PASSWORD_DEFAULT);
   
$mysqli = require _DIR_."/database.php";
     
$sql ="INSERT INTO users (name, email, password_hash)
       VALUES(?, ?, ?)";

$stmt = $mysqli->stmt_init();

if (! $stmt->prepare($sql)){
    die("SQL error:".$mysqli->error);
}

$stmt->bind_param("sss",
                  $_POST["name"]
                  $_POST["email"]
                  $password_hash);

$stmt->execute();

echo"Signup sucessful";

     print_r($_POST);
     var_dump($password_hash);

?>
