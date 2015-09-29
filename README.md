# goapi
computes the exported API of a set of Go packages


## Install

```bash
$> go get github.com/vbatts/goapi
```

## Usage

```bash
$> goapi -h
Usage of goapi:
  -allow_new
        allow API additions (default true)
  -c string
        optional comma-separated filename(s) to check API against
  -contexts string
        optional comma-separated list of <goos>-<goarch>[-cgo] to override default contexts.
  -except string
        optional filename of packages that are allowed to change without triggering a failure in the tool
  -gopath
        include package names from GOPATH as well
  -next string
        optional filename of tentative upcoming API features for the next release. This file can be lazily maintained. It only affects the delta warnings from the -c file printed on success.
  -v    verbose debugging
$> goapi -gopath github.com/vbatts/tar-split/tar/asm > asm-api.txt
$> cat asm-api.txt
pkg github.com/vbatts/tar-split/tar/asm, const OptFileCheck = 1
pkg github.com/vbatts/tar-split/tar/asm, const OptFileCheck Options
pkg github.com/vbatts/tar-split/tar/asm, const OptSegment = 2
pkg github.com/vbatts/tar-split/tar/asm, const OptSegment Options
pkg github.com/vbatts/tar-split/tar/asm, const OptVerify = 4
pkg github.com/vbatts/tar-split/tar/asm, const OptVerify Options
pkg github.com/vbatts/tar-split/tar/asm, func NewInputTarStream(io.Reader, storage.Packer, storage.FilePutter) (io.Reader, error)
pkg github.com/vbatts/tar-split/tar/asm, func NewOutputTarStream(storage.FileGetter, storage.Unpacker) io.ReadCloser
pkg github.com/vbatts/tar-split/tar/asm, type Options int
pkg github.com/vbatts/tar-split/tar/asm, var DefaultInputOptions Options
pkg github.com/vbatts/tar-split/tar/asm, var DefaultOutputOptions Options
$> goapi -gopath -c asm-api.txt github.com/vbatts/tar-split/tar/asm
$> echo $?
0
```
