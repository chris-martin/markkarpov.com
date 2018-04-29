---
title: Backpack tutorial
desc: Everything you should know about Backpack to make use of it
date:
  published: April 29, 2018
---

```toc
```

> Backpack is a proposal to add mixin libraries to Haskell. Mixin libraries
  can have signatures which permit implementations of values and types to be
  deferred, while allowing a library with missing implementations to still
  be type-checked.

This is a short tutorial that explains practical bits about backpack, so you
can read this and start hacking straight away. For a more complete
description see [this GHC proposal][ghc-proposal].

## Motivation

Motivation for Backpack is best described in the above-mentioned proposal.
For me though, Backpack is a reliable way to eliminate any unwanted
polymorphism and dictionary passing and so I consider it a tool for solving
that problem. If not the issues with performance I'd probably not bother to
learn about Backpack, but well, it's totally worth it.

## Signatures

Recall from the quote at the beginning of the tutorial:

> Mixin libraries can have signatures which permit implementations of values
  and types to be deferred

In practice this means that we have one more type of source file to addition
to `.hs` files: so called *signatures* which have extension `.hsig`.
Signatures are much like [hs-boot files](hs-boot).

```haskell
module MyKey where

type Key = ()
```

TODO
also mention here how to require instances of data types

definite vs indefinite libraries

## Instantiation of signatures

cabal tricks

```
library my-keys
  exposed-modules: MyKey
  build-depends: base

library
  build-depends: unpacked-containers, my-keys
  mixins: unpacked-containers (Set as MyKey.Set) requires (Key as MyKey)
```

Consider using a separate library for instantiation as well as modules from
the same library (need to check if this works at all).

## De

[ghc-proposal]: https://github.com/ezyang/ghc-proposals/blob/backpack/proposals/0000-backpack.rst
[hs-boot]: https://downloads.haskell.org/~ghc/latest/docs/html/users_guide/separate_compilation.html#how-to-compile-mutually-recursive-modules
