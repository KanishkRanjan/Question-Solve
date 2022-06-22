## Find the Missing Number
```
int getMissingNo( int a[], int n)

{

    // For xor of all the elements in array

    int x1 = a[0];

    // For xor of all the elements from 1 to n+1

   	int x2 = 1;

    for (int i = 1; i < n; i++)
		x1 = x1 ^ a[i];

    for(int i = 2; i <= n + 1; i++)
		x2 = x2 ^ i;

    return (x1 ^ x2);`
}
```

## How to swap two numbers without using a temporary variable?

```
// C++ code to swap using XOR
#include <bits/stdc++.h>

using namespace std;

int main()
{
	int x = 10, y = 5;
	// Code to swap 'x' (1010) and 'y' (0101)
	x = x ^ y; // x now becomes 15 (1111)
	y = x ^ y; // y becomes 10 (1010)
	x = x ^ y; // x becomes 5 (0101)
	cout << "After Swapping: x =" << x << ", y=" << y;
	return 0;
}

// This code is contributed by mohit kumar.

```

## Find the two non-repeating elements in an array of repeating elements/ Unique Numbers 2

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

/* This function sets the values of
*x and *y to non-repeating elements
in an array arr[] of size n*/
void get2NonRepeatingNos(int arr[], int n, int* x, int* y)
{
	/* Will hold Xor of all elements */
	int Xor = arr[0];

	/* Will have only single set bit of Xor */
	int set_bit_no;
	int i;
	*x = 0;
	*y = 0;

	/* Get the Xor of all elements */
	for (i = 1; i < n; i++)
		Xor ^= arr[i];

	/* Get the rightmost set bit in set_bit_no */
	set_bit_no = Xor & ~(Xor - 1);

	/* Now divide elements in two sets by
	comparing rightmost set bit of Xor with bit
	at same position in each element. */
	for (i = 0; i < n; i++) {

		/*Xor of first set */
		if (arr[i] & set_bit_no)
			*x = *x ^ arr[i];
		/*Xor of second set*/
		else {
			*y = *y ^ arr[i];
		}
	}
}

/* Driver code */
int main()
{
	int arr[] = { 2, 3, 7, 9, 11, 2, 3, 11 };
	int n = sizeof(arr) / sizeof(*arr);
	int* x = new int[(sizeof(int))];
	int* y = new int[(sizeof(int))];
	get2NonRepeatingNos(arr, n, x, y);
	cout << "The non-repeating elements are " << *x
		<< " and " << *y;
}

// This code is contributed by rathbhupendra
```


## Detect if two integers have opposite signs

Let the given integers be x and y. The sign bit is 1 in negative numbers, and 0 in positive numbers. The XOR of x and y will have the sign bit as 1 iff they have opposite sign. In other words, XOR of x and y will be negative number number iff x and y have opposite signs. The following code use this logic.

```
// C++ Program to Detect
// if two integers have opposite signs.
#include<iostream>
using namespace std;

bool oppositeSigns(int x, int y)
{
	return ((x ^ y) < 0);
}

int main()
{
	int x = 100, y = -100;
	if (oppositeSigns(x, y) == true)
	cout << "Signs are opposite";
	else
	cout << "Signs are not opposite";
	return 0;
}

// this code is contributed by shivanisinghss2110
```
