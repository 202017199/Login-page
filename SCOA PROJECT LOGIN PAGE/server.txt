<?php 

	session_start();

	$username = "";
	$email ="";
	$errors = array();

//We connect the database here 

$db = mysqli_connect('localhost','root','','registration');
//if the register button is clicked

if (isset($_POST['register'])) {
	
	$username = mysqli_real_escape_string($db,$_POST['username']);
	$email = mysqli_real_escape_string($db,$_POST['email']);
	$phone = mysqli_real_escape_string($db,$_POST['phone']);
	$password_1 = mysqli_real_escape_string($db,$_POST['password_1']);
	$password_2 = mysqli_real_escape_string($db,$_POST['password_2']);

	//make sure all filled are filled

	if (empty($username)) {
		array_push($errors, "Username is required");
	}

	if (empty($email)) {
		array_push($errors, "Email is required");
	}

	if (empty($phone)) {
		array_push($errors, "Phone number is required");
	}

	if (empty($password_1)) {
		array_push($errors, "Password is required");
	}

	if ($password_1 != $password_2) {
		array_push($errors, "The two passwords do not match");
	}

	//if the is no error

	if (count($errors)==0) {

		$password=md5($password_1) ; //encrypt the data before storing in DB

		$sql = "INSERT INTO user (username,email,phone,password) VALUES ('$username','$email','$phone','$password')";
		mysqli_query($db,$sql);

		$_SESSION['username'] = $username;
		$_SESSION['success'] = "You logged in now ";
		header('location: index.php');
	}

}

if (isset($_POST['login'])) {
	
	$username = mysqli_real_escape_string($db,$_POST['username']);

	$password = mysqli_real_escape_string($db,$_POST['password']);
	

	//make sure all filled are filled

	if (empty($username)) {
		array_push($errors, "Username is required");
	}

	if (empty($password)) {
		array_push($errors, "Password is required");
	}

	if (count($errors)==0) {
		$password = md5($password);
		$query="SELECT * FROM user WHERE username='$username' AND password = '$password' ";
		$result = mysqli_query($db,$query);

		//$query1="SELECT * FROM subjects WHERE username='$username' AND password = '$password' ";
		//$result2 = mysqli_query($db,$query1);

		if (mysqli_num_rows($result)==1) {
			//login user

		$_SESSION['username'] = $username;
		$_SESSION['success'] = "You logged in now ";
		header('location: index.php');
		}else{
			
			array_push($errors,"Wrong username/password");
			header('location: login.php');
		}
	}
}

//logout
if (isset($_GET['logout'])) {
	session_destroy();
	unset($_SESSION['username']);
	header('location: login.php'); 
}

?>