// <!-- # **Instructions**

// * Using the previous example as a guide, create an app that has two web servers.
// * One that listens on port 7000 and one that listens on port 7500.
// * The one listening on port 7000 will always tell the user something good about themselves.
// * The one listening on 7500 will always tell the user something bad about themselves.
// * Make sure you create a Github repo and commit this code!

// **Bonus**

// * Look for other ways to expand what your server can do. As possibilities:
//   * Generate the good/bad phrase randomly from a list of predefined phrases
//   * Use the `twitter` package inside the response to also return a random tweet

//  -->
var http = require("http");

var PORTOne = 7000;
var PORTTwo = 7500;

// Create a generic function to handle requests and responses
function handleRequest(request, response) {

  // Send the below string to the client when the user visits the PORT URL
  response.end("It Works!! Path Hit: " + request.url);
}

function good(request, response){
	response.end(randomCompliment())
}

function bad(request, response) {
	response.end(randomInsults())
}

function randomInsults (){
	var insults = [
	"You look awful today", 
	"Hope you drop your lunch", 
	"Looks like someone hit you with the ugly bus"]
	var randomizer = insults[Math.floor(Math.random() * insults.length)];
	return randomizer;
}

function randomCompliment(){
	var compliment = [
	"Nice hat",
	"You look like a person today",
	"You put your shoes on the right sides today"]
	var randomizer = compliment[Math.floor(Math.random() * compliment.length)];
	return randomizer;
}

var server1 = http.createServer(good)

var server2 = http.createServer(bad)

server1.listen(PORTOne, function() {

  // Log (server-side) when our server has started
  console.log("Server listening on: http://localhost:" + PORTOne);
});

server2.listen(PORTTwo, function() {

  // Log (server-side) when our server has started
  console.log("Server listening on: http://localhost:" + PORTTwo);
})