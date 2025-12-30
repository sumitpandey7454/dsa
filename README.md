1. Bubble Sort (Easy & Classic)
class BubbleSort {
    public static void main(String[] args) {
        int[] a = {5, 3, 1, 4, 2};

        for (int i = 0; i < a.length - 1; i++)
            for (int j = 0; j < a.length - 1 - i; j++)
                if (a[j] > a[j + 1]) {
                    int t = a[j];
                    a[j] = a[j + 1];
                    a[j + 1] = t;
                }

        for (int n : a) System.out.print(n + " ");
    }
}


One-liner idea:
Bubble Sort repeatedly swaps adjacent elements if they are in the wrong order.

2. Selection Sort (Shortest Logic)
class SelectionSort {

    static void selectionSort(int[] arr, int start) {

        // Base case: only one element left
        if (start >= arr.length - 1)
            return;

        // Find index of minimum element
        int minIndex = start;
        for (int i = start + 1; i < arr.length; i++) {
            if (arr[i] < arr[minIndex]) {
                minIndex = i;
            }
        }

        // Swap minimum element with first unsorted element
        int temp = arr[start];
        arr[start] = arr[minIndex];
        arr[minIndex] = temp;

        // Recursive call for remaining array
        selectionSort(arr, start + 1);
    }

    public static void main(String[] args) {
        int[] arr = {64, 25, 12, 22, 11};

        selectionSort(arr, 0);

        for (int x : arr) {
            System.out.print(x + " ");
        }
    }
}


One-liner idea:
Selection Sort selects the minimum element and places it at the correct position.

3. Insertion Sort (Most Intuitive)
class InsertionSort {
    public static void main(String[] args) {
        int[] a = {5, 3, 1, 4, 2};

        for (int i = 1; i < a.length; i++) {
            int key = a[i], j = i - 1;
            while (j >= 0 && a[j] > key) {
                a[j + 1] = a[j];
                j--;
            }
            a[j + 1] = key;
        }

        for (int n : a) System.out.print(n + " ");
    }
}

One-liner idea:
Insertion Sort inserts each element into its correct position in the sorted part.

*************************************************************
1. Linear Search — Full Code
class LinearSearch {
    public static void main(String[] args) {
        int[] a = {5, 3, 1, 4, 2};
        int key = 4;
        int pos = -1;

        for (int i = 0; i < a.length; i++) {
            if (a[i] == key) {
                pos = i;
                break;
            }
        }

        if (pos != -1)
            System.out.println("Found at index " + pos);
        else
            System.out.println("Not Found");
    }
}


One-liner:
Linear search checks each element one by one.

2. Binary Search — Full Code (Iterative)

⚠️ Array must be sorted

class BinarySearch {
    public static void main(String[] args) {
        int[] a = {1, 2, 3, 4, 5};
        int key = 4;

        int low = 0, high = a.length - 1;
        int pos = -1;

        while (low <= high) {
            int mid = (low + high) / 2;

            if (a[mid] == key) {
                pos = mid;
                break;
            }
            else if (a[mid] < key)
                low = mid + 1;
            else
                high = mid - 1;
        }

        if (pos != -1)
            System.out.println("Found at index " + pos);
        else
            System.out.println("Not Found");
    }
}


One-liner:
Binary search repeatedly divides the sorted array into halves.

******************************
FULL Java Code — Doubly Linked List (10 Operations)
import java.util.Scanner;

class DoublyLinkedListMenu {

    class Node {
        int data;
        Node prev, next;
        Node(int d) {
            data = d;
            prev = next = null;
        }
    }

    Node head = null;

    // 1. Insert at beginning
    void insertBeg(int x) {
        Node n = new Node(x);
        if (head != null)
            head.prev = n;
        n.next = head;
        head = n;
    }

    // 2. Insert at end
    void insertEnd(int x) {
        Node n = new Node(x);
        if (head == null) {
            head = n;
            return;
        }
        Node t = head;
        while (t.next != null)
            t = t.next;
        t.next = n;
        n.prev = t;
    }

    // 3. Insert at position
    void insertAtPos(int x, int pos) {
        if (pos == 1) {
            insertBeg(x);
            return;
        }
        Node t = head;
        for (int i = 1; i < pos - 1 && t != null; i++)
            t = t.next;

        if (t == null) {
            System.out.println("Invalid Position");
            return;
        }

        Node n = new Node(x);
        n.next = t.next;
        n.prev = t;
        if (t.next != null)
            t.next.prev = n;
        t.next = n;
    }

    // 4. Delete from beginning
    void deleteBeg() {
        if (head == null) {
            System.out.println("List Empty");
            return;
        }
        head = head.next;
        if (head != null)
            head.prev = null;
    }

    // 5. Delete from end
    void deleteEnd() {
        if (head == null)
            return;

        if (head.next == null) {
            head = null;
            return;
        }

        Node t = head;
        while (t.next != null)
            t = t.next;

        t.prev.next = null;
    }

    // 6. Delete by value
    void deleteByValue(int key) {
        Node t = head;

        while (t != null && t.data != key)
            t = t.next;

        if (t == null) {
            System.out.println("Element Not Found");
            return;
        }

        if (t == head) {
            deleteBeg();
            return;
        }

        if (t.next != null)
            t.next.prev = t.prev;

        if (t.prev != null)
            t.prev.next = t.next;
    }

    // 7. Search
    void search(int key) {
        Node t = head;
        int pos = 1;
        while (t != null) {
            if (t.data == key) {
                System.out.println("Found at position " + pos);
                return;
            }
            t = t.next;
            pos++;
        }
        System.out.println("Not Found");
    }

    // 8. Display forward
    void displayForward() {
        if (head == null) {
            System.out.println("List Empty");
            return;
        }
        Node t = head;
        while (t != null) {
            System.out.print(t.data + " ");
            t = t.next;
        }
        System.out.println();
    }

    // 9. Display backward
    void displayBackward() {
        if (head == null)
            return;

        Node t = head;
        while (t.next != null)
            t = t.next;

        while (t != null) {
            System.out.print(t.data + " ");
            t = t.prev;
        }
        System.out.println();
    }

    // 10. Count nodes
    void count() {
        int c = 0;
        Node t = head;
        while (t != null) {
            c++;
            t = t.next;
        }
        System.out.println("Total nodes = " + c);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        DoublyLinkedListMenu l = new DoublyLinkedListMenu();

        int ch, x, pos;

        do {
            System.out.println("\n--- DOUBLY LINKED LIST MENU ---");
            System.out.println("1.Insert Beg");
            System.out.println("2.Insert End");
            System.out.println("3.Insert at Position");
            System.out.println("4.Delete Beg");
            System.out.println("5.Delete End");
            System.out.println("6.Delete by Value");
            System.out.println("7.Search");
            System.out.println("8.Display Forward");
            System.out.println("9.Display Backward");
            System.out.println("10.Count Nodes");
            System.out.println("11.Exit");
            System.out.print("Enter choice: ");

            ch = sc.nextInt();

            switch (ch) {
                case 1:
                    System.out.print("Enter value: ");
                    x = sc.nextInt();
                    l.insertBeg(x);
                    break;

                case 2:
                    System.out.print("Enter value: ");
                    x = sc.nextInt();
                    l.insertEnd(x);
                    break;

                case 3:
                    System.out.print("Enter value & position: ");
                    x = sc.nextInt();
                    pos = sc.nextInt();
                    l.insertAtPos(x, pos);
                    break;

                case 4:
                    l.deleteBeg();
                    break;

                case 5:
                    l.deleteEnd();
                    break;

                case 6:
                    System.out.print("Enter value: ");
                    x = sc.nextInt();
                    l.deleteByValue(x);
                    break;

                case 7:
                    System.out.print("Enter key: ");
                    x = sc.nextInt();
                    l.search(x);
                    break;

                case 8:
                    l.displayForward();
                    break;

                case 9:
                    l.displayBackward();
                    break;

                case 10:
                    l.count();
                    break;

                case 11:
                    System.out.println("Exit");
                    break;

                default:
                    System.out.println("Invalid Choice");
            }
        } while (ch != 11);
    }
}

********************************************
import java.util.Scanner;

class CircularLinkedListMenu {

    class Node {
        int data;
        Node next;
        Node(int d) { data = d; next = null; }
    }

    Node head = null, tail = null;

    // 1. Insert at beginning
    void insertBeg(int x) {
        Node n = new Node(x);
        if (head == null) {
            head = tail = n;
            n.next = head;
        } else {
            n.next = head;
            tail.next = n;
            head = n;
        }
    }

    // 2. Insert at end
    void insertEnd(int x) {
        Node n = new Node(x);
        if (head == null) {
            head = tail = n;
            n.next = head;
        } else {
            tail.next = n;
            tail = n;
            tail.next = head;
        }
    }

    // 3. Insert at position
    void insertAtPos(int x, int pos) {
        if (pos == 1) {
            insertBeg(x);
            return;
        }

        Node t = head;
        for (int i = 1; i < pos - 1 && t.next != head; i++)
            t = t.next;

        if (t.next == head) {
            System.out.println("Invalid Position");
            return;
        }

        Node n = new Node(x);
        n.next = t.next;
        t.next = n;
    }

    // 4. Delete from beginning
    void deleteBeg() {
        if (head == null)
            return;

        if (head == tail) {
            head = tail = null;
        } else {
            head = head.next;
            tail.next = head;
        }
    }

    // 5. Delete from end
    void deleteEnd() {
        if (head == null)
            return;

        if (head == tail) {
            head = tail = null;
            return;
        }

        Node t = head;
        while (t.next != tail)
            t = t.next;

        t.next = head;
        tail = t;
    }

    // 6. Delete by value
    void deleteByValue(int key) {
        if (head == null)
            return;

        if (head.data == key) {
            deleteBeg();
            return;
        }

        Node t = head;
        while (t.next != head && t.next.data != key)
            t = t.next;

        if (t.next == head) {
            System.out.println("Not Found");
            return;
        }

        if (t.next == tail)
            tail = t;

        t.next = t.next.next;
    }

    // 7. Search
    void search(int key) {
        if (head == null)
            return;

        Node t = head;
        int pos = 1;
        do {
            if (t.data == key) {
                System.out.println("Found at position " + pos);
                return;
            }
            t = t.next;
            pos++;
        } while (t != head);

        System.out.println("Not Found");
    }

    // 8. Display
    void display() {
        if (head == null) {
            System.out.println("List Empty");
            return;
        }

        Node t = head;
        do {
            System.out.print(t.data + " ");
            t = t.next;
        } while (t != head);
        System.out.println();
    }

    // 9. Count nodes
    void count() {
        if (head == null) {
            System.out.println("Total nodes = 0");
            return;
        }

        int c = 0;
        Node t = head;
        do {
            c++;
            t = t.next;
        } while (t != head);

        System.out.println("Total nodes = " + c);
    }

    // 10. Display last node
    void displayLast() {
        if (tail != null)
            System.out.println("Last node = " + tail.data);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        CircularLinkedListMenu l = new CircularLinkedListMenu();

        int ch, x, pos;

        do {
            System.out.println("\n--- CIRCULAR LINKED LIST MENU ---");
            System.out.println("1.Insert Beg");
            System.out.println("2.Insert End");
            System.out.println("3.Insert at Pos");
            System.out.println("4.Delete Beg");
            System.out.println("5.Delete End");
            System.out.println("6.Delete by Value");
            System.out.println("7.Search");
            System.out.println("8.Display");
            System.out.println("9.Count");
            System.out.println("10.Display Last");
            System.out.println("11.Exit");
            System.out.print("Enter choice: ");

            ch = sc.nextInt();

            switch (ch) {
                case 1:
                    x = sc.nextInt();
                    l.insertBeg(x);
                    break;
                case 2:
                    x = sc.nextInt();
                    l.insertEnd(x);
                    break;
                case 3:
                    x = sc.nextInt();
                    pos = sc.nextInt();
                    l.insertAtPos(x, pos);
                    break;
                case 4:
                    l.deleteBeg();
                    break;
                case 5:
                    l.deleteEnd();
                    break;
                case 6:
                    x = sc.nextInt();
                    l.deleteByValue(x);
                    break;
                case 7:
                    x = sc.nextInt();
                    l.search(x);
                    break;
                case 8:
                    l.display();
                    break;
                case 9:
                    l.count();
                    break;
                case 10:
                    l.displayLast();
                    break;
                case 11:
                    System.out.println("Exit");
                    break;
            }
        } while (ch != 11);
    }
}
---------------------------------------------------
import java.util.Scanner;

class SinglyLinkedListMenu {

    class Node {
        int data;
        Node next;
        Node(int d) {
            data = d;
            next = null;
        }
    }

    Node head = null;

    // 1. Insert at beginning
    void insertBeg(int x) {
        Node n = new Node(x);
        n.next = head;
        head = n;
    }

    // 2. Insert at end
    void insertEnd(int x) {
        Node n = new Node(x);
        if (head == null) {
            head = n;
            return;
        }
        Node t = head;
        while (t.next != null)
            t = t.next;
        t.next = n;
    }

    // 3. Insert at position
    void insertAtPos(int x, int pos) {
        if (pos == 1) {
            insertBeg(x);
            return;
        }
        Node t = head;
        for (int i = 1; i < pos - 1 && t != null; i++)
            t = t.next;

        if (t == null) {
            System.out.println("Invalid Position");
            return;
        }

        Node n = new Node(x);
        n.next = t.next;
        t.next = n;
    }

    // 4. Delete from beginning
    void deleteBeg() {
        if (head == null)
            System.out.println("List Empty");
        else
            head = head.next;
    }

    // 5. Delete from end
    void deleteEnd() {
        if (head == null || head.next == null) {
            head = null;
            return;
        }
        Node t = head;
        while (t.next.next != null)
            t = t.next;
        t.next = null;
    }

    // 6. Delete by value
    void deleteByValue(int key) {
        if (head == null)
            return;

        if (head.data == key) {
            head = head.next;
            return;
        }

        Node t = head;
        while (t.next != null && t.next.data != key)
            t = t.next;

        if (t.next == null)
            System.out.println("Element Not Found");
        else
            t.next = t.next.next;
    }

    // 7. Search
    void search(int key) {
        Node t = head;
        int pos = 1;
        while (t != null) {
            if (t.data == key) {
                System.out.println("Found at position " + pos);
                return;
            }
            t = t.next;
            pos++;
        }
        System.out.println("Not Found");
    }

    // 8. Display
    void display() {
        if (head == null) {
            System.out.println("List Empty");
            return;
        }
        Node t = head;
        while (t != null) {
            System.out.print(t.data + " ");
            t = t.next;
        }
        System.out.println();
    }

    // 9. Count nodes
    void count() {
        int c = 0;
        Node t = head;
        while (t != null) {
            c++;
            t = t.next;
        }
        System.out.println("Total nodes = " + c);
    }

    // 10. Reverse list
    void reverse() {
        Node prev = null, curr = head, next;
        while (curr != null) {
            next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }
        head = prev;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        SinglyLinkedListMenu l = new SinglyLinkedListMenu();

        int ch, x, pos;

        do {
            System.out.println("\n--- SINGLY LINKED LIST MENU ---");
            System.out.println("1.Insert Beg");
            System.out.println("2.Insert End");
            System.out.println("3.Insert at Position");
            System.out.println("4.Delete Beg");
            System.out.println("5.Delete End");
            System.out.println("6.Delete by Value");
            System.out.println("7.Search");
            System.out.println("8.Display");
            System.out.println("9.Count");
            System.out.println("10.Reverse");
            System.out.println("11.Exit");
            System.out.print("Enter choice: ");

            ch = sc.nextInt();

            switch (ch) {
                case 1:
                    x = sc.nextInt();
                    l.insertBeg(x);
                    break;
                case 2:
                    x = sc.nextInt();
                    l.insertEnd(x);
                    break;
                case 3:
                    x = sc.nextInt();
                    pos = sc.nextInt();
                    l.insertAtPos(x, pos);
                    break;
                case 4:
                    l.deleteBeg();
                    break;
                case 5:
                    l.deleteEnd();
                    break;
                case 6:
                    x = sc.nextInt();
                    l.deleteByValue(x);
                    break;
                case 7:
                    x = sc.nextInt();
                    l.search(x);
                    break;
                case 8:
                    l.display();
                    break;
                case 9:
                    l.count();
                    break;
                case 10:
                    l.reverse();
                    break;
                case 11:
                    System.out.println("Exit");
                    break;
                default:
                    System.out.println("Invalid Choice");
            }
        } while (ch != 11);
    }
}
***********************************************************
import java.util.Scanner;

class StackArray {

    int[] stack;
    int top = -1;
    int size;

    StackArray(int size) {
        this.size = size;
        stack = new int[size];
    }

    void push(int x) {
        if (top == size - 1) {
            System.out.println("Stack Overflow");
            return;
        }
        stack[++top] = x;
    }

    void pop() {
        if (top == -1) {
            System.out.println("Stack Underflow");
            return;
        }
        System.out.println("Popped: " + stack[top--]);
    }

    void peek() {
        if (top == -1)
            System.out.println("Stack Empty");
        else
            System.out.println("Top = " + stack[top]);
    }

    void display() {
        if (top == -1) {
            System.out.println("Stack Empty");
            return;
        }
        for (int i = top; i >= 0; i--)
            System.out.print(stack[i] + " ");
        System.out.println();
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter stack size: ");
        int n = sc.nextInt();

        StackArray s = new StackArray(n);
        int ch, x;

        do {
            System.out.println("\n--- STACK MENU ---");
            System.out.println("1.Push");
            System.out.println("2.Pop");
            System.out.println("3.Peek");
            System.out.println("4.Display");
            System.out.println("5.Exit");
            System.out.print("Enter choice: ");

            ch = sc.nextInt();

            switch (ch) {
                case 1:
                    x = sc.nextInt();
                    s.push(x);
                    break;
                case 2:
                    s.pop();
                    break;
                case 3:
                    s.peek();
                    break;
                case 4:
                    s.display();
                    break;
                case 5:
                    System.out.println("Exit");
                    break;
                default:
                    System.out.println("Invalid Choice");
            }
        } while (ch != 5);
    }
}
********************************************************************
import java.util.Scanner;

class QueueArray {

    int[] queue;
    int front = 0, rear = -1, size;

    QueueArray(int size) {
        this.size = size;
        queue = new int[size];
    }

    void enqueue(int x) {
        if (rear == size - 1) {
            System.out.println("Queue Overflow");
            return;
        }
        queue[++rear] = x;
    }

    void dequeue() {
        if (front > rear) {
            System.out.println("Queue Underflow");
            return;
        }
        System.out.println("Deleted: " + queue[front++]);
    }

    void peek() {
        if (front > rear)
            System.out.println("Queue Empty");
        else
            System.out.println("Front = " + queue[front]);
    }

    void display() {
        if (front > rear) {
            System.out.println("Queue Empty");
            return;
        }
        for (int i = front; i <= rear; i++)
            System.out.print(queue[i] + " ");
        System.out.println();
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter queue size: ");
        int n = sc.nextInt();

        QueueArray q = new QueueArray(n);
        int ch, x;

        do {
            System.out.println("\n--- QUEUE MENU ---");
            System.out.println("1.Enqueue");
            System.out.println("2.Dequeue");
            System.out.println("3.Peek");
            System.out.println("4.Display");
            System.out.println("5.Exit");
            System.out.print("Enter choice: ");

            ch = sc.nextInt();

            switch (ch) {
                case 1:
                    x = sc.nextInt();
                    q.enqueue(x);
                    break;
                case 2:
                    q.dequeue();
                    break;
                case 3:
                    q.peek();
                    break;
                case 4:
                    q.display();
                    break;
                case 5:
                    System.out.println("Exit");
                    break;
                default:
                    System.out.println("Invalid Choice");
            }
        } while (ch != 5);
    }
}
