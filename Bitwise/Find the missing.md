https://www.geeksforgeeks.org/find-the-missing-number/

    int MissingNumber(vector<int>& a, int n) {


    int n_elements_sum = n * (n + 1) / 2;
    int sum = 0;

    for (int i = 0; i < n - 1; i++)
        sum += a[i];
    return n_elements_sum - sum;


    }
# Find the Missing Number

-   Difficulty Level : [Easy](https://www.geeksforgeeks.org/easy/)
-   Last Updated : 27 Apr, 2022

You are given a list of n-1 integers and these integers are in the range of 1 to n. There are no duplicates in the list. One of the integers is missing in the list. Write an efficient code to find the missing integer.  
**Example:** 

**Input:** arr[] = {1, 2, 4, 6, 3, 7, 8}
**Output:** 5
**Explanation:** The missing number from 1 to 8 is 5

**Input:** arr[] = {1, 2, 3, 5}
**Output:** 4
**Explanation:** The missing number from 1 to 5 is 4

[Recommended PracticeMissing number in arrayTry It!](https://practice.geeksforgeeks.org/problems/missing-number-in-array1416/1/)

**Method 1:** This method uses the technique of the summation formula. 

-   **Approach:** The length of the array is n-1. So the sum of all n elements, i.e sum of numbers from 1 to n can be calculated using the formula _n*(n+1)/2_. Now find the sum of all the elements in the array and subtract it from the sum of first n natural numbers, it will be the value of the missing element.
-   **Algorithm:** 
    1.  Calculate the sum of first n natural numbers as _sumtotal= n*(n+1)/2_
    2.  Create a variable sum to store the sum of array elements.
    3.  Traverse the array from start to end.
    4.  Update the value of sum as _sum = sum + array[i]_
    5.  Print the missing number as _sumtotal – sum_
-   **Implementation:**

-   C++14
-   C
-   Java
-   Python
-   C#
-   PHP
-   Javascript

`#include <bits/stdc++.h>`

`using` `namespace` `std;`

`// Function to get the missing number`

`int` `getMissingNo(``int` `a[],` `int` `n)`

`{`

    `int` `total = (n + 1) * (n + 2) / 2;`

    `for` `(``int` `i = 0; i < n; i++)`

        `total -= a[i];`

    `return` `total;`

`}`

`// Driver Code`

`int` `main()`

`{`

    `int` `arr[] = { 1, 2, 4, 5, 6 };`

    `int` `n =` `sizeof``(arr) /` `sizeof``(arr[0]);`

    `int` `miss = getMissingNo(arr, n);`

    `cout << miss;`

`}`

**Output**

3

-   **Complexity Analysis:** 
    -   **Time Complexity:** O(n).   
        Only one traversal of the array is needed.
    -   **Space Complexity:** O(1).   
        No extra space is needed

**Modification for Overflow**  

-   **Approach:** The approach remains the same but there can be overflow if n is large. In order to avoid integer overflow, pick one number from known numbers and subtract one number from given numbers. This way there won’t have Integer Overflow ever.
-   **Algorithm:** 
    1.  Create a variable _sum = 1_ which will store the missing number and a counter variable _c = 2_.
    2.  Traverse the array from start to end.
    3.  Update the value of sum as _sum = sum – array[i] + c_ and update c as _c++_.
    4.  Print the missing number as a _sum_.

-   C++
-   C
-   Java
-   Python3
-   C#
-   Javascript

`#include <bits/stdc++.h>`

`using` `namespace` `std;`

`int` `getMissingNo(``int` `a[],` `int` `n)`

`{`

    `int` `i, total = 1;`

    `for` `(i = 2; i <= (n + 1); i++) {`

        `total += i;`

        `total -= a[i - 2];`

    `}`

    `return` `total;`

`}`

`// Driver Program`

`int` `main()`

`{`

    `int` `arr[] = { 1, 2, 3, 5 };`

    `cout << getMissingNo(arr,` `sizeof``(arr) /` `sizeof``(arr[0]));`

    `return` `0;`

`}`

`// This code is contributed by Aditya Kumar (adityakumar129)`

**Output:** 

4

-   **Complexity Analysis:** 
    -   **Time Complexity:** O(n).   
        Only one traversal of the array is needed.
    -   **Space Complexity:**O(1).   
        No extra space is needed

_Thanks to Sahil Rally for suggesting this improvement._  
**Method 2:** This method uses the technique of XOR to solve the problem.  

-   **Approach:**   
    _XOR has certain properties_ 
    -   Assume a1 ^ a2 ^ a3 ^ …^ an = a and a1 ^ a2 ^ a3 ^ …^ an-1 = b
    -   Then a ^ b = an
-   **Algorithm:** 
    1.  Create two variables _a = 0_ and _b = 0_
    2.  Run a loop from 1 to n with i as counter.
    3.  For every index update _a_ as _a = a ^ i_
    4.  Now traverse the array from start to end.
    5.  For every index update _b_ as _b = b ^ array[i]_
    6.  Print the missing number as _a ^ b_.
-   **Implementation:**

-   C++
-   C
-   Java
-   Python3
-   C#
-   PHP
-   Javascript

`#include <bits/stdc++.h>`

`using` `namespace` `std;`

`// Function to get the missing number`

`int` `getMissingNo(``int` `a[],` `int` `n)`

`{`

    `// For xor of all the elements in array`

    `int` `x1 = a[0];`

    `// For xor of all the elements from 1 to n+1`

    `int` `x2 = 1;`

    `for` `(``int` `i = 1; i < n; i++)`

        `x1 = x1 ^ a[i];`

    `for` `(``int` `i = 2; i <= n + 1; i++)`

        `x2 = x2 ^ i;`

    `return` `(x1 ^ x2);`

`}`

`// Driver Code`

`int` `main()`

`{`

    `int` `arr[] = { 1, 2, 4, 5, 6 };`

    `int` `n =` `sizeof``(arr) /` `sizeof``(arr[0]);`

    `int` `miss = getMissingNo(arr, n);`

    `cout << miss;`

`}`

**Output:** 

3

-   **Complexity Analysis:** 
    -   **Time Complexity:** O(n).   
        Only one traversal of the array is needed.
    -   **Space Complexity:** O(1).   
        No extra space is needed.

**Method 3:** This method will work only in python.   
**Approach:**   
Take the sum of all elements in the array and subtract that from the sum of n+1 elements. For Eg:   
If my elements are li=[1,2,4,5] then take the sum of all elements in li and subtract that from the sum of len(li)+1 elements. The following code shows the demonstration. 

-   C++
-   C
-   Java
-   Python3
-   C#
-   Javascript

`// C++ program to find the missing Number`

`#include <bits/stdc++.h>`

`using` `namespace` `std;`

`// getMissingNo takes list as argument`

`int` `getMissingNo(``int` `a[],` `int` `n)`

`{`

    `int` `n_elements_sum = n * (n + 1) / 2;`

    `int` `sum = 0;`

    `for` `(``int` `i = 0; i < n - 1; i++)`

        `sum += a[i];`

    `return` `n_elements_sum - sum;`

`}`

`// Driver code`

`int` `main()`

`{`

    `int` `a[] = { 1, 2, 4, 5, 6 };`

    `int` `n =` `sizeof``(a) /` `sizeof``(a[0]) + 1;`

    `int` `miss = getMissingNo(a, n);`

    `cout << (miss);`

    `return` `0;`

`}`

`// This code is contributed by Aditya Kumar (adityakumar129)`

**Output:**

3

_**Time Complexity:** O(n)_

_**Auxiliary Space:** O(1)_  
Please write comments if you find anything incorrect, or you want to share more information about the topic discussed above.