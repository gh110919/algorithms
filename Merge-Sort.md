### Сортировка слиянием (Merge Sort)

###### Алгоритм сортировки, который рекурсивно делит массив пополам, сортирует каждую половину и затем объединяет отсортированные половины.

```ts
/* Функция сортировки слиянием */
function mergeSort(arr: number[]): number[] {
  /* Если массив содержит менее двух элементов, возвращаем его */
  if (arr.length < 2) return arr;

  /* Находим середину массива */
  const mid = Math.floor(arr.length / 2);

  /* Рекурсивно сортируем левую часть массива */
  const left = mergeSort(arr.slice(0, mid));

  /* Рекурсивно сортируем правую часть массива */
  const right = mergeSort(arr.slice(mid));

  /* Сливаем две отсортированные части */
  return merge(left, right);
}

/* Функция слияния двух отсортированных массивов */
function merge(left: number[], right: number[]): number[] {
  /* Результирующий массив */
  const result = [];

  /* Пока оба массива не пусты */
  while (left.length && right.length) {
    /* Сравниваем первые элементы и добавляем наименьший в результат */
    if (left[0] < right[0]) result.push(left.shift());
    else result.push(right.shift());
  }

  /* Добавляем оставшиеся элементы */
  return result.concat(left).concat(right);
}

/* Тестовые кейсы */
const testCases = [[], [1], [5, 3, 8, 4, 2], [2, 2, 2], [9, 7, 5, 3, 1]];

testCases.forEach((testCase) => {
  console.log(
    `Исходный массив: [${testCase}] -> Отсортированный массив: [${mergeSort(
      testCase
    )}]`
  );
});
```
