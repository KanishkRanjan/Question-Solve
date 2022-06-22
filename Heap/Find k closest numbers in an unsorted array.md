#### Given an unsorted array and two numbers x andk, find k closest values to x.


**Input :** arr[] = {10, 2, 14, 4, 7, 6}, x = 5, k = 3 
**Output :** 4 6 7
Three closest values of x are 4, 6 and 7.

**Input :** arr[] = {-10, -50, 20, 17, 80}, x = 20, k = 2
**Output :** 17, 20


Sol^n

1) Make a max heap of differences with first k elements.
2) For every element starting from (K+1)th element, do following.
	a) Find difference of curretnt element with x.
	b)If difference is more than root of heap, ignore current element.
	c)Else insert the current element to the heap after removing the root.
3) Finally the heap has k closest elements.

```
// C++ program to find k closest elements
#include <bits/stdc++.h>
using namespace std;

void printKclosest(int arr[], int n, int x,
				int k)
{
	// Make a max heap of difference with
	// first k elements.
	priority_queue<pair<int, int> > pq;
	for (int i = 0; i < k; i++)
		pq.push({ abs(arr[i] - x), i });

	// Now process remaining elements.
	for (int i = k; i < n; i++) {

		int diff = abs(arr[i] - x);

		// If difference with current
		// element is more than root,
		// then ignore it.
		if (diff > pq.top().first)
			continue;

		// Else remove root and insert
		pq.pop();
		pq.push({ diff, i });
	}

	// Print contents of heap.
	while (pq.empty() == false) {
		cout << arr[pq.top().second] << " ";
		pq.pop();
	}
}

// Driver program to test above functions
int main()
{
	int arr[] = { -10, -50, 20, 17, 80 };
	int x = 20, k = 2;
	int n = sizeof(arr) / sizeof(arr[0]);
	printKclosest(arr, n, x, k);
	return 0;
}
```

**Time Complexity**:O(nLogK)
