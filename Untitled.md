#Chapter 15. Regular Expressions
##特殊符号和字符
| Notation      |  Description    |Example RE |
|:------------- |:---------------:| -------------:|
| literal       | Match literal string value literal |         ---|
| re1\|re2      | centered        |      $12      |
| . | are neat        |            $1 |
|^
|$
|*
|+
|?
|{N}
|{M,N}
|[...]
|[x-y]
|[^...]
|(...)

这是一个普通段落。

<table>
    <tr>
        <td>Foo</td>
    </tr>
</table>

这是另一个普通段落。


> ## 这是一个标题。
> 
> 1.   这是第一行列表项。
> 2.   这是第二行列表项。
> 
> 给出一些例子代码：
> 
>     return shell_exec("echo $input | $markdown_script");
> 
> 
>*   Red
>*   Green
>*   Blue
>+   Red
>+   Green
>+   Blue
>
1.  Bird
2.  McHale
3.  Parish

*   Bird

*   Magic

*   A list item with a blockquote:

    > This is a blockquote
    > inside a list item.
    
    
*   一列表项包含一个列表区块：

        <代码写在这>
        fwffew
        
Here is an example of AppleScript:

    	tell application "Foo"
       	 beep
    	end tell
    	
* * *

***

*****

- - -

---------------------------------------

*single asterisks*

_single underscores_

**double asterisks**

__double underscores__

Use the `printf()` function.

``There is a literal backtick (`) here.``
##15.2. Special Symbols and Characters
###Table 15.1. Common Regular Expression Symbols and Special Characters

| Notation      |  Description    |Example RE |
|:------------- |:---------------| -------------:|
|**Symbols**
|literal | Match literal string value literal|foo
|re1\|re2 |Match regular expressions re1 or re2|foo\|bar
|.|Match any character (except NEWLINE)|b.b|^|Match start of string|^Dear|$|Match end of string|/bin/*sh$|*|Match 0 or more occurrences of preceding RE|[A-Za-z0-9]*|+|Match 1 or more occurrences of preceding RE|[a-z]+\.com|?|Match 0 or 1 occurrence(s) of preceding RE|goo?|{N}|Match N occurrences of preceding RE|[0-9]{3}|{M,N}|Match from M to N occurrences of preceding RE|[0-9]{5,9}
|[...]|Match any single character from character class|[aeiou]
|[..x-y..]|Match any single character in the range from x to y|[0-9],[A-Za-z]|[^...]|Do not match any character from character class, including any ranges, if present|[^aeiou], [^A-Za-z0-9_]
|(*\|+\|?\| {})?|Apply "non-greedy" versions of above occurrence/ repetition symbols ( *, +, ?, {})|.*?[a-z]|(...)|Match enclosed RE and save as subgroup|([0-9]{3})?, f(oo|u)bar|**Special Characters**
|\d|Match any decimal digit, same as \[0-9\](\D is inverse of \d: do not match any numeric digit)|data\d+.txt
|\w|Match any alphanumeric character, same as \[A-Za-z0-9_\] (\W is inverse of \w)|\[A-Za-z_\]\w+
|\s|Match any whitespace character, same as \[ \n\t\r\v \f\] (\S is inverse of \s)|of\sthe
|**\b**|Match any word boundary (\B is inverse of \b)|\bThe\b
|**\nn**|Match saved subgroup nn (see (...) above)|price: \16
|\c|Match any special character c verbatim (i.e., with out its special meaning, literal)|\\., \\\\, \\*
|**\A(\Z)**|Match start (end) of string (also see ^ and $ above)|\ADear* To match a pattern starting from the beginning, you must use the carat symbol( ^ ) or the special character \A (backslash-capital "A"). Similarly, the dollar sign (\$) or \Z will match a pattern from the end of a string.

	```
	^FromAny		string that starts with From
	/bin/tcsh$		Any string that ends with /bin/tcsh
	^Subject: hi$ 	Any string consisting solely of the string Subject: hi
	\bthe			Any word that starts with the	\bthe\b			Matches only the word the	\Bthe			Any string that contains but does not begin with the
	```
	
	```python
	>>> m = re.search('^The', 'The end.')
	>>> if m is not None: m.group()	...	'The'	>>> m = re.search('^The', 'end. The')	>>> if m is not None: 
	...		m.group()	...	>>> m = re.search(r'\bthe', 'bite the dog') # at a boundary
	>>> if m is not None: m.group()	...	'the'	>>> m = re.search(r'\bthe', 'bitethe dog') # no boundary
	>>> if m is not None:
	...		m.group()	...	>>> m = re.search(r'\Bthe', 'bitethe dog') # no boundary	>>> if m is not None:
	...		m.group() ...	'the'
	```
* if a caret ( ^ ) is the firstcharacter immediately inside the open left bracket, this symbolizes a directive not to match any of the characters in the given character set.

	```
z.[0-9]			"z" followed by any character then followed by a single digit[r-u][env-y]	"r" "s," "t" or "u" followed by "e," "n," "v," "w," "x," or "y"[us]			followed by "u" or "s"[^aeiou]		A non-vowel character (Exercise: Why do we say "non-vowels" rather than "consonants"?)[^\t\n]			Not a TAB or NEWLINE["-a]			In an ASCII system, all characters that fall between '"' and "a," i.e., between ordinals 34 and 97
	```
	
* question mark(**?**) is used more than once (overloaded), meaning either matching 0 or 1 occurrences, or its other meaning: if it follows any matching using the close operators(*, +, ?, { }), it will direct the regular expression engine to match as few repetitions as possible.
*  there are special characters that may represent character sets.
  
	```
\w+-\d+				Alphanumeric string and number separated by a hyphen
[A-Za-z]\w*			Alphabetic first character, additional characters (if present) can be alphanumeric (almost equivalent to the set of valid Python identifiers [see exercises])
\d{3}-\d{3}-\d{4}	(American) telephone numbers with an area code prefix, as in 800-555-1212\w+@\w+\.com	 	Simple e-mail addresses of the form XXX@YYY.com	```
* if we want to extract any specific strings or substrings that were part of a successful match. The answer is yes. To accomplish this, surround any RE with a pair of parentheses.
	* A pair of parentheses ( ( ) ) can accomplish either (or both) of the below when used with regular expressions:
		* Grouping regular expressions (对正则表达式进行分组)		* Matching subgroups (匹配子组)

	```
	\d+(\.\d*)?		Strings representing simple floating point number
	(Mr?s?\. )?[A-Z][a-z]* [ A-Za-z-]+		First name and last name, with a restricted first name (must start with uppercase; lowercase only for remaining letters, if any), the full name prepended by an optional title of "Mr.," "Mrs.," "Ms.," or "M.," and a flexible last name, allowing for multiple words, dashes, and uppercase letters
	```

##15.3. REs and Python

* two object
	* regex object (return by re.compile)
	* match object (return by re.math / re.search)


###Table 15.2. Common Regular Expression Functions and Methods|Function/Method| Description|
|:---|:----|
|**re Module Function Only**
|compile(pattern, flags=0)|Compile RE pattern with any optional flags and return a regex object
|**re Module Functions and regex Object Methods**
|match(pattern, string, flags=0)|Attempt to match RE pattern to string with optional flags; return match object on success, None on failure
|search(pattern, string, flags=0)|Search for first occurrence of RE pattern within string with optional flags; return match object on success, None on failure
|findall(pattern, string[,flags])|Look for all (non-overlapping) occurrences of pattern in string; return a list of matches
|finditer(pattern, string[, flags])|Same as findall() except returns an iterator instead of a list; for each match, the iterator returns a match object
|split(pattern, string, max=0)|Split string into a list according to RE pattern delimiter and return list of successful matches, splitting at most max times (split all occurrences is the default)
|sub(pattern, repl, string, max=0)|Replace all occurrences of the RE pattern in string with repl, substituting all occurrences unless max provided (also see subn () which, in addition, returns the number of substitutions made)
|**Match Object Methods**
|group(num=0)|Return entire match (or specific subgroup num)
|groups()|Return all matching subgroups in a tuple (empty if thereweren't any)

###15.3.2. Compiling REs with compile()
* Almost all of the re module functions we will be describing shortly are available as methods for regexobjects.

###15.3.3. Match Objects and the group() and groups () Methods
* returned on successful calls to match() or search(). Match objects have two primary methods, group() and groups().
	* group() will either return the entire match, or a specific subgroup,
	* groups() will simply return a tuple consisting of only/all the <font color=red>subgroups</font>
	
	```python
	>>> m = re.match('(\w\w\w)-(\d\d\d)', 'abc-123')	>>> m.group()	# entire match	'abc-123'	>>> m.group(1)	# subgroup 1	'abc'	>>> m.group(2)	# subgroup 2	'123'	>>> m.groups()	# all subgroups	('abc', '123')
					
	>>> m = re.match('ab', 'ab')	# no subgroups	>>> m.group()					# entire match	'ab'	>>> m.groups()					# all subgroups	()
	
	>>> m = re.match('(a(b))', 'ab')	# two subgroups	>>> m.group()						# entire match	'ab'	>>> m.group(1)						# subgroup 1
	'ab'	>>> m.group(2)						# subgroup 2	'b'	>>> m.groups()               		# all subgroups	('ab', 'b')
	```

###15.3.4. Matching Strings with match()
* The match() function attempts to match the pattern to the string, starting <font color=red>at the begining</font>. 

	```python
	>>> m = re.match('foo', 'foo') # pattern matches string
	>>> if m is not None: # show match if successful
	... 	m.group()	...	
	'foo'
	```

###15.3.5. Looking for a Pattern within a String with search() (Searching versus Matching)
* It works exactly in the same way as match except that it searches for <font color=red>the first occurrence</font> of the given RE pattern anywhere with its string argument.

	```python
	>>> m = re.match('foo', 'seafood') # no match 
	>>> if m is not None:
	>>> 	m.group()	...	>>>
	>>> m = re.search('foo', 'seafood') # use search() instead 
	>>> if m is not None:
	>>> 	m.group()	...	'foo' # search succeeds where match failed
	```


###15.3.6. Finding Every Occurrence with findall()
* It looks for all non-overlapping occurrences of an RE pattern in a string
* The list will be empty if no occurrences are found but if successful, the list will consist of all matches found (grouped in left-to-right order of occurrence)

	```python
	>>> re.findall('car', 'car')	['car']	>>> re.findall('car', 'scary')	['car']	>>> re.findall('car', 'carry the barcardi to the car')	['car', 'car', 'car']
	```


###15.3.7. Searching and Replacing with sub() [and subn()]



###15.3.8. Splitting (on Delimiting Pattern) with split()

