### Быстрая сортировка (Quick Sort)

###### Эффективный алгоритм сортировки, который выбирает "опорный" элемент и делит массив на части, меньшие и большие опорного элемента, и затем рекурсивно сортирует эти части.

```ts
function quickSort(arr: number[]): number[] {
  if (arr.length < 2) return arr;
  const pivot = arr[Math.floor(Math.random() * arr.length)];
  const less = arr.filter((x) => x < pivot);
  const greater = arr.filter((x) => x > pivot);
  return quickSort(less).concat(pivot).concat(quickSort(greater));
}
```
