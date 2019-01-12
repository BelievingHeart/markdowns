[//]: # (#include #regex #regular expression)
--------------------------------meta character---------------------------------
\d			: any digit
.			: any thing
\w			: any word, namely a->z, A->Z and 0->9
\W			: any thing but not word
\s			: any whitespace, namely space or tab
\S			: any thing but not whitespace


--------------------------------quantifier---------------------------------
*			: followed by 0 or more of the thing before *
?			: followed optionaly by the thing before ?  			Note: ? after greedy match tells it to be not greedy
+			: followed by 1 or more of the thing before +
{min, max}	: followed by number between min and max of the thing before {min, max}
{n}			: followed by n of the thing before {n}


--------------------------------position---------------------------------
^			: begin of line
$			: end of line
\b			: word boundary, all punctuations are considered word boundary


--------------------------------character classes---------------------------------
[thing1 thing2 ...] : matches thing1 or thing2 or ...						Note: don't need \ to escape inside []

	special character in []:
    	1. - : literal - or "through"   [a-z], [A-Z], [0-9] ...
        2. ^ : literal ^ or "not" 		[^a-z], [^/d], [^abc]->not any one of abc, [a^bc]->a or ^ or b or c
        
--------------------------------alternation---------------------------------
(option1 | option2 | option3) : option1 or option2 or option3

--------------------------------capture expression---------------------------------
()			: Using () to enclose a part of regex. Use \1, \2 ... to refer to this part inside regex
			  and use $1, $2 ... to refer to this part outside of regex. \0 and $0 refers to the whole regex.
