# Implementation

```python
from math import isqrt


def prime_factor(n: int) -> list[int]:
	primes = []
	for i in range(2, isqrt(n) + 1):
		while not n % i:
			primes.append(i)
			n //= i
		
	return primes

if __name__ == "__main__":
	print(prime_factor(1848721))
```

- **[[Time Complexity]]:** $O(log(n))$
- **[[Space Complexity]]:** $O(1)$, excluding output array