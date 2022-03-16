<?php include('server.php'); ?>
<!DOCTYPE html>
<html>
<head>
	<title>User registration </title>
	<link rel="stylesheet" type="text/css" href="style.css">

	<script src="https://kit.fontawesome.com/11471afff0.js" crossorigin="anonymous"></script>


</head>
<body style="background-color: #1c87c9"> 

	<div class="header">
		<h2>Register Here</h2>
	</div>

	<form method="post" action="register.php">

		<?php include("errors.php"); ?>

		<div class="input-group">
			<label><i class="fa thin fa-user"></i> Username</label>
			<input type="text" placeholder="username" name="username" value="<?php echo $username; ?>">			
		</div>

		<div class="input-group">
			<label ><i class="fa thin fa-envelope-o"></i> Email</label>
			<input type="text" placeholder="rayza@gmail.com" name="email" value="<?php echo $email; ?>">			
		</div>

		<div class="input-group">
			<label><i class="fa thin fa-phone"></i> Phone number</label>
			<input type="text" placeholder="e.g 0761115501" name="phone">			
		</div>

		<div class="input-group">
			<label><i class="fa thin fa-lock"></i> Password</label>
			<input type="password" placeholder="password" name="password_1">			
		</div>

		<div class="input-group">
			<label><i class="fa thin fa-lock"></i> Confirm Password</label>
			<input type="password" placeholder="re-password" name="password_2">			
		</div>

		<div class="input-group">
			<button type="submit" name="register" class="btn">Register</button>		
		</div>
		<p>
			Already a member?<a href="login.php">Sign in</a>
		</p>
	</form>

</body>
</html>