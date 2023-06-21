# 03.Handling different routes

We pass in the path as an argument to the middleware

```jsx
app.use("/",(req,res,next)=>{
	console.log("in a  middleware")
	res.send('<h1>Hello there</h1>')
}
```

Now whenever we visit `/` we will get that middleware to trigger(alose triggers for any middleware that is unhandled)

## Specificity

middlewares at the top will get executed first and won’t move to the next one, unless `next()` is used 

Example:- The paths `/add-product` and `/` will both be matched if `/add-product`  is visited

Whichever is placed higher will be executed

```jsx

app.use("/",(req,res,next)=>{
	console.log("Always executes")
	res.send('<h1>Hello there</h1>')
	next()
}

app.use("/add-product",(req,res,next)=>{
	console.log("in a  middleware")
	res.send('<h1>Hello there</h1>')
}

app.use("/",(req,res,next)=>{
	console.log("I wont be called")
	res.send('<h1>Hello there</h1>')
}
```