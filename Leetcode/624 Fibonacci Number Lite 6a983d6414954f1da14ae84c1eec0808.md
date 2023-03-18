# 624. Fibonacci Number Lite

Algorithm: Recursion
Difficulty: Easy
Last Review Time: January 4, 2023 10:40 PM
No: 624

```java
public class Solution {
  public int fibonacci(int K) {
    // Write your solution here
    if(K < 0){
      return 0;
    }
    if(K == 1){
      return 1;
    }
    if(K == 2){
      return 1;
    }
    return fibonacci(K-1) + fibonacci(K-2);
  }
}
```

1. Subproblem: the fibonacci number is the sum of the first two number before current fibonacci number. 

```java
fibonacci(K) = fibonacci(K-1) + fibonacci(K-2)
```

1. Base Case: 0th fibonacci number and 1st fibonacci number. 

```java
    if(K == 1){
      return 1;
    }
    if(K == 2){
      return 1;
    }
```

1. Specific Condition: When K ≤ 0, program return 0

```java
    if(K < 0){
      return 0;
    }
```