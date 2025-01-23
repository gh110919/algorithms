### Алгоритм Флойда-Уоршелла (Floyd-Warshall Algorithm)

###### Алгоритм поиска кратчайших путей между всеми парами вершин в взвешенном графе.

```ts
/* Алгоритм Флойда-Уоршелла */
function floydWarshall(graph: number[][]): number[][] {
  /* Создаем копию графа для хранения минимальных расстояний */
  const dist = graph.map((row) => row.slice());
  const len = graph.length;

  /* Внешний цикл по промежуточным вершинам */
  for (let k = 0; k < len; k++) {
    /* Цикл по строкам */
    for (let i = 0; i < len; i++) {
      /* Цикл по столбцам */
      for (let j = 0; j < len; j++) {
        /* Проверяем, можно ли улучшить минимальное расстояние */
        if (dist[i][k] + dist[k][j] < dist[i][j]) {
          /* Обновляем минимальное расстояние */
          dist[i][j] = dist[i][k] + dist[k][j];
        }
      }
    }
  }
  /* Возвращаем матрицу минимальных расстояний */
  return dist;
}

/* Тест 1: Простой тест со всеми одинаковыми весами */
const graph1 = [
  [0, 1, Infinity],
  [1, 0, 1],
  [Infinity, 1, 0],
];
const result1 = floydWarshall(graph1);
/* Ожидаемый результат:
[
  [0, 1, 2],
  [1, 0, 1],
  [2, 1, 0]
] */
console.log(result1);

/* Тест 2: Тест с нулевыми расстояниями */
const graph2 = [
  [0, Infinity, 3],
  [2, 0, Infinity],
  [Infinity, 7, 0],
];
const result2 = floydWarshall(graph2);
/* Ожидаемый результат:
[
  [0, 10, 3],
  [2, 0, 5],
  [9, 7, 0]
] */
console.log(result2);

/* Тест 3: Тест с уже минимальными расстояниями */
const graph3 = [
  [0, 5, Infinity, 10],
  [Infinity, 0, 3, Infinity],
  [Infinity, Infinity, 0, 1],
  [Infinity, Infinity, Infinity, 0],
];
const result3 = floydWarshall(graph3);
/* Ожидаемый результат:
[
  [0, 5, 8, 9],
  [Infinity, 0, 3, 4],
  [Infinity, Infinity, 0, 1],
  [Infinity, Infinity, Infinity, 0]
] */
console.log(result3);
```
