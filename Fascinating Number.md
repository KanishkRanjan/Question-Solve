# Fascinating Number

-   Difficulty Level : [Medium](https://www.geeksforgeeks.org/medium/)
-   Last Updated : 14 May, 2021

Given a number N, the task is to check whether it is fascinating or not.   
**Fascinating Number**: When a number( 3 digits or more ) is multiplied by 2 and 3, and when both these products are concatenated with the original number, then it results in all digits from 1 to 9 present exactly once. There could be any number of zeros and are ignored.   
**Examples:**   
 

> **Input:** 192   
> **Output:** Yes   
> After multiplication with 2 and 3, and concatenating with original number, resultant number is 192384576 which contains all digits from 1 to 9.  
> **Input:** 853   
> **Output:** No   
> After multiplication with 2 and 3, and concatenating with original number, the resultant number is 85317062559. In this, number 4 is missing and the number 5 has appeared multiple times.   
>  

[Recommended: Please solve it on “_**PRACTICE**_ ” first, before moving on to the solution.](https://practice.geeksforgeeks.org/problems/fascinating-number/0)   
 

**Approach**:   
 

1.  Check if the given number has three digits or more. If not, print No.
2.  Else, Multiply the given number with 2 and 3.
3.  Concatenate these products with the given number to form a string.
4.  Traverse this string, keep the frequency count of the digits.
5.  Print No if any digit is missing or has appeared multiple times.
6.  Else, print Yes.

Below is the implementation of above approach:   
 

`// C++ program to implement`

`// fascinating number`

`#include <bits/stdc++.h>`

`using` `namespace` `std;`

`// function to check if number`

`// is fascinating or not`

`bool` `isFascinating(``int` `num)`

`{`

    `// frequency count array`

    `// using 1 indexing`

    `int` `freq[10] = {0};`

    `// obtaining the resultant number`

    `// using string concatenation`

    `string val =` `""` `+ to_string(num) +`

                      `to_string(num * 2) +`

                      `to_string(num * 3);`

    `// Traversing the string`

    `// character by character`

    `for` `(``int` `i = 0; i < val.length(); i++)`

    `{`

        `// gives integer value of`

        `// a character digit`

        `int` `digit = val[i] -` `'0'``;`

        `// To check if any digit has`

        `// appeared multiple times`

        `if` `(freq[digit] and digit != 0 > 0)`

            `return` `false``;`

        `else`

            `freq[digit]++;`

    `}`

    `// Traversing through freq array to`

    `// check if any digit was missing`

    `for` `(``int` `i = 1; i < 10; i++)`

    `{`

        `if` `(freq[i] == 0)`

            `return` `false``;`

    `}`

    `return` `true``;`

`}`

`// Driver code`

`int` `main()`

`{`

    `// Input number`

    `int` `num = 192;`

    `// Not a valid number`

    `if` `(num < 100)`

        `cout <<` `"No"` `<< endl;`

    `else`

    `{`

        `// Calling the function to`

        `// check if input number`

        `// is fascinating or not`

        `bool` `ans = isFascinating(num);`

        `if` `(ans)`

            `cout <<` `"Yes"``;`

        `else`

            `cout <<` `"No"``;`

    `}`

`}`

`// This code is contributed`

`// by Subhadeep`

**Output:** 

Yes