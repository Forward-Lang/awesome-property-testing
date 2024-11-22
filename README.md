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
	- **Closure**: Yes.  For any $a, b$ in the set of real numbers $\mathbb{R}$, $a + b$ is also in $\mathbb{R}$.
- Subtraction (`-`)
	- **Commutative**: No.  $a - b \neq b - a$ in general.
	- **Associative**: No.  $(a - b) - c \neq a - (b - c)$.
	- **Identity**: Yes.  The identity element is 0: $a - 0 = a$.
	- **Inverse**: Yes.  Subtraction is essentially addition with the additive inverse: $a - b = a + (-b)$.
	- **Closure**: Yes.  For any $a, b$ in $\mathbb{R}$, $a - b$ is in $\mathbb{R}$.
- Multiplication (`*`)
	- **Commutative**: Yes.  $a \cdot b = b \cdot a$.
	- **Associative**: Yes.  $(a \cdot b) \cdot c = a \cdot (b \cdot c)$.
	- **Distributive**: Yes (over addition and subtraction).  $a \cdot (b + c) = a \cdot b + a \cdot c$.
	- **Identity**: Yes.  The identity element is 1: $a \cdot 1 = a$.
	- **Inverse**: Yes (for nonzero elements).  The multiplicative inverse of $a \neq 0$ is $1/a$: $a \cdot (1/a) = 1$.
	- **Closure**: Yes.  For $a, b \in \mathbb{R}$, $a \cdot b \in \mathbb{R}$.
	- **Absorption**: Yes.  The absorbing element is 0: $a \cdot 0 = 0$.
- Division (`/`)
	- **Commutative**: No.  $a / b \neq b / a$ in general.
	- **Distributive**: No.  Division does not distribute over addition or subtraction.
	- **Identity**: Yes.  Dividing by 1 does not change the value: $a / 1 = a$.
	- **Inverse**: Yes (for nonzero elements).  Division is multiplication by the reciprocal: $a / b = a \cdot (1/b)$, assuming $b \neq 0$.
	- **Closure**: Yes (if excluding division by 0).  For $a, b \in \mathbb{R}$ and $b \neq 0$, $a / b \in \mathbb{R}$.
- Floor Division (`//`)
- Modulus (`%`)
- Exponentiation (`**`)
- **Arithmetic Relations**:

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

  
### 2. **Strings**:
- **Basic Operations**:
 - Concatenation (`+`): Concatenation involves joining two strings $s_1$ and $s_2$ end-to-end.
	- **Commutative**: No.  $s_1 + s_2 \neq s_2 + s_1$.  Example: "hello" + "world" ≠ "world" + "hello".
	- **Associative**: Yes.  $(s_1 + s_2) + s_3 = s_1 + (s_2 + s_3)$.  Example: ("a" + "b") + "c" = "a" + ("b" + "c") = "abc".
	- **Identity**: Yes.  The identity element is the empty string $\epsilon$: $s + \epsilon = s$.
	- **Inverse**: No.  There’s no general inverse operation for concatenation (you can't uniquely undo concatenation without extra context).
	- **Closure**: Yes.  If $s_1$ and $s_2$ are strings, $s_1 + s_2$ is also a string.
 - Repetition (`*`): Repetition creates a new string by repeating a base string $s$ $n$-times (e.g., $s * n$).
	- **Commutative**: No.  $s * n \neq n * s$.  Example: "a" * 3 = "aaa", but 3 * "a" is undefined in most languages.
	- **Distributive**: No.  Repetition doesn’t distribute over addition or concatenation. Example: $(s_1 + s_2) * n \neq (s_1 * n) + (s_2 * n)$.
	- **Identity**: Yes.  The identity element is 1: $s * 1 = s$.
	- **Inverse**: No.  There is no universal way to "undo" repetition without ambiguity.
	- **Closure**: Yes.  Repeating a string $s$ $n$-times results in another string.
	- **Absorption**: Yes (in a specific sense).  Repetition by 0 results in the empty string: $s * 0 = \epsilon$.
 - Slicing (`str[start:end]`): Slicing extracts a sub-string from a given string.
	- **Commutative**: No.  The order of indices matters: $s[1:3] \neq s[3:1]$ (and reversing indices is often invalid).
	- **Identity**: Yes.  The identity slice is $[:]$, which returns the whole string: $s[:] = s$.
	- **Inverse**: No.  Slicing cannot be reversed unless the original context is known.
	- **Idempotent**: Yes.  Reapplying the same slice gives the same result: $s[1:3][0:2] = s[1:3]$.
	- **Closure**: Yes.  A slice of a string is always a string.
 - Length (`len()`): Length calculates the number of characters in a string.
	- **Distributive**: No.  Length doesn’t distribute over concatenation or slicing: $len(s_1 + s_2) = len(s_1) + len(s_2)$, but this isn’t distribution in a strict sense.
	- **Identity**: Yes.  $len(\epsilon) = 0$.
	- **Idempotent**: Yes.  Reapplying the length operation gives the same result: $len(len(s)) = len(s)$.
	- **Closure**: Yes.  The length of a string is always a non-negative integer.

---

### **1. String Comparison**

String comparison involves checking the equality or relative lexicographical order of two strings.

1.  **Equality (==):** Checks if two strings are the same.
    
    -   **Commutative**: Yes. s1==s2  ⟺  s2==s1s_1 == s_2 \iff s_2 == s_1.
    -   **Associative**: Not applicable.
    -   **Identity**: No identity element exists.
    -   **Closure**: Yes. Always results in a Boolean value (True or False).
    -   **Symmetric**: Yes. Equality is symmetric.
    -   **Transitive**: Yes. If s1==s2s_1 == s_2 and s2==s3s_2 == s_3, then s1==s3s_1 == s_3.
2.  **Lexicographical Order (<, >, <=, >=):** Compares strings based on their order in the alphabet or Unicode table.
    
    -   **Commutative**: No. s1<s2≠s2<s1s_1 < s_2 \neq s_2 < s_1.
    -   **Associative**: Not applicable.
    -   **Identity**: Not relevant.
    -   **Closure**: Yes. Always results in a Boolean value.
    -   **Symmetric**: No. s1<s2s_1 < s_2 doesn’t imply s2<s1s_2 < s_1.
    -   **Transitive**: Yes. If s1<s2s_1 < s_2 and s2<s3s_2 < s_3, then s1<s3s_1 < s_3.

### **2. String Search/Containment (`in`, `find`, or `index`)**

These operations determine whether a substring exists within a string.

1.  **Containment (`in`):**
    
    -   **Commutative**: No. "a"in"ab"≠"ab"in"a""a" in "ab" \neq "ab" in "a".
    -   **Associative**: Not applicable.
    -   **Identity**: No identity element exists.
    -   **Closure**: Yes. Always results in a Boolean value.
    -   **Symmetric**: No. Containment is directional.
    -   **Transitive**: Not applicable.
2.  **Find/Index:** Returns the position of the first occurrence of a substring.
    
    -   **Commutative**: No. The order of the strings matters.
    -   **Associative**: Not applicable.
    -   **Identity**: No identity element exists.
    -   **Closure**: Yes. Returns an integer or a "not found" indicator.
    -   **Symmetric**: No.
    -   **Transitive**: Not applicable.

### **3. String Replacement (`replace`)**

This operation replaces all occurrences of a substring s1s_1 in ss with another substring s2s_2.

-   **Commutative**: No. s.replace("a","b")≠s.replace("b","a")s.replace("a", "b") \neq s.replace("b", "a").
-   **Associative**: No. Chaining replacements doesn’t guarantee equality:  
    s.replace("a","b").replace("b","c")≠s.replace("a","c")s.replace("a", "b").replace("b", "c") \neq s.replace("a", "c").
-   **Identity**: Yes. Replacing """" (empty string) with """" doesn’t alter the string.
-   **Closure**: Yes. The result is always a string.
-   **Idempotent**: Yes, under certain conditions: s.replace("x","y").replace("x","y")=s.replace("x","y")s.replace("x", "y").replace("x", "y") = s.replace("x", "y").
-   **Absorption**: No. There’s no absorbing element.

### **4. String Reversal (`[::-1]`)**

This operation reverses the order of characters in a string.

-   **Commutative**: No. s[::−1]≠ss[::-1] \neq s unless ss is a palindrome.
-   **Associative**: Not applicable.
-   **Identity**: Yes. Applying reversal twice gives the original string: (s[::−1])[::−1]=s(s[::-1])[::-1] = s.
-   **Closure**: Yes. The result is always a string.
-   **Idempotent**: No. Applying reversal doesn’t yield the same string unless the input is symmetric.
-   **Absorption**: No.

### **5. Case Conversion (`lower`, `upper`, `capitalize`, etc.)**

These operations change the case of characters in a string.

-   **Commutative**: No. s.lower().upper()≠s.upper().lower()s.lower().upper() \neq s.upper().lower() in general.
-   **Associative**: No. Chaining case operations might not result in the same outcome:  
    s.lower().capitalize()≠s.capitalize().lower()s.lower().capitalize() \neq s.capitalize().lower().
-   **Identity**: Yes. Applying lowerlower or upperupper to an already lowercase or uppercase string leaves it unchanged.
-   **Closure**: Yes. The result is always a string.
-   **Idempotent**: Yes. Applying lowerlower or upperupper multiple times has no additional effect.
-   **Absorption**: No.

### **6. Substring Splitting and Joining (`split`, `join`)**

1.  **Splitting (`split`):** Breaks a string into parts based on a delimiter.
    
    -   **Commutative**: No. The delimiter order or existence affects the split.
    -   **Associative**: No. Nesting splits isn’t generally equivalent.
    -   **Identity**: Yes. Splitting on a non-existent delimiter leaves the string intact as a single-element list.
    -   **Closure**: Yes. Results in a list of strings.
    -   **Idempotent**: No. Re-splitting the result is not equivalent to the original split.
2.  **Joining (`join`):** Combines elements of a list into a single string using a delimiter.
    
    -   **Commutative**: No. The order of elements in the list matters.
    -   **Associative**: Yes. Joining nested joins results in a single string.
    -   **Identity**: Yes. Joining an empty list results in an empty string.
    -   **Closure**: Yes. The result is always a string.
    -   **Idempotent**: No.

### **7. String Formatting**

Operations like interpolation, substitution, or formatting (e.g., f-strings in Python or printf-style in C) insert values into string templates.

-   **Commutative**: No. The order of values and placeholders matters.
-   **Associative**: No. Nesting formatted strings doesn’t guarantee equality.
-   **Identity**: Yes. An empty template or unused placeholders do not alter the original template.
-   **Closure**: Yes. Results in a string.
-   **Idempotent**: No.

### Additional Operations:

1.  **Trimming (`strip`, `lstrip`, `rstrip`)**: Removes whitespace or specific characters from a string.
2.  **Character Counting (`count`)**: Counts the occurrences of a substring.
3.  **Checking Operations (`startswith`, `endswith`, `isalnum`, `isdigit`, etc.)**: Boolean checks on string properties.

These string operations can be examined in-depth using the same properties framework, making them a rich area for logical exploration! Let me know if you'd like a specific one analyzed further.

---
  
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
eyJkaXNjdXNzaW9ucyI6eyJVZkZXbDFLMnJKMnd3Wnd3Ijp7In
N0YXJ0Ijo2MjQyLCJlbmQiOjYzMjksInRleHQiOiJJbnZlcnNl
Kio6IE5vLiAgVGhlcmUgaXMgbm8gdW5pdmVyc2FsIHdheSB0by
BcInVuZG9cIiByZXBldGl0aW9uIHdpdGhvdXQgYW1iaWd1aXTi
gKYifSwiR2FyV3ByM2FuZ0RoUGtiSiI6eyJzdGFydCI6NTU4Ni
wiZW5kIjo1NzI1LCJ0ZXh0IjoiSW52ZXJzZSoqOiBOby4gIFRo
ZXJl4oCZcyBubyBnZW5lcmFsIGludmVyc2Ugb3BlcmF0aW9uIG
ZvciBjb25jYXRlbmF0aW9uICh5b3UgY2Fu4oCmIn19LCJjb21t
ZW50cyI6eyIzOHhUTFk4cWE1Q0o2cmNCIjp7ImRpc2N1c3Npb2
5JZCI6IlVmRldsMUsyckoyd3dad3ciLCJzdWIiOiJnaDo4MTc2
MjE3MyIsInRleHQiOiJ3aGF0IGFib3V0IHJlcGVhdGluZyBuZW
dhdGl2ZSB0aW1lcz8iLCJjcmVhdGVkIjoxNzMyMjg3MDI2Njcw
fSwiYlhGQnVCM094SThuUWFZdSI6eyJkaXNjdXNzaW9uSWQiOi
JHYXJXcHIzYW5nRGhQa2JKIiwic3ViIjoiZ2g6ODE3NjIxNzMi
LCJ0ZXh0Ijoid2hhdCBhYm91dCBzcGxpdD8iLCJjcmVhdGVkIj
oxNzMyMjg3MTMzODQyfX0sImhpc3RvcnkiOlstNjM3NDk4MDIz
LC0xMDU2NjUwMDAyLC0xMDIxOTkzOTMzLDE1MzczODYwMzEsMj
AxNjUzMzE3MCwxODAzMTc0MjIyLC0xOTAzNjA0MTAxLC02NjQ1
OTgyNDEsMTY0NDU2NjY2MSwtMTIwNjgxNTQzOCwxMjk4Njk4Mz
QsNjg1NzU0OTc5LDEzMTY4Mzk2NjYsMTc0NTY3NTU2NF19
-->