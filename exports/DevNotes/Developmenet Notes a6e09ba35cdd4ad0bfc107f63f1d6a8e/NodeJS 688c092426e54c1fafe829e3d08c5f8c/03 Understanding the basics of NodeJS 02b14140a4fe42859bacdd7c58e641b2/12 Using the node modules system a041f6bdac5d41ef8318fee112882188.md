# 12.Using the node modules system

We can split our file into smaller modules to make it easier to maintain.

Let’s move the route handling logic to a seperate file called `routes.js`

```jsx
if (url === '/') {
    res.write('<html>');
    res.write('<head><title>Enter Message</title><head>');
    res.write(
      '<body><form action="/message" method="POST"><input type="text" name="message"><button type="submit">Send</button></form></body>'
    );
    res.write('</html>');
    return res.end();
  }
  if (url === '/message' && method === 'POST') {
    const body = [];
    req.on('data', chunk => {
      console.log(chunk);
      body.push(chunk);
    });
    return req.on('end', () => {
      const parsedBody = Buffer.concat(body).toString();
      const message = parsedBody.split('=')[1];
      fs.writeFile('message.txt', message, err => {
        res.statusCode = 302;
        res.setHeader('Location', '/');
        return res.end();
      });
    });
  }
  res.setHeader('Content-Type', 'text/html');
  res.write('<html>');
  res.write('<head><title>My First Page</title><head>');
  res.write('<body><h1>Hello from my Node.js Server!</h1></body>');
  res.write('</html>');
  res.end();
```

Now we need to add a function to handle these requests, we can do that by 

```jsx
const requestHandler = ((req,res)=>{/*routing logic here*/})
```

We then make export this code to make it usable from `app.js`

We do this by ending `routes.js` with

```jsx
exports.handler = requestHandler;
```

Now we need to import this in `app.js` which we do by

```jsx
const routes = require('./routes');
```

Then we pass in the requestHandler function into the http server

```jsx
const server = http.createServer(routes.handler);
```

And the server logic is split into modules effectively

[app.js](12%20Using%20the%20node%20modules%20system%20a041f6bdac5d41ef8318fee112882188/app%20js%2033b8375c17e34de28d447713eb9a1f23.md)

[routes.js](12%20Using%20the%20node%20modules%20system%20a041f6bdac5d41ef8318fee112882188/routes%20js%20493695363e2f49fda937269402f4d9d4.md)