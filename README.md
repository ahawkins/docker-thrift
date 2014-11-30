# Thrift Docker Image

> The Apache Thrift software framework, for scalable cross-language
> services development, combines a software stack with a code generation
> engine to build services that work efficiently and seamlessly between
> C++, Java, Python, PHP, Ruby, Erlang, Perl, Haskell, C#, Cocoa,
> JavaScript, Node.js, Smalltalk, OCaml and Delphi and other languages.

Read more about [Thrift](https://thrift.apache.org).

# How To Use This Image

This is image is intended to run as an executable. Files are provided
by mounting a directory. Here's an example of compiling
`service.thrift` to ruby.

    docker run -v "$(pwd):/data" ahawkins/thrift --gen rb /data/service.thrift
