# 4. Selection Sort

Last Review Time: January 20, 2023 4:59 PM
Tags: Array, Sorting

```java
public class Solution {
  public int[] solve(int[] array) {
    // Write your solution here
    for(int i = 0; i < array.length; ++i){
      int mi = i;
      for(int j = i ; j < array.length; ++j){
        if(array[j] < array[mi]){
          mi = j;
        }
      }
      int temp = array[i];
      array[i] = array[mi];
      array[mi] = temp;
    }
    return array;
  }
}
```