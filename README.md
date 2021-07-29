tabwriter
============

[![Build Status](https://github.com/jormin/tabwriter/workflows/test/badge.svg?branch=master)](https://github.com/jormin/tabwriter/actions?query=workflow%3Atest)
[![Codecov](https://codecov.io/gh/jormin/tabwriter/branch/master/graph/badge.svg)](https://codecov.io/gh/jormin/tabwriter)
[![GoDoc](https://godoc.org/github.com/jormin/tabwriter?status.svg)](http://godoc.org/github.com/jormin/tabwriter)
[![Go Report Card](https://goreportcard.com/badge/github.com/jormin/tabwriter)](https://goreportcard.com/report/github.com/jormin/tabwriter)

This is an extended version of [text/tabwriter](https://github.com/golang/go/blob/master/src/text/tabwriter/tabwriter.go).

Compared with the official version, it uses [mattn/go-runewidth](https://github.com/mattn/go-runewidth) to calculate the variable width of unicode characters to adds more support to most (but not all) Chinese/Japanese/Korean characters, emojis, "fullwidth" Latin characters, etc. 

Since the official version is already frozen，i create this extended version.

looking for more information with this issue [text/tabwriter: character width #8273](https://github.com/golang/go/issues/8273).

Usage
-----

```
go get github.com/jormin/tabwriter
```

Changes
-----

###### Official version

```
// Update the cell width.
func (b *Writer) updateWidth() {
	b.cell.width += utf8.RuneCount(b.buf[b.pos:])
	b.pos = len(b.buf)
}
```

###### This extended version

```
// Update the cell width.
func (b *Writer) updateWidth() {
	// b.cell.width += utf8.RuneCount(b.buf[b.pos:])
	b.cell.width += runewidth.StringWidth(string(b.buf[b.pos:]))
	b.pos = len(b.buf)
}
```

License
-------

under the [MIT](./LICENSE) License