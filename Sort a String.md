Given a string consisting of lowercase letters, arrange all its letters in ascending order.
**Example 1:**

**Input:**
S = "edcab"
**Output:** "abcde"
**Explanation:** characters are in ascending
order in "abcde".

**Example 2:**

**Input:**
S = "xzy"
**Output:** "xyz"
**Explanation:** characters are in ascending
order in "xyz".

```
// C++ program to sort a string of characters
#include<bits/stdc++.h>
using namespace std;

// function to print string in sorted order
void sortString(string &str)
{
sort(str.begin(), str.end());
cout << str;
}

// Driver program to test above function
int main()
{
	string s = "geeksforgeeks";
	sortString(s);
	return 0;
}

```



```
// C++ program to sort a string of characters
#include<bits/stdc++.h>
using namespace std;

const int MAX_CHAR = 26;

// function to print string in sorted order
void sortString(string &str)
{
	// Hash array to keep count of characters.
	// Initially count of all characters is
	// initialized to zero.
	int charCount[MAX_CHAR] = {0};
	
	// Traverse string and increment
	// count of characters
	for (int i=0; i<str.length(); i++)

		// 'a'-'a' will be 0, 'b'-'a' will be 1,
		// so for location of character in count
		// array we will do str[i]-'a'.
		charCount[str[i]-'a']++;
	
	// Traverse the hash array and print
	// characters
	for (int i=0;i<MAX_CHAR;i++)
		for (int j=0;j<charCount[i];j++)
			cout << (char)('a'+i);
}

// Driver program to test above function
int main()
{
	string s = "geeksforgeeks";
	sortString(s);
	return 0;
}
```
