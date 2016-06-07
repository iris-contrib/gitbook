# Middleware

**Quick view**

```go
// First point to the static files
iris.Static("/assets", "./public/assets", 1)

// Then declare which middleware to use (custom or not)
iris.Use(myMiddleware)
iris.UseFunc(myFunc)

// Now declare routes
iris.Get("/myroute", func(c *iris.Context) {
    // do stuff
})
iris.Get("/secondroute", myMiddlewareFunc, myRouteHandlerfunc)

// Now run our server
iris.Listen(":8080")

```


Middleware in Iris is not complicated, they are similar to simple Handlers.
They implement the Handler interface as well:

```go
type Handler interface {
	Serve(*Context)
}
type Middleware []Handler
```

Handler middleware example:

```go

type myMiddleware struct {}

func (m *myMiddleware) Serve(c *iris.Context){
	shouldContinueToTheNextHandler := true

	if shouldContinueToTheNextHandler {
		c.Next()
	}else{
	    c.WriteText(403,"Forbidden !!")
	}

}

iris.Use(&myMiddleware{})

iris.Get("/home", func (c *iris.Context){
	c.WriteHTML(iris.StatusOK,"<h1>Hello from /home </h1>")
})

iris.Listen(":8080")
```

HandlerFunc middleware example:

```go

func myMiddleware(c *iris.Context){
	c.Next()
}

iris.UseFunc(myMiddleware)

```

HandlerFunc middleware for a specific route:

```go

func mySecondMiddleware(c *iris.Context){
	c.Next()
}

iris.Get("/dashboard", func(c *iris.Context) {
    loggedIn := true
    if loggedIn {
        c.Next()
    }
}, mySecondMiddleware, func (c *iris.Context){
    c.Write("The last HandlerFunc is the main handler, everything before that is middleware for this route /dashboard")
})

iris.Listen(":8080")

```

> Note that middleware must come before route declaration.


Make use of the built-in Iris [middleware](https://github.com/kataras/iris/tree/master/middleware), view practical [examples here](https://github.com/iris-contrib/examples)

```go
package main

import (
 "github.com/kataras/iris"
 "github.com/kataras/iris/middleware/logger"
)

type Page struct {
	Title string
}

iris.Config().Templates.Directory = "./yourpath/templates"

iris.Use(logger.DefaultHandler())

iris.Get("/", func(c *iris.Context) {
		c.Render("index.html", Page{"My Index Title"})
})

iris.Listen(":8080")
```
