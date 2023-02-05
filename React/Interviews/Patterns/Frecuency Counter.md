Use objects or Maps to collect values/frequencies of values. This pattern can be used to avoid nested loops or expensive operations with arrays/strings.

Given to arrays of numbers, write a function that returns true if the second array contains all the numbers from the first array, squared. The occurrences should match, the order is irrelevant.

```js
arr1 = [1,2,3] arr2=[9,1,4]
freqCounter(arr1, arr2) // TRUE

arr1 = [1,2,3] arr2=[9,4,4]
freqCounter(arr1, arr2) // false

arr1 = [3,2,2] arr2=[9,4,4]
freqCounter(arr1, arr2) // TRUE
```

The "naive" approach would be to loop through `arr1` and nest a loop for `arr2` and write the logic there, this would entail a *O(n^2)*.

If we use Objects or Maps, we could eliminate the nested loop:

```js
const freqCounter = (array1, array2) => {
  if (arr1.length !== array2.length) {
    return false;
  }
  const arr1FreqMap = new Map();
  const arr2FreqMap = new Map();

  for (let number of array1) {
    arr1FreqMap.set(number, (arr1FreqMap.get(number) || 0) + 1);
  }
  for (let number of array2) {
    arr2FreqMap.set(number, (arr2FreqMap.get(number) || 0) + 1);
  }

  for (const [key, occurrences] of arr1FreqMap) {
    if (!arr2FreqMap.has(key ** 2)) {
      console.log("Does not have the Squared");
      return false;
    }

    if (occurrences !== arr2FreqMap.get(key ** 2)) {
      return false;
    }
  }
  return true;
};
```
