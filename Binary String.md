# Given a binary string, count number of substrings that start and end with 1.
A **Simple Solution** is to run two loops. Outer loops picks every 1 as starting point and inner loop searches for ending 1 and increments count whenever it finds 1.


```
// A simple C++ program to count number of
// substrings starting and ending with 1
#include<iostream>

using namespace std;

int countSubStr(char str[])
{
int res = 0; // Initialize result

// Pick a starting point
for (int i=0; str[i] !='\0'; i++)
{
		if (str[i] == '1')
		{
			// Search for all possible ending point
			for (int j=i+1; str[j] !='\0'; j++)
			if (str[j] == '1')
				res++;
		}
}
return res;
}

// Driver program to test above function
int main()
{
char str[] = "00100101";
cout << countSubStr(str);
return 0;
}
```
