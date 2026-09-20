# EX 4A Kadane's Algorithm - Dynamic Programming

## DATE: 18-08-2026

## AIM:

To write a Java program to compute the maximum net energy that can be collected from any contiguous block of buildings arranged in a circular grid using **Kadane’s Algorithm**.

The buildings either generate or consume energy. Since the grid is circular, the maximum subarray sum may wrap around the end to the beginning.

---

## Algorithm:

1. Read the number of buildings `n` and the net energy values.
2. Use **Kadane’s Algorithm** to find the maximum subarray sum (non-circular case).
3. Use **Kadane’s Algorithm (inverted)** to find the minimum subarray sum.
4. Compute the total sum of all energy values.
5. If all values are negative, return the maximum value directly.
6. Otherwise, compute the maximum circular sum as
   `totalSum - minSum`.
7. The answer is the maximum of:

   * Normal maximum subarray sum
   * Circular maximum subarray sum
8. Print the result.

---

## Program:

```java
/*
Kadane's Algorithm
Developed by: Ligneshwar K
Register Number: 212223230113
*/

import java.util.*;

public class SolarEnergyMaximizer {

    public static int maxCircularEnergy(int[] energy) {
        int totalSum = 0;
        int maxSum = energy[0];
        int currMax = energy[0];
        int minSum = energy[0];
        int currMin = energy[0];

        for (int i = 1; i < energy.length; i++) {
            int val = energy[i];
            currMax = Math.max(val, currMax + val);
            maxSum = Math.max(maxSum, currMax);

            currMin = Math.min(val, currMin + val);
            minSum = Math.min(minSum, currMin);

            totalSum += val;
        }
        totalSum += energy[0];

        if (maxSum < 0) return maxSum;
        return Math.max(maxSum, totalSum - minSum);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] energy = new int[n];
        for (int i = 0; i < n; i++) {
            energy[i] = sc.nextInt();
        }
        System.out.println(maxCircularEnergy(energy));
    }
}
```

---

## Output:

<img width="858" height="273" alt="image" src="https://github.com/user-attachments/assets/ae9d6938-7e5f-4e86-8c66-afafdd877030" />

---

## Result:

The program was successfully implemented using Kadane’s Algorithm and the output was verified.

# EX 4B Frog Jump - Dynamic Programming

## DATE: 20-08-2026

## AIM:

To write a Java program for the given constraints to compute the number of distinct ways a frog can reach the n-th step by jumping either 1 or 2 steps at a time.

The solution must be implemented using **Dynamic Programming**.

---

## Algorithm:

1. Read the value of `n` (number of steps).
2. If `n` is 0 or 1, return 1 (only one way).
3. Create an array `dp[]` of size `n + 1`.
4. Initialise `dp[0] = 1` and `dp[1] = 1`.
5. For each step from 2 to n, compute:
   `dp[i] = dp[i − 1] + dp[i − 2]`
6. The final answer is stored in `dp[n]`.
7. Print the result.

---

## Program:

```java
/*
Frog Jump
Developed by: Ligneshwar K
Register Number: 212223230113
*/

import java.util.Scanner;

public class FrogJump {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        scanner.close();
        System.out.println(countWays(n));
    }

    public static int countWays(int n) {
        if (n <= 1) return 1;
        int[] dp = new int[n + 1];
        dp[0] = 1;
        dp[1] = 1;
        for (int i = 2; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        return dp[n];
    }
}
```

---

## Output:

<img width="516" height="245" alt="image" src="https://github.com/user-attachments/assets/ce873ee1-d03e-41aa-9960-d13896c3d00a" />

---

## Result:

The program was successfully implemented using Dynamic Programming and the expected output was verified.

If you want, I can prepare **EX 4C, 4D** also.

# EX 4C Coin Change Problem - Dynamic Programming

## DATE: 21-08-2026

## AIM:

To write a Java program to find the minimum number of coins required to make a given amount using the **Coin Change Dynamic Programming approach**.
If the given amount cannot be formed using the available denominations, return **-1**.

---

## Algorithm:

1. Read the coin denominations array and the target amount.
2. Create a DP array `dp[]` of size `amount + 1`, filled with a large value (amount + 1).
3. Set `dp[0] = 0` because 0 coins are needed to make amount 0.
4. For each amount `i` from 1 to `amount`, check each coin:

   * If `coin <= i`, update
     `dp[i] = min(dp[i], dp[i - coin] + 1)`
5. After filling the DP table:

   * If `dp[amount]` is still greater than amount, return **-1**.
   * Else return `dp[amount]`.
6. Print the result.

---

## Program:

```java
/*
Coin Change using Dynamic Programming
Developed by: Ligneshwar K
Register Number: 212223230113
*/

import java.util.*;

public class Solution {
    public int coinChange(int[] coins, int amount) {
        int max = amount + 1;
        int[] dp = new int[amount + 1];
        Arrays.fill(dp, max);
        dp[0] = 0;

        for (int i = 1; i <= amount; i++) {
            for (int coin : coins) {
                if (coin <= i) {
                    dp[i] = Math.min(dp[i], dp[i - coin] + 1);
                }
            }
        }
        return dp[amount] > amount ? -1 : dp[amount];
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Solution solution = new Solution();

        String coinsLine = scanner.nextLine();
        String amountLine = scanner.nextLine();

        coinsLine = coinsLine.replaceAll("[^0-9,]", "");
        String[] coinsStr = coinsLine.split(",");
        int[] coins = new int[coinsStr.length];

        for (int i = 0; i < coinsStr.length; i++) {
            coins[i] = Integer.parseInt(coinsStr[i]);
        }

        int amount = Integer.parseInt(amountLine.replaceAll("[^0-9]", ""));
        int result = solution.coinChange(coins, amount);
        System.out.println(result);

        scanner.close();
    }
}
```

---

## Output:

<img width="601" height="357" alt="image" src="https://github.com/user-attachments/assets/04a38571-9a3c-4824-b424-592b48322b56" />


## Result:

The program was successfully implemented using Dynamic Programming, and the expected output was verified.

---

If you want **EX 4D** also prepared, just tell me!

# EX 4D Longest Common SubSequence - Dynamic Programming

## DATE: 26-08-2026

## AIM:

To write a Java program to find the length of the **Longest Common Subsequence (LCS)** between two given strings using **Dynamic Programming**.

---

## Algorithm:

1. Read the two input strings `text1` and `text2`.
2. Create a 2D DP matrix `dp[m+1][n+1]` where `m` and `n` are the lengths of the strings.
3. Fill the DP table from bottom-right to top-left:

   * If characters match:
     `dp[i][j] = 1 + dp[i+1][j+1]`
   * Else:
     `dp[i][j] = max(dp[i+1][j], dp[i][j+1])`
4. The value at `dp[0][0]` gives the length of the LCS.
5. Print the result.

---

## Program:

```java
/*
Program to implement Longest Common SubSequence
Developed by: Ligneshwar K
Register Number: 212223230113
*/

import java.util.Scanner;

public class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        int[][] dpGrid = new int[text1.length() + 1][text2.length() + 1];

        for (int col = text2.length() - 1; col >= 0; col--) {
            for (int row = text1.length() - 1; row >= 0; row--) {
                if (text1.charAt(row) == text2.charAt(col)) {
                    dpGrid[row][col] = 1 + dpGrid[row + 1][col + 1];
                } else {
                    dpGrid[row][col] = Math.max(dpGrid[row + 1][col], dpGrid[row][col + 1]);
                }
            }
        }
        return dpGrid[0][0];
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Solution sol = new Solution();

        String text1 = sc.nextLine().replaceAll("\"", "");
        String text2 = sc.nextLine().replaceAll("\"", "");

        int lcsLength = sol.longestCommonSubsequence(text1, text2);
        System.out.println("Length of Longest Common Subsequence: " + lcsLength);

        sc.close();
    }
}
```

---

## Output:

<img width="1152" height="297" alt="image" src="https://github.com/user-attachments/assets/43c9f0ba-d6fe-4de2-9777-310b89646bd1" />

---

## Result:

The program was successfully implemented using Dynamic Programming and the expected output was verified.

# EX 4E Longest Increasing Subsequence – Dynamic Programming

## DATE: 27-08-2026

## AIM:

To write a Java program to compute the length of the **Longest Increasing Subsequence (LIS)** in a given integer array using **Dynamic Programming**.

---

## Algorithm:

1. Read the array size `n` and the array elements.
2. Create a DP array `dp[]` of size `n`, initialized with 1 (each number is an LIS of length 1).
3. For each index `i` from 1 to n−1:

   * Check previous elements `j` from 0 to i−1.
   * If `nums[i] > nums[j]`, update
     `dp[i] = max(dp[i], dp[j] + 1)`
4. Find the maximum value in the DP array — this is the LIS length.
5. Print the result.

---

## Program:

```java
/*
Program to implement Reverse a String
Developed by: Ligneshwar K
Register Number: 212223230113
*/

import java.util.*;

public class LongestIncreasingSubsequence {
    public static int lengthOfLIS(int[] nums) {
        int[] dp = new int[nums.length];
        Arrays.fill(dp, 1);

        for (int i = 1; i < nums.length; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[i] > nums[j]) {
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                }
            }
        }

        int longest = 0;
        for (int c : dp) {
            longest = Math.max(longest, c);
        }
        return longest;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int[] nums = new int[n];

        for (int i = 0; i < n; i++) {
            nums[i] = scanner.nextInt();
        }

        int result = lengthOfLIS(nums);
        System.out.println("Length of Longest Increasing Subsequence: " + result);

        scanner.close();
    }
}
```

---

## Output:

<img width="1203" height="282" alt="image" src="https://github.com/user-attachments/assets/84789017-ea66-4602-b337-e272c483b622" />

---

## Result:

The program was successfully implemented using Dynamic Programming and the expected output was verified.

---
