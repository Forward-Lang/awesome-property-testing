# Awesome Property Testing [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

A curated collection of property tests for various data structures, algorithms, and properties.
This repository aims to provide a comprehensive set of property-based tests across different programming languages, frameworks, and domains.
Property testing is a powerful technique to help you ensure your code behaves correctly under a wide range of conditions by automatically generating input values and testing the properties of your code.

## Contents

- [What is Property Testing?](#what-is-property-testing)
- [Why Property Testing?](#why-property-testing)
- [Property Tests](#property-tests)
  - [Queues](#queues)
  - [Lists](#lists)
  - [Strings](#strings)
  - [Numbers](#numbers)
  - [More Tests](#more-tests)
- [Popular Property Testing Libraries](#popular-property-testing-libraries)

## Contributing

We welcome contributions to this repository! 
Please read the [contribution guidelines](CONTRIBUTING.md) first, and follow the steps writen there.

## What is Property Testing

Property testing is a technique where you define general properties (invariants) about your program, and then the testing framework generates random inputs to check whether the properties hold true. 
Unlike traditional unit tests, which test specific scenarios, property tests explore a broader set of possible inputs, including edge cases, and often find bugs that you might not have considered.

For example, when testing a queue, a property might be that the size of the queue never goes negative after enqueue and dequeue operations, or that the first item dequeued is always the first one enqueued (FIFO).

## Why Property Testing

- **Automates Edge Case Discovery**: Property tests generate a wide range of input values, which often uncovers edge cases that you wouldn't think of manually.
- **Helps Prove Correctness**: If a property test passes for all generated inputs, it helps give you confidence that your code behaves as expected across many scenarios.
- **Improves Code Quality**: Property testing encourages writing more general and robust code that handles a variety of situations, rather than specific predefined cases.

## Property Tests

### Numbers

- **Arithmetic Operations**:
- Addition (`+`)
	- **Commutative**: $a + b = b + a$.
	- **Associative**: $(a + b) + c = a + (b + c)$.  
	- **Identity**: The identity element is 0: $a + 0 = a$.
	- **Inverse**: For any $a$, the additive inverse is $-a$: $a + (-a) = 0$.
	- **Idempotent**: No.  $a + a \neq a$ unless $a = 0$.
	- **Closure**: Yes.  For any $a, b$ in the set of real numbers $\mathbb{R}$, $a + b$ is also in $\mathbb{R}$.
- Subtraction (`-`)
	- **Commutative**: No.  $a - b \neq b - a$ in general.
	- **Associative**: No.  $(a - b) - c \neq a - (b - c)$.
	- **Identity**: Yes.  The identity element is 0: $a - 0 = a$.
	- **Inverse**: Yes.  Subtraction is essentially addition with the additive inverse: $a - b = a + (-b)$.
	- **Idempotent**: No.  $a - a = 0$, so the result is not $a$.
	- **Closure**: Yes.  For any $a, b$ in $\mathbb{R}$, $a - b$ is in $\mathbb{R}$.
	- **Symmetric**: No.  Subtraction is not symmetric because $a - b \neq b - a$.
- Multiplication (`*`)
	- **Commutative**: Yes.  $a \cdot b = b \cdot a$.
	- **Associative**: Yes.  $(a \cdot b) \cdot c = a \cdot (b \cdot c)$.
	- **Distributive**: Yes (over addition and subtraction).  $a \cdot (b + c) = a \cdot b + a \cdot c$.
	- **Identity**: Yes.  The identity element is 1: $a \cdot 1 = a$.
	- **Inverse**: Yes (for nonzero elements).  The multiplicative inverse of $a \neq 0$ is $1/a$: $a \cdot (1/a) = 1$.
	- **Idempotent**: No.  $a \cdot a \neq a$ unless $a = 0$ or $a = 1$.
	- **Closure**: Yes.  For $a, b \in \mathbb{R}$, $a \cdot b \in \mathbb{R}$.
	- **Absorption**: Yes.  The absorbing element is 0: $a \cdot 0 = 0$.
- Division (`/`)
	- **Commutative**: No.  $a / b \neq b / a$ in general.
	- **Associative**: No.  $(a / b) / c \neq a / (b / c)$.
	- **Distributive**: No.  Division does not distribute over addition or subtraction.
	- **Identity**: Yes.  Dividing by 1 does not change the value: $a / 1 = a$.
	- **Inverse**: Yes (for nonzero elements).  Division is multiplication by the reciprocal: $a / b = a \cdot (1/b)$, assuming $b \neq 0$.
	- **Idempotent**: No.  $a / a = 1$, so the result is not $a$.
	- **Closure**: Yes (if excluding division by 0).  For $a, b \in \mathbb{R}$ and $b \neq 0$, $a / b \in \mathbb{R}$.
	- **Symmetric**: No.  Division is not symmetric because $a / b \neq b / a$.
- Floor Division (`//`)
- Modulus (`%`)
- Exponentiation (`**`)

### **Summary Table**

| Property         | Addition (+) | Subtraction (-) | Multiplication (*) | Division (/) |
|------------------|--------------|------------------|---------------------|--------------|
| **Commutative**  | Yes          | No               | Yes                 | No           |
| **Associative**  | Yes          | No               | Yes                 | No           |
| **Distributive** | No           | No               | Yes                 | No           |
| **Identity**     | Yes (0)      | Yes (0)          | Yes (1)             | Yes (1)      |
| **Inverse**      | Yes          | Yes              | Yes (nonzero)       | Yes (nonzero)|
| **Idempotent**   | No           | No               | No                  | No           |
| **Closure**      | Yes          | Yes              | Yes                 | Yes (except b = 0) |
| **Absorption**   | No           | No               | Yes (0)             | No           |
| **Symmetric**    | No           | No               | No                  | No           |
| **Transitive**   | N/A          | N/A              | N/A                 | N/A          |

  
### 2. **Strings**:
- **Basic Operations**:
  - Concatenation (`+`)
  - Repetition (`*`)
  - Slicing (`str[start:end]`)
  - Length (`len()`)

### **1. Concatenation (+ or .)**

Concatenation involves joining two strings s1s_1 and s2s_2 end-to-end.

1.  **Commutative**: No.  
    s1+s2≠s2+s1s_1 + s_2 \neq s_2 + s_1.  
    Example: "hello" + "world" ≠ "world" + "hello".
    
2.  **Associative**: Yes.  
    (s1+s2)+s3=s1+(s2+s3)(s_1 + s_2) + s_3 = s_1 + (s_2 + s_3).  
    Example: ("a" + "b") + "c" = "a" + ("b" + "c") = "abc".
    
3.  **Distributive**: No.  
    Concatenation doesn’t distribute over any operation like addition or slicing.
    
4.  **Identity**: Yes.  
    The identity element is the empty string ϵ\epsilon: s+ϵ=ss + \epsilon = s.
    
5.  **Inverse**: No.  
    There’s no general inverse operation for concatenation (you can't uniquely undo concatenation without extra context).
    
6.  **Idempotent**: No.  
    s+s≠ss + s \neq s, unless s=ϵs = \epsilon.
    
7.  **Closure**: Yes.  
    If s1s_1 and s2s_2 are strings, s1+s2s_1 + s_2 is also a string.
    
8.  **Absorption**: No.  
    There’s no absorbing element for concatenation.
    
9.  **Symmetric**: No.  
    Concatenation is not symmetric as the order matters.
    
10.  **Transitive**: Not applicable.  
    Transitivity is not meaningful for concatenation.
    
### **2. Repetition (∗*)**

Repetition creates a new string by repeating a base string ss nn-times (e.g., s∗ns * n).

1.  **Commutative**: No.  
    s∗n≠n∗ss * n \neq n * s.  
    Example: "a" * 3 = "aaa", but 3 * "a" is undefined in most languages.
    
2.  **Associative**: Yes (for scalar repetition).  
    (s∗n)∗m=s∗(n∗m)(s * n) * m = s * (n * m).  
    Example: ("a" * 2) * 3 = "aa" * 3 = "aaaaaa".
    
3.  **Distributive**: No.  
    Repetition doesn’t distribute over addition or concatenation.  
    Example: (s1+s2)∗n≠(s1∗n)+(s2∗n)(s_1 + s_2) * n \neq (s_1 * n) + (s_2 * n).
    
4.  **Identity**: Yes.  
    The identity element is 1: s∗1=ss * 1 = s.
    
5.  **Inverse**: No.  
    There is no universal way to "undo" repetition without ambiguity.
    
6.  **Idempotent**: No.  
    s∗n≠ss * n \neq s unless n=1n = 1.
    
7.  **Closure**: Yes.  
    Repeating a string ss nn-times results in another string.
    
8.  **Absorption**: Yes (in a specific sense).  
    Repetition by 0 results in the empty string: s∗0=ϵs * 0 = \epsilon.
    
9.  **Symmetric**: No.  
    Repetition is not symmetric.
    
10.  **Transitive**: Not applicable.  
    Transitivity doesn’t apply to repetition.
    
### **3. Slicing ([start:end])**

Slicing extracts a substring from a given string.

1.  **Commutative**: No.  
    The order of indices matters: s[1:3]≠s[3:1]s[1:3] \neq s[3:1] (and reversing indices is often invalid).
    
2.  **Associative**: No.  
    Nesting slices doesn’t always give the same result as a single slice.
    
3.  **Distributive**: No.  
    Slicing doesn’t distribute over concatenation or repetition.
    
4.  **Identity**: Yes.  
    The identity slice is [:][:], which returns the whole string: s[:]=ss[:] = s.
    
5.  **Inverse**: No.  
    Slicing cannot be reversed unless the original context is known.
    
6.  **Idempotent**: Yes.  
    Reapplying the same slice gives the same result: s[1:3][0:2]=s[1:3]s[1:3][0:2] = s[1:3].
    
7.  **Closure**: Yes.  
    A slice of a string is always a string.
    
8.  **Absorption**: No.  
    There’s no absorbing element in slicing.
    
9.  **Symmetric**: No.  
    Slicing is not symmetric as the indices and order matter.
    
10.  **Transitive**: Not applicable.  
    Transitivity doesn’t apply to slicing.
    
### **4. Length (len(s)len(s))**

Length calculates the number of characters in a string.

- **Commutative**: Not applicable.  
    Length isn’t a binary operation.
    
- **Associative**: Not applicable.  
    Associativity doesn’t apply to length as it’s a single-input function.
    
- **Distributive**: No.  
    Length doesn’t distribute over concatenation or slicing: len(s1+s2)=len(s1)+len(s2)len(s_1 + s_2) = len(s_1) + len(s_2), but this isn’t distribution in a strict sense.
    
- **Identity**: Yes.  
    len(ϵ)=0len(\epsilon) = 0.
    
- **Inverse**: No.  
    There’s no inverse operation for length.
    
- **Idempotent**: Yes.  
    Reapplying the length operation gives the same result: len(len(s))=len(s)len(len(s)) = len(s).
    
- **Closure**: Yes.  
    The length of a string is always a non-negative integer.
    
- **Absorption**: No.  
    There’s no absorbing element for length.
    
- **Symmetric**: Not applicable.  
    Symmetry doesn’t apply to length.
    
- **Transitive**: Not applicable.  
    Transitivity doesn’t apply to length.
    

  
### 3. **Lists**:
- **Basic Operations**:
  - Indexing (`list[index]`)
  - Slicing (`list[start:end]`)
  - Length (`len()`)
  - Adding elements (`list.append()`, `list.insert()`)
  - Removing elements (`list.remove()`, `list.pop()`)
  - Modifying elements (`list[index] = value`)
  - Concatenation (`+`)
  - Repetition (`*`)
- **List Methods**:
  - Sort (`list.sort()`)
  - Reverse (`list.reverse()`)
  - Extend (`list.extend()`)
  - Copy (`list.copy()`)
  - Count occurrences (`list.count()`)
  - Find index (`list.index()`)
  - Clear list (`list.clear()`)
  
### 4. **Stacks** (often implemented with lists in Python):
- **Basic Operations**:
  - Push (add an element to the stack): `stack.append()`
  - Pop (remove and return the top element): `stack.pop()`
  - Peek (view the top element without removing it): `stack[-1]`
  - Check if empty: `not stack` or `len(stack) == 0`
  - Size (number of elements in stack): `len(stack)`
  - Clear stack: `stack.clear()`

### Operations on Numbers

- **Test if dividing by  zero**. 

[See the full list of number property tests](property-tests/numbers.md)

### Operations on Strings


[See the full list of string property tests](property-tests/strings.md)

### Operations on Lists

- **Test if list reversal followed by another reversal results in the original list**.
- **Test if list concatenation is associative**.
- **Test if the length of a list remains the same after reversal**.
- **Test if adding elements to the front or back of the list gives the expected results**.

[See the full list of list property tests](property-tests/lists.md)

### Operations on Stacks

- **Test if a queue is empty after a pop from an empty queue**.
- **Test if enqueue followed by dequeue returns the correct element**.
- **Test if the queue maintains the correct size after multiple enqueue and dequeue operations**.
- **Test for commutative property for queue reversals**.
- **Test if the queue's size is always non-negative**.

[See the full list of queue property tests](property-tests/queues.md)

### More Tests

- We will continue to add tests for additional data structures and algorithms over time. Stay tuned for more!

## Popular Property Testing Libraries

Here are some popular property testing libraries that can help you get started in various programming languages:

- **[QuickCheck](https://hackage.haskell.org/package/QuickCheck)** - Haskell
- **[Hypothesis](https://hypothesis.readthedocs.io/en/latest/)** - Python
- **[FsCheck](https://fscheck.github.io/FsCheck/)** - F#
- **[ScalaCheck](https://github.com/typelevel/scalacheck)** - Scala
- **[fast-check](https://github.com/dubzzz/fast-check)** - JavaScript
- **[Test.check](https://github.com/clojure/test.check)** - Clojure

Feel free to contribute any other libraries you use for property testing!
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwNTgyNDA4OTcsLTE5MDM2MDQxMDEsLT
Y2NDU5ODI0MSwxNjQ0NTY2NjYxLC0xMjA2ODE1NDM4LDEyOTg2
OTgzNCw2ODU3NTQ5NzksMTMxNjgzOTY2NiwxNzQ1Njc1NTY0XX
0=
-->