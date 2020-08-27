# Big O

Big O. Time and Space complexity. 


## Space Complexity 

#### Example 1

In this example the `sum(_:)` function is being called recursively and decrementing the value of `k` until it reaches the `base case` of 0 and return the value from the `call stack`. Here the `runtime complexity` is `O(n)` as we count how many times the recursive call happens and the `space complexity` is also `O(n)` as it takes space on the call stack. 

```swift 
func sum(_ k: Int) -> Int {
  guard k > 0 else {
    return 0
  }
  return k + sum(k - 1)
}

sum(5) // 5 + 4 + 3 + 2 + 1 = 15
```

<pre> 
sum(5)
  => sum(4)
    => sum(3)
      => sum(2)
        => sum(1) 
          => sum(0)
</pre>

## Resources 

