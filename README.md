# STL Cheat Sheet

This is a summary of the various STL data structures and functions that are especially useful for competitive programming.

## STL Data Structures

### Vector
* **Syntax**: `vector<T> v`

* **Insertion** [amortized O(1) time]: `v.push_back()` or `v.emplace_back()` //emplace_back is useful for objects with constructor of multiple arguements. <br/>
*Note: `v.insert` has linear complexity due to need of always needing to reallocate vector*

* **Deletion** [O(1) time]: `v.pop_back()` or `v.pop_front()` or `v.erase()`

* **Referencing** [O(1) time]: `v.front()`, `v.back()`, `v[index]`, `v.at(index)`

* **Resize** [O(N) time]: `v.resize(new_size)` 
* **Reserve** [O(1) time]: `v.reserve(k)' allows for users to reserve k contiguous blocks of memory for the vector that reduces reallocation overhead. This DOES NOT initialize the k spaces.

### Pair
* **Syntax**: `pair<U,V> p`

* **Make Pair** [O(1) time]: `make_pair(a,b)`

* **Accessing value** [O(1) time]: `p.first` is the first element, `p.second` is the second element

* **Comparison** [O(1) time]: Default > and < only compare the first element. == works as expected by comparing both the first and second elements

### Heap
*Creates heaps, that allow us to access min/max element in O(1) time*

* **Syntax**: `priority_queue<T, vector<T>, Compare_Class> pq;`<br/>
max heap: `priority_queue<int> pq;` (*default*)<br/>
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

* **Heapify** [O(2N) time]: `make_heap(iter_begin,iter_end)`

* **Insertion** [O(logN) time]: `pq.push()`

* **Removing element** [O(logN) time]: `pq.pop()`

* **Accessing min/max** [O(1) time]: `pq.top()`

* **Checking if empty** [O(1) time]: `pq.empty()`

### Map
*Stores (key,value) pairs, in an sorted manner. Keys are sorted using a self-balancing red-black tree*

* **Syntax**: `map<U,V> mp`

* **Iterator**: `map<U,V>::iterator itr`

* **Insertion** [O(logN) time]: `mp[key]=value` or `mp.insert(make_pair(key,value))` <br/>
*In the case that you know location of the insertion, you can reduce time complexity to O(1) by providing a hint `mp.insert(key,value, itr_hint)`*

* **Look-Up** [O(logN) time]: key is `itr->first`, value is `itr->second` or simply `mp[key]` or `mp.at(key)` <br\>
`mp.upper_bound(key)`, `mp.lower_bound(key)` can be used

* **Deletion** [O(logN) time]: `mp.erase(key)` or `mp.erase(itr)` or `mp.erase(itr_begin,itr_end)` <br/>
*Note: logN time is due to searching and rebalancing the tree, deleting entire map is an O(N) operation*

### Unordered Map
*Stores (key,value) pairs as a hash table (i.e. an array of linked lists). Keys must be unique*

* **Syntax**: `unordered_map<U,V> hash`

* **Iterator**: `unordered_map<U,V>::iterator itr`

* **Insertion** [O(1) time]: `mp[key]=value` or `mp.insert(make_pair(key,value))` [Duplicate keys ARE NOT ALLOWED]

* **Look-Up** [O(1) time]: key is `itr->first`, value is `itr->second` or simply `mp[key]` or `mp.at(key)`

* **Deletion** [O(1) time]: `mp.erase(key)` or `mp.erase(itr)` or `mp.erase(itr_begin,itr_end)` <br/>

*Note: As with all hash tables, collision in key hash will make the time complexity of methods O(num_keys_colliding) intead of O(1). So worst case complexity is O(N).*

### Set
*Make sets of unique elements, wherein the elements are sorted (by using a binary search tree)*

* **Syntax**: `set<T, compare Class> s` <br/>
`set<T> s` or `set<T,less<T>> s` *(default sorting in ascending order)* <br/>
`set<T,greater<T>> s` *(to sort in descending order)*

* **Insertion** [O(logN) time]: `s.insert(elem)`

* **Search** [O(logN) time]: `s.find(elem)`, `s.upper_bound(elem)`, `s.lower_bound(elem)`

* **Deletion** [O(logN) time]: `s.erase(elem)` or `s.erase(itr)`

* **Modification**: Elements cannot be modified.

### Unordered Set
*Make sets of unique elements, wherein the indices are hashed*

* **Syntax**: `unordered_set<T> us`

* **Insertion** [O(1) time]: `us.insert(elem)`

* **Search** [O(1) time]: `us.find(elem)`

* **Deletion** [O(1) time]: `us.erase(elem)` or `us.erase(itr)`

* **Modification**: Elements cannot be modified.

*Note: As with all hash tables, collision in key hash will make the time complexity of methods O(num_keys_colliding) intead of O(1). So worst case complexity is O(N).*

### Multiset
*A set that stores elements is sorted order but allows for duplicate elements*

* **Syntax**: `multiset<T, compare Class> ms`
<br/>
`multiset<T> s` or `multiset<T,less<T>> ns` *(default sorting in ascending order)* <br/>
`multiset<T,greater<T>> ms` *(to sort in descending order)*

* **Insertion** [O(logN) time]: `ms.insert(val)`

* **Search** [O(logN) time]: `ms.find(val)`, `ms.upper_bound(val)`, `ms.lower_bound(val)`, `ums.equal_range(val)` returns a pair of first and last iterators of val

* **Deletion** [O(logN) time]: `ms.erase(val)` deletes all instances of val. `ms.erase(itr)` deletes the element instance the iterator is pointing at

* **Modification**: Elements cannot be modified.

### Unordered Multiset
*Just like an unordered set, but allows for duplicate elements*

* **Syntax**: `unordered_multiset<T> ums`

* **Insertion** [O(1) time]: `ums.insert(val)`

* **Search** [O(1) time]: `ums.find(val)`, `ums.equal_range(val)` returns a pair of first and last iterators of val

* **Deletion** [O(1) time]: `ums.erase(val)` deletes all instances of val. `ums.erase(itr)` deletes the element instance the iterator is pointing at

* **Modification**: Elements cannot be modified.

## STL functions

### Upper Bound
*Uses Binary Search to return iterator to first element in [begin,end) of ordered object that is strictly greater than value* <br/>
* Time complexity = O(logN)
* Syntax: `upper_bound(itr_begin,itr_end, value)`
* If no upper bound is found, itr_end is returned

### Lower Bound
*Uses Binary Search to return iterator to first element in [begin,end) of ordered object that is greater or equal to than value* <br/>
* Time complexity = O(logN)
* Syntax: `lower_bound(itr_begin,itr_end, value)`
* If no lower bound is found, itr_end is returned

### Swap
*Swaps the value of two variables (variables should therefore be of same type)*
* Time Complexity = O(1)
* Syntax: `swap(a,b)`

### Sort
*Uses as optimized mixture of QuickSort, HeapSort and InsertionSort called IntroSort to order data **IN-PLACE**. By default, it uses QuickSort but if QuickSort is doing unfair partitioning and taking more than NlogN time, it switches to HeapSort and when the array size becomes really small, it switches to InsertionSort*
* Time Complexity = O(N logN)
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
