# Big O

Big O. Time and Space complexity. 

In Computer Science and Programming the way in which we measure the performance and efficiency of algorithms is using **Big O notation**, _denoted_ `O()`. 

## Runtime Complexity 

Runtime complexity is described as the performance over time as the size of the input grows. 


#### Example 1

In the example below the runtime complexity of `calculateAverageAge` is `O(n)`, read (big O of n). As the size of the `ages` array grows the efficiency of this algorithm grows linearly.

It is `O(n)` since we are iterating through each element, represented as `n` in the `ages` array. 

```swift 
func calculateAverageAge(_ ages: [Int]) -> Double {
  var sumOfAges = 0
  for age in ages {
    sumOfAges += age
  }
  return Double(sumOfAges / ages.count)
}
```

The Big O chart below shows common runtime complexities. 

![big O chart](https://miro.medium.com/max/1200/1*_nsMVEEkIr1CH8aHjTNbzA.jpeg)


#### Multi-Part Algorithms 

In this example the runtimes are added because we finish the work of the first `for loop` before doing the second. 

So we conclude that this runtime is `O(A + B)`. 

```swift 
func compoundFuncOne(_ arrA: [Int], _ arrB: [Int]) {
  for num in arrA {
    print(num)
  }
  for num in arrB {
    print(num)
  }
}
```

In this example we perform work in the inner `for loop` for every element in the outer `for loop` therefore we multiply the runtimes. 

The runtime becomes `O(A * B)`. 

```swift 
func compoundFuncTwo(_ arrA: [Int], _ arrB: [Int]) {
  for a in arrA {
    for b in arrB {
      print("\(a) + \(b)")
    }
  }
}
```

#### `O(log n)` runtime

One of the best examples of `O(log n)` runtime is binary search, where the given sorted array is cut in half on each search. Similar algorithms that divides the problem in halves like merge sort, quicksort do have `O(log n)` runtime in their final runtimes but since more work is involved those end up with `O(n log n)` runtimes. 

#### Drop the constants 

In calculating Big O runtimes we drop the constants. 

Below the given runtime when compounded is `O(n + n)` or `O(2n)` or better written as `O(n)`. 

```swift 
let names = ["Alex", "Paul"]

for char in names {
  print(char.lowercased())
}

for char in names {
  print(char.uppercased())
}
```


## Space Complexity 

Space complexity is defined as the amount of memory a given algorithm takes. 

#### Example 1

In this example the `sum(_:)` function is being called recursively and decrementing the value of `k` until it reaches the `base case` of 0 and returns the value from the `call stack`. Here the `runtime complexity` is `O(n)` as we count how many times the recursive call happens and the `space complexity` is also `O(n)` as it takes space on the call stack. 

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

#### Challenge 1

What is the runtime complexity of the given algorithm? 

```swift
func sumProduct(_ arr: [Int]) {
  var sum = 0
  var product = 1
  for num in arr {
    sum += num
  }
  for num in arr {
    product *= num
  }
  print("sum is \(sum), and product is \(product)")
}
```

<details> 
  <summary>Solution</summary>
  
`O(n)` because we add the runtimes and since both for loops are iterating through the same array denoted a `n` it is `O(n)`

</details>

#### Challenge 2

What is the runtime complexity of the given algorithm? 

```swift
func printPairs(_ arr: [Int]) {
  for i in 0..<arr.count {
    for j in 0..<arr.count {
      print("\(arr[i]), \(arr[j])")
    }
  }
}
```

<details> 
  <summary>Solution</summary>
  
`O(n ^ 2)` here the first for loop calls the inner for loop on each of it's elements, so we multiply the runtimes. Since both are the same collection and we use `n` to represent the collection we say the runtime is `n * n ` or `O(n ^ 2)`.

</details>

#### Challenge 3

What is the runtime complexity of the given algorithm? 

```swift

```

<details> 
  <summary>Solution</summary>
  

</details>

#### Challenge 4

What is the runtime complexity of the given algorithm? 

```swift

```

<details> 
  <summary>Solution</summary>
  

</details>

#### Challenge 5

What is the runtime complexity of the given algorithm? 

```swift

```

<details> 
  <summary>Solution</summary>
  

</details>


#### Challenge 6

What is the runtime complexity of the given algorithm? 

```swift

```

<details> 
  <summary>Solution</summary>
  

</details>


#### Challenge 7

What is the runtime complexity of the given algorithm? 

```swift

```

<details> 
  <summary>Solution</summary>
  

</details>

#### Challenge 8

What is the runtime complexity of the given algorithm? 

```swift

```

<details> 
  <summary>Solution</summary>
  

</details>

#### Challenge 9

What is the runtime complexity of the given algorithm? 

```swift

```

<details> 
  <summary>Solution</summary>
  

</details>

#### Challenge 10

What is the runtime complexity of the given algorithm? 

```swift

```

<details> 
  <summary>Solution</summary>
  

</details>

## Resources 

1. [Cracking the Coding Interview](http://www.crackingthecodinginterview.com/)
2. [Big O Cheatsheet](https://www.bigocheatsheet.com/)

