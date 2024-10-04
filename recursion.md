
# Recursion Cheat Sheet in C++

## 1. Basic Recursion Structure

- A function that calls itself to solve a smaller version of the same problem.
- Each recursive function must have:
  1. **Base case**: Stops the recursion.
  2. **Recursive call**: Reduces the problem size and approaches the base case.

### Structure of a Recursive Function

```cpp
void recursiveFunction(int n) {
    // Base Case: Stop the recursion
    if (n == 0) {
        return;
    }

    // Recursive Call: Call the function with a smaller input
    recursiveFunction(n - 1);
}
```

---

## 2. Classic Recursion Examples

### 2.1 Factorial of a Number

- Factorial of `n` is the product of all integers from `1` to `n` (denoted `n!`).
```cpp
int factorial(int n) {
    if (n == 0 || n == 1) {
        return 1;
    }
    return n * factorial(n - 1);
}
```

### 2.2 Fibonacci Series

- Fibonacci sequence: `0, 1, 1, 2, 3, 5, 8, ...`
```cpp
int fibonacci(int n) {
    if (n == 0) return 0;
    if (n == 1) return 1;
    return fibonacci(n - 1) + fibonacci(n - 2);
}
```



## 3. Advanced Recursion Problems

### 3.1 Power of a Number (Exponentiation)

- `power(x, n)` computes `x^n`.
```cpp
int power(int x, int n) {
    if (n == 0) return 1;
    return x * power(x, n - 1);
}
```

### 3.2 Tower of Hanoi

- Move `n` disks from source to destination using an auxiliary rod, following the Tower of Hanoi rules.
```cpp
void towerOfHanoi(int n, char from_rod, char to_rod, char aux_rod) {
    if (n == 1) {
        cout << "Move disk 1 from rod " << from_rod << " to rod " << to_rod << endl;
        return;
    }
    towerOfHanoi(n - 1, from_rod, aux_rod, to_rod);
    cout << "Move disk " << n << " from rod " << from_rod << " to rod " << to_rod << endl;
    towerOfHanoi(n - 1, aux_rod, to_rod, from_rod);
}
```

### 3.3 Greatest Common Divisor (GCD) Using Euclid’s Algorithm

```cpp
int gcd(int a, int b) {
    if (b == 0) {
        return a;
    }
    return gcd(b, a % b);
}
```

### 3.4 Reverse a String Using Recursion

```cpp
void reverseString(string &str, int start, int end) {
    if (start >= end) {
        return;
    }
    swap(str[start], str[end]);
    reverseString(str, start + 1, end - 1);
}
```

---

## 4. Backtracking Using Recursion

### 4.1 N-Queens Problem

- Place `n` queens on an `n x n` chessboard such that no two queens attack each other.
```cpp
bool isSafe(vector<vector<int>>& board, int row, int col, int n) {
    for (int i = 0; i < col; i++)
        if (board[row][i])
            return false;
    for (int i = row, j = col; i >= 0 && j >= 0; i--, j--)
        if (board[i][j])
            return false;
    for (int i = row, j = col; i < n && j >= 0; i++, j--)
        if (board[i][j])
            return false;
    return true;
}

bool solveNQueensUtil(vector<vector<int>>& board, int col, int n) {
    if (col >= n)
        return true;
    for (int i = 0; i < n; i++) {
        if (isSafe(board, i, col, n)) {
            board[i][col] = 1;
            if (solveNQueensUtil(board, col + 1, n))
                return true;
            board[i][col] = 0;
        }
    }
    return false;
}

bool solveNQueens(int n) {
    vector<vector<int>> board(n, vector<int>(n, 0));
    return solveNQueensUtil(board, 0, n);
}
```

### 4.2 Subset Sum Problem

- Given a set of non-negative integers and a target value, determine if there is a subset whose sum is equal to the target.
```cpp
bool isSubsetSum(vector<int>& set, int n, int sum) {
    if (sum == 0) return true;
    if (n == 0 && sum != 0) return false;

    if (set[n - 1] > sum)
        return isSubsetSum(set, n - 1, sum);

    return isSubsetSum(set, n - 1, sum) || isSubsetSum(set, n - 1, sum - set[n - 1]);
}
```

## 6. Tail Recursion

- Tail recursion occurs when the recursive call is the last operation in the function.
```cpp
void tailRecursion(int n) {
    if (n == 0) return;
    cout << n << " ";
    tailRecursion(n - 1); // Recursive call at the end (tail recursion)
}
```

---

## 7. Memoization in Recursion (Top-Down DP)

- Memoization stores results of subproblems to avoid redundant calculations.
```cpp
int fibonacciMemo(int n, vector<int>& dp) {
    if (n <= 1) return n;
    if (dp[n] != -1) return dp[n];
    dp[n] = fibonacciMemo(n - 1, dp) + fibonacciMemo(n - 2, dp);
    return dp[n];
}
```

---

## 8. Key Considerations in Recursion

- **Base Case**: Ensure the recursion has a well-defined base case to prevent infinite recursion.
- **Stack Overflow**: Recursion consumes stack memory; deep recursion may lead to a stack overflow.
- **Tail Recursion Optimization**: Some compilers optimize tail-recursive functions to prevent stack overflow.
- **Memoization**: Used to optimize recursion by caching previously computed results.


