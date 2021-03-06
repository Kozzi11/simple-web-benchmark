# Simple Web Benchmark

A simple web benchmark of Go, Rust, D, Scala and Node.js.

## Testing

The stats gathered by the [hey](https://github.com/rakyll/hey) tool (please run it twice for
the JIT optimizations where it's applicable):

    sh -c "$GOPATH/bin/hey -n 50000 -c 256 -t 10 'http://127.0.0.1:3000/'"
    sh -c "$GOPATH/bin/hey -n 50000 -c 256 -t 10 'http://127.0.0.1:3000/greeting/hello'"

### MacOS Note

By default, MacOS has low limits on the number of concurrent connections, so
few kernel parameters tweaks may be required:

    sudo sysctl -w kern.ipc.somaxconn=12000
    sudo sysctl -w kern.maxfilesperproc=1048576
    sudo sysctl -w kern.maxfiles=1148576

### Automation

Please use the Scala script
(using (sbt Script runner)[http://www.scala-sbt.org/1.x/docs/Scripts.html#sbt+Script+runner])
to run all the test automatically:

    ./run.scala <list of languages>

Please specify the required languages separated by space (* wildcard is supported for all).

### Preliminary Results

Hardware: MacBook Pro (CPU: 2.3 GHz Intel Core i7, Mem: 16 GB 1600 MHz DDR3)

Software: Go 1.9, Rust 1.20.0, Scala 2.12.3, Node.js 8.5.0, LDC 1.3.0.

![](results/mac.png?raw=true)

## Usage

Please change the required directory before running the server.

### Go

    go run main.go

### Rust

    cargo run --release

### D

Please use LLVM based [LDC](https://github.com/ldc-developers/ldc#installation)
compiler as DMD is a reference D compiler that provides only basic optimizations.
If ldc2 executable is not in path, please use the fully qualified path name.

    dub run --compiler=ldc2 --build=release

### Scala

    sbt run

### Node.js

    node main.js
