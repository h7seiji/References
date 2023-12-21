# Trie

Tries are special trees (prefix trees) that make searching and storing strings more efficient.

## Time complexity

- Search: O(m)
- Insert: O(m)
- Remove: O(m)

## Corner cases

- Searching for a string in an empty trie
- Inserting empty strings into a trie

## Techniques

- Sometimes preprocessing a dictionary of words (given in a list) into a trie, will improve the efficiency of searching for a word of length k, among n words. Searching becomes O(k) instead of O(n).
