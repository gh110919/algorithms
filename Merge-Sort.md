### Сортировка слиянием (Merge Sort)

###### Алгоритм сортировки, который рекурсивно делит массив пополам, сортирует каждую половину и затем объединяет отсортированные половины.

```ts
function mergeSort(arr: number[]): number[] {
  if (arr.length < 2) return arr;
  const mid = Math.floor(arr.length / 2);
  const left = mergeSort(arr.slice(0, mid));
  const right = mergeSort(arr.slice(mid));
  return merge(left, right);
}

function merge(left: number[], right: number[]): number[] {
  const result = [];
  while (left.length && right.length) {
    if (left[0] < right[0]) result.push(left.shift());
    else result.push(right.shift());
  }
  return result.concat(left).concat(right);
}
```
