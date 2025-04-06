---
title: OpenAPI integration
tags: ["go", "openapi", "swagger", "redoc"]
---

Today we will look at how you can serve, validate, and build api documentation using openapi, swagger and redoc. Although this tutorial for building bundles of openapi is language agnostic we are using go for serving the html files. Generally you can use any language for serving static file content 😄. Let's begin

!!! warning
    You will need nodejs, pnpm installed on system.

## Preparing and building openapi
---
- Create folder apidocs/docs using `mkdir -p apidocs/docs`
- Copy content from https://raw.githubusercontent.com/swagger-api/swagger-petstore/refs/heads/master/src/main/resources/openapi.yaml in `docs/oapi.yaml`
- Install redocly to build and lint `pnpm install @redocly/cli@latest`.
- Lint the file using command `node_modules/.bin/redocly lint docs/oapi.yaml`.
- Build the single api file using command `node_modules/.bin/redocly bundle docs/oapi/oapi.yaml -o docs/openapi.yaml`.

## Downloading and modifying swagger bundle
---
- Download the source code zip file from [swagger-ui project](https://github.com/swagger-api/swagger-ui/releases/)
![swagger-download-page](../assets/images/swagger-download-page.png)
- Unzip it and copy dist folder in `apidocs/docs` folder.
- Copy the built `apidocs/openapi.yaml` into `apidocs/docs/dist` folder.
- Rename some of attribute in dist folder js file to point to copied openapi.yaml file.
- Build the redocs using `node_modules/.bin/redocly build-docs $(OAPI_PATH) -o ./docs/redoc/index.html` this will build redocs index html in mentioned path

## Serving with golang
---
Below script is self explantory. We used embed package to embed index.html from redoc and Swagger bundle completely in our binary. You can also remove the generated files after binary done building.
```go
package main

import (
        "context"
        "embed"
        "errors"
        "log"
        "net/http"
        "os"
        "os/signal"
        "syscall"
        "time"
)

var (
        //go:embed docs/redoc
        redfs embed.FS
        //go:embed docs/swagger
        swagfs embed.FS
)

// We are embedding the filesystem into it directly
// so we won't need any files to be kept around other than binary
func main() {
    // graceful shutdown
    ctx, cancel := context.WithTimeout(context.Background(), 3*time.Minute)
    defer cancel()
    ch := make(chan os.Signal, 1)
    signal.Notify(ch, os.Interrupt, syscall.SIGINT, syscall.SIGTERM)
    // mux
    mux := http.NewServeMux()
    mux.Handle("/docs/swagger/", http.FileServer(http.FS(swagfs)))
    mux.Handle("/docs/redoc/", http.FileServer(http.FS(redfs)))
    srv := http.Server{
        Addr:    "127.0.0.1:3003",
        Handler: mux,
    }
    log.Printf("[INFO] server started on %s", srv.Addr)
    // start
    go func() {
        if err := srv.ListenAndServe(); err != nil {
            if errors.Is(err, http.ErrServerClosed) {
                log.Println("[INFO] http server closed")
                return
            }
            log.Printf("[ERROR] %v\n", err)
        }
    }()
    <-ch
    srv.Shutdown(ctx)
}
```
