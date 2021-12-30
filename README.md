# zlib build package

[![build](https://github.com/mattnite/zig-zlib/actions/workflows/build.yml/badge.svg)](https://github.com/mattnite/zig-zlib/actions/workflows/build.yml)

## Like this project?

do some self promotion here

## How to use

This repo contains code for your `build.zig` that can statically compile zlib, as well as some idiomatic Zig bindings for zlib that you can use in your application.

### Link and add bindings to your application

In order to statically link zlib into your application and access the bindings with a configurable import string:

```zig
const zlib = @import("path/to/zlib.zig");

pub fn build(b: *std.build.Builder) void {
    ...

    const lib = zlib.create(b, target, mode, .{
        .import_str = "zlib",
    });

    const exe = b.addExecutable("my-program", "src/main.zig");
    lib.link(exe);
}
```

Now code that is part of the `my-program` executable can import the zlib bindings with `@import("zlib")`.

### Only link to your application

In order to just link to the application, all you need to do is omit the `.import_str` argument to zlib's create options:

```zig
    const lib = zlib.create(b, target, mode, .{});
```