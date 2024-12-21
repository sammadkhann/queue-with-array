# queue-with-array

queue.h

#include<iostream>
using namespace std;

class Queue {
private:
    int* array;
    int size;
    int front;
    int rear;
    int count;

public:
    Queue(int size);
    ~Queue();
    void enqueue(int num);
    void dequeue();
    bool isFull();
    bool isEmpty();
    int peek();
    void display();
};

imp

#include "Queue.h"
#include <iostream>
using namespace std;


Queue::Queue(int size) {
    array = new int[size];
    this->size = size;
    front = 0;
    rear = -1;
    count = 0;
}

Queue::~Queue() {
    delete[] array;
}


void Queue::enqueue(int num) {
    if (isFull()) {
        cout << "The queue is full. Cannot enqueue " << num << ".\n";
    }
    else {
        rear = (rear + 1) % size;
        array[rear] = num;
        count++;
    }
}


void Queue::dequeue() {
    if (isEmpty()) {
        cout << "The queue is empty. Cannot dequeue.\n";
    }
    else {
        front = (front + 1) % size;
        count--;
    }
}

bool Queue::isFull() {
    return count == size;
}


bool Queue::isEmpty() {
    return count == 0;
}


int Queue::peek() {
    if (!isEmpty()) {
        return array[front];
    }
    else {
        cout << "The queue is empty. No front element.\n";
        return -1;
    }
}


void Queue::display() {
    if (isEmpty()) {
        cout << "The queue is empty.\n";
    }
    else {
        cout << "Queue elements:\n";
        for (int i = 0; i < count; i++) {
            int index = (front + i) % size;
            cout << "array[" << index << "] = " << array[index] << endl;
        }
    }
}


#include "Queue.h"
#include <iostream>
using namespace std;

int main() {
    int size, choice, num;

    cout << "Enter the size of the queue: ";
    cin >> size;

    Queue myQueue(size);

    do {
        cout << "\n--- Queue Menu ---\n";
        cout << "1. Enqueue\n";
        cout << "2. Dequeue\n";
        cout << "3. Peek\n";
        cout << "4. Display\n";
        cout << "5. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
        case 1:
            cout << "Enter the number to enqueue: ";
            cin >> num;
            myQueue.enqueue(num);
            break;

        case 2:
            myQueue.dequeue();
            break;

        case 3:
            num = myQueue.peek();
            if (num != -1) {
                cout << "Front element is: " << num << endl;
            }
            break;

        case 4:
            myQueue.display();
            break;

        case 5:
            cout << "Exiting program.\n";
            break;

        default:
            cout << "Invalid choice. Please try again.\n";
        }
    } while (choice != 5);

    return 0;
}
