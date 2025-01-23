### Сортировка выбором (Selection Sort)

###### Алгоритм сортировки, который делит массив на две части: отсортированную и неотсортированную. На каждой итерации он находит минимальный элемент в неотсортированной части и меняет его местами с первым элементом неотсортированной части.

```ts
function selectionSort(arr: number[]): number[] {
  let n = arr.length;
  for (let i = 0; i < n; i++) {
    let minIndex = i;
    for (let j = i + 1; j < n; j++) {
      if (arr[j] < arr[minIndex]) {
        minIndex = j;
      }
    }
    if (minIndex !== i) {
      [arr[i], arr[minIndex]] = [arr[minIndex], arr[i]];
    }
  }
  return arr;
}
```
