### Сортировка вставками (Insertion Sort)

###### Алгоритм сортировки, который строит окончательно отсортированный массив по одному элементу за раз, перемещая элементы в правильное место.

```ts
/*
  Алгоритм сортировки вставками
  Функция принимает массив чисел и возвращает отсортированный массив
*/
function insertionSort(arr: number[]): number[] {
  let n = arr.length; /* Получаем длину массива */
  for (let i = 1; i < n; i++) {
    let key = arr[i]; /* Сохраняем текущее значение в переменную key */
    let j = i - 1;
    /* 
      Сравниваем текущий элемент с предыдущими элементами 
      и перемещаем элементы, которые больше key, на одну позицию вперед 
    */
    while (j >= 0 && arr[j] > key) {
      arr[j + 1] = arr[j];
      j--;
    }
    arr[j + 1] = key; /* Вставляем key в правильную позицию */
  }
  return arr; /* Возвращаем отсортированный массив */
}

/*
  Тест-кейсы для проверки работы алгоритма
*/

/* Тест-кейс 1: обычный случай */
let arr1 = [5, 2, 4, 6, 1, 3];
console.log(insertionSort(arr1)); /* Ожидаемый результат: [1, 2, 3, 4, 5, 6] */

/*
  Тест-кейс 2: массив с повторяющимися элементами
*/
let arr2 = [5, 5, 5, 5];
console.log(insertionSort(arr2)); /* Ожидаемый результат: [5, 5, 5, 5] */

/*
  Тест-кейс 3: массив из одного элемента
*/
let arr3 = [1];
console.log(insertionSort(arr3)); /* Ожидаемый результат: [1] */

/*
  Тест-кейс 4: уже отсортированный массив
*/
let arr4 = [1, 2, 3, 4, 5];
console.log(insertionSort(arr4)); /* Ожидаемый результат: [1, 2, 3, 4, 5] */

/*
  Тест-кейс 5: массив отсортированный в обратном порядке
*/
let arr5 = [5, 4, 3, 2, 1];
console.log(insertionSort(arr5)); /* Ожидаемый результат: [1, 2, 3, 4, 5] */

```
