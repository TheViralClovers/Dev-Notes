# 10.Blocking vs Non Blocking code

Instead of using `writeFileSync()` method we can use `writeFile()` This does not wait for the file to be created and data to be pushed before executing the rest of the code, instead we directly go to the next part

```jsx
return req.on('end', () => {
      const parsedBody = Buffer.concat(body).toString();
      const message = parsedBody.split('=')[1];
      fs.writeFile('message.txt', message, err => {
        res.statusCode = 302;
        res.setHeader('Location', '/');
        return res.end();
      });
    });
```

Here we added an event listener that executes after the message has been completely written (it perfomrs redirection to `/` in this case