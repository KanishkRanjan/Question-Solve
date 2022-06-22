Given an array and a number k where k is smaller than the size of the array, we need to find the k’th smallest element in the given array. It is given that all array elements are distinct.

**Examples:**  

> **Input**: arr[] = {7, 10, 4, 3, 20, 15}, k = 3   
> **Output**: 7
> 
> **Input**: arr[] = {7, 10, 4, 3, 20, 15}, k = 4   
> **Output**: 10


## Maxheap using STL

We can implement max and min heap using a priority queue.
To find the kth minimum element in an array we will max heapify the array until the size of the heap becomes k.
After that for each entry we will pop the top element from the heap/Priority Queue.

```
// C++ code to implement the approach
#include<bits/stdc++.h>
using namespace std;

// Function to find the kth smallest array element
int kthSmallest(int arr[], int n, int k) {

	// For finding min element we need (Max heap)priority queue
	priority_queue<int> pq;
	
	for(int i = 0; i < k; i++)
	{		
		// First push first K elememts into heap
		pq.push(arr[i]);
	}
	// Now check from k to last element
	for(int i = k; i < n; i++)
	{
	
		// If current element is < top that means
		// there are other k-1 lesser elements
		// are present at bottom thus, pop that element
		// and add kth largest element into the heap till curr
		// at last all the greater element than kth element will get pop off
		// and at the top of heap there will be kth smallest element
		if(arr[i] < pq.top())
		{
			pq.pop();
			// Push curr element
			pq.push(arr[i]);
		}
	}

	// Return top of element
	return pq.top();
}


// Driver's code:
int main()
{
	int n = 10;
	int arr[n] = {10, 5, 4 , 3 ,48, 6 , 2 , 33, 53, 10};
	int k = 4;
	cout<< "Kth Smallest Element is: "<<kthSmallest(arr, n, k);

}

```

## Using Min Heap-HeapSelect

We can find k'th smallest element in time complexity better than 0(NlogN). A simple optimization is to create a Min Heap of the given n elements and call extractMin() k times.

```
// A C++ program to find k'th smallest element using min heap
#include <climits>
#include <iostream>
using namespace std;

// Prototype of a utility function to swap two integers
void swap(int* x, int* y);

// A class for Min Heap
class MinHeap {
	int* harr; // pointer to array of elements in heap
	int capacity; // maximum possible size of min heap
	int heap_size; // Current number of elements in min heap
public:
	MinHeap(int a[], int size); // Constructor
	void MinHeapify(int i); // To minheapify subtree rooted with index i
	int parent(int i) { return (i - 1) / 2; }
	int left(int i) { return (2 * i + 1); }
	int right(int i) { return (2 * i + 2); }

	int extractMin(); // extracts root (minimum) element
	int getMin() { return harr[0]; } // Returns minimum
};

MinHeap::MinHeap(int a[], int size)
{
	heap_size = size;
	harr = a; // store address of array
	int i = (heap_size - 1) / 2;
	while (i >= 0) {
		MinHeapify(i);
		i--;
	}
}

// Method to remove minimum element (or root) from min heap
int MinHeap::extractMin()
{
	if (heap_size == 0)
		return INT_MAX;

	// Store the minimum value.
	int root = harr[0];

	// If there are more than 1 items, move the last item to root
	// and call heapify.
	if (heap_size > 1) {
		harr[0] = harr[heap_size - 1];
		MinHeapify(0);
	}
	heap_size--;

	return root;
}

// A recursive method to heapify a subtree with root at given index
// This method assumes that the subtrees are already heapified
void MinHeap::MinHeapify(int i)
{
	int l = left(i);
	int r = right(i);
	int smallest = i;
	if (l < heap_size && harr[l] < harr[i])
		smallest = l;
	if (r < heap_size && harr[r] < harr[smallest])
		smallest = r;
	if (smallest != i) {
		swap(&harr[i], &harr[smallest]);
		MinHeapify(smallest);
	}
}

// A utility function to swap two elements
void swap(int* x, int* y)
{
	int temp = *x;
	*x = *y;
	*y = temp;
}

// Function to return k'th smallest element in a given array
int kthSmallest(int arr[], int n, int k)
{
	// Build a heap of n elements: O(n) time
	MinHeap mh(arr, n);

	// Do extract min (k-1) times
	for (int i = 0; i < k - 1; i++)
		mh.extractMin();

	// Return root
	return mh.getMin();
}

// Driver program to test above methods
int main()
{
	int arr[] = { 12, 3, 5, 7, 19 };
	int n = sizeof(arr) / sizeof(arr[0]), k = 2;
	cout << "K'th smallest element is " << kthSmallest(arr, n, k);
	return 0;
}
```

## Using Max-Heap

we can also use Max Heap for finding the k'th smallest element. Following is an algorithm.

1) Build a Max-Heap MH of the first k elements (arr[0] to ar[n-1]) of the given array . O(k)
2) For each element, after the k'th element (arr[k] to arr[n-1]), compare it with root of MH.
	a)If the element is less than the root then make it root and call heapify for MH
	//The step 2 is O((n-k)*logK)
	b) Else ignore it.
3) Finally, the root of the MH is the kth smallest element.

**Time Complexity:** O(K+(n-k)*LogK)

Implementation of the above algorithm
```
// A C++ program to find k'th smallest element using max heap
#include <climits>
#include <iostream>
using namespace std;

// Prototype of a utility function to swap two integers
void swap(int* x, int* y);

// A class for Max Heap
class MaxHeap {
	int* harr; // pointer to array of elements in heap
	int capacity; // maximum possible size of max heap
	int heap_size; // Current number of elements in max heap
public:
	MaxHeap(int a[], int size); // Constructor
	void maxHeapify(int i); // To maxHeapify subtree rooted with index i
	int parent(int i) { return (i - 1) / 2; }
	int left(int i) { return (2 * i + 1); }
	int right(int i) { return (2 * i + 2); }

	int extractMax(); // extracts root (maximum) element
	int getMax() { return harr[0]; } // Returns maximum

	// to replace root with new node x and heapify() new root
	void replaceMax(int x)
	{
		harr[0] = x;
		maxHeapify(0);
	}
};

MaxHeap::MaxHeap(int a[], int size)
{
	heap_size = size;
	harr = a; // store address of array
	int i = (heap_size - 1) / 2;
	while (i >= 0) {
		maxHeapify(i);
		i--;
	}
}

// Method to remove maximum element (or root) from max heap
int MaxHeap::extractMax()
{
	if (heap_size == 0)
		return INT_MAX;

	// Store the maximum value.
	int root = harr[0];

	// If there are more than 1 items, move the last item to root
	// and call heapify.
	if (heap_size > 1) {
		harr[0] = harr[heap_size - 1];
		maxHeapify(0);
	}
	heap_size--;

	return root;
}

// A recursive method to heapify a subtree with root at given index
// This method assumes that the subtrees are already heapified
void MaxHeap::maxHeapify(int i)
{
	int l = left(i);
	int r = right(i);
	int largest = i;
	if (l < heap_size && harr[l] > harr[i])
		largest = l;
	if (r < heap_size && harr[r] > harr[largest])
		largest = r;
	if (largest != i) {
		swap(&harr[i], &harr[largest]);
		maxHeapify(largest);
	}
}

// A utility function to swap two elements
void swap(int* x, int* y)
{
	int temp = *x;
	*x = *y;
	*y = temp;
}

// Function to return k'th largest element in a given array
int kthSmallest(int arr[], int n, int k)
{
	// Build a heap of first k elements: O(k) time
	MaxHeap mh(arr, k);

	// Process remaining n-k elements. If current element is
	// smaller than root, replace root with current element
	for (int i = k; i < n; i++)
		if (arr[i] < mh.getMax())
			mh.replaceMax(arr[i]);

	// Return root
	return mh.getMax();
}

// Driver program to test above methods
int main()
{
	int arr[] = { 12, 3, 5, 7, 19 };
	int n = sizeof(arr) / sizeof(arr[0]), k = 4;
	cout << "K'th smallest element is " << kthSmallest(arr, n, k);
	return 0;
}
```


