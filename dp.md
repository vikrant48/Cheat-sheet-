
# Dynamic Programming (DP) Cheat Sheet in C++

## 1. Introduction to Dynamic Programming

- **Dynamic Programming (DP)** is an optimization technique used to solve problems by breaking them down into overlapping subproblems and storing the solutions to avoid redundant work.
- **Two main approaches:**
  1. **Top-Down (Memoization):** Solve the problem recursively and store the results of subproblems.
  2. **Bottom-Up (Tabulation):** Iteratively solve all subproblems from the smallest to the largest.

---

## 2. Top-Down (Memoization)

### 2.1 Fibonacci Sequence using Memoization

```cpp
int fibMemo(int n, vector<int>& dp) {
    if (n <= 1) return n;
    if (dp[n] != -1) return dp[n];
    dp[n] = fibMemo(n - 1, dp) + fibMemo(n - 2, dp);
    return dp[n];
}
```

### 2.2 Minimum Steps to 1 (Recursive + Memoization)

- You are given a number `n`. In one step, you can:
  1. Subtract 1 from `n`.
  2. If `n` is divisible by 2, divide it by 2.
  3. If `n` is divisible by 3, divide it by 3.

- Find the minimum number of steps to reach `1`.

```cpp
int minSteps(int n, vector<int>& dp) {
    if (n == 1) return 0;
    if (dp[n] != -1) return dp[n];

    int res = minSteps(n - 1, dp);
    if (n % 2 == 0) res = min(res, minSteps(n / 2, dp));
    if (n % 3 == 0) res = min(res, minSteps(n / 3, dp));

    return dp[n] = 1 + res;
}
```

---

## 3. Bottom-Up (Tabulation)

### 3.1 Fibonacci Sequence using Tabulation

```cpp
int fibTab(int n) {
    vector<int> dp(n + 1);
    dp[0] = 0;
    dp[1] = 1;
    for (int i = 2; i <= n; i++) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }
    return dp[n];
}
```

### 3.2 Longest Common Subsequence (LCS)

- Given two strings `X` and `Y`, find the length of the longest common subsequence.
```cpp
int lcs(string X, string Y) {
    int m = X.length(), n = Y.length();
    vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));

    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (X[i - 1] == Y[j - 1])
                dp[i][j] = 1 + dp[i - 1][j - 1];
            else
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]);
        }
    }
    return dp[m][n];
}
```

---

## 4. DP on Sequences

### 4.1 Longest Increasing Subsequence (LIS)

- Given an array of integers, find the length of the longest increasing subsequence.

```cpp
int lis(vector<int>& nums) {
    int n = nums.size();
    vector<int> dp(n, 1);

    for (int i = 1; i < n; i++) {
        for (int j = 0; j < i; j++) {
            if (nums[i] > nums[j]) {
                dp[i] = max(dp[i], dp[j] + 1);
            }
        }
    }

    return *max_element(dp.begin(), dp.end());
}
```

### 4.2 Knapsack Problem (0/1)

- Given a set of items, each with a weight and a value, determine the maximum value that can be carried in a knapsack of a given capacity.

```cpp
int knapsack(vector<int>& wt, vector<int>& val, int W, int n) {
    vector<vector<int>> dp(n + 1, vector<int>(W + 1, 0));

    for (int i = 1; i <= n; i++) {
        for (int w = 1; w <= W; w++) {
            if (wt[i - 1] <= w) {
                dp[i][w] = max(val[i - 1] + dp[i - 1][w - wt[i - 1]], dp[i - 1][w]);
            } else {
                dp[i][w] = dp[i - 1][w];
            }
        }
    }
    return dp[n][W];
}
```

---

## 5. Matrix-based DP

### 5.1 Matrix Chain Multiplication

- Given a sequence of matrices, find the minimum cost of multiplying them.

```cpp
int matrixChainOrder(vector<int>& dims, int n) {
    vector<vector<int>> dp(n, vector<int>(n, 0));

    for (int len = 2; len < n; len++) {
        for (int i = 1; i < n - len + 1; i++) {
            int j = i + len - 1;
            dp[i][j] = INT_MAX;
            for (int k = i; k < j; k++) {
                int cost = dp[i][k] + dp[k + 1][j] + dims[i - 1] * dims[k] * dims[j];
                dp[i][j] = min(dp[i][j], cost);
            }
        }
    }
    return dp[1][n - 1];
}
```

### 5.2 Unique Paths in a Grid

- A robot is located at the top-left corner of an `m x n` grid and can only move either down or right. Find how many unique paths the robot can take to reach the bottom-right corner.

```cpp
int uniquePaths(int m, int n) {
    vector<vector<int>> dp(m, vector<int>(n, 1));

    for (int i = 1; i < m; i++) {
        for (int j = 1; j < n; j++) {
            dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
        }
    }

    return dp[m - 1][n - 1];
}
```

---

## 6. Space Optimization in DP

- DP solutions can often be optimized to use **O(1)** or **O(n)** space, instead of **O(n^2)** or **O(n)**.

### 6.1 Space-Optimized Fibonacci

```cpp
int fibSpaceOptimized(int n) {
    int a = 0, b = 1;
    for (int i = 2; i <= n; i++) {
        int c = a + b;
        a = b;
        b = c;
    }
    return b;
}
```
## some more example 
### Coin Change - Minimum Coins
Problem: Find the minimum number of coins that make a given value.
```cpp
int coinChange(vector<int>& coins, int amount) {
    vector<int> dp(amount + 1, amount + 1);
    dp[0] = 0;

    for (int i = 1; i <= amount; i++) {
        for (int coin : coins) {
            if (i - coin >= 0) {
                dp[i] = min(dp[i], dp[i - coin] + 1);
            }
        }
    }
    return dp[amount] > amount ? -1 : dp[amount];
}

```
### Edit Distance (Levenshtein Distance)
Problem: Given two strings, find the minimum number of operations required to convert one string into the other.
```cpp
int editDistance(string word1, string word2) {
    int m = word1.size(), n = word2.size();
    vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));

    for (int i = 0; i <= m; i++) dp[i][0] = i;
    for (int j = 0; j <= n; j++) dp[0][j] = j;

    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (word1[i - 1] == word2[j - 1])
                dp[i][j] = dp[i - 1][j - 1];
            else
                dp[i][j] = 1 + min({dp[i - 1][j], dp[i][j - 1], dp[i - 1][j - 1]});
        }
    }
    return dp[m][n];
}

```
### Subset Sum Problem
Problem: Determine if a subset with a given sum exists.
```cpp
bool subsetSum(vector<int>& nums, int target) {
    int n = nums.size();
    vector<vector<bool>> dp(n + 1, vector<bool>(target + 1, false));
    
    for (int i = 0; i <= n; i++) dp[i][0] = true;

    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= target; j++) {
            if (nums[i - 1] <= j)
                dp[i][j] = dp[i - 1][j] || dp[i - 1][j - nums[i - 1]];
            else
                dp[i][j] = dp[i - 1][j];
        }
    }
    return dp[n][target];
}

```
### Matrix Chain Multiplication
```cpp
int matrixChainMultiplication(vector<int>& p, int n) {
    vector<vector<int>> dp(n, vector<int>(n, 0));

    for (int len = 2; len < n; len++) {
        for (int i = 1; i < n - len + 1; i++) {
            int j = i + len - 1;
            dp[i][j] = INT_MAX;
            for (int k = i; k < j; k++) {
                int cost = dp[i][k] + dp[k + 1][j] + p[i - 1] * p[k] * p[j];
                dp[i][j] = min(dp[i][j], cost);
            }
        }
    }
    return dp[1][n - 1];
}

```
### Rod Cutting Problem
Problem: Given a rod of length n and prices for different lengths, determine the maximum revenue obtainable.
```cpp
int rodCutting(vector<int>& prices, int n) {
    vector<int> dp(n + 1, 0);

    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= i; j++) {
            dp[i] = max(dp[i], prices[j - 1] + dp[i - j]);
        }
    }
    return dp[n];
}

```
### Maximum Subarray Sum (Kadane’s Algorithm)
Problem: Find the maximum sum of a contiguous subarray.
```cpp
int maxSubArray(vector<int>& nums) {
    int maxSum = nums[0], currSum = nums[0];
    for (int i = 1; i < nums.size(); i++) {
        currSum = max(nums[i], currSum + nums[i]);
        maxSum = max(maxSum, currSum);
    }
    return maxSum;
}

```
### Minimum Path Sum in Grid
```cpp
int minPathSum(vector<vector<int>>& grid) {
    int m = grid.size(), n = grid[0].size();
    vector<vector<int>> dp(m, vector<int>(n, 0));
    
    dp[0][0] = grid[0][0];
    for (int i = 1; i < m; i++) dp[i][0] = dp[i - 1][0] + grid[i][0];
    for (int j = 1; j < n; j++) dp[0][j] = dp[0][j - 1] + grid[0][j];
    
    for (int i = 1; i < m; i++) {
        for (int j = 1; j < n; j++) {
            dp[i][j] = grid[i][j] + min(dp[i - 1][j], dp[i][j - 1]);
        }
    }
    return dp[m - 1][n - 1];
}

```

## 7. Key Considerations in DP

- **State Definition**: Clearly define what each `dp[i]` or `dp[i][j]` represents.
- **State Transition**: Identify how the current state can be calculated from previous states.
- **Base Case**: Properly initialize base cases for the recurrence.
- **Top-Down vs Bottom-Up**: Choose memoization (top-down) for problems with fewer distinct states and tabulation (bottom-up) for problems where all states need to be solved.
- **Space Optimization**: Reduce the space complexity by reusing previous states if possible.
