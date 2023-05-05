<!DOCTYPE html>
<html>
<head>
	<title>Move an <a> element vertically with CSS</title>
	<style>


#target_website {
			position:absolute;
			width:100%;
			height:100%;
			z-index:2;
			opacity:0.40001;
			z-index:1;
}

#aaa {
	position:absolute;
	padding-left: 450px;
	padding-top:525px;
	z-index:10;
}


	</style>
</head>
<body>



<iframe id="target_website" src="site.html"></iframe>

<a href="#" id="aaa" onclick="alert(1)">click</a>

</body>
</html>
