# Install

The only requirement is the [Go Programming Language](https://golang.org/dl), at least v1.7.

```sh
$ go get -u github.com/kataras/iris
```

this will update the dependencies also.

* If you are connected to the internet through **China**, according to [this](https://github.com/kataras/iris/issues/98), you might have problems installing Iris.   
  **Follow the below steps**:

1. [https:\/\/github.com\/northbright\/Notes\/blob\/master\/Golang\/china\/get-golang-packages-on-golang-org-in-china.md](https://github.com/northbright/Notes/blob/master/Golang/china/get-golang-packages-on-golang-org-in-china.md)

1. `$ go get github.com/kataras/iris` **without -u**

* If you have any problems installing Iris, just delete the directory `$GOPATH/src/github.com/kataras/iris` , open your shell and run `go get -u github.com/kataras/iris/iris` .




> NOTE: **If you want the fasthttp version of iris **, then install [v5](https://github.com/kataras/iris/tree/5.0.0) instead, its [examples](https://github.com/iris-contrib/examples/tree/5.0.0), [book](https://docs-v5.iris-go.com), [middleware](https://github.com/iris-contrib/middleware/tree/5.0.0) and [plugins](https://github.com/iris-contrib/plugin/tree/5.0.0) are expecting an import path of:
```
gopkg.in/kataras/iris.v5
```
