# Big O Notation

Big O. Time and Space complexity. 

In Computer Science and Programming the way in which we measure the performance and efficiency of algorithms is using **Big O notation**, _denoted_ `O()`. 

## Runtime Complexity 

Runtime complexity is used to describe the efficiency of a given algorithm as the size of the input grows. 

| Big O Notation | Name | 
|:-----:|:------:|
| O(1) | constant |
| O(log n) | logarithmic	| 
| O(n) | linear	| 
| O(n log n) | linearithmic	| 
| O(n ^ 2) | quadratic	| 
| O(n ^ 3) | cubic	| 
| O(n ^ y) | polynomial	| 
| O(2 ^ n) | exponential	| 
| O(n!) | factorial	| 


#### Example 1

In the example below the runtime complexity of `calculateAverageAge` is `O(n)`, read (big O of n). As the size of the `ages` array grows the efficiency of this algorithm grows linearly.

It is `O(n)` since we are iterating through each element, represented as `n` in the `ages` array. `n` is the length of the array.

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

In this example the runtimes are added because we finish the work of the first `for loop` before running the second `for loop`. 

So we conclude that this runtime is `O(A + B)`. We use the variables `A` and `B` to represent each array since they are different. If the two arrays were the same the runtime would be for example `A` + `A` which would be `O(A)` since we ignore constants.  

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

The runtime becomes `O(A * B)` or `O(AB)`. 

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

One of the best examples of `O(log n)` runtime is binary search, where the given sorted array is cut in half on each search. 

Similar algorithms that divides problems in halves like merge sort, quicksort do have `O(log n)` runtime in their final runtimes but since more work is involved those end up with `O(n log n)` runtimes. 

#### Drop the constants 

In calculating Big O runtimes we drop the constants. 

Below the given runtime is `O(n + n)` or `O(2n)` or better written as `O(n)` since we ignore constants in runtime calculations. 

```swift 
let names = ["Alex", "Paul"]

for char in names {
  print(char.lowercased())
}

for char in names {
  print(char.uppercased())
}
```

#### Some runtimes of Swift Built-in types 

#### `contains(_:)` on a Array 

`O(n)`

#### `contains(_:)` on a Set 

`O(1)`

#### `sorted()` on a collection 

`O(n log n)`

#### `map()`, `filter()`, `reduce()`

`O(n)`

## Space Complexity 

Space complexity is defined as the amount of memory needed for a given algorithm. As the input sizes increases the amount of space increases accordingly. 


| Type | Bit Width | Range |
|:-----:|:------:|:------:|
| Int8 | 1byte | -127 to 127 |
| UInt8 | 1byte	| 0 to 255 |
| Int32 |	4bytes | -2147483648 to 2147483647 |
| UInt32 | 4bytes | 0 to 4294967295 |
| Int64 |	8bytes | -9223372036854775808 to 9223372036854775807 |
| UInt64 | 8bytes | 0 to 18446744073709551615 |
| Float |	4bytes | 1.2E-38 to 3.4E+38 (~6 digits) |
| Double | 8bytes | 2.3E-308 to 1.7E+308 (~15 digits) |

> Note: If you're on a 64-bit platform, Int is the same size a Int64. You can try this in playgrounds by running `print(Int.max)`. On my machine the output is `9223372036854775807`.

#### Example 1 

Here the `add(:_)` function takes two inputs of type `Int` and returns and `Int`. Each of those variables take up `constant` memory or `8 bytes` each on a 64-bit platform like macOS, we calculate the space each variable takes which is 8 bytes from variable `a` + 8 bytes for variable `b` which sums up to 16 bytes, therefore when concluding the big O complexities we ignore constants and get a space complexity of `O(1)`.  

```swift 
func add(_ a: Int, _ b: Int) -> Int {
  return a + b
}
```

#### Example 2 

The `addSavings(:_)` function takes an input array `savings` and iterates this array for each `Double` element it contains, since this array is not a constant and has `n` elements we have to consider this when calculating space complexity, therefore we conclude that the amount of memory it takes for the given algorithm is `O(n)`. 

Space complexity calculation: size of array * memory per element, n * 8 bytes, since we ignore the constant the space complexity is `O(n)`. 

```swift 
func addSavings(_ savings: [Double]) -> Double {
  var sum = 0.0
  for saving in savings {
    sum += saving
  }
  return sum
}
```

#### Example 3

In this example the `sum(_:)` function is being called recursively and decrementing the value of `k` until it reaches the `base case` of 0 and returns the value from the `call stack`. Here the `runtime complexity` is `O(n)` as we count how many times the recursive call happens and the `space complexity` is also `O(n)` as it takes space on the call stack. 

```swift 
func recursionSum(_ k: Int) -> Int {
  guard k > 0 else {
    return 0
  }
  return k + recursionSum(k - 1)
}

recursionSum(5) // 5 + 4 + 3 + 2 + 1 = 15
```

Call Stack 

<pre> 
recursionSum(5)
  => recursionSum(4)
    => recursionSum(3)
      => recursionSum(2)
        => recursionSum(1) 
          => recursionSum(0)
</pre>

#### Example 4 

In this example though we are calling `pairSum()` n times, the calls do not remain on the call stack like in `recursionSum(:_)` so here the space complexity is constant `O(1)`.

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

## 1. Runtime Complexity

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
func printUnorderedPairs(_ arrA: [Int], _ arrB: [Int]) {
  for i in 0..<arrA.count {
    for j in 0..<arrB.count {
      if arrA[i] < arrB[j] {
        print("\(arrA[i]), \(arrB[j])")
      }
    }
  }
}
```

<details> 
  <summary>Solution</summary>
  
`O(ab)`, here since we have two different arrays a and b we treat the runtime using different variables a and b. As before we multiply such runtimes where the for loops are nested and result to a runtime of `O(a * b)` or `O(ab)`. 
  
</details>

#### Challenge 4

What is the runtime complexity of the given algorithm? 

```swift
func printUnorderedPairs(_ arrA: [Int], _ arrB: [Int]) {
  for i in 0..<arrA.count {
    for j in 0..<arrB.count {
      for k in 0..<100 {
        if arrA[i] < arrB[j] {
          print("\(arrA[i]), \(arrB[j]), \(k)")
        }
      }
    }
  }
}
```

<details> 
  <summary>Solution</summary>

The runtime is `O(ab)` regardless of the third `for loop`, remember when it comes to calculating runtimes that we drop the constants. 

</details>

#### Challenge 5

What is the runtime complexity of the given algorithm? 

```swift
func firstHalf(_ arr: [Int]) {
  for i in 0..<arr.count / 2 {
    print(arr[i])
  }
}
```

<details> 
  <summary>Solution</summary>
  
The runtime is `O(n)` despite the fact that we only iterate through first half of the array. 
  
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

## 2. Space Complexity

#### Challenge 1

What is the space complexity of the given algorithm? 

```swift
func addNumbers(a: Int, b: Int, c: Int) -> Int {
  return a + b + c
}
```

<details> 
  <summary>Solution</summary>

Space complexity is `O(1)`. a + b + c or 8 bytes + 8 bytes + 8 bytes = 24 bytes, we ignore constants as with calculating runtime and get a constant space complexity. 

</details>

#### Challenge 2

What is the space complexity of the given algorithm? 

```swift
func calculateShoppingCart(prices: [Double]) -> Double {
  var totalPrice = 0.0
  for price in prices {
    totalPrice += price
  }
  return totalPrice
}
```

<details> 
  <summary>Solution</summary>
  
Here we have an array of Double, the size of a Double is 8 bytes. The array has n elements. If we calculate each element's space needed for the for loop we see that n (size of array) * 8 bytes equates to a space complexity of `O(n * 8 bytes)` or `O(n)` again as we ignore the constant space taken. 

</details>


#### Challenge 3

What is the space complexity of the given algorithm? 

```swift
func square(_ value: Int) -> Int {
  return value * value
}
```

<details> 
  <summary>Solution</summary>
  
`O(1)`

</details>


#### Challenge 4

What is the space complexity of the given algorithm? 

```swift
func sayHiNTimes(_ k: Int) {
  guard k > 0 else {
    print("Be polite")
    return
  }
  for _ in 0..<k {
    print("hi")
  }
}
```

<details> 
  <summary>Solution</summary>
  
This algorithim is not taking up extra memory than supplied by the input. The input passed in is a constant, k of type `Int` which takes up 8 bytes and we disregard in our space complexity calculations, therefore the space complexity is `O(1)`. 

</details>


#### Challenge 5

What is the space complexity of the given algorithm? 

```swift
func listOfHiTimes(_ k: Int) -> [Int] {
  guard k > 0 else { return [] }
  var list = [Int]()
  for i in 0..<k {
    list.append(i)
  }
  return list
}
```

<details> 
  <summary>Solution</summary>
  
In this example the variable `list` array scales linearlly with the size of the input `k` which consumes memory inside the `for` loop when values are appending to it. Here the space complexity is `O(n)`.

</details>

#### Challenge 6

What is the space complexity of the given algorithm? 

```swift

```

<details> 
  <summary>Solution</summary>
  

</details>

## Resources 

1. [Cracking the Coding Interview](http://www.crackingthecodinginterview.com/)
2. [Big O Cheatsheet](https://www.bigocheatsheet.com/)
3. [Understanding Space Complexity](https://www.baeldung.com/cs/space-complexity)
4. [Interview Cake - Big O Notation](https://www.interviewcake.com/article/python/big-o-notation-time-and-space-complexity?)
5. [8 time complexities that every programmer should know](https://adrianmejia.com/most-popular-algorithms-time-complexity-every-programmer-should-know-free-online-tutorial-course/)

