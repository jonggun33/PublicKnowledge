= ASCIIDoc : The Cheatsheet
:description: This document is for quick-referencing ASCIIDoc grammar.
:authors: Jonggun Gim
:sectnums:
:toc: left
//:doctype: manpage
:access: meonly
:source-highlighter: highlight.js
:showtitle:
:toclevels: 1
//:toc-placement: preamble


== About this document
{description}

https://docs.asciidoctor.org/asciidoc/latest/key-concepts/#attributes[Grammar]

{authors}

.Revisions
[format="csv", options="header"]
|===
Date, Description
2021/01/06, Initial Draft
|===

== Document Structure

== Header Attributes
* author
* authorinitials
* description
* doctitle
* email


== Blocks

[NOTE]
====
This is a *NOTE*.
====

.Source Code block
[source, perl]
----
use DBI;
my $dbh = DBI->connect()
  or die
----

[quote, A-Ha , 90's show]
____
The sun always shines on TV.
____

.Definitions
apple:: a red fruit
pear:: a yellow fruit

[WARNING]
This is an example note.


== Table
.Header and Footer
[options="header,footer"]
|====
|col1|col2|col3
|1|2|afasd
|3|4|adsfasd
|3| 6|adfa
|====

.CSV style
[format="csv", cols="4"]
[options="header"]
|====
col1,col2,col3,col4
1,2,3,4
a,b,c,d
|====

.Colum, Row Merge
[options="header", cols="4*^"]
|====
|Date|Time|Examiner|Blood Pressure
.2+|2021/01/05 |09:00 |Gim >|70-100
|15:00 |Lee |71-101
|22021/01/06 3+|TBD
|====


== Listing
====
* Asia
** Korea
** Japan
* Europe
** France
** Netherlands
====

. Wash hands
. Eat the food
. Brush teeth


* [x] Eggs
* [ ] Spinach
* [x] Ham


== Hyperlink
http://www.google.com[Google]

== Code Block
[source, python]
----
def name():
  return 'name'
----

== Text Formatting
This is *bold* stuff!

__This is Italic.__

+mono *bold*+

H~2~O, CO~2~, x^2^

forced +
line break

Werewolves are alergic to ~~cinnamons~~.

-- ... -> <- => <= 

''''

== Referencing
=== Cross referencing
[[here]]
This is a reference target

Here is the reference <<here>> defined above.

=== footnote
I went to Bangladesh footnote:[From 2001 to 2002]

== Mathematical Notations
https://chrome.google.com/webstore/detail/mathjax-3-plugin-for-gith/peoghobgdhejhcmgoppjpjcidngdfkod[MathJax 3 Plugin for Github]

$-1 \leq \frac{\langle x, y \rangle}{\Vert x \Vert \Vert y \Vert} \leq 1$

$sin(\theta)^2 + cos(\theta)^2 = 1$

$x = a \times b \div \sqrt[3]{c}$

$ \alpha + \beta $

$x^{10} = A_{2,3} + c^{1/2}$

$e^{i \pi} + 1 = 0$

$x = {-b \pm \sqrt{b^2-4ac} \over 2a}.$

== HTML embedding
++++
<input type="text" name="email">
<input type="checkbox" name="subscribe">
++++

