---
layout: post
title: 'XML Shredding In SQL Is A Recipe For Arthritis'
category: Coding
tags:
  - xml
  - sql
  - csharp
comments: true
---

At work I've been spending a lot of time the past couple of weeks doing the same thing: serialize the records in a table as XML, pass it up to the client, then back down to another database to be deserialized and merged. It's nothing fancy, but it's certainly tedious. It's generally been a pattern of:

Generate the XML: (easy)
<pre class="prettyprint lang-sql">
SELECT
  Column1,
  Column2,
  Column3,
  Column4,
  Column5
FROM FooTable Foo
FOR XML AUTO, ROOT(&apos;Root&apos;)
</pre>

To create something like this:
<div class="well">&lt;Root&gt;
&lt;Foo Column1="Value1" Column2="Value2" Column3="Value3" Column4="Value4" Column5="Value5" /&gt;
&lt;/Root&gt;</div>
But having to type this out has been the arthritic step. For larger tables, this can take a while.

<pre class="prettyprint lang-sql">
SELECT
    a.value(&apos;@Column1&apos;, &apos;varchar(20)&apos;) Column1,
    a.value(&apos;@Column2&apos;, &apos;varchar(20)&apos;) Column2,
    a.value(&apos;@Column3&apos;, &apos;varchar(20)&apos;) Column3,
    a.value(&apos;@Column4&apos;, &apos;varchar(20)&apos;) Column4,
    a.value(&apos;@Column5&apos;, &apos;varchar(20)&apos;) Column5
FROM
    @XmlValue.nodes(&apos;/Root/Foo&apos;) T(a)
</pre>
I know of nothing to automatically generate something like this, and yesterday I decided enough is enough (after coming to a table that was 65 columns wide). I wanted a way to quickly write the SELECT clause of something like this for me. Quick and easy was important, because if it were a chore to use I'd likely just write it out, grumbling the whole time.

The table definition is easy to generate via Management Studio. Right Click the window &gt; Script Table As &gt; Create To &gt; New Query Window and you get something like:
<pre class="prettyprint lang-sql">
CREATE TABLE [dbo].[FooTable](
    [Column1] [varchar(20)] NULL,
    [Column2] [varchar(20)] NULL,
    [Column3] [varchar(20)] NULL,
    [Column4] [varchar(20)] NULL,
    [Column5] [varchar(20)] NULL,
//...[constraint and references]...
</pre>

I settled on using the clipboard as the medium so I don't need to deal with saving a file or using a form for input. With this pinned to my taskbar, I just copy the table definition text to my clipboard and click the icon. Voila! The result is ready to be pasted. There's nothing fancy here. Just convenience.
<pre class="prettyprint lang-csharp">

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
using System.Windows.Forms;
 
namespace MasterShredder
{
    class Program
    {
        [STAThread]
        static void Main(string[] args)
        {
            string contents = null;
            contents = Clipboard.GetText();
 
            if (string.IsNullOrEmpty(contents))
            {
                Console.WriteLine("I'm expecting the column definition to be in your clipboard.");
                Console.WriteLine("Expected format:  [ColumnName] [ColumnType] [NULL or NOT NULL],");
                Console.Read();
            }
            else
            {
 
                string[] lines = contents.Split('\n');
                StringBuilder result = new StringBuilder();
 
                foreach (string line in lines)
                {
                	//Strip new line and tab characters.
                    string cleanLine = line.Replace(Environment.NewLine, "").Replace("\t", "");
                    string[] parts = cleanLine.Split(' ');
                    if (parts.Length > 2)
                    {                       
                        string name = parts[0].Replace("[", "").Replace("]", "");
                        string type = parts[1].Replace("[", "").Replace("]", "");
 
                        // type definition was split. i.e. decimal(18, 6) 
                        if(parts[2].EndsWith(")"))
                        {
                            type += parts[2];
                        }
                        string lineResult = String.Format(",a.value('@{0}', '{1}') {0}", name, type);
                        result.AppendLine(lineResult);
                        Console.WriteLine(lineResult);
                    }
                }
 
                if(!string.IsNullOrEmpty(result.ToString()))
                {
                    Clipboard.SetText(result.ToString());
                }
            }
        }
    }
}
 
</pre>

Oh, and if this is crappy, <a title="fork it and fix it on gist." href="https://gist.github.com/2323419" target="_blank">fork and fix it on gist</a>.
