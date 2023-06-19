# 09.Understanding Event driven code execution

We need to know that even listeners such as `req.on('end')` won’t block the execution of the code, it instead lets the remaining code below it to execute, the compiler will internally set a process to wait for the chunks to come through from `req.on('end')` while the rest of the code is getting executed

```jsx
req.on('end', () => {
      const parsedBody = Buffer.concat(body).toString();
      const message = parsedBody.split('=')[1];
      fs.writeFileSync('message.txt', message);
	    res.statusCode = 302;
	    res.setHeader('Location', '/');
	    return res.end();
  });

  res.setHeader('Content-Type', 'text/html');
  res.write('<html>');
  res.write('<head><title>My First Page</title><head>');
  res.write('<body><h1>Hello from my Node.js Server!</h1></body>');
  res.write('</html>');
  res.end();
```

Here 

```jsx
req.on('end', () => {
      const parsedBody = Buffer.concat(body).toString();
      const message = parsedBody.split('=')[1];
      fs.writeFileSync('message.txt', message);
	    res.statusCode = 302;
	    res.setHeader('Location', '/');
	    return res.end();
  });
```

Will setup a listener, and wait till all the chunk come through before execution of the code inside this block, while

```jsx
 res.setHeader('Content-Type', 'text/html');
  res.write('<html>');
  res.write('<head><title>My First Page</title><head>');
  res.write('<body><h1>Hello from my Node.js Server!</h1></body>');
  res.write('</html>');
  res.end();
```

This starts getting executed while `res.on('end')` is waiting

This is done so that requests don’t take forever to process and instead runs parallely