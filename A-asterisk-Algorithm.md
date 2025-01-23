### Алгоритм А-звездочка (A\* Algorithm)

###### Алгоритм поиска пути, который использует эвристическую функцию для оценки стоимости кратчайшего пути.

```ts
interface Node {
  position: number;
  g: number; // cost from start to node
  h: number; // heuristic cost from node to goal
  f: number; // total cost (g + h)
  parent: Node | null;
}

function aStar(
  graph: Map<number, Map<number, number>>,
  start: number,
  goal: number,
  heuristic: (a: number, b: number) => number
): number[] {
  const openList = new Set<Node>();
  const closedList = new Set<Node>();
  const startNode: Node = {
    position: start,
    g: 0,
    h: heuristic(start, goal),
    f: 0,
    parent: null,
  };
  startNode.f = startNode.g + startNode.h;
  openList.add(startNode);

  while (openList.size > 0) {
    let currentNode = Array.from(openList).reduce((a, b) =>
      a.f < b.f ? a : b
    );
    if (currentNode.position === goal) {
      const path = [];
      while (currentNode) {
        path.push(currentNode.position);
        currentNode = currentNode.parent;
      }
      return path.reverse();
    }

    openList.delete(currentNode);
    closedList.add(currentNode);

    graph.get(currentNode.position).forEach((weight, neighbor) => {
      if (Array.from(closedList).find((node) => node.position === neighbor))
        return;
      const gScore = currentNode.g + weight;
      let neighborNode = Array.from(openList).find(
        (node) => node.position === neighbor
      );

      if (!neighborNode) {
        neighborNode = {
          position: neighbor,
          g: gScore,
          h: heuristic(neighbor, goal),
          f: 0,
          parent: currentNode,
        };
        neighborNode.f = neighborNode.g + neighborNode.h;
        openList.add(neighborNode);
      } else if (gScore < neighborNode.g) {
        neighborNode.g = gScore;
        neighborNode.f = neighborNode.g + neighborNode.h;
        neighborNode.parent = currentNode;
      }
    });
  }
  return [];
}
```
