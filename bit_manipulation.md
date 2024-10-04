
# Bit Manipulation Cheat Sheet in C++

## 1. Basic Bitwise Operators

### AND (`&`)
- `a & b`: Performs bitwise AND. Each bit of the result is `1` if both corresponding bits of `a` and `b` are `1`.
```cpp
int a = 5;  // 101
int b = 3;  // 011
int result = a & b; // 001 => 1
```

### OR (`|`)
- `a | b`: Performs bitwise OR. Each bit of the result is `1` if at least one corresponding bit of `a` or `b` is `1`.
```cpp
int a = 5;  // 101
int b = 3;  // 011
int result = a | b; // 111 => 7
```

### XOR (`^`)
- `a ^ b`: Performs bitwise XOR. Each bit of the result is `1` if the corresponding bits of `a` and `b` are different.
```cpp
int a = 5;  // 101
int b = 3;  // 011
int result = a ^ b; // 110 => 6
```

### NOT (`~`)
- `~a`: Performs bitwise NOT (inversion). Each bit of `a` is flipped (0 becomes 1, and 1 becomes 0).
```cpp
int a = 5;  // 101
int result = ~a; // 010 => -6 (Two's complement)
```

### Left Shift (`<<`)
- `a << n`: Shifts bits of `a` to the left by `n` positions, adding zeros from the right.
```cpp
int a = 5;  // 101
int result = a << 1; // 1010 => 10
```

### Right Shift (`>>`)
- `a >> n`: Shifts bits of `a` to the right by `n` positions, discarding bits on the right.
```cpp
int a = 5;  // 101
int result = a >> 1; // 10 => 2
```

---

## 2. Common Bit Manipulation Techniques

### 2.1 Check if a Number is Odd/Even
- **Odd**: If the last bit is `1`, the number is odd.
- **Even**: If the last bit is `0`, the number is even.
```cpp
bool isOdd(int x) {
    return x & 1;
}
```

### 2.2 Get the `i`-th Bit
- Extract the bit at the `i`-th position (0-based index).
```cpp
int getBit(int num, int i) {
    return (num & (1 << i)) != 0;
}
```

### 2.3 Set the `i`-th Bit
- Set the bit at the `i`-th position to `1`.
```cpp
int setBit(int num, int i) {
    return num | (1 << i);
}
```

### 2.4 Clear the `i`-th Bit
- Set the bit at the `i`-th position to `0`.
```cpp
int clearBit(int num, int i) {
    return num & ~(1 << i);
}
```

### 2.5 Toggle the `i`-th Bit
- Toggle (invert) the bit at the `i`-th position.
```cpp
int toggleBit(int num, int i) {
    return num ^ (1 << i);
}
```

---

## 3. More Advanced Techniques

### 3.1 Count the Number of Set Bits (Hamming Weight)
- Count how many bits are `1` in a number.
```cpp
int countSetBits(int num) {
    int count = 0;
    while (num) {
        count += (num & 1);
        num >>= 1;
    }
    return count;
}
```

### 3.2 Check if a Number is a Power of 2
- A number is a power of `2` if it has exactly one set bit.
```cpp
bool isPowerOfTwo(int num) {
    return (num > 0) && (num & (num - 1)) == 0;
}
```

### 3.3 Find the Only Non-Repeating Element (XOR Trick)
- In a list where every element appears twice except one, find that one unique element.
```cpp
int findUnique(vector<int>& nums) {
    int result = 0;
    for (int num : nums) {
        result ^= num;
    }
    return result;
}
```

### 3.4 Swap Two Numbers Without Using Temporary Variable
```cpp
void swap(int& a, int& b) {
    a = a ^ b;
    b = a ^ b;
    a = a ^ b;
}
```

### 3.5 Reverse Bits of a Number
```cpp
unsigned int reverseBits(unsigned int num) {
    unsigned int result = 0;
    for (int i = 0; i < 32; i++) {
        result <<= 1;
        result |= (num & 1);
        num >>= 1;
    }
    return result;
}
```

---

## 4. Bit Manipulation Problems

### 4.1 Find the Two Non-Repeating Elements
- In an array where every element repeats twice except two elements, find the two unique elements.
```cpp
void findTwoUnique(vector<int>& nums, int& x, int& y) {
    int xor_sum = 0;
    for (int num : nums) xor_sum ^= num;

    int rightmost_bit = xor_sum & -xor_sum;
    x = 0, y = 0;
    for (int num : nums) {
        if (num & rightmost_bit)
            x ^= num;
        else
            y ^= num;
    }
}
```

### 4.2 Find Missing Number (0 to n)
- In an array containing numbers from `0` to `n`, one number is missing.
```cpp
int findMissingNumber(vector<int>& nums) {
    int n = nums.size();
    int xor_sum = 0;
    for (int i = 0; i <= n; i++) xor_sum ^= i;
    for (int num : nums) xor_sum ^= num;
    return xor_sum;
}
```

### 4.3 Find the Single Number in an Array (Elements Repeat Thrice)
- In an array where every element repeats three times except one, find the unique element.
```cpp
int singleNumber(vector<int>& nums) {
    int ones = 0, twos = 0;
    for (int num : nums) {
        ones = (ones ^ num) & ~twos;
        twos = (twos ^ num) & ~ones;
    }
    return ones;
}
```

---

## 5. Additional Bit Manipulation Tricks

### 5.1 Flip All Bits
- Flip all bits of a number.
```cpp
int flipAllBits(int num) {
    return ~num;
}
```

### 5.2 Get the Lowest Set Bit
- Get the rightmost `1` bit.
```cpp
int lowestSetBit(int num) {
    return num & (-num);
}
```

### 5.3 Remove the Lowest Set Bit
- Remove the rightmost `1` bit.
```cpp
int removeLowestSetBit(int num) {
    return num & (num - 1);
}
```

### 5.4 Get the Number of Leading Zeros
```cpp
int countLeadingZeros(int num) {
    return __builtin_clz(num);
}
```

### 5.5 Get the Number of Trailing Zeros
```cpp
int countTrailingZeros(int num) {
    return __builtin_ctz(num);
}
```
