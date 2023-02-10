```js
const binarySearch = (hayStack, needle) => {
  if (needle < hayStack[0]) {
    return -1;
  }
  if (needle > hayStack[hayStack.length - 1]) {
    return -1;
  }

  let i = 0;
  let j = hayStack.length;

  while (i < j) {
    let middleIndex = Math.floor(i + (j - i) / 2);
    let valueInMiddle = hayStack[middleIndex];
    if (valueInMiddle === needle) {
      return middleIndex;
    } else if (needle < valueInMiddle) {
      j = middleIndex;
    } else {
      i = middleIndex + 1;
    }
  }
  return -1;
};
```

![[Pasted image 20230210113427.png]]