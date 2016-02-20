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

