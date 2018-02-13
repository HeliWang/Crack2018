# 2 Keys Keyboard

Initially on a notepad only one character 'A' is present. You can perform two operations on this notepad for each step:

1. `Copy All`: You can copy all the characters present on the notepad \(partial copy is not allowed\).
2. `Paste`: You can paste the characters which are copied **last time**.

Given a number`n`. You have to get**exactly**`n`'A' on the notepad by performing the minimum number of steps permitted. Output the minimum number of steps to get`n`'A'.

**Example 1:**

```
Input: 3
Output: 3
Explanation:
Intitally, we have one character 'A'.
In step 1, we use Copy All operation.
In step 2, we use Paste operation to get 'AA'.
In step 3, we use Paste operation to get 'AAA'.
```

**Solution:**

```cpp
int minSteps(int n) {
    vector<int> dp(n + 1, 0);
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j < i; j++) {
            if (i % j == 0) {
                dp[i] = dp[j] + i / j;
            }
        }
    }
    return dp[n];
}
```





# 4 Keys Keyboard

Imagine you have a special keyboard with the following keys:

`Key 1: (A)`: Print one 'A' on screen.

`Key 2: (Ctrl-A)`: Select the whole screen.

`Key 3: (Ctrl-C)`: Copy selection to buffer.

`Key 4: (Ctrl-V)`: Print buffer on screen appending it after what has already been printed.

Now, you can only press the keyboard for**N**times \(with the above four keys\), find out the maximum numbers of 'A' you can print on screen.

```
Input: N = 3
Output: 3
Explanation: 
We can at most get 3 A's on screen by pressing following key sequence:
A, A, A
```

```
Input: N = 7
Output: 9
Explanation: 
We can at most get 9 A's on screen by pressing following key sequence:
A, A, A, Ctrl A, Ctrl C, Ctrl V, Ctrl V
```

**Solution:**

```cpp
int maxA(int N) {
    vector<int> dp (N + 1, 0);
    for (int i = 1; i <= N; i++) {
        dp[i] = max(dp[i], dp[i-1] + 1);
        for (int j = 1; j < i - 2; j++) {
            dp[i] = max(dp[i], dp[j]*(i-j-1));
            
        }
    }
    return dp[N];
}
```



