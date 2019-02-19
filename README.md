# Thrift Docker Image

> The Apache Thrift software framework, for scalable cross-language
> services development, combines a software stack with a code generation
> engine to build services that work efficiently and seamlessly between
> C++, Java, Python, PHP, Ruby, Erlang, Perl, Haskell, C#, Cocoa,
> JavaScript, Node.js, Smalltalk, OCaml and Delphi and other languages.

Read more about [Thrift](https://thrift.apache.org).

# How To Use This Image

This image provides a linux-based thrift compiler for generating runtime code
from `.thrift` files.  Files are provided to the compiler by mounting
a directory into the container.  Here's an example of compiling 
`service.thrift` for Ruby:

    docker run --rm -v "$(pwd):/data" -w "/data" ahawkins/thrift thrift --gen rb service.thrift

This image does not provide any thrift runtime libraries.  To use
the generated code you will need to set up a language runtime environment
and install the thrift runtime for that language.  The best way to do this
is to create your own Dockerfile that starts with this image and then
add your own content.

For reference, the 
[Apache Thrift CI Dockerfile](https://github.com/apache/thrift/blob/master/build/docker/ubuntu-bionic/Dockerfile)
builds a docker container that contains runtime environments for all of the
languages that thrift supports.  That image is used when building Apache Thrift.

# For Windows Users

The thrift project provides a Docker for Windows based 
[Dockerfile](https://github.com/apache/thrift/tree/master/build/docker/msvc2017)
that can be used to build the thrift compiler on Windows.
