```
// A O(n) C++ program to count number of
// substrings starting and ending with 1
#include<iostream>

using namespace std;

int countSubStr(char str[])
{
int m = 0; // Count of 1's in input string

// Traverse input string and count of 1's in it
for (int i=0; str[i] !='\0'; i++)
{
		if (str[i] == '1')
		m++;
}

// Return count of possible pairs among m 1's
return m*(m-1)/2;
}

// Driver program to test above function
int main()
{
char str[] = "00100101";
cout << countSubStr(str);
return 0;
}
```
