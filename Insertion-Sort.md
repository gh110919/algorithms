### Сортировка вставками (Insertion Sort)

###### Алгоритм сортировки, который строит окончательно отсортированный массив по одному элементу за раз, перемещая элементы в правильное место.

```ts
function insertionSort(arr: number[]): number[] {
  let n = arr.length;
  for (let i = 1; i < n; i++) {
    let key = arr[i];
    let j = i - 1;
    while (j >= 0 && arr[j] > key) {
      arr[j + 1] = arr[j];
      j--;
    }
    arr[j + 1] = key;
  }
  return arr;
}
```
