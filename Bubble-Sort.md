### Сортировка пузырьком (Bubble Sort)

###### Простой алгоритм сортировки, который повторно проходит по массиву, сравнивая соседние элементы и меняя их местами, если они находятся в неправильном порядке.

```ts
function bubbleSort(arr: number[]): number[] {
  let n = arr.length;
  /* Проходим по всему массиву */
  for (let i = 0; i < n; i++) {
    /* Проходим по массиву до последнего неотсортированного элемента */
    for (let j = 0; j < n - 1; j++) {
      /* Сравниваем текущий элемент с следующим */
      if (arr[j] > arr[j + 1]) {
        /* Если текущий элемент больше, меняем их местами */
        [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
      }
    }
  }
  /* Возвращаем отсортированный массив */
  return arr;
}

/* Тест кейс 1: Пустой массив */
console.assert(
  JSON.stringify(bubbleSort([])) === JSON.stringify([]),
  "Test Case 1 Failed"
);

/* Тест кейс 2: Один элемент */
console.assert(
  JSON.stringify(bubbleSort([1])) === JSON.stringify([1]),
  "Test Case 2 Failed"
);

/* Тест кейс 3: Уже отсортированный массив */
console.assert(
  JSON.stringify(bubbleSort([1, 2, 3, 4, 5])) ===
    JSON.stringify([1, 2, 3, 4, 5]),
  "Test Case 3 Failed"
);

/* Тест кейс 4: Массив с элементами в обратном порядке */
console.assert(
  JSON.stringify(bubbleSort([5, 4, 3, 2, 1])) ===
    JSON.stringify([1, 2, 3, 4, 5]),
  "Test Case 4 Failed"
);

/* Тест кейс 5: Массив с дублирующимися элементами */
console.assert(
  JSON.stringify(bubbleSort([3, 1, 2, 3, 1])) ===
    JSON.stringify([1, 1, 2, 3, 3]),
  "Test Case 5 Failed"
);

/* Тест кейс 6: Массив с отрицательными элементами */
console.assert(
  JSON.stringify(bubbleSort([-1, -3, -2, 0, 2])) ===
    JSON.stringify([-3, -2, -1, 0, 2]),
  "Test Case 6 Failed"
);

console.log("All test cases passed!");
```
