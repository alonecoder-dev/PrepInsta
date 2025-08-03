
-----

# Strong Password Checker

## Problem Statement 🧑‍💻

A national bank requires a tool to audit customer passwords based on a "strong password policy." The tool must calculate the **minimum number of steps** (insert, delete, or replace a character) needed to make a given password strong.

A strong password must meet these criteria:

  * **Length**: It must be between **6** and **20** characters long.
  * **Character Types**: It must contain at least one **lowercase letter**, one **uppercase letter**, and one **digit**.
  * **No Repeating Characters**: It must not contain three or more consecutive identical characters (e.g., `aaa` is invalid).

-----

## Constraints

  * `1 <= password.length <= 50`
  * `password` consists of letters, digits, `.` or `!`.

-----

## Solution Overview

The goal is to find the minimum number of operations by optimally combining fixes for three types of violations:

1.  **Missing Character Classes**: Lacking a lowercase, uppercase, or digit.
2.  **Repeated Characters**: Runs of 3 or more identical characters (e.g., `aaaa`).
3.  **Invalid Length**: Too short (`< 6`) or too long (`> 20`).

The logic is handled separately for three length-based cases.

### Notation

  * $n$: The current length of the password.
  * `missingType`: The number of missing character types (0 to 3).
  * `replaceNeed`: The number of replacements needed to break all consecutive repeating character sequences. For a run of length $L$, this is $\\lfloor L/3 \\rfloor$.

### Case 1: Length \< 6

Here, we only need to consider insertions and replacements. An insertion can potentially fix a missing character type and shorten a repeat run simultaneously. The minimum steps will be the maximum of the changes required.

  * **`insertNeed`**: $6 - n$
  * **`answer`**: $\\max(\\text{missingType, insertNeed})$

*Note: The original text had `max(missingType, insertNeed, replaceNeed)`. However, an insertion is always better than a replacement for short passwords because it also helps satisfy the length requirement. The number of replacements needed for repeats is implicitly handled by the `insertNeed` and `missingType` counts. The most efficient approach uses insertions that simultaneously add missing character types.*

### Case 2: 6 ≤ Length ≤ 20

The length is valid, so we only need to fix missing character types and repeating characters. Since insertions or deletions are not required, we use replacements.

  * **`answer`**: $\\max(\\text{missingType, replaceNeed})$

### Case 3: Length \> 20

We must perform `overLen = n - 20` deletions. These deletions can be used strategically to reduce the `replaceNeed`.

1.  **Greedy Deletions**: Prioritize using deletions on repeating character runs to gain the most benefit.
      * Deleting 1 character from a run of length $L$ where $L \\pmod 3 = 0$ saves one replacement.
      * Deleting 2 characters from a run of length $L$ where $L \\pmod 3 = 1$ saves one replacement.
      * Deleting 3 characters from any run saves one replacement.
2.  **Final Calculation**: After using all `overLen` deletions, the total steps are the initial deletions plus the remaining fixes.
      * **`answer`**: `overLen` + $\\max(\\text{missingType, remainingReplacementNeed})$

The overall complexity is $O(n)$ time and $O(n)$ space.

-----

## C++ Implementation

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <numeric>
#include <algorithm>

using namespace std;

int strongPasswordChecker(string password) {
    int n = password.length();
    int missingType = 3;
    if (any_of(password.begin(), password.end(), ::islower)) missingType--;
    if (any_of(password.begin(), password.end(), ::isupper)) missingType--;
    if (any_of(password.begin(), password.end(), ::isdigit)) missingType--;

    vector<int> repeats;
    for (int i = 0; i < n; ) {
        int j = i;
        while (j < n && password[i] == password[j]) {
            j++;
        }
        if (j - i >= 3) {
            repeats.push_back(j - i);
        }
        i = j;
    }

    if (n < 6) {
        int insertNeed = 6 - n;
        return max(missingType, insertNeed);
    } 
    
    if (n <= 20) {
        int replaceNeed = 0;
        for (int len : repeats) {
            replaceNeed += len / 3;
        }
        return max(missingType, replaceNeed);
    }

    int overLen = n - 20;
    int deletions = overLen;
    int replaceNeed = 0;

    // Use deletions to reduce replacements
    for (int i = 0; i < repeats.size() && deletions > 0; ++i) {
        if (repeats[i] % 3 == 0) {
            repeats[i]--;
            deletions--;
        }
    }
    for (int i = 0; i < repeats.size() && deletions > 0; ++i) {
        if (repeats[i] % 3 == 1) {
            int d = min(deletions, 2);
            repeats[i] -= d;
            deletions -= d;
        }
    }

    for (int len : repeats) {
        if (len >= 3 && deletions > 0) {
            int d = min(deletions, len - 2);
            len -= d;
            deletions -= d;
        }
        if (len >= 3) {
            replaceNeed += len / 3;
        }
    }

    return overLen + max(missingType, replaceNeed);
}

int main() {
    string password;
    cin >> password;
    cout << strongPasswordChecker(password) << endl;
    return 0;
}
```

-----

## Examples

  * **Input**: `a`

      * $n=1$, `missingType=2` (uppercase, digit), `insertNeed=5`.
      * **Output**: `max(2, 5) = 5`

  * **Input**: `aA1`

      * $n=3$, `missingType=0`, `insertNeed=3`.
      * **Output**: `max(0, 3) = 3`

  * **Input**: `1337C0d3`

      * $n=8$, `missingType=0`, no repeats. Length is valid.
      * **Output**: `0`

-----

-----

# Reverse Signed 32-bit Integer

## Problem Statement 🏦

For a legacy ATM system using a 32-bit architecture, you need to reverse the digits of a customer's PIN, which is stored as a signed 32-bit integer. You **cannot use 64-bit integers** for any part of the calculation.

The algorithm must ensure:

  * The **sign** of the original number is preserved.
  * If the reversed number overflows the signed 32-bit integer range, the function must return **0**.

-----

## Constraints

  * The input `x` is a signed 32-bit integer: $-2^{31} \\le x \\le 2^{31} - 1$.

-----

## C++ Implementation & Explanation

This compact C++ solution reverses the integer while staying entirely within the 32-bit domain by checking for potential overflow **before** performing the multiplication.

```cpp
#include <iostream>
#include <climits> // For INT_MAX, INT_MIN

using namespace std;

int reverseInt(int x) {
    int reversed_num = 0;
    while (x != 0) {
        int digit = x % 10;
        x /= 10;

        // Check for overflow before multiplying `reversed_num` by 10
        if (reversed_num > INT_MAX / 10 || (reversed_num == INT_MAX / 10 && digit > 7)) {
            return 0;
        }
        // Check for underflow before multiplying `reversed_num` by 10
        if (reversed_num < INT_MIN / 10 || (reversed_num == INT_MIN / 10 && digit < -8)) {
            return 0;
        }
        
        reversed_num = reversed_num * 10 + digit;
    }
    return reversed_num;
}

int main() {
    int x;
    cin >> x;
    cout << reverseInt(x) << endl;
    return 0;
}
```

### How It Works

1.  **Extract Digit**: It pops the last digit using the modulo operator (`x % 10`) and shrinks the original number using integer division (`x /= 10`).
2.  **Pre-emptive Overflow Check**: Before the critical `reversed_num * 10 + digit` step, it checks if this operation would overflow.
      * **Positive Overflow**: The maximum 32-bit signed integer is $2,147,483,647$. The check `rev > INT_MAX / 10` handles cases where `rev` is already too large. If `rev == INT_MAX / 10` (which is 214748364), the next digit cannot be greater than 7.
      * **Negative Underflow**: The minimum is $-2,147,483,648$. Similar logic applies, but with `INT_MIN` and a check for a digit less than -8.
3.  **Return Value**: If no overflow is detected, it updates `reversed_num` and continues the loop. If an overflow would occur, it immediately returns `0`, fulfilling the requirement.

This method cleverly avoids intermediate values that would exceed the 32-bit range, making it safe for the constrained ATM environment.

-----

## Examples

  * **Input**: `123`

      * Reverses to `321`.
      * **Output**: `321`

  * **Input**: `-123`

      * Reverses to `-321`.
      * **Output**: `-321`

  * **Input**: `120`

      * Reverses to `021`, which is `21`.
      * **Output**: `21`