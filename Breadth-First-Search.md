### Поиск в ширину (Breadth-First Search, BFS)

###### Алгоритм поиска в графе, который сначала исследует все вершины на текущем уровне перед переходом к вершинам на следующем уровне.

```ts
function bfs(graph: Map<number, number[]>, start: number): number[] {
  const visited = new Set<number>();
  const queue = [start];
  const result = [];
  while (queue.length > 0) {
    const node = queue.shift();
    if (!visited.has(node)) {
      visited.add(node);
      result.push(node);
      queue.push(...graph.get(node));
    }
  }
  return result;
}
```
