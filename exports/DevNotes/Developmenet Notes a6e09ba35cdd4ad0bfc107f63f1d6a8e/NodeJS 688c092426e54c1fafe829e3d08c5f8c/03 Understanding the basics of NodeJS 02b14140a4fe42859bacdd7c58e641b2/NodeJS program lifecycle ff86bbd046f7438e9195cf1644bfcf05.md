# NodeJS program lifecycle

![Untitled](NodeJS%20program%20lifecycle%20ff86bbd046f7438e9195cf1644bfcf05/Untitled.png)

Once we run the command `node app.js` in our terminal , the script is started, which parses code, registers variables and fucntions.

This creates something known as an event loop, here it is a single threaded loop that keeps running as long as we dont use a `process.exit()` method in our server

This event loop, takes in incoming requests and processes them

```jsx
const server = http.createServer((req,res)=>{
	conosle.log(req)
	process.exit() //for a hard exit
})
```

Server terminates in this scenario (program exits from temrinal instead of being in a loop)