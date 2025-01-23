### Бинарный поиск (Binary Search)

###### Эффективный алгоритм поиска в отсортированном массиве, который на каждой итерации делит массив на половины.

```ts
/* 
  Функция для выполнения бинарного поиска в отсортированном массиве 
*/
function binarySearch(arr: number[], target: number): number {
  let left = 0; /* Инициализируем левый указатель на начало массива */
  let right =
    arr.length - 1; /* Инициализируем правый указатель на конец массива */

  while (left <= right) {
    /* Пока левый указатель не превысит правый */
    const mid = Math.floor(
      (left + right) / 2
    ); /* Находим середину текущего диапазона */

    if (arr[mid] === target)
      return mid /* Если значение в середине равно цели, возвращаем индекс */;
    else if (arr[mid] < target)
      left =
        mid +
        1; /* Если значение в середине меньше цели, сдвигаем левый указатель вправо */
    else
      right =
        mid -
        1; /* Если значение в середине больше цели, сдвигаем правый указатель влево */
  }

  return -1; /* Если цель не найдена, возвращаем -1 */
}

/* 
  Функция для тестирования бинарного поиска 
*/
function testBinarySearch() {
  const testCases = [
    {
      arr: [1, 2, 3, 4, 5],
      target: 3,
      expected: 2,
    } /* Тестовый случай: цель находится в середине массива */,
    {
      arr: [1, 2, 3, 4, 5],
      target: 1,
      expected: 0,
    } /* Тестовый случай: цель находится в начале массива */,
    {
      arr: [1, 2, 3, 4, 5],
      target: 5,
      expected: 4,
    } /* Тестовый случай: цель находится в конце массива */,
    {
      arr: [1, 2, 3, 4, 5],
      target: 6,
      expected: -1,
    } /* Тестовый случай: цель отсутствует в массиве */,
    { arr: [], target: 1, expected: -1 } /* Тестовый случай: массив пустой */,
  ];

  testCases.forEach(({ arr, target, expected }, index) => {
    const result = binarySearch(arr, target); /* Выполняем бинарный поиск */
    if (result === expected) {
      console.log(
        `Test case ${index + 1} passed.`
      ); /* Выводим сообщение о прохождении теста */
    } else {
      console.log(
        `Test case ${
          index + 1
        } failed. Expected ${expected}, but got ${result}.`
      );
      /* Выводим сообщение о провале теста */
    }
  });
}

/* Запуск тестирования */
testBinarySearch();
```
