### Поиск в глубину (Depth-First Search, DFS)

###### Алгоритм поиска в графе, который сначала исследует как можно дальше вдоль каждого пути перед возвратом назад.

```ts
function dfs(graph: Map<number, number[]>, start: number): number[] {
  const visited = new Set<number>();
  const stack = [start];
  const result = [];
  while (stack.length > 0) {
    const node = stack.pop();
    if (!visited.has(node)) {
      visited.add(node);
      result.push(node);
      stack.push(...graph.get(node));
    }
  }
  return result;
}
```
