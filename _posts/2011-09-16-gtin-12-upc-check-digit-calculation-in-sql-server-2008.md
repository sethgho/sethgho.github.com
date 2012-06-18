---
layout: post
category: Coding
title: 'GTIN 12 UPC Check Digit Calculation in SQL Server 2008'
tags:
  - barcode
  - check-digit
  - sql
  - upc
comments: true
---

I recently needed to generate the check digit for a <a href="http://en.wikipedia.org/wiki/Universal_Product_Code">GTIN-12 UPC code</a> in SQL. The calculation method for the check digit varies depending on what kind of barcode you’re implementing, so I popped on over to Google to get the necessary algorithm. Naturally, and regardless of simplicity, I checked for any available code snippets. The only I found weren’t GTIN-12, and were in C or C++. So for anyone looking to do it (or something similar) in T-SQL, here’s a scalar function to do just that.

<script src="https://gist.github.com/c7a5dbba4d729c9adbf6.js"> </script>

Scalar functions are killer, but I’ll only ever be using it for a single record.
