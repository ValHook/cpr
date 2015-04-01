# C++ Requests: Curl for People [![Build Status](https://travis-ci.org/whoshuu/cpr.svg?branch=master)](https://travis-ci.org/whoshuu/cpr)

C++ Requests is a simple wrapper around libcurl inspired by the excellent [Python Requests](https://github.com/kennethreitz/requests) project.

Despite its name, libcurl's easy interface is anything but, and making mistakes misusing it is a common source of error and frustration. Using the more expressive language facilities of C++11, this library captures the essence of making network calls into a few concise idioms.

Here's a quick GET request:

```c++
#include <cpr.h>
#include <iostream>

int main(int argc,  char** argv) {
    auto r = cpr::Get(Url{"https://api.github.com/repos/whoshuu/cpr/contributors"},
                      Authentication{"user", "pass"},
                      Parameters{{"anon", "true"}, {"key", "value"}});
    r.status_code;                  // 200
    r.headers["content-type"];      // application/json; charset=utf-8
    r.text;                         // JSON text string
}
```

And here's [less functional, more complicated code, without cpr](https://gist.github.com/whoshuu/2dc858b8730079602044).

## Install

The easiest way to install is to use cmake:

```shell
mkdir build
cd build
cmake ..
make
```

By default, your system libcurl is used to build this library. If you want to use the embedded libcurl, then run:

```shell
cmake -DUSE_SYSTEM_CURL=OFF ..
make
```

A successful build should produce a single library archive that you can link against your project. You should also make the include directory visible to your build as well so that you can include `cpr.h`.

## Features

C++ Requests currently supports:

* Custom headers
* Url encoded parameters
* Url encoded POST values
* Basic authentication scheme
* Timeout specification

## Planned

Support for the following will be forthcoming (in rough order of implementation priority):

* Multipart form POST upload
* File POST upload
* :cookie: support!
* Digest authentication
* Asynchronous requests
* Proxy support

and much more!

## Disclaimer

This library is very much in a pre-alpha stage. Please don't attempt to use this in any serious or critical production environment. If you do use it and find bugs you'd like to report, see below!

## Contributing

Please fork this repository and contribute back using [pull requests](https://github.com/whoshuu/cpr/pulls). Features can be requested using [issues](https://github.com/whoshuu/cpr/issues). All code, comments, and critiques are greatly appreciated.