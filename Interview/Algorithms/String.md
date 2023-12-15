# String

## Time complexity

- Access: O(1)
- Search: O(n)
- Insert: O(n)
- Remove: O(n)

## Operations involving another string

- Find Substring: O(n.m)
- Concatenated strings: O(n+m)
- Slice: O(m)
- Split (by token): O(n+m)
- Strip (remove leading and trailing whitespaces): O(n)

## Techniques

- Counting characters
  - Python has Counter class. If not allowed use hashmap
- String of unique characters
  - Use a 26-bit bitmask to indicate which lower case latin characters are inside the string
- Anagram
  - Frequency counting of characters
- Palindrome
  - Reverse the string and it should be equal to itself.
  - Have two pointers at the start and end of the string. Move the pointers inward till they meet. At every point in time, the characters at both pointers should match.

## Things to look out for

- Ask about input character set and case sensitivity. Usually the characters are limited to lowercase Latin characters, for example a to z.

## Corner cases

- Empty string
- String with 1 or 2 characters
- String with repeated characters
- Strings with only distinct characters
