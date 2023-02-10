Given two crystal balls that will break if dropped from high enough distance, determine the exact spot in which it will break in the most optimized way.

```js
const crystalBalls = (floorsArr) => {
  safeSpot = 0;
  jumpDist = Math.floor(Math.sqrt(floorsArr.length));

  for (; safeSpot < floorsArr.length - jumpDist; safeSpot++) {
    if (floorsArr[safeSpot + jumpDist]) {
      break;
    }
  }

  for (let index = safeSpot; index <= safeSpot + jumpDist; index++) {
    const element = floorsArr[index];
    if (element) {
      return index;
    }
  }
  return -1;
};
```

![[Pasted image 20230210150348.png]]