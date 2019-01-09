# migo [![Build Status](https://travis-ci.org/nickng/migo.svg?branch=master)](https://travis-ci.org/nickng/migo) [![GoDoc](https://godoc.org/github.com/nickng/migo?status.svg)](http://godoc.org/github.com/nickng/migo)

## `nickng/migo` is a MiGo Types library in Go.

MiGo (mini-go) calculus is a introduced in [this
paper](http://mrg.doc.ic.ac.uk/publications/fencing-off-go-liveness-and-safety-for-channel-based-programming/)
to capture core concurrency features of Go.

This library was designed to work with MiGo types, i.e. the types of
communication primitives in the MiGo calculus, where the values to be
sent/received are abstracted away, for static analysis and verification.

## Install

The package can be installed using `go get`:

    go get github.com/nickng/migo

## MiGo types

Syntax:

    identifier = [a-zA-Z0-9_.,#/]
    digit      = [0-9]
    program    = definition* ;
    definition = "def " identifier "(" param ")" ":" def-body ;
    param      =
               | params
               ;
    params     = identifier
               | params "," identifier
               ;
    def-body   = def-stmt+
               ;
    prefix     = "send" identifier
               | "recv" identifier
               | "tau"
               ;
    memprefix  = "read"  identifier
               | "write" identifier
               ;
    def-stmt   = "let" identifier = "newchan" identifier, digit+ ";"
               | prefix ";"
               | "letmem" identifier ";"
               | memprefix ";"
               | "close" identifier ";"
               | "call"  identifier "(" params ")" ";"
               | "spawn" identifier "(" params ")" ";"
               | "if" def-stmt+ "else" def-stmt+ "endif" ";"
               | "select" ( "case" prefix ";" def-stmt* )* "endselect" ";"
               ;

## Verification of MiGo

[Gong](https://github.com/nickng/gong) is a liveness and safety checker of MiGo
types. The tool accepts MiGo types format generated by this package.
