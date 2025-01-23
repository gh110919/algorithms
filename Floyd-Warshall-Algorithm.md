### Алгоритм Флойда-Уоршелла (Floyd-Warshall Algorithm)

###### Алгоритм поиска кратчайших путей между всеми парами вершин в взвешенном графе.

```ts
function floydWarshall(graph: number[][]): number[][] {
  const dist = graph.map((row) => row.slice());
  const len = graph.length;
  for (let k = 0; k < len; k++) {
    for (let i = 0; i < len; i++) {
      for (let j = 0; j < len; j++) {
        if (dist[i][k] + dist[k][j] < dist[i][j]) {
          dist[i][j] = dist[i][k] + dist[k][j];
        }
      }
    }
  }
  return dist;
}
```
