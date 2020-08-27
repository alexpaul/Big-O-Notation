# Big O

Big O. Time and Space complexity. 

In Computer Science and Programming the way in which we measure the performance and efficiency of algorithms is using **Big O notation**, _denoted_ `O()`. 

## Runtime Complexity 

Runtime complexity is described as the performance over time as the size of the input grows. 


#### Example 1

In this example the performance of `calculateAverageAge` is `O(n)`, linear. As the size of the `ages` array grows the efficiency of this algorithm grows linearly.

```swift 
func calculateAverageAge(_ ages: [Int]) -> Double {
  var sumOfAges = 0
  for age in ages {
    sumOfAges += age
  }
  return Double(sumOfAges / ages.count)
}
```

![big O chart](https://miro.medium.com/max/1200/1*_nsMVEEkIr1CH8aHjTNbzA.jpeg)


## Space Complexity 

Space complexity is defined as the amount of memory a given algorithm takes. 

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

Call Stack 

<pre> 
sum(5)
  => sum(4)
    => sum(3)
      => sum(2)
        => sum(1) 
          => sum(0)
</pre>

#### Example 2 

In this example though we are calling `pairSum()` n times, the calls do not remain on the call stack like in `Example 1` so here the space complexity is constant `O(1)`.

```swift 
func pairSumSequence(_ k: Int) -> Int {
  var sum = 0
  for i in 0..<k {
    sum += pairSum(i, i + 1)
  }
  return sum
}

func pairSum(_ a: Int, _ b: Int) -> Int {
  return a + b
}

pairSumSequence(3) // 9
```

## Challenges 

#### 1. Challenge 1 
<details> 
  <summary>Solution</summary>
  
Testing.....  

</details>

## Resources 

[Cracking the Coding Interview](http://www.crackingthecodinginterview.com/)
[Big O Cheatsheet](https://www.bigocheatsheet.com/)

