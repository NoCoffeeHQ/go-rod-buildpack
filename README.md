# go-rod buildpack

This is a very custom buildpack for installing Chromium required by the go-rod module. This prevents the download of the browser binary during the lifetime of the application.

## Usage

Follow the 3 steps:

1. Add the buildpacks in your `.buildpacks` file in your main Go project

```
https://github.com/Scalingo/apt-buildpack
https://github.com/Scalingo/go-buildpack.git
https://github.com/nocoffeehq/go-rod-buildpack.git
```

2. Create the Aptfile in your main Go project

```
libnss3 libxss1 libasound2 libxtst6 libgtk-3-0 libgbm1 ca-certificates fonts-liberation fonts-noto-color-emoji fonts-noto-cjk timezone tzdata process reaper dumb-init xvfb

https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
```

2. Add the following file in your main Go project

Filename: `./getbrowser/getbrowser.go`

```go
package main

import (
  "fmt"

  "github.com/go-rod/rod/lib/launcher"
  "github.com/go-rod/rod/lib/utils"
)

func main() {
  p, err := launcher.NewBrowser().Get()
  utils.E(err)

  fmt.Println(p)
}

```

3. Set the env variable

`GET_BROWSER_BIN_NAME=getbrowser`

Re-deploy your project and you should be good!