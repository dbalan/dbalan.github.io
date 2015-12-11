---
layout: post
title: "Recursion"
date: 2015-08-22 00:28
comments: true
categories:
- haskell
- recursion
- fibonacci numbers
---

```haskell
fibonacci :: [Integer]
fibonacci = 1:1:(zipWith (+) fibonacci (tail fibonacci))
```

Above is a simple function that generates an infinite stream of fibonacci numbers. Its written in haskell.

This is a piece of code that made me think a lot lately, it make clever use of recursion to define the stream and computes with a linear number of additions. I think its pretty damn sexy!

## Notes:
- Many thanks to a co-worker who helped me figure this out.
- I hear that there are more efficient ways to compute fibonacci numbers (namley O(logn)). - should investigate this
