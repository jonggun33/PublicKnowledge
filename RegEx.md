# Regular Expression... for beginning or refreshing ..

## What's there to know
---
* One letter pattern
* Matching a word
* Matching repeated pattern
* Word/String boundaries
* Subexpression
* Backreference
* Look-around
* Conditional Search
* Python RegEx
---

If you program or perform a day-to-day works using a computer long enough, you will inevitably come across occasions where you want to:

1. check if a certain string is present in the given string
1. apply modification to only certain words or sentence 

Depending on the urgency and complexity of the task, you will decide to deploy on of the following method (in adcending order of complexity):

1. Eyeball and Quick-hand Method
1. Find/Replace function provided by the editor
1. Regular Expression
1. String Manipulation Programming
1. Parser

Regular Expression is a mini language that can boost the efficiency and effectiveness of pattern finding/replacing that can be embedded into programming languages (perl, python, JavaScript) or tools (grep, vim, Microsoft Word, Microsoft SQL Server). 
This mini languages is used to define patterns to be used in search and replacement. 
The hosting tool provide ways to define Regular Expression pattern, and methods to find or replace the pattern against a target string. Here is a example using python.
```python
import re
pattern = re.compile(r'Hello') # define a pattern
pattern.match('Hello World')   # match the pattern against a target string
```

If you aim to match one or two pattern(s) from the target string, Regular Expression is sufficient, but if you want to extrat set of elements that compromise a structured documents such as XML or programming source code, parser can be much more handy choice.

=== Concise but comprehensive Regular Expression Use Cases
This section lists simplified versions of all the RegEx use cases covered in this book whose details will be explained in fuller detail in respective chapters.
I will focus on the grammar of the Regular Expression, hiding the detials of details that will vary according to the tool of your choice. +

First, matching a letter from a string is the siplest form of valid regular expression.
```bash
target: this is my happiest X-mas
pattern: X 
result: this is my happies X-mas
```

