# Big O Notation

When we have different ways to write a function or solve a problem we can use Big O notation to help us determine which one performs the best

## The problem with time performance

- same machines will record different times
- when measuring time performance on machines results will vary depending on different machines
- for fast algorithms, speed measurements may not be precise enough

Instead of using time to measure we can use the number of actions machine has to perform

# Introducing Big O

- a way to formalize fuzzy counting
- allows us to formally talk about the runtime of an algorithm grows as the inputs grow
- we mostly care about the trends andhow the general look of the performance is
-

## Simplifying Big O

- Constants dont matter
  - O(2n) is the same as O(n)
  - O(500) is the same as O(1)
  - O(13n^2) is the same as O(n^2)
  - If we look at these graphically, no matter the constant the graph of run time is going to be the same
- Smaller Terms Don't matter
  - O(n+10) is the same as O(n)
  - O(1000n+50) is the same as O(n)
  - O(n^2 + 5n +8) is the same as O(n^2)

## Big O Shorthands

- arithmetic operations are constant
- variable assignments are constant
- accessing elements in an array by index or key is constant
- in a loop, the complexity is the length of the loop times the complexity of whatever happens inside the llop

## Time complexity

- how we can analyze the run time of an application as the input increases

## Space Complexity

- how much additional memory do we need in order to run our algorithm
- auxilary space complexity
  - the space that is taken up by the algorithm
  - does not take into account the space that the input needs
- Rules of thumb
  - most primitives are constant space (booleans, numbers, undefined, null)
  - strings require O(n) space where n is the length of the string
  - reference types are generally O(n) where n is the length of an array or the number of keys for objects

## Logrithms

rule of thumb

- the logrithm of a number roughly measures the ammount of times you can divide a number by 2 before you get a value that is less thnan or equal to one
- for example 8 can be divided by 2 3 times, where a number like 25 is 4...something
