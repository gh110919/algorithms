### Сортировка пузырьком (Bubble Sort)

###### Простой алгоритм сортировки, который повторно проходит по массиву, сравнивая соседние элементы и меняя их местами, если они находятся в неправильном порядке.

```ts
function bubbleSort(arr: number[]): number[] {
  let n = arr.length;
  for (let i = 0; i < n; i++) {
    for (let j = 0; j < n - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
      }
    }
  }
  return arr;
}
```
