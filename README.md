# Build
1. Install [Golang](https://golang.org/dl/) (tested against 1.7 versions), set GOPATH:

 ```bash
GOPATH="${HOME}/go/"
```

2. Get source code for Go Tapdance and all dependencies:

 ```bash
go get github.com/SergeyFrolov/gotapdance github.com/Sirupsen/logrus \
           github.com/agl/ed25519/extra25519 github.com/zmap/zcrypto/x509 \
           github.com/zmap/zcrypto/tls golang.org/x/crypto/curve25519 \
           golang.org/x/mobile/cmd/gomobile  
```

3. There are 3 versions of TapDance client:

  * [Command Line Interface](cli)

  * Mobile: native applications in Java/Objective C for Android or iOS. Golang bindings are used as a shared library.

    * [Android application in Java](android)
    
    * iOS version: coming ~~soon~~ eventually

    * [Golang Bindings](proxybind)

  * [Pure Golang cross-platform GUI](gui) – ugly, not maintaed, lives as PoC. This code compiles virtually everywhere (tested on Ubuntu and Android, but supposed to work on iOS and Windows PC as well)

# Usage
After one of the above clients is built and launched, it will start listening for requests on port 10500.
Thus, you will need to ask your particular application(e.g. browser) to proxy connection via 127.0.0.1:10500.

1. In firefox (both mobile and desktop) I prefer to type ```about:config``` into address line and set the following:

 ```
network.proxy.http_port = 10500
network.proxy.http = 127.0.0.1
network.proxy.ssl_port = 10500
network.proxy.ssl = 127.0.0.1
network.proxy.type = 1
```

 To disable proxying you may simply set ```network.proxy.type``` back to ```5``` or ```0```.

 The same settings are available somewhere in GUI.

2. Some utilities use following enivoronment variables: 

 ```bash
export https_proxy=127.0.0.1:10500
export http_proxy=127.0.0.1:10500
wget https://twitter.com
```
Most of the popular utilities also have a flag to specify a proxy.

3. Coming soon: tunneling of the whole device for Android.
