---
layout: post
title: 'Enterprise Library Sometimes Chops XML into 2033 Characters'
tags:
  - csharp
  - enterprise-library
  - sql
  - xml
category: Coding
comments: true

---

This morning I began what I thought would be an uneventful task in .NET: connect to one database, download as XML some rows from a table that have changed since a given time, then pass that XML to a stored procedure in another database so that the changes can be merged. Just two tables: one relatively small, the other just a 2-column relationship table for the first table. Here’s a contrived snippet to serve the same purpose:

The SQL:
<script src="https://gist.github.com/54ed9afcd6a310263fd1.js"></script>

The Code:
<script src="https://gist.github.com/51e8870440b56384686d.js"></script>

In my application, it was this second table that tripped me a bit. The first only had a few changed rows, so the XML was only 500-1000 characters. The second table generated a much longer XML string – 3864 characters long. My initial plan was to return two tables, each 1 column and 1 row. When using <a href="http://msdn.microsoft.com/en-us/library/microsoft.practices.enterpriselibrary.data.database.executedataset(v=pandp.31).aspx" target="_blank">Database.ExecuteDataSet</a> to fetch the results, however, the second table yielded two rows. I backtracked, second guessed myself, and even grabbed a couple of guys in the hall to double check my code. No one could explain it. It seemed odd that this hasn’t come up before for someone here. I did a bit of Googling and only found a couple of results. This <a href="http://support.microsoft.com/kb/310378" target="_blank">Microsoft Knowledgebase Article</a> just says it’s “by design” and to use <a href="http://msdn.microsoft.com/en-us/library/system.data.sqlclient.sqlcommand.executexmlreader(v=vs.71).aspx" target="_blank">SQLCommand.ExecuteXmlReader</a>.

The next question that came up was “Well, what does it do if I return a long XML value among other values in the same row?” I tested this out and everything worked as expected. All of the XML was in a single column value as it should be.

I still can’t exactly explain it. <a href="http://msdn.microsoft.com/en-us/library/microsoft.practices.enterpriselibrary.data.database.executescalar(v=pandp.31).aspx" target="_blank">ExecuteScalar</a> has a character limit of 2033 characters. I suspect that because each table in my result set is just a single column value, something somewhere is relying on ExecuteScalar.

My solution? In my stored procedure I just stored each of my table results as an XML typed variable, then returned the two together in the same row.
