# Sorting and searching

## Complexity

- Bubble sort - Time: O(n2) - Space: O(1)
- Insertion sort - Time: O(n2) - Space: O(1)
- Selection sort - Time: O(n2) - Space: O(1)
- Quicksort - Time: O(nlog(n)) - Space: O(log(n))
- Mergesort - Time: O(nlog(n)) - Space: O(n)
- Heapsort - Time: O(nlog(n)) - Space: O(1)
- Counting sort - Time: O(n + k) - Space: O(k)
- Radix sort - Time: O(nk) - Space: O(n + k)
- Binary search - Time: O(log(n))

## Things to look out for

- Make sure you know the time and space complexity of the language's default sorting algorithm! The time complexity is almost definitely O(nlog(n)).
- In Python, it's Timsort.

## Corner cases

- Empty sequence
- Sequence with one element
- Sequence with two elements
- Sequence containing duplicate elements.

## Techniques

- Sorted inputs
  - When a given sequence is in a sorted order (be it ascending or descending), using binary search should be one of the first things that come to your mind.
- Sorting an input that has limited range
  - Counting sort is a non-comparison-based sort you can use on numbers where you know the range of values beforehand.
