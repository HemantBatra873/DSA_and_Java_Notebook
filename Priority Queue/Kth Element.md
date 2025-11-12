# Kth element problem

https://leetcode.com/problems/k-closest-points-to-origin/solutions/220235/java-three-solutions-to-this-classical-k-8h9n/

You need to find the kth element in a group of element.

## 1st approach 

Use normal sorting and return kth element 

## 2nd approach 

Use pq only keep k elements using constraint and return top element when kth element is needed. This is online situation.

## 3rd element 

Use quick sort element. It returns index of the sorted element and then if idx > k search on the left if idx < k search right else if idx == k return idx.

