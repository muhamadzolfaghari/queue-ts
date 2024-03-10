# Implementing a Queue Data Structure in TypeScript

⏭ A queue allows us to maintain a list of tasks or procedures in a FIFO (First In, First Out) order. We can sequentially add items to the queue (enqueue), and when needed, retrieve the first item from the queue (peek) or remove it from the queue (dequeue).

🚧 One common approach to implementing a queue is by using an array and utilizing the unshift method to retrieve the first item. However, this approach has a drawback: the time complexity is O(n) each time due to the need to rearrange the entire array when removing the first element.

✅  Another approach is to use a head and a tail to manage the queue. By convention:

The end of the sequence where elements are added is called the back, tail, or rear of the queue. The end from which elements are removed is called the head or front of the queue. This analogy aligns with how people line up to wait for goods or services. In this scenario, the time complexity for common queue operations is approximately constant (O(1)).

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
