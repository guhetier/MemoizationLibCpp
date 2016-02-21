# MemoizationLibCpp

MemoizationLibCpp is a C++11 librairy to build memoized functions easily.
It provides extended hash functions and specialized hash table too.

## Example of use

Below is an example of how to use MemoizationLibCpp get a memoized version of the computation of the binomial coefficients.

```cpp
#include "src/fixedPoint.hpp"

long binomialCoeff(function<long(pair<int, int>)> f, pair<int, int> p)
{
    int n = get<0>(p);
    int k = get<1>(p);

    // Trivial cases
    if(n<k)
        return (long)0;
    if(k == 0)
        return (long)1;

    // Apply recursive definition elsewhere
    return f(make_pair(n-1,k)) + f(make_pair(n-1, k-1));
}

int main(){

    Memo<pair<int, int>, long> pascalMem (binomialCoeff);
    cout << pascalMem(make_pair(100, 50)) << end;
}
```

## Options

The memoisation operator has the following signature : 

```cpp
Memo<P, R [, T]> (sdt::function<R(T)> [, int, std::function<std::size_t(T)>]);
```

### Required template parameters
- P is the type of the argument of the function. The memoized function can only have one parameter, use tuples several parameters are needed.
- R is the return type of the function.

### Optional template parameters
T is the type of the hash table that is used to store computed values.
Default hash table is std::unordered_map but two other tables are implemented. One is a light standard hash table, the other is a size limited hash table.
The second may be use to perform memory-limited memoization. More information on that subject may be found on the paper present in this repository.

### Arguments :
- The function to be memoized
- The initial size of the hash table used to store data during memoization
- The hash function used by the hash table. By default, it is an extension of std::hash which reucrsively hash vectors and tupples.

