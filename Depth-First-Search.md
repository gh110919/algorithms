### Поиск в глубину (Depth-First Search, DFS)

###### Алгоритм поиска в графе, который сначала исследует как можно дальше вдоль каждого пути перед возвратом назад.

```ts
function dfs(graph: Map<number, number[]>, start: number): number[] {
  /* Создаем множество для хранения посещенных узлов */
  const visited = new Set<number>();
  /* Создаем стек и добавляем в него начальный узел */
  const stack = [start];
  /* Создаем массив для хранения результата обхода */
  const result = [];

  /* Цикл, пока в стеке есть узлы */
  while (stack.length > 0) {
    /* Извлекаем последний узел из стека */
    const node = stack.pop();
    /* Если узел не был посещен */
    if (!visited.has(node)) {
      /* Помечаем узел как посещенный */
      visited.add(node);
      /* Добавляем узел в результат */
      result.push(node);
      /* Добавляем все связанные узлы в стек */
      stack.push(...graph.get(node));
    }
  }

  /* Возвращаем массив результата */
  return result;
}

/* Тестовые кейсы */

/* Тестовый случай 1: Простой граф с одним узлом */
const graph1 = new Map<number, number[]>([[1, []]]);
console.log(dfs(graph1, 1)); /* Результат: [1] */

/* Тестовый случай 2: Граф с одним ребром */
const graph2 = new Map<number, number[]>([
  [1, [2]],
  [2, []],
]);
console.log(dfs(graph2, 1)); /* Результат: [1, 2] */

/* Тестовый случай 3: Граф с несколькими ребрами */
const graph3 = new Map<number, number[]>([
  [1, [2, 3]],
  [2, [4]],
  [3, [4]],
  [4, []],
]);
console.log(dfs(graph3, 1)); /* Результат: [1, 3, 4, 2] */

/* Тестовый случай 4: Граф с циклом */
const graph4 = new Map<number, number[]>([
  [1, [2]],
  [2, [3]],
  [3, [1]],
]);
console.log(dfs(graph4, 1)); /* Результат: [1, 2, 3] */

/* Тестовый случай 5: Несвязанный граф */
const graph5 = new Map<number, number[]>([
  [1, [2]],
  [2, []],
  [3, [4]],
  [4, []],
]);
console.log(dfs(graph5, 1)); /* Результат: [1, 2] */
console.log(dfs(graph5, 3)); /* Результат: [3, 4] */
```
