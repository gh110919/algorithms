### Алгоритм Дейкстры (Dijkstra's Algorithm)

###### Алгоритм поиска кратчайшего пути от одной вершины графа до всех остальных.

```ts
function dijkstra(
  graph: Map<number, Map<number, number>> /* Граф, представленный в виде Map */,
  start: number /* Начальная вершина */
): Map<number, number> {
  const distances = new Map<
    number,
    number
  >(); /* Создаем Map для хранения расстояний от начальной вершины до остальных */
  const visited =
    new Set<number>(); /* Создаем Set для хранения посещенных вершин */
  distances.set(
    start,
    0
  ); /* Устанавливаем расстояние до начальной вершины равным 0 */
  const queue = new Set<number>(
    graph.keys()
  ); /* Создаем очередь, содержащую все вершины графа */

  while (queue.size > 0) {
    /* Пока в очереди есть вершины */
    let minNode =
      null; /* Переменная для хранения вершины с минимальным расстоянием */
    queue.forEach((node) => {
      /* Проходим по всем вершинам в очереди */
      if (minNode === null || distances.get(node) < distances.get(minNode)) {
        /* Если minNode не установлен или расстояние до текущей вершины меньше расстояния до minNode */
        minNode = node; /* Устанавливаем текущую вершину как minNode */
      }
    });
    queue.delete(minNode); /* Удаляем minNode из очереди */
    visited.add(minNode); /* Добавляем minNode в посещенные вершины */
    graph.get(minNode).forEach((weight, neighbor) => {
      /* Проходим по всем соседям minNode */
      if (!visited.has(neighbor)) {
        /* Если сосед еще не посещен */
        const newDist =
          distances.get(minNode) +
          weight; /* Вычисляем новое расстояние до соседа */
        if (!distances.has(neighbor) || newDist < distances.get(neighbor)) {
          /* Если расстояние до соседа еще не установлено или новое расстояние меньше текущего */
          distances.set(neighbor, newDist); /* Обновляем расстояние до соседа */
        }
      }
    });
  }
  return distances; /* Возвращаем Map с расстояниями до всех вершин */
}

/* 
  Тестовый граф #1
  Граф:
  1 -> 2 (вес 1)
  1 -> 3 (вес 4)
  2 -> 3 (вес 2)
  3 -> 4 (вес 1)
*/
const graph1 = new Map<number, Map<number, number>>([
  [
    1,
    new Map<number, number>([
      [2, 1],
      [3, 4],
    ]),
  ] /* Определение рёбер и весов графа */,
  [2, new Map<number, number>([[3, 2]])],
  [3, new Map<number, number>([[4, 1]])],
  [4, new Map<number, number>()],
]);

const result1 = dijkstra(
  graph1,
  1
); /* Запуск алгоритма Дейкстры для тестового графа #1 */
/* Ожидаемый результат для графа #1:
  1: 0
  2: 1
  3: 3
  4: 4
*/
console.log(result1); /* Выводим результат для тестового графа #1 */

/* 
  Тестовый граф #2
  Граф:
  1 -> 2 (вес 1)
  1 -> 3 (вес 2)
  2 -> 3 (вес 1)
  3 -> 4 (вес 3)
  4 -> 5 (вес 1)
*/
const graph2 = new Map<number, Map<number, number>>([
  [
    1,
    new Map<number, number>([
      [2, 1],
      [3, 2],
    ]),
  ] /* Определение рёбер и весов графа */,
  [2, new Map<number, number>([[3, 1]])],
  [3, new Map<number, number>([[4, 3]])],
  [4, new Map<number, number>([[5, 1]])],
  [5, new Map<number, number>()],
]);

const result2 = dijkstra(
  graph2,
  1
); /* Запуск алгоритма Дейкстры для тестового графа #2 */
/* Ожидаемый результат для графа #2:
  1: 0
  2: 1
  3: 2
  4: 5
  5: 6
*/
console.log(result2); /* Выводим результат для тестового графа #2 */

/* 
  Тестовый граф #3 (с циклом)
  Граф:
  1 -> 2 (вес 10)
  1 -> 3 (вес 5)
  3 -> 4 (вес 2)
  4 -> 2 (вес 3)
  2 -> 5 (вес 1)
*/
const graph3 = new Map<number, Map<number, number>>([
  [
    1,
    new Map<number, number>([
      [2, 10],
      [3, 5],
    ]),
  ] /* Определение рёбер и весов графа */,
  [2, new Map<number, number>([[5, 1]])],
  [3, new Map<number, number>([[4, 2]])],
  [4, new Map<number, number>([[2, 3]])],
  [5, new Map<number, number>()],
]);

const result3 = dijkstra(
  graph3,
  1
); /* Запуск алгоритма Дейкстры для тестового графа #3 */
/* Ожидаемый результат для графа #3:
  1: 0
  2: 8
  3: 5
  4: 7
  5: 9
*/
console.log(result3); /* Выводим результат для тестового графа #3 */
```
