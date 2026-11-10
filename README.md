# Longest-substrings-without-repeating-characters
LeetCode 3 Longest Substring Without Repeating Characters solution in Python
# LeetCode 3: Longest Substring Without Repeating Characters

## Problem
Given a string `s`, find the length of the longest substring without duplicate characters.

A substring is a contiguous part of the string. `"pwke"` is a subsequence of `"pwwkew"`, not a substring.

## Examples

| Input | Output | Explanation |
|-------|--------|-------------|
| `s = "abcabcbb"` | `3` | The answer is `"abc"` |
| `s = "bbbbb"` | `1` | The answer is `"b"` |
| `s = "pwwkew"` | `3` | The answer is `"wke"` |

## Constraints
- `0 <= s.length <= 10^5`
- `s` consists of English letters, digits, symbols and spaces.

## Approach: Sliding Window
Keep a window `[left, right]` over the string that never contains a repeated character.

1. Move `right` one step at a time to add a new character.
2. While the new character is already inside the window, remove the character at `left` and move `left` forward.
3. Add the new character to the window.
4. Update `best` with the current window length `right - left + 1`.

A `while` loop (not `if`) is needed for step 2, because more than one character may have to be removed
before the duplicate is gone (for example in `"pwwkew"`).

A `set` stores the characters currently in the window, so checking for a duplicate is fast.
In C, an array `seen[256]` is used instead (`0` = not in window, `1` = in window).

### Walkthrough: `"abcabcbb"`

| right | char | Duplicate? | left | Window | Length | best |
|-------|------|------------|------|--------|--------|------|
| 0 | a | no | 0 | `a` | 1 | 1 |
| 1 | b | no | 0 | `ab` | 2 | 2 |
| 2 | c | no | 0 | `abc` | 3 | 3 |
| 3 | a | yes | 1 | `bca` | 3 | 3 |
| 4 | b | yes | 2 | `cab` | 3 | 3 |
| 5 | c | yes | 3 | `abc` | 3 | 3 |
| 6 | b | yes | 5 | `cb` | 2 | 3 |
| 7 | b | yes | 7 | `b` | 1 | 3 |

Result: `3`

### Edge cases

| Input | Output |
|-------|--------|
| `""` | `0` |
| `"a"` | `1` |
| `"abcd"` | `4` |
| `"bbbb"` | `1` |
| `"a b"` | `3` (a space counts as a character) |

## Complexity
- Time: O(n), each character is added once and removed at most once
- Space: O(k), where k is the number of distinct characters in the window

## Brute force vs Sliding Window

| Approach | Time |
|----------|------|
| Check every substring | O(n^2) or O(n^3) |
| Sliding Window | O(n) |

## Concepts Used
- Sliding Window
- Two pointers (`left`, `right`)
- Set (Python)

## Language
Python 3

## Link
https://leetcode.com/problems/longest-substring-without-repeating-characters
