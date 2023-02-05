Creating pointers that correspond to an Index or position and move towards a specific direction.

```js
function countUniqueValues(arr) {
  if (arr.length === 0) return 0;
  var i = 0;
  for (var j = 1; j < arr.length; j++) {
    if (arr[i] !== arr[j]) {
      i++;
      arr[i] = arr[j];
    }
  }
  return i + 1;
}```

In the above example, `i` will move way slower than `j`, `j` is "scouting" ahead, if 
`j!==i` we move `i` one space and save the value of `array[j]` in `i` position, this way we make sure to start comparing for a new value. This only works because we were provided an ordered array.

	