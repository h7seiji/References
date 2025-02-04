# Regular Expressions

<https://developers.google.com/edu/python/regular-expressions>

## Basic Patterns

The power of regular expressions is that they can specify patterns, not just fixed characters. Here are the most basic patterns which match single chars:

- `a, X, 9, <` -- ordinary characters just match themselves exactly. The meta-characters which do not match themselves because they have special meanings are: . ^ $ * + ? { [ ] \ | ( )
- `.` (a period) -- matches any single character except newline '\n'
- `\w` -- (lowercase w) matches a "word" character: a letter or digit or underbar [a-zA-Z0-9_]. Note that although "word" is the mnemonic for this, it only matches a single word char, not a whole word. \W (upper case W) matches any non-word character.
- `\b` -- boundary between word and non-word
- `\s` -- (lowercase s) matches a single whitespace character -- space, newline, return, tab, form [ \n\r\t\f]. \S (upper case S) matches any non-whitespace character.
- `\t, \n, \r` -- tab, newline, return
- `\d` -- decimal digit [0-9] (some older regex utilities do not support \d, but they all support \w and \s)
- `^` = start, $ = end -- match the start or end of the string
- `\` -- inhibit the "specialness" of a character. So, for example, use \. to match a period or \\ to match a slash. If you are unsure if a character has special meaning, such as '@', you can try putting a slash in front of it, \@.

```python
  ## Search for pattern 'iii' in string 'piiig'.
  ## All of the pattern must match, but it may appear anywhere.
  ## On success, match.group() is matched text.
  match = re.search(r'iii', 'piiig') # found, match.group() == "iii"
  match = re.search(r'igs', 'piiig') # not found, match == None

  ## . = any char but \n
  match = re.search(r'..g', 'piiig') # found, match.group() == "iig"

  ## \d = digit char, \w = word char
  match = re.search(r'\d\d\d', 'p123g') # found, match.group() == "123"
  match = re.search(r'\w\w\w', '@@abcd!!') # found, match.group() == "abc"
```

## Repetition

Things get more interesting when you use + and * to specify repetition in the pattern

- `+`  -- 1 or more occurrences of the pattern to its left, e.g. 'i+' = one or more i's
- `*` -- 0 or more occurrences of the pattern to its left
- `?` -- match 0 or 1 occurrences of the pattern to its left

### Leftmost & Largest

First the search finds the leftmost match for the pattern, and second it tries to use up as much of the string as possible -- i.e. + and *go as far as possible (the + and* are said to be "greedy").

```python
  ## i+ = one or more i's, as many as possible.
  match = re.search(r'pi+', 'piiig') # found, match.group() == "piii"

  ## Finds the first/leftmost solution, and within it drives the +
  ## as far as possible (aka 'leftmost and largest').
  ## In this example, note that it does not get to the second set of i's.
  match = re.search(r'i+', 'piigiiii') # found, match.group() == "ii"

  ## \s* = zero or more whitespace chars
  ## Here look for 3 digits, possibly separated by whitespace.
  match = re.search(r'\d\s*\d\s*\d', 'xx1 2   3xx') # found, match.group() == "1 2   3"
  match = re.search(r'\d\s*\d\s*\d', 'xx12  3xx') # found, match.group() == "12  3"
  match = re.search(r'\d\s*\d\s*\d', 'xx123xx') # found, match.group() == "123"

  ## ^ = matches the start of string, so this fails:
  match = re.search(r'^b\w+', 'foobar') # not found, match == None
  ## but without the ^ it succeeds:
  match = re.search(r'b\w+', 'foobar') # found, match.group() == "bar"
```

## Group Extraction

The "group" feature of a regular expression allows you to pick out parts of the matching text. Suppose for the emails problem that we want to extract the username and host separately. To do this, add parentheses ( ) around the username and host in the pattern, like this: r'([\w.-]+)@([\w.-]+)'. In this case, the parentheses do not change what the pattern will match, instead they establish logical "groups" inside of the match text. On a successful search, match.group(1) is the match text corresponding to the 1st left parentheses, and match.group(2) is the text corresponding to the 2nd left parentheses. The plain match.group() is still the whole match text as usual.

```python
  str = 'purple alice-b@google.com monkey dishwasher'
  match = re.search(r'([\w.-]+)@([\w.-]+)', str)
  if match:
    print(match.group())   ## 'alice-b@google.com' (the whole match)
    print(match.group(1))  ## 'alice-b' (the username, group 1)
    print(match.group(2))  ## 'google.com' (the host, group 2)
```
