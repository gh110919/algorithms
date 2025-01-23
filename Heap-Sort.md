### Сортировка кучей (Heap Sort)

###### Алгоритм сортировки, который сначала строит "кучу" из массива, а затем многократно извлекает максимальный элемент из кучи и перестраивает её.

```ts
/* Функция heapify перестраивает поддерево с корнем в узле i так, чтобы оно удовлетворяло свойствам кучи. */
function heapify(arr: number[], i: number, max: number): void {
  let index = i;
  let leftChild = 2 * i + 1;
  let rightChild = 2 * i + 2;

  /* Если левый дочерний элемент существует и больше корня, обновляем индекс */
  if (leftChild < max && arr[leftChild] > arr[index]) {
    index = leftChild;
  }

  /* Если правый дочерний элемент существует и больше корня, обновляем индекс */
  if (rightChild < max && arr[rightChild] > arr[index]) {
    index = rightChild;
  }

  /* Если корневой элемент не на своем месте, меняем его и вызываем heapify рекурсивно */
  if (index !== i) {
    [arr[i], arr[index]] = [arr[index], arr[i]];
    heapify(arr, index, max);
  }
}

/* Функция heapSort выполняет сортировку массива arr. */
function heapSort(arr: number[]): number[] {
  /* Строим максимальную кучу из массива */
  buildMaxHeap(arr);

  /* Проходим по массиву с конца, меняем первый элемент с текущим последним и перестраиваем кучу */
  for (let i = arr.length - 1; i > 0; i--) {
    [arr[0], arr[i]] = [arr[i], arr[0]];
    heapify(arr, 0, i);
  }
  return arr;
}

/* Функция buildMaxHeap строит максимальную кучу из массива arr. */
function buildMaxHeap(arr: number[]): void {
  /* Идем от середины массива к началу и вызываем heapify для каждого элемента */
  for (let i = Math.floor(arr.length / 2); i >= 0; i--) {
    heapify(arr, i, arr.length);
  }
}

/* Тесткейсы для проверки работы алгоритма сортировки кучей */

/* Тест 1: Проверка с неотсортированным массивом */
let arr1 = [4, 10, 3, 5, 1];
console.log(heapSort(arr1)); /* Ожидаемый результат: [1, 3, 4, 5, 10] */

/* Тест 2: Проверка с отсортированным массивом */
let arr2 = [1, 2, 3, 4, 5];
console.log(heapSort(arr2)); /* Ожидаемый результат: [1, 2, 3, 4, 5] */

/* Тест 3: Проверка с массивом в обратном порядке */
let arr3 = [5, 4, 3, 2, 1];
console.log(heapSort(arr3)); /* Ожидаемый результат: [1, 2, 3, 4, 5] */

/* Тест 4: Проверка с массивом, содержащим одинаковые элементы */
let arr4 = [5, 5, 5, 5, 5];
console.log(heapSort(arr4)); /* Ожидаемый результат: [5, 5, 5, 5, 5] */

/* Тест 5: Проверка с пустым массивом */
let arr5: number[] = [];
console.log(heapSort(arr5)); /* Ожидаемый результат: [] */
```
