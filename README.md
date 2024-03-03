# queue-ts
A queue for TypeScript

```ts
// A queue structure which is use generic type for 
export default class Queue<T> {
  private readonly elements: Record<number, T>;
  private head: number;
  private tail: number;

  constructor() {
    this.elements = {};
    this.head = 0;
    this.tail = 0;
  }

  enqueue(element: T): void {
    this.elements[this.tail] = element;
    this.tail++;
  }

  dequeue(): T {
    if (this.isEmpty) {
      throw new Error("Queue is empty, can't dequeue");
    }

    const item = this.elements[this.head];
    delete this.elements[this.head];
    this.head++;
    return item;
  }

  peek() {
    if (this.isEmpty) {
      throw new Error("Queue is empty, can't peek");
    }

    return this.elements[this.head];
  }

  get length() {
    return this.tail - this.head;
  }

  get isEmpty() {
    return this.tail === this.head;
  }
}

const queue = new Queue<string>();
queue.enqueue("first");
queue.enqueue("second");
queue.enqueue("third");

queue.dequeue(); // out: first (remove from queue)
queue.dequeue(); // out: second (will remove from queue)
queue.peek();    // out: third (won't removed from queue) 
queue.dequeue(); // out: third (will be removed from queue)
queue.dequeue()  // out: throw an error "Queue is empty, can't dequeue"
```
