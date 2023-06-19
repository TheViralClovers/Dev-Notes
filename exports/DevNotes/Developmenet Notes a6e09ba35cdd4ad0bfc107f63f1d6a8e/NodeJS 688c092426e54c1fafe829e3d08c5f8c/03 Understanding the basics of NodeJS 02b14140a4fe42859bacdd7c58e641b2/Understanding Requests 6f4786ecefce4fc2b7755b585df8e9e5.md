# Understanding Requests

We can understand the req incoming to the server by logging it to the console

```jsx
const server = http.createServer((req,res)=>{
	conosle.log(req.url,req.method,req.headers)
})
```

Here we log 3 parts of the req object to the console

**url** : stores the url from where the request originated

**method** : stores the method of request i.e GET,POST e.t.c

**headers** : Other parameters that are passed to indicate the type of content being sent 

![Untitled](Understanding%20Requests%206f4786ecefce4fc2b7755b585df8e9e5/Untitled.png)

/ → url

GET → method

{} → header object