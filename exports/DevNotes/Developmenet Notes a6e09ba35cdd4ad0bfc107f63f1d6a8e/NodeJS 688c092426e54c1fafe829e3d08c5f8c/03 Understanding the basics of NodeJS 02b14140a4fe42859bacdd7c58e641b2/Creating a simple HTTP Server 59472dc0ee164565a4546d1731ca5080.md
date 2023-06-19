# Creating a simple HTTP Server

For this we will be using the http module inside an ‘app.js’ file, use `node app.js` to run the server in the terminal

First we import the module

```jsx
const http = require('http')
```

Now we call the method createServer()

```jsx
http.createServer()
```

This takes in a listener function as an argument, a listener function basically looks like this

```jsx
fucntion rqListener(req,res){}//Here we take in the incoming request, and the server response as arguments 
```

We can turn this into an anonymous arrow fucntion and pass it directly like this

```jsx
http.createServer((req,res)=>{
	conosle.log(req)
})
```

Now to listen for incoming requests, we need to call the listen method on the above fucntion after declaring it to a constant ‘server’ like this

```jsx
const server = http.createServer((req,res)=>{
	conosle.log(req)
})
```

Now call the listen() method and pass in the port number(optional) and it will starte a server in [localhost](http://localhost) by default, for this example lets go with 3000

```jsx
server.listen(3000)
```

visiting [localhost:3000](http://localhost:3000) will log the request to the console