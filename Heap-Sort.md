### Сортировка кучей (Heap Sort)

###### Алгоритм сортировки, который сначала строит "кучу" из массива, а затем многократно извлекает максимальный элемент из кучи и перестраивает её.

```ts
function heapify(arr: number[], i: number, max: number): void {
  let index = i;
  let leftChild = 2 * i + 1;
  let rightChild = 2 * i + 2;
  if (leftChild < max && arr[leftChild] > arr[index]) {
    index = leftChild;
  }
  if (rightChild < max && arr[rightChild] > arr[index]) {
    index = rightChild;
  }
  if (index !== i) {
    [arr[i], arr[index]] = [arr[index], arr[i]];
    heapify(arr, index, max);
  }
}

function heapSort(arr: number[]): number[] {
  buildMaxHeap(arr);
  for (let i = arr.length - 1; i > 0; i--) {
    [arr[0], arr[i]] = [arr[i], arr[0]];
    heapify(arr, 0, i);
  }
  return arr;
}

function buildMaxHeap(arr: number[]): void {
  for (let i = Math.floor(arr.length / 2); i >= 0; i--) {
    heapify(arr, i, arr.length);
  }
}
```
