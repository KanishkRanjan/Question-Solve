Given two strings of lowercase alphabets and a value k, the task is to find if two strings are K-anagrams of each other or not.  
Two strings are called **k-anagrams** if following two conditions are true. 

1.  Both have same number of characters.
2.  Two strings can become anagram by changing at most k characters in a string.

**Examples :**  

**Input: ** str1 = "anagram" , str2 = "grammar" , k = 3
**Output: ** Yes
Explanation: We can update maximum 3 values and 
it can be done in changing only 'r' to 'n' 
and 'm' to 'a' in str2.

**Input: ** str1 = "geeks", str2 = "eggkf", k = 1
**Output: ** No
Explanation: We can update or modify only 1 
value but there is a need of modifying 2 characters. 
i.e. g and f in str 2.


```
// C++ program to check if two strings are k anagram
// or not.
#include<bits/stdc++.h>
using namespace std;
const int MAX_CHAR = 26;

// Function to check that string is k-anagram or not
bool arekAnagrams(string str1, string str2, int k)
{
	// If both strings are not of equal
	// length then return false
	int n = str1.length();
	if (str2.length() != n)
		return false;

	int count1[MAX_CHAR] = {0};
	int count2[MAX_CHAR] = {0};

	// Store the occurrence of all characters
	// in a hash_array
	for (int i = 0; i < n; i++)
		count1[str1[i]-'a']++;
	for (int i = 0; i < n; i++)
		count2[str2[i]-'a']++;
	
	int count = 0;

	// Count number of characters that are
	// different in both strings
	for (int i = 0; i < MAX_CHAR; i++)
		if (count1[i] > count2[i])
			count = count + abs(count1[i]-count2[i]);

	// Return true if count is less than or
	// equal to k
	return (count <= k);
}

// Driver code
int main()
{
	string str1 = "anagram";
	string str2 = "grammar";
	int k = 2;
	if (arekAnagrams(str1, str2, k))
		cout << "Yes";
	else
		cout<< "No";
	return 0;
}
```



**Method 2:**   
We can optimize above solution. Here we use only one count array to store counts of characters in str1. We traverse str2 and decrement occurrence of every character in count array that is present in str2. If we find a character that is not there in str1, we increment count of different characters. If count of different character become more than k, we return false.

```
// Optimized C++ program to check if two strings
// are k anagram or not.
#include<bits/stdc++.h>
using namespace std;

const int MAX_CHAR = 26;

// Function to check if str1 and str2 are k-anagram
// or not
bool areKAnagrams(string str1, string str2, int k)
{
	// If both strings are not of equal
	// length then return false
	int n = str1.length();
	if (str2.length() != n)
		return false;

	int hash_str1[MAX_CHAR] = {0};

	// Store the occurrence of all characters
	// in a hash_array
	for (int i = 0; i < n ; i++)
		hash_str1[str1[i]-'a']++;

	// Store the occurrence of all characters
	// in a hash_array
	int count = 0;
	for (int i = 0; i < n ; i++)
	{
		if (hash_str1[str2[i]-'a'] > 0)
			hash_str1[str2[i]-'a']--;
		else
			count++;

		if (count > k)
			return false;
	}

	// Return true if count is less than or
	// equal to k
	return true;
}

// Driver code
int main()
{
	string str1 = "fodr";
	string str2 = "gork";
	int k = 2;
	if (areKAnagrams(str1, str2, k) == true)
		cout << "Yes";
	else
		cout << "No";
	return 0;
}
```

**Method 3:**  

-   In this method the idea is to initialize an array or a list and the base case would be to check the strings and if they have different lengths then they cannot form an anagram.
-   Otherwise convert the strings into character array and sort them.
-   Then iterate till the length of the string and if the character are not equal then add it to the list and check if list size is less than equal to K then it is possible to form K anagram else not.


```
// CPP program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check k
// anagram of two strings
bool kAnagrams(string str1, string str2, int k)
{
	int flag = 0;

	// First Condition: If both the
	// strings have different length ,
	// then they cannot form anagram
	if (str1.length() != str2.length())
		return false;
	int n = str1.length();
	// Converting str1 to Character Array arr1
	char arr1[n];

	// Converting str2 to Character Array arr2
	char arr2[n];

	strcpy(arr1, str1.c_str());
	strcpy(arr2, str2.c_str());
	// Sort arr1 in increasing order
	sort(arr1, arr1 + n);

	// Sort arr2 in increasing order
	sort(arr2, arr2 + n);

	vector<char> list;

	// Iterate till str1.length()
	for (int i = 0; i < str1.length(); i++) {

		// Condition if arr1[i] is
		// not equal to arr2[i]
		// then add it to list
		if (arr1[i] != arr2[i]) {
			list.push_back(arr2[i]);
		}
	}

	// Condition to check if
	// strings for K-anagram or not
	if (list.size() <= k)
		flag = 1;

	if (flag == 1)
		return true;
	else
		return false;
}

// Driver Code
int main()
{

	string str1 = "anagram", str2 = "grammar";
	int k = 3;

	// Function Call
	kAnagrams(str1, str2, k);
	if (kAnagrams(str1, str2, k) == true)
		cout << "Yes";
	else
		cout << "No";

	// This code is contributed by bolliranadheer
}
```