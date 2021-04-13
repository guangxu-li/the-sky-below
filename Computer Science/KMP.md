#algorithm #pattern-search #snippet 

The **Knuth-Morris-Pratt (KMP) algorithm** is an algorithm that is used to search for a substring (`W`), in a given string (`S`), in O(m+n)O(m+n) time (where m and n are the lengths of `W` and `S`).

# Key idea

The key idea used to achieve this [[Time Complexity]] is to minimize the amount of backtracking when a character of `W` does not match with that of `S`. This can only be done if we know two things:

1.  Whether or not a proper prefix of `W` occurs more than once in `S` after at least one character has been correctly found; if it does, it can be skipped when resuming the process of matching after a mismatch.
2.  Length of the proper prefix.

# Using an array
Before starting the actual algorithm, a one-dimensional array is initialized with the number of characters that can be skipped after a mismatch. `arr[i` represents the number of characters that can be skipped when `W[i+1]` does not match with a character in `S`.

# Failure function
`dp` is initialized using the failure function `f(i)`. This function is based on the fact that:

_When a mismatch occurs, all the previous characters match correctly; this implies that if a prefix of `W` occurred in this set of matching characters, then that prefix is also a suffix of `W`_.

In other words, `dp[i]` will represent the length of the longest proper prefix of `W`, which is also a proper suffix of `W` (considering `W` till the `i-th` index only).

The following is the code used to initialize `arr`:

```python
def longest_common_pre_suf(W: str) -> list[int]:
    dp = [0] * len(W)

    for i in range(1, len(W)):
        j = dp[i - 1]
        while j > 0 and W[i] != W[j]:
            j = dp[j - 1]
        
        dp[i] = j + (W[i] == W[j])
        
    return dp
```

^cdfb1c

# Implementation
`longest_common_pre_suf` code implementation [[KMP#^cdfb1c]]
```python
def longest_common_pre_suf(W: str) -> list[int]:
    dp = [0] * len(W)

    for i in range(1, len(W)):
        j = dp[i - 1]
        while j > 0 and W[i] != W[j]:
            j = dp[j - 1]
        
        dp[i] = j + (W[i] == W[j])
        
    return dp

def kmp_search(s: str, pattern: str) -> list[int]:
    partial, ret, j = longest_common_pre_suf(pattern), [], 0

    for i in range(len(s)):
        while j > 0 and s[i] != pattern[j]:
            j = partial[j - 1]
        
        j += s[i] == pattern[j]
        if j == len(pattern):
            ret.append(i + 1 - j)
            j = partial[j - 1]
    
    return ret
```

# [[Complexity]]:
- **[[Time Complexity]]:** In the worst case, both strings was scanned from start to the end, so the time complexity is `O(m + n)`