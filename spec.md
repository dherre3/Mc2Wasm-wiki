# Translation Specification

Work in progress...

## Arrays
New interface needs to be defined since WebAssembly does not
have an array data type. 

For starters, we will have a global mutable variable that will
keep track of the next index on the main memory array that is free. 
No garbage collection of memory will be implemented
initially, no strategy to re-utilize memory will be implemented,
later there are some thoughts on an interprocedural analysis that may
aid the cause. 
once an array has been instantiated, it will remain in memory for 
the duration of the WebAssembly instance. 

Arrays will be accessed in a column major fashion, since this is the way Matlab
implements their array accesses.

The arrays will be passed by reference, contrary to Matlab
where arrays are passed by value. A use of the [Copy Array Semantics](#copy_semantics) 
algorithm will be used for this purposes. The reason for this is avoiding unnecessary copies of the
array.

Here are the array accesses in Matlab:
```
a = ones(3,3)
a(start_exp:
```
Here are the function helpers in WebAssembly:

In memory arrays will be represented as follows:
### Array Allocation
```
array = (for i to dim_num sizedi),dim_num,
           type_idx,total_length---(INDEX_PTR)--- data...,\0)
Example:

a = [[1,2],[12,3]]
(4,0, 2, 2,2, 1,2,12,3,\0)
```

#### create_array_1d(length: i32, type: i32)
    
Declares a one dimensional array 

     @param length, takes length of array
     @param type, each type will have an index, 
     1 -> i32, 2-> i64, 3->f32, 4->f64, 5->char, 
     @return point index to start of array.

#### create_array(type: i32, array_indices: i32)

Declaring a multi-dimensional array

     @param type, each type will have an index, 
     1 -> i32, 2-> i64, 3->f32, 4->f64, 5->char,
     @param array_indices, index pointing to the array of dimensions 
     @return point index to start of array.

### Array fetching
There will be two types of array accesses, a one element fetch,
and a multiple colon operator fetch.
To represent the first type, a function `array_single_access()` will
be implemented, this will take two i32 numbers, signifying the array to
be fetch from and an array of indices along the dimensions of the array,
where each index i represents the index in the ith dimension of the array.
The main memory segment that WebAssembly offers will probably work as a 
heap where allocation of elements will be done on request, (Note: since there
is no deallocation for the time being, the will be lots of fragmentation happening,
and a highly inefficient use of memory). 
For the multiple array accesses, implemented in Matlab via colon operators, there will be a 
function called `array_multiple_access()`, this function will take two i32 numbers. 
One to represent the array to be accessed and the second represents the indices as an
array of arrays, where each index of the array signifies an array of elements to be wrapped
in the ith dimension of the original array.

#### array_single_access(array_idx->Array<T>:i32, indices_array->Array<i32>: i32) 
This function will grab the indices_array, will calculate the
offset to the array element and retrieve that element
    
     @param array_idx: i32, array to be accessed
     @param indices: i32, array that contains accesing index. 
     @throws trap when array index out of bounds
     @return element indexed by the indices.
     
#### array_multiple_access(array_idx->Array<T>:i32, indices_array->Array<Array<i32>> i32)
This function will grab the indices_array, which is an array of arrays, and will run a for-loop
that will grab the elements an copy them to a newly allocated array.
       
      @param array_idx: i32, array to be accessed
      @param indices: i32, array that contains accesing index. 
      @throws trap when array index out of bounds
      @return a reference to the allocated created array with the elements






### check_bounds()

### 
[1,3,4,5,6,6]

### TODO
- [ ] Define semantics for stepping:
    - One possibility would be to assume every index
        is a stepping array, this would be bad to performance
    - Make a transformation of all array accesses to be a single array
      of accessed indices. 
    - Make an array of arrays where every index of the indexing expression is an array on its own.  
## References

- <a name="copy_semantics"></a>Copy Semantics 
