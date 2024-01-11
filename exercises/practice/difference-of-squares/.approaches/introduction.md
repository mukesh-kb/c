# Introduction

There are few ways to solve Difference of Squares problem.
One approach is to use a [formula and reuse of already computed N*(N+1)/2][formula and reuse of already computed N*(N+1)/2 in N*(N+1)*(2*N+1)/6] and reuses  instead of looping to calculate the solution.

## Approach: Use formula and reuse N*(N+1)/2 result

**difference_of_squares.h**

```c
#ifndef DIFFERENCE_OF_SQUARES_H
#define DIFFERENCE_OF_SQUARES_H

unsigned int sum_of_squares(unsigned int number);
unsigned int square_of_sum(unsigned int number);
unsigned int difference_of_squares(unsigned int number);

#endif
```

**difference_of_squares.c**

```c
#include "difference_of_squares.h"

void compute_the_three(unsigned int number)
{
    unsigned int sum, sq_of_sum, sum_of_sq, diff;
    if(not_in_cache)
    {   
        sum = compute_sum(number);
        sq_of_sum = sum*sum;
        sum_of_sq = sum*(2*number+1)/3; // Reuse N*(N+1)/2 
        diff = sq_of_sum - sum_of_sq;
        //Store in cache (number, sum, sq_of_sum, sum_of_sq, diff)
    }
}

unsigned int compute_sum(unsigned int number)
{
    unsigned int sum;
    sum = number*(number+1)/2;
    return sum;
}

unsigned int square_of_sum(unsigned int number)
{
   if(not_in_cache)
   {
      compute_the_three(number);
   }
   // return cache.sq_of_sum; 
}

unsigned int sum_of_squares(unsigned int number)
{
   if(not_in_cache)
   {
      compute_the_three(number);
   }
   // return cache.sum_of_sq; 
}

unsigned int difference_of_squares(unsigned int number)
{
   if(not_in_cache)
   {
      compute_the_three(number);
   }
   // return cache.diff; 
}
```


[formula]: https://learnersbucket.com/examples/algorithms/difference-between-square-of-sum-of-numbers-and-sum-of-square-of-numbers/
[approach-formula-reuse]: https://exercism.org/tracks/c/exercises/difference-of-squares/approaches/formula-and-reuse
