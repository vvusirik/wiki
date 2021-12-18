# C++
## STL
### Iterators
https://www.youtube.com/watch?v=vO2AlrBf5rQ

4 kinds of standard iterators:
1. Insert Iterator - Inserts elements in a container starting at the iterator position.
```[cpp]
vector<int> vec1 = {4, 5};
vector<int> vec2 = {12, 14, 16, 18};
vector<int>::iterator it = find(vec2.begin(), vec2.end(), 16);
insert_iterator<vector<int>> i_itr(vec2, it);
copy(
    vec1.begin(), vec1.end(), // source
    i_itr); // dest
```
    * Other insert iterators include: `back_insert_iterator`, `front_insert_iterator`

2. Stream Iterator - iterates through elements in a stream source like standard in.
```[cpp]
vector<string> vec4;

// Insert elements from standard in to vec4
copy(
    istream_iterator<string>(cin), istream_iterator<string>(), // source
    back_inserter(vec4) // dest
);

// Stream elements to std out
copy(
    vec4.begin(), vec4.end(), 
    ostream_iterator<string>(cout, " ")
);

```

3. Reverse Iterator - Iterate through elements in reverse
```[cpp]
vector<int> vec = {4, 5, 6, 7};
reverse_iterator<vector<int>::iterator> ritr;
for (ritr = vec.rbegin(); ritr != vec.rend(); ritr++) {
    cout << *ritr << endl;
}
```
4. Move Iterator - Like normal iterator but dereference converts the underlying value to an rvalue, ie elements are moved rather than copied.

### Algorithms
Replace loops with STL algorithm function calls. 
NOTE: Algorithms process elements in half open ranges: [begin, end)

#### Examples
`min_element`
```
vector<int> vec = {4, 2, 5, 1, 3, 9};
vector<int>::iterator itr = min_element(vec.begin(), vec.end());
```

`copy` - See examples above. 
`copy(source_itr, source_vec.end(), back_inserter(dest_vec));`
* Note that this needs 3 iterators as input.
* Not an efficient way of copying vec elements from one vector to another since elements are inserted one by one.

`insert` - More efficient than copy since elements are inserted all at once.
`vec.insert(dest_vec.end(), source_itr, source_vec.end())`

`find_if` - Takes in an iterator range and a function
```
bool isOdd(int i) {
    return i % 2;
}

int main() {
    vector<int> vec = {2, 4, 5, 9, 2};
    vector<int>::iterator itr = find_if(vec.begin(), vec.end(), isOdd);
}
```
