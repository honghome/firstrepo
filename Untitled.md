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
|**\A(\Z)**|Match start (end) of string (also see ^ and $ above)|\ADear
* if a caret ( ^ ) is the firstcharacter immediately inside the open left bracket, this symbolizes a directive not to match any of the characters in the given character set.

	```python
z.[0-9]			"z" followed by any character then followed by a single digit[r-u][env-y]	"r" "s," "t" or "u" followed by "e," "n," "v," "w," "x," or "y"[us]			followed by "u" or "s"[^aeiou]		A non-vowel character (Exercise: Why do we say "non-vowels" rather than "consonants"?)[^\t\n]			Not a TAB or NEWLINE["-a]			In an ASCII system, all characters that fall between '"' and "a," i.e., between ordinals 34 and 97
	```
	
