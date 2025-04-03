# Longest Common Subsequence (LCS)

This repository contains a C++ implementation of the Longest Common Subsequence (LCS) problem. The goal of the LCS problem is to find the length of the longest subsequence that is common to two sequences.

## Problem Statement

Given two sequences (strings) `X` and `Y`, the task is to find the length of the longest common subsequence.

### Input
- Two strings `X` and `Y`.

### Output
- The length of the longest common subsequence.

## Code Explanation

The implementation uses a dynamic programming approach to solve the problem. The main steps are as follows:

1. **Initialization**: A 2D array `dp` is created where `dp[i][j]` represents the length of the longest common subsequence of the first `i` characters of `X` and the first `j` characters of `Y`.

2. **DP Table Construction**:
   - Iterate through each character of both strings.
   - If `X[i-1] == Y[j-1]`, then `dp[i][j] = dp[i-1][j-1] + 1`.
   - Otherwise, `dp[i][j] = max(dp[i-1][j], dp[i][j-1])`.

3. **Result**: The length of the longest common subsequence is found in `dp[m][n]`, where `m` and `n` are the lengths of `X` and `Y`, respectively.

## Code

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <algorithm>

using namespace std;

// Function to find the length of the Longest Common Subsequence
int longestCommonSubsequence(const string& X, const string& Y) {
    int m = X.length();
    int n = Y.length();

    // Create a DP table with dimensions (m+1) x (n+1)
    vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));

    // Fill the DP table
    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (X[i - 1] == Y[j - 1]) {
                dp[i][j] = dp[i - 1][j - 1] + 1; // Characters match
            } else {
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]); // Take the maximum
            }
        }
    }

    // The length of the longest common subsequence is in dp[m][n]
    return dp[m][n];
}

int main() {
    string X = "AGGTAB";
    string Y = "GXTXAYB";

    int length = longestCommonSubsequence(X, Y);
    cout << "Length of Longest Common Subsequence: " << length << endl;

    return 0;
}
