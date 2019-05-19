<html>

<head>

	<title>NinjaMan</title>

	<style type="text/css">

		* {

			margin: 0;

			padding: 0;

		}

		.row {

			line-height: 0;

		}

		.wall {

			background-color: blue;

			height: 40px; 

			width: 40px;

			display: inline-block;

		}

		.sushi {

			background-color: black;

			height: 40px; 

			width: 40px;

			display: inline-block;

			background-image: url('img/sushi.png');

			background-size: contain;

		}

		.onigiri {

			background-color: black;

			height: 40px; 

			width: 40px;

			display: inline-block;

			background-image: url('img/onigiri.png');

			background-size: contain;

		}

		.pumpky {

			background-color: black;

			height: 40px; 

			width: 40px;

			display: inline-block;

			background-image: url('img/pumpky.gif');

			background-size: contain;

		}

		.bluey {

			background-color: black;

			height: 40px; 

			width: 40px;

			display: inline-block;

			background-image: url('img/bluey.gif');

			background-size: contain;

		}

		.pinky {

			background-color: black;

			height: 40px; 

			width: 40px;

			display: inline-block;

			background-image: url('img/pinky.gif');

			background-size: contain;

		}

		.red {

			background-color: black;

			height: 40px; 

			width: 40px;

			display: inline-block;

			background-image: url('img/red.gif');

			background-size: contain;

		}

		.blank {

			background-color: black;

			height: 40px; 

			width: 40px;

			display: inline-block;

		}

		#ninjaman {

			background-color: black;

			height: 40px; 

			width: 40px;

			display: inline-block;

			background-image: url('img/ninja.gif');

			background-size: contain;

			position: absolute;

			left: 40px;

			top: 40px;

		}

	</style>

</head>

<body>

	<div id ='world'></div>

		<div id='ninjaman'></div>

		<div id="score">Score: </div>

		<div id='lives'>Lives Remaining: 3</div>

</body>

<script type="text/javascript">





	var world = [

		[1,1,0,2,1],

		[1,0,2,2,1],

		[1,2,1,3,1],

		[1,2,2,3,1],

		[1,0,2,2,1],

		[1,2,0,2,1],

		[1,3,1,2,1],

		[1,0,2,2,1],

		[1,2,1,2,0],

		[1,2,3,2,1],

		[1,2,1,0,1],

		[1,3,2,3,1],

		[1,3,2,3,1],

		[1,4,0,0,1],

		[1,1,5,0,1],

		[1,0,0,6,1],

		[1,7,0,1,1]

	];



function randomize(world) {

  var index = world.length;

  while (0 !== index) {

    var random = Math.floor(Math.random() * index);

    index -= 1; 

    

    var temp = world[index];

    world[index] = world[random];

    world[random] = temp;

  }

  return world;

}

	randomize(world)



	var worldDict = {

		0: 'blank',

		1: 'wall',

		2: 'sushi',

		3: 'onigiri',

		4: 'pinky',

		5: 'pumpky',

		6: 'bluey',

		7: 'red',

	}



	function drawWorld(){

		output = "";



		for(var row = 0; row < world.length; row++){

			output += "<div class = 'row'>"

			for(var x = 0; x < world[row].length; x++){

				output += "<div class = '" + worldDict[world[row][x]] +"'></div>"

		}

		output+="</div>"

	}



		document.getElementById('world').innerHTML = output;

			}

		drawWorld();



		var ninjaman = {

			x: 1,

			y: 1,

			score: 0,

			lives: 3

		}



		function drawNinjaman(){

			document.getElementById('ninjaman').style.top = ninjaman.y * 40 + 'px'

			document.getElementById('ninjaman').style.left = ninjaman.x * 40 + 'px'

		}

		drawNinjaman()



		document.onkeydown = function(e){

			if(e.keyCode == 37){

				if(world[ninjaman.y] [ninjaman.x - 1] != 1){

					ninjaman.x--;

				}

			}

			if(e.keyCode == 39){

				if(world[ninjaman.y] [ninjaman.x + 1] != 1){

					ninjaman.x++;

				}

			}

			if(e.keyCode == 38){

				if(world[ninjaman.y - 1] [ninjaman.x] != 1){

					ninjaman.y--;

				}

			}

			if(e.keyCode == 40){

				if(world[ninjaman.y + 1] [ninjaman.x] != 1){

					ninjaman.y++;

				}

			}

			

			if (world[ninjaman.y][ninjaman.x] == 2) {

				ninjaman.score += 10;

				}

			if (world[ninjaman.y][ninjaman.x] == 3) {

				ninjaman.score += 5;

				}

			if (world[ninjaman.y][ninjaman.x] == 3 || world[ninjaman.y][ninjaman.x] == 2) {

				world[ninjaman.y][ninjaman.x] = 0;

				}

			if (world[ninjaman.y][ninjaman.x] == 4 || world[ninjaman.y][ninjaman.x] == 5 || world[ninjaman.y][ninjaman.x] == 6 || world[ninjaman.y][ninjaman.x] == 7) {

				window.alert('Life Lost!');

				randomize(world);

				ninjaman.lives -= 1;

					if(ninjaman.lives == 0){

						window.alert('Game Over!');

						document.write("Final Score: " + ninjaman.score);

					}



				}



			drawNinjaman()

			drawWorld()

			document.getElementById("score").innerHTML = "Score: " + ninjaman.score;

			document.getElementById("lives").innerHTML = "Lives Remaining: " + ninjaman.lives;



		}



		// Basic Challenge:

		//keep score of how many sushis ninjaman eats (completed)

		// sushi = 10pts onigiri = 5



		//Intermediate Challenge:

		//Randomize world when loading page (completed)





		//Advanced Challenge:

		//Add ghosts that chase ninjaman around (incomplete, added ghosts but unable to come up with how to make them chase ninjaman)

		// Give ninjaman 3 lives where Game Over occurs when a ghost hits NinjaMan 3 times (completed)



</script>



</html>
