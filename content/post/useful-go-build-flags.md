---
title: "Useful Go Build Flags"
date: 2018-05-15T15:53:10Z
description: A handy guide to a few of Go's build command line options.
twitter:
 image: https://lukeeckley.com/images/avatar@2x.jpg
---
## Go Link Documentation

It's all [here](https://golang.org/cmd/link). But what's the fun in just posting this link here.

## Setting a Go Variable at Build

A very handy build flag that allows you to set a variable from the command line at build time. Looks at the following example:

{{< highlight go >}}
package main

import (
    "fmt"
)

var who string

func main() {
    fmt.Printf("Hello, %s\n", who)
}
{{< /highlight >}}

Using the defaults we get the following results:

{{< highlight bash >}}
[me@localhost ~]$ go run main.go
Hello,
{{< /highlight >}}

By adding the `-X` linker flag we can change `who` at compile time. This is just a silly example but this could be useful for updating version information in the binary at compile time.

{{< highlight bash >}}
[me@localhost ~]$ go run -ldflags "-X main.who=Universe" main.go
Hello, Universe
{{< /highlight >}}

## Bonus Content

The symbol table can be viewed using the `go tool nm` command. Just pass it the name of the executable, object file or archive. Make it easy on yourself and just grep the output looking for your variable.

{{< highlight bash >}}
[me@localhost ~]$ go tool nm main | grep who
  5390f0 D main.who
{{< /highlight >}}

## Shrinking Your Go Binaries

In this day and age I don't really think it's neccessary to make our static go executables many order of magnatude smaller - but on some occasions it would be nice. For an example I wrote a program to save the Windows 10 Spotlight photos to a folder on the desktop. The size after a `go build` is `5,728,768 Bytes`. I know, that's not very large. But let's improve on it. The first thing is to strip the binary.

Build it without the flags for our reference point:

```
C:\Users\Luke\go\src\spotlight> go build

C:\Users\Luke\go\src\spotlight> dir
02/16/2018  01:52 PM         5,728,768 spotlight.exe
```

We can omit the symbol table, debug information and the DWARF table with the following flags: `-s -w`

Building it with the flags like so:
```
C:\Users\Luke\go\src\spotlight>go build -ldflags "-s -w" -o spotlight-s-w.exe

C:\Users\Luke\go\src\spotlight>dir
02/16/2018  03:29 PM         3,943,424 spotlight-s-w.exe
02/16/2018  01:52 PM         5,728,768 spotlight.exe
```
We already decreased the size by over 30%. Why stop there? One of the best executable packers available is [UPX](https://upx.github.io/). It is dead simple to use. I ran it with -9 to get the maximum compression at a cost of speed.
```
C:\Users\Luke\go\src\spotlight>upx -9 -o spotlight-s-w-upx.exe spotlight-s-w.exe
                       Ultimate Packer for eXecutables
                          Copyright (C) 1996 - 2017
UPX 3.94w       Markus Oberhumer, Laszlo Molnar & John Reiser   May 12th 2017

        File size         Ratio      Format      Name
   --------------------   ------   -----------   -----------
   3943424 ->   1275904   32.36%    win64/pe     spotlight-s-w-upx.exe

Packed 1 file.

C:\Users\Luke\go\src\spotlight>dir
02/16/2018  03:29 PM         1,275,904 spotlight-s-w-upx.exe
02/16/2018  03:29 PM         3,943,424 spotlight-s-w.exe
02/16/2018  01:52 PM         5,728,768 spotlight.exe
```
Wow. UPX gave us a binary that's only 32.36% the size of the stripped executable from go. The end result is a binary that is only 22.27% of the original size. That is incredible.

## Windows Executable Without Console Window

I find this unsightly to have a console window open when I run an exe and I don't need to see any output. I couldn't find this documented on any golang site. I can't remember where I found it, but it is good to know:

Just add `"-H=windowsgui"` to your linker flags. Console window gone. You're Welcome.

## Summary

So to sum up this article we could build our earlier `Hello, World` example with the following flags to incorporate everything we have learned:
```
C:\Users\Luke\go\src\hello>go build -ldflags "-X main.who=Universe -H=windowsgui -s -w"
```

