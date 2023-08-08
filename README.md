# go-rod Buildpack

This is a buildpack for installing Chromium required by the go-rod module. This prevents the download of the browser binary during the lifetime of the application.

## Installation

Add the buildpack in your `.buildpacks` file:

```
https://github.com/Scalingo/go-buildpack.git
https://github.com/Scalingo/java-buildpack.git
https://github.com/nocoffeehq/go-rod-buildpack.git
```