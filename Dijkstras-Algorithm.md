### Алгоритм Дейкстры (Dijkstra's Algorithm)

###### Алгоритм поиска кратчайшего пути от одной вершины графа до всех остальных.

```ts
function dijkstra(
  graph: Map<number, Map<number, number>>,
  start: number
): Map<number, number> {
  const distances = new Map<number, number>();
  const visited = new Set<number>();
  distances.set(start, 0);
  const queue = new Set<number>(graph.keys());
  while (queue.size > 0) {
    let minNode = null;
    queue.forEach((node) => {
      if (minNode === null || distances.get(node) < distances.get(minNode)) {
        minNode = node;
      }
    });
    queue.delete(minNode);
    visited.add(minNode);
    graph.get(minNode).forEach((weight, neighbor) => {
      if (!visited.has(neighbor)) {
        const newDist = distances.get(minNode) + weight;
        if (!distances.has(neighbor) || newDist < distances.get(neighbor)) {
          distances.set(neighbor, newDist);
        }
      }
    });
  }
  return distances;
}
```
