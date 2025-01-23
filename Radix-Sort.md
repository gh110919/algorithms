### Алгоритм поразрядной сортировки (Radix Sort)

###### Алгоритм сортировки, который сортирует числа, сравнивая их отдельные разряды.

```ts
function radixSort(arr: number[]): number[] {
  const maxNum = Math.max(...arr) * 10;
  let divisor = 10;
  while (divisor < maxNum) {
    const buckets = [...Array(10)].map(() => []);
    for (let num of arr) {
      buckets[Math.floor((num % divisor) / (divisor / 10))].push(num);
    }
    arr = [].concat(...buckets);
    divisor *= 10;
  }
  return arr;
}
```
