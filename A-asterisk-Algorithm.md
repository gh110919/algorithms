### Алгоритм А-звездочка (A\* Algorithm)

###### Алгоритм поиска пути, который использует эвристическую функцию для оценки стоимости кратчайшего пути.

```ts
/* Определяем интерфейс Node */
interface Node {
  position: number; /* Позиция узла */
  g: number; /* Стоимость от старта до узла */
  h: number; /* Эвристическая стоимость от узла до цели */
  f: number; /* Общая стоимость (g + h) */
  parent: Node | null; /* Родительский узел */
}

/* Определяем эвристическую функцию (Манхэттенское расстояние) */
function heuristic(a: number, b: number): number {
  return Math.abs(a - b);
}

function aStar(
  graph: Map<number, Map<number, number>>, /* Граф в виде карты */
  start: number, /* Стартовая позиция */
  goal: number, /* Целевая позиция */
  heuristic: (a: number, b: number) => number /* Эвристическая функция */
): number[] {
  const openList = new Set<Node>(); /* Открытый список */
  const closedList = new Set<Node>(); /* Закрытый список */
  const startNode: Node = {
    position: start,
    g: 0, /* Начальная стоимость от старта до узла */
    h: heuristic(start, goal), /* Начальная эвристическая стоимость от узла до цели */
    f: 0, Начальная общая стоимость
    parent: null, /* Нет родителя для стартового узла */
  };
  startNode.f = startNode.g + startNode.h; /* Общая стоимость стартового узла */
  openList.add(startNode); /* Добавляем стартовый узел в открытый список */

  while (openList.size > 0) {
    /* Пока в открытом списке есть узлы, находим узел с наименьшей общей стоимостью */
    let currentNode = Array.from(openList).reduce((a, b) =>
      a.f < b.f ? a : b
    );
    if (currentNode.position === goal) {
      /* Если текущий узел - цель, восстанавливаем путь, двигаясь от цели к старту */
      const path = [];
      while (currentNode) {
        path.push(currentNode.position);
        currentNode = currentNode.parent;
      }
      return path.reverse(); /* Возвращаем путь в правильном порядке */
    }

    openList.delete(currentNode); /* Удаляем текущий узел из открытого списка */
    closedList.add(currentNode); /* Добавляем текущий узел в закрытый список */

    /* Проходим по соседям текущего узла */
    graph.get(currentNode.position).forEach((weight, neighbor) => {
      if (Array.from(closedList).find((node) => node.position === neighbor))
        return; /* Пропускаем соседей, которые уже в закрытом списке */
      const gScore = currentNode.g + weight; /* Новая стоимость от старта до соседнего узла */
      let neighborNode = Array.from(openList).find(
        (node) => node.position === neighbor
      );

      if (!neighborNode) {
        /* Если соседний узел не в открытом списке */
        neighborNode = {
          position: neighbor,
          g: gScore,
          h: heuristic(neighbor, goal), /* Вычисляем эвристическую стоимость для соседнего узла */
          f: 0,
          parent: currentNode, /* Устанавливаем текущий узел как родительский */
        };
        neighborNode.f = neighborNode.g + neighborNode.h; /* Вычисляем общую стоимость */
        openList.add(neighborNode); /* Добавляем соседний узел в открытый список */
      } else if (gScore < neighborNode.g) {
        /* Если новая стоимость лучше текущей */
        neighborNode.g = gScore; /* Обновляем стоимость от старта */
        neighborNode.f = neighborNode.g + neighborNode.h; /* Обновляем общую стоимость */
        neighborNode.parent = currentNode; /* Обновляем родительский узел */
      }
    });
  }
  return []; /* Возвращаем пустой массив, если путь не найден */
}

/* Определяем граф как карту */
const graph = new Map<number, Map<number, number>>();
graph.set(
  1,
  new Map<number, number>([
    [2, 1],
    [3, 4],
  ])
);
graph.set(
  2,
  new Map<number, number>([
    [1, 1],
    [3, 2],
    [4, 5],
  ])
);
graph.set(
  3,
  new Map<number, number>([
    [1, 4],
    [2, 2],
    [4, 1],
  ])
);
graph.set(
  4,
  new Map<number, number>([
    [2, 5],
    [3, 1],
  ])
);

/* Тестируем A* алгоритм */
function testAStar() {
  const start = 1; /* Стартовая позиция */
  const goal = 4; /* Целевая позиция */
  const path = aStar(graph, start, goal, heuristic); /* Запускаем A* алгоритм */

  console.log("Path found:", path); /* Выводим найденный путь */

  /* Ожидаемый результат [1, 2, 3, 4] или [1, 3, 4] в зависимости от эвристики и структуры графа */
  if (path.length > 0 && path[0] === start && path[path.length - 1] === goal) {
    console.log("Test passed!"); /* Тест пройден */
  } else {
    console.log("Test failed!"); /* Тест не пройден */
  }
}

/* Добавление стандартных тесткейсов */

/* Тест 1: Проверка, когда стартовая и целевая позиции одинаковы */
function testSameStartGoal() {
  const start = 1;
  const goal = 1;
  const path = aStar(graph, start, goal, heuristic);
  console.log("Test Same Start/Goal:", path);
  console.log(
    path.length === 1 && path[0] === start ? "Test passed!" : "Test failed!"
  );
}

/* Тест 2: Проверка, когда цель недостижима */
function testUnreachableGoal() {
  const start = 1;
  const goal = 5; /* Позиция 5 не существует в графе */
  const path = aStar(graph, start, goal, heuristic);
  console.log("Test Unreachable Goal:", path);
  console.log(path.length === 0 ? "Test passed!" : "Test failed!");
}

/* Тест 3: Проверка для сложного графа */
function testComplexGraph() {
  const complexGraph = new Map<number, Map<number, number>>();
  complexGraph.set(
    1,
    new Map<number, number>([
      [2, 1],
      [3, 3],
    ])
  );
  complexGraph.set(
    2,
    new Map<number, number>([
      [1, 1],
      [4, 1],
    ])
  );
  complexGraph.set(
    3,
    new Map<number, number>([
      [1, 3],
      [4, 1],
    ])
  );
  complexGraph.set(
    4,
    new Map<number, number>([
      [2, 1],
      [3, 1],
    ])
  );
  const start = 1;
  const goal = 4;
  const path = aStar(complexGraph, start, goal, heuristic);
  console.log("Test Complex Graph:", path);
  console.log(
    path.join(" -> ") === "1 -> 2 -> 4" || path.join(" -> ") === "1 -> 3 -> 4"
      ? "Test passed!"
      : "Test failed!"
  );
}

/* Запускаем все тесты */
function runAllTests() {
  testAStar();
  testSameStartGoal();
  testUnreachableGoal();
  testComplexGraph();
}

runAllTests(); /* Запускаем все тесты */
```
