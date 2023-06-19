# Routing Requests

If we want custom content to be printed in each url route, we can do so by setting them up in the server like this

```jsx
const server = http.createServer((req,res)=>{
	const url = req.url
	if(url=='/') {
		res.write('<html>')
		res.write('<head><title>Enter Message </title><head>')
		res.write('<body><form action = "/message" method="POST"><input type="text" name ="message"><button type="submit">Send</button></form></body>')
		res.write('</html>')
		return res.end()
	}
	res.setHeader('Content-Type','text/html')
	res.write('<html>')
	res.write('<head><title>My First Page</title><head>')
	res.write('<body><h1>Hello from my NodeJS Server!</h1></body>')
	res.write('</html>')
	res.end();
})
	

```

Here if we visit [localhost:3000](http://localhost:3000) we get a form , and once we submit the form, we will be redirected to /message which will display the ‘hello from NodeJS Server’

Notice that we are returning from the function after `res.end()` because we don’t want to go to the next lines