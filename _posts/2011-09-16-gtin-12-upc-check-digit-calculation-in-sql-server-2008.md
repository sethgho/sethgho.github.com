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

<pre class="prettyprint lang-sql">
CREATE FUNCTION dbo.CalculateBarcodeGTIN12CheckDigit(@input CHAR(11))
RETURNS INT
AS
BEGIN
DECLARE @evenDigitSum INT = 0
,@oddDigitSum INT = 0
,@i TINYINT = 0
,@result INT;
 
-- check if given Barcode is Numeric , if not return error status -1
IF(ISNUMERIC(@input) = 0
OR LEN(RTRIM(LTRIM(@input))) != 11)
RETURN -1
 
-- start the compute BarCode checksum algorithm
SET @i = 1
WHILE (@i <= 11)
BEGIN
--Add odd and even digits separately;
IF((@i % 2) = 0)
SET @evenDigitSum += CONVERT(TINYINT, SUBSTRING(@input,@i,1))
ELSE
SET @oddDigitSum += CONVERT(TINYINT, SUBSTRING(@input,@i,1))
SET @i += 1
END
 
--As per: http://en.wikipedia.org/wiki/Universal_Product_Code
--Multiply odd sum by 3, add to even sum, and mod 10.
SET @result = ((@oddDigitSum * 3) + @evenDigitSum) % 10;
IF(@result = 0)
RETURN 0
ELSE
RETURN 10 - @result;
 
RETURN -1
END
GO
</pre>

Scalar functions are killer, but I’ll only ever be using it for a single record.
