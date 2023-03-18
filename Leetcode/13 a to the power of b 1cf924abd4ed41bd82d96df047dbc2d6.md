# 13. a to the power of b

Last Review Time: January 4, 2023 11:03 PM
No: 13

```java
public class Solution {
  public long temp(int a, int current, int b){
    if(current == b){
      return a;
    }
    return a * temp(a, current + 1, b);
  }
  

	public long power(int a, int b) {
    // Write your solution here
    
    // Cause 0 ^ 0 = 1
    if(b == 0){
      return 1;
    }

    // all the power of 0 is 0
    if(a == 0){
      return 0;
    }

    // Only signal change
    if(a == -1 || a == 1){
      if(b % 2 == 0){
        return 1;
      }
      else{
        return a;
      }
    }
    long ans = temp(a, 1, b);
    

    return ans;
  }
}
```

```java
public class Solution {
  public long power(int a, int b) {
    // Write your solution here
    if(a == 1 || a == -1){
      if(b % 2 == 0){
        return 1;
      }
      else{
        return a;
      }
    }
    if(b == 0)
      return 1;
    return a * power(a, b - 1);
  }
}
```

```java
public class Solution {
  public long power(int a, int b) {
    // Write your solution here
    if(a == 1 || a == -1){
      if(b % 2 == 0){
        return 1;
      }
      else{
        return a;
      }
    }
    if(b == 0){
      return 1;
    }
    if(b % 2 == 0){
      return power(a, b / 2) * power(a, b / 2);
    }
    else{
      return power(a, b / 2) * power(a, b / 2) * a;
    }
    
  }
}
```