# STL Cheat Sheet

This is a summary of the various STL data structions and functions that are especially useful for competitive programming.

## STL Data Structures

### Vector
* **Syntax**: `vector<T> v`

* **Insertion** [amortized O(1) time]: `v.push_back()` or `v.emplace_back()` //emplace_back is useful for objects with constructor of multiple arguements. <br/>
*Note: `v.insert` has linear complexity due to need of always needing to reallocate vector*

* **Deletion** [O(1) time]: `v.pop_back()` or `v.pop_front()` or `v.erase()`

* **Referencing** [O(1) time]: `v.front()`, `v.back()`, `v[index]`, `v.at(index)`

* **Resize** [O(N) time]: `v.resize(new_size)`

### Pair
* **Syntax**: `pair<U,V> p`

* **Make Pair** [O(1) time]: `make_pair(a,b)`

* **Accessing value** [O(1) time]: `p.first` is the first element, `p.second` is the second element

* **Comparison** [O(1) time]: Default > and < only compare the first element. == works as expected by comparing both the first and second elements

### Heap
*Creates heaps, that allow us to access min/max element in O(1) time*

* **Syntax**: `priority_queue<T, vector<T>, Compare_Class> pq;`<br/>
max heap: `priority_queue<int> pq;` //default<br/>
min heap: `priority_queue<int,vector<int>,greater<int>> pq;` <br/>
*Custom heap (max heap of pairs of int based on second element):* <br/>
```
struct my_cmp{
    bool operator()(const pair<int,int> &a, const pair<int,int> const &b) const{
        return a.second < b.second;
    }
};

priority_queue<pair<int,int>, vector<pair<int,int>>, my_cmp>
```

* **Heapify** [O(2N) time]: `make_heap(first_iter,last_iter)`

* **Insertion** [O(log N) time]: `pq.push()`

* **Removing element** [O(log N) time]: `pq.pop()`

* **Accessing min/max** [O(1) time]: `pq.top()`

* **Checking if empty** [O(1) time]: `pq.empty()`


## STL functions

### Upper Bound
*Uses Binary Search to return iterator to first element in [begin,end) strictly greater than value* <br/>
* Time complexity = O(log N)
* Syntax: `upper_bound(itr_begin,itr_end, value)`
* If no upper bound is found, itr_end is returned

### Lower Bound
*Uses Binary Search to return iterator to first element in [begin,end) greater or equal to than value* <br/>
* Time complexity = O(log N)
* Syntax: `lower_bound(itr_begin,itr_end, value)`
* If no lower bound is found, itr_end is returned

### Swap
*Swaps the value of two variables (variables should therefore be of same type)*
* Time Complexity = O(1)
* Syntax: `swap(a,b)`

### Sort
*Uses as optimized mixture of QuickSort, HeapSort and InsertionSort called IntroSort to order data **IN-PLACE**. By default, it uses QuickSort but if QuickSort is doing unfair partitioning and taking more than NlogN time, it switches to HeapSort and when the array size becomes really small, it switches to InsertionSort*
* Time Complexity = O(NlogN)
* Syntax: `sort(itr_begin,itr_end, cmp)`
* Ascending order: `sort(v.begin(),v.end());` <br/>
Descending order: `sort(v.begin(),v.end(),greater<int>());`<br/>
Custom (eg. sorting pairs of int in descending order of second element)
```
bool my_cmp(const pair<int,int> &a, const pair<int,int> const &b){
    //true indicates a is before b
    return a.second > b.second; 
}
vector<pair<int,int>> v = {{0,1},{2,3},{4,5}};
sort(v.begin(),v.end(),cmp);
```
