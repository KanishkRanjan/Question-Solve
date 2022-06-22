Given an integer **N** and an integer **D**, **rotate the binary representation** of the integer **N by D** digits to the **left** as well as **right** and print the **results** in **decimal values** after each of the rotation.  
**Note**: Integer N is stored using **16 bits**. i.e. 12 will be stored as 0000.....001100.


**Input:**
N = 28, D = 2
**Output:**
112
7
**Explanation**: 28 in Binary is:
000...011100
Rotating left by 2 positions, it becomes
00...1110000 = 112 (in decimal).
Rotating right by 2 positions, it becomes
000...000111 = 7 (in decimal).



```
// C++ code to rotate bits
// of number
#include<iostream>

using namespace std;
#define INT_BITS 32
class gfg
{
	
/*Function to left rotate n by d bits*/
public:
int leftRotate(int n, unsigned int d)
{
	
	/* In n<<d, last d bits are 0. To
	put first 3 bits of n at
	last, do bitwise or of n<<d
	with n >>(INT_BITS - d) */
	return (n << d)|(n >> (INT_BITS - d));
}

/*Function to right rotate n by d bits*/
int rightRotate(int n, unsigned int d)
{
	/* In n>>d, first d bits are 0.
	To put last 3 bits of at
	first, do bitwise or of n>>d
	with n <<(INT_BITS - d) */
	return (n >> d)|(n << (INT_BITS - d));
}
};

/* Driver code*/
int main()
{
	gfg g;
	int n = 16;
	int d = 2;
	cout << "Left Rotation of " << n <<
			" by " << d << " is ";
	cout << g.leftRotate(n, d);
	cout << "\nRight Rotation of " << n <<
			" by " << d << " is ";
	cout << g.rightRotate(n, d);
	getchar();
}

// This code is contributed by SoM15242

```
