Recursion is a Function that calls itself until the problem is solved, we can consider the problem solved when we reach the Base Case.

ALWAYS think what your Base Case is.


This [video](https://www.youtube.com/watch?v=ngCos392W4w) helps a lot on visualizing how to build a recursive function based on its iterations.
The purpose of Recursion is that in each invocation of the recursive function, we get a little closer to the solution of a problem.

1. What is the simples possible input?
2. Play around with examples and visualize.
3. Relate hard cases to simpler cases.
4. Generalize the pattern.
5. Write code by combining recursive pattern with the base case.

# Factorial
![[Pasted image 20230213164408.png]]
In the above doodle we can clearly see that each factorial is calculated by multiplying the current value of `n` by the previous number's factorial.

```js
const factorial = (n) => {
  if (n < 1) {
    return 1;
  }

  return n * factorial(n - 1);
};```

# String Reversal

![[Pasted image 20230213192103.png]]

Above we can see that the smallest work we can do in each invocation is to get the last character of the string and concat the reverse of the REST of the string.

```js
const reverse = (str) => {
  console.log("STR", str);

  if (str.length === 1) {
    return str;
  }

  const strLength = str.length;

  return str[strLength - 1] + reverse(str.slice(0, strLength - 1));
};

```
