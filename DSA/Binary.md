# Binary

## Python

```
def decimalToBinary(n):
    return bin(n).replace("0b", "")
```

```
def binaryToDecimal(n):
    return int(n, 2)
```

## Corner cases

- Be aware and check for overflow/underflow
- Negative numbers

## Techniques

- Test kth bit is set: num & (1 << k) != 0.
- Set kth bit: num |= (1 << k)
- Turn off kth bit: num &= ~(1 << k).
- Toggle the kth bit: num ^= (1 << k).
- Multiply by 2k: num << k
- Divide by 2k: num >> k
- Check if a number is a power of 2: (num & num - 1) == 0 or (num & (-num)) == num
- Swapping two variables: num1 ^= num2; num2 ^= num1; num1 ^= num2
