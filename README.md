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

#### Addition (+)

1. **Commutative**: $$a + b = b + a$$.

2. **Associative**: $$(a + b) + c = a + (b + c)$$.
   
4. **Identity**: The identity element is 0: $$a + 0 = a$$.

5. **Inverse**: For any $$a$$, the additive inverse is $$-a$$: $$a + (-a) = 0$$.

6. **Idempotent**: No.  
   $$a + a \neq a$$ unless $$a = 0$$.

7. **Closure**: Yes.  
   For any $$a, b$$ in the set of real numbers $$\mathbb{R}$$, $$a + b$$ is also in $$\mathbb{R}$$.

#### Subtraction (-)

1. **Commutative**: No.  
   $$a - b \neq b - a$$ in general.

2. **Associative**: No.  
   $$(a - b) - c \neq a - (b - c)$$.

3. **Distributive**: No (not directly relevant on its own).

4. **Identity**: Yes.  
   The identity element is 0: $$a - 0 = a$$.

5. **Inverse**: Yes.  
   Subtraction is essentially addition with the additive inverse: $$a - b = a + (-b)$$.

6. **Idempotent**: No.  
   $$a - a = 0$$, so the result is not $$a$$.

7. **Closure**: Yes.  
   For any $$a, b$$ in $$\mathbb{R}$$, $$a - b$$ is in $$\mathbb{R}$$.

8. **Absorption**: No.  
   There is no "absorbing" element for subtraction.

9. **Symmetric**: No.  
   Subtraction is not symmetric because $$a - b \neq b - a$$.

10. **Transitive**: Not applicable to subtraction as a binary operation.

#### Multiplication (\(*\))

1. **Commutative**: Yes.  
   $$a \cdot b = b \cdot a$$.

2. **Associative**: Yes.  
   $$(a \cdot b) \cdot c = a \cdot (b \cdot c)$$.

3. **Distributive**: Yes (over addition and subtraction).  
   $$a \cdot (b + c) = a \cdot b + a \cdot c$$.

4. **Identity**: Yes.  
   The identity element is 1: $$a \cdot 1 = a$$.

5. **Inverse**: Yes (for nonzero elements).  
   The multiplicative inverse of $$a \neq 0$$ is $$1/a$$: $$a \cdot (1/a) = 1$$.

6. **Idempotent**: No.  
   $$a \cdot a \neq a$$ unless $$a = 0$$ or $$a = 1$$.

7. **Closure**: Yes.  
   For $$a, b \in \mathbb{R}$$, $$a \cdot b \in \mathbb{R}$$.

8. **Absorption**: Yes.  
   The absorbing element is 0: $$a \cdot 0 = 0$$.

9. **Symmetric**: No.  
   Symmetry is not a property of multiplication.

10. **Transitive**: Not applicable to multiplication as a binary operation.

#### Division (/)

1. **Commutative**: No.  
   $$a / b \neq b / a$$ in general.

2. **Associative**: No.  
   $$(a / b) / c \neq a / (b / c)$$.

3. **Distributive**: No.  
   Division does not distribute over addition or subtraction.

4. **Identity**: Yes.  
   Dividing by 1 does not change the value: $$a / 1 = a$$.

5. **Inverse**: Yes (for nonzero elements).  
   Division is multiplication by the reciprocal: $$a / b = a \cdot (1/b)$$, assuming $$b \neq 0$$.

6. **Idempotent**: No.  
   $$a / a = 1$$, so the result is not $$a$$.

7. **Closure**: Yes (if excluding division by 0).  
   For $$a, b \in \mathbb{R}$$ and $$b \neq 0$$, $$a / b \in \mathbb{R}$$.

8. **Absorption**: No.  
   There is no "absorbing" element for division.

9. **Symmetric**: No.  
   Division is not symmetric because $$a / b \neq b / a$$.

10. **Transitive**: Not applicable to division as a binary operation.

---

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

- **Arithmetic Operations**:
  - Addition (`+`)
  - Subtraction (`-`)
  - Multiplication (`*`)
  - Division (`/`)
  - Floor Division (`//`)
  - Modulus (`%`)
  - Exponentiation (`**`)
  
### 2. **Strings**:
- **Basic Operations**:
  - Concatenation (`+`)
  - Repetition (`*`)
  - Slicing (`str[start:end]`)
  - Length (`len()`)
  
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

- Addition
- Subst
- **Test if dividing by a non-zero number gives the correct result**.

[See the full list of number property tests](property-tests/numbers.md)

### Operations on Strings

- **Test if string reversal followed by another reversal results in the original string**.
- **Test if string concatenation is associative**.
- **Test if concatenating an empty string with another string results in the original string**.

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

[See more tests here](property-tests/more_tests.md)

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
eyJoaXN0b3J5IjpbLTIwODYyNTE2MzhdfQ==
-->