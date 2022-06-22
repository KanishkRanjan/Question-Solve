Given an arrya of  `n` numbers and a positive integer `k`. The problem is to find `k` numbers with most occurrences, i.e., the top k numbers having the maximum frequency. If two number have the same frequency then the larger number should be given preference. The numbers should be displayed in decreaing order of their frequencies. It is assumed that the array consists of `k` numbers with most occurrences.

**Examples:** 

> **Input:**   
> arr[] = {3, 1, 4, 4, 5, 2, 6, 1},   
> k = 2  
> **Output:** 4 1  
> **Explanation:**  
> Frequency of **4** = 2  
> Frequency of **1** = 2  
> These two have the maximum frequency and  
> **4** is larger than **1**.
> 
> **Input :**   
> arr[] = {7, 10, 11, 5, 2, 5, 5, 7, 11, 8, 9},  
> k = 4  
> **Output:** 5 11 7 10  
> **Explanation:**   
> Frequency of **5** = 3  
> Frequency of **11** = 2  
> Frequency of **7** = 2  
> Frequency of **10** = 1  
> These four have the maximum frequency and  
> **5** is largest among rest.


### Methode 1
- *Approach:* The thought process should begin from creating a `HashMap` to store element-frequency pair in the HashMap. HashMap is used to perform insertion and updation in constant time. Then sort the element-frequency pair in decreasing order of frequency. This gives the information about each element and the number of times they are present in the array. To get k elements of the array, print the first k elements of the sorted array.

- *Algorithm:* 
	1) Create Hashmap hm, to store key-value pair, i.e. element-frequency pair.
	2) Traverse the array from start to end.
	3) For every element in the array update hm\[array\[i\]\]++
	4) Store the element-frequency pair in a vector and sort the vector in decreasing order of frequency.
	5) Print the first k elements of sorted array.


```
// C++ implementation to find k numbers with most
// occurrences in the given array
#include <bits/stdc++.h>

using namespace std;

// comparison function to sort the 'freq_arr[]'
bool compare(pair<int, int> p1, pair<int, int> p2)
{
	// if frequencies of two elements are same
	// then the larger number should come first
	if (p1.second == p2.second)
		return p1.first > p2.first;

	// sort on the basis of decreasing order
	// of frequencies
	return p1.second > p2.second;
}

// function to print the k numbers with most occurrences
void print_N_mostFrequentNumber(int arr[], int n, int k)
{
	// unordered_map 'um' implemented as frequency hash table
	unordered_map<int, int> um;
	for (int i = 0; i < n; i++)
		um[arr[i]]++;

	// store the elements of 'um' in the vector 'freq_arr'
	vector<pair<int, int> > freq_arr(um.begin(), um.end());

	// sort the vector 'freq_arr' on the basis of the
	// 'compare' function
	sort(freq_arr.begin(), freq_arr.end(), compare);

	// display the top k numbers
	cout << k << " numbers with most occurrences are:\n";
	for (int i = 0; i < k; i++)
		cout << freq_arr[i].first << " ";
}

// Driver program to test above
int main()
{
	int arr[] = { 3, 1, 4, 4, 5, 2, 6, 1 };
	int n = sizeof(arr) / sizeof(arr[0]);
	int k = 2;
	print_N_mostFrequentNumber(arr, n, k);
	return 0;
}

```


### Method 2:
- *Approach:* Create a HashMap to store element-frequency pair in the HashMap. HashMap is used to perform insertion and updation in constand time. Then use a priority queue to store the element-frequency pair(Max-Heap). This gives the element which has maximum frequency at the the root of the Priority Queue. Remove the top or root of Priority Queue K times and print the element. To insert and delete the top of the priority queue O(log n) time is required.
- *Algorithm:* 
	1) Create a Hashmap hm, to store key-value pair, i.e. element-frequency pair.
	2) Traverse the array from start to end.
	3) For every element in the array update hm\[array\[i]]++
	4) Store the element-frequency pair in a Priority Queue and creat the Priority Queue, this takes O(n) time.
	5) Run a loop k times and in each iteration remove the top of teh priority queue and print the element.

```
// C++ implementation to find k numbers with most
// occurrences in the given array
#include <bits/stdc++.h>

using namespace std;

// comparison function defined for the priority queue
struct compare {
	bool operator()(pair<int, int> p1, pair<int, int> p2)
	{
		// if frequencies of two elements are same
		// then the larger number should come first
		if (p1.second == p2.second)
			return p1.first < p2.first;

		// insert elements in the priority queue on the basis of
		// decreasing order of frequencies
		return p1.second < p2.second;
	}
};

// function to print the k numbers with most occurrences
void print_N_mostFrequentNumber(int arr[], int n, int k)
{
	// unordered_map 'um' implemented as frequency hash table
	unordered_map<int, int> um;
	for (int i = 0; i < n; i++)
		um[arr[i]]++;

	

	// priority queue 'pq' implemented as max heap on the basis
	// of the comparison operator 'compare'
	// element with the highest frequency is the root of 'pq'
	// in case of conflicts, larger element is the root
	priority_queue<pair<int, int>, vector<pair<int, int> >,
				compare>
		pq(um.begin(), um.end());

	// display the top k numbers
	cout << k << " numbers with most occurrences are:\n";
	for (int i = 1; i <= k; i++) {
		cout << pq.top().first << " ";
		pq.pop();
	}
}

// Driver program to test above
int main()
{
	int arr[] = { 3, 1, 4, 4, 5, 2, 6, 1 };
	int n = sizeof(arr) / sizeof(arr[0]);
	int k = 2;
	print_N_mostFrequentNumber(arr, n, k);
	return 0;
}
```

**Time Complexity:** O(k long d +d)
**AuxiliarySpace:** O(d) 