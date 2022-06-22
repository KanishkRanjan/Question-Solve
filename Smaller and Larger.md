Given a sorted array **Arr** of size **N** and a value **X**, find the number of array elements less than or equal to **X** and elements more than or equal to **X**. 

**Example 1:**

**Input:**
N = 7, X = 0
Arr[] = {1, 2, 8, 10, 11, 12, 19}
**Output:** 0 7
**Explanation:** There are no elements less or
equal to 0 and 7 elements greater or equal
to 0.

**Example 2:**

**Input:**
N = 7, X = 5
Arr[] = {1, 2, 8, 10, 11, 12, 19}
**Output:** 2 5
**Explanation:** There are 2 elements less or
equal to 5 and 5 elements greater or equal
to 5.

**upper will help when all element are simialar**

3 3
3 3 3

out: 3 3


```
class Solution{
public:	
	vector<int> getMoreAndLess(int arr[], int n, int x) {
        vector<int>ans(2);

        ans[0] = upper_bound(arr,arr+n,x) - arr;
        ans[1] = n - (lower_bound(arr,arr+n,x) - arr);
        return ans;
	}
};
```
	