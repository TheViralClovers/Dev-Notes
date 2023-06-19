# Redirecting Requests

Here we redirect a user from one URL to another

```jsx
const http = require('http');
const fs = require('fs');

const server = http.createServer((req, res) => {
  const url = req.url;
  const method = req.method;
  if (url === '/') {
    res.write('<html>');
    res.write('<head><title>Enter Message</title><head>');
    res.write('<body><form action="/message" method="POST"><input type="text" name="message"><button type="submit">Send</button></form></body>');
    res.write('</html>');
    return res.end();
  }
  if (url === '/message' && method === 'POST') {
    fs.writeFileSync('message.txt', 'DUMMY');
    res.statusCode = 302;
    res.setHeader('Location', '/');
    return res.end();
  }
  res.setHeader('Content-Type', 'text/html');
  res.write('<html>');
  res.write('<head><title>My First Page</title><head>');
  res.write('<body><h1>Hello from my Node.js Server!</h1></body>');
  res.write('</html>');
  res.end();
});

server.listen(3000);
```

In this case, we are redirecting a user from [localhost](http://localhost):3000/message back to localhost:3000 and we also write output to a file `’DUMMY’` in this case to `message.txt` file

We use `302` to indicate redirection, and we set the header to the place we want to be redirected to after writing the file

```jsx
 if (url === '/message' && method === 'POST') {
    fs.writeFileSync('message.txt', 'DUMMY');
    res.statusCode = 302;
    res.setHeader('Location', '/');
    return res.end();
  }
```

[app.js](Redirecting%20Requests%207f0cf4059cf9424492260571b635d8ad/app%20js%2090f524625d6747fc8218624762446f2e.md)