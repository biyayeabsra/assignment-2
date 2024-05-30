class Node {
    int data;
    Node next;

    public Node(int data) {
        this.data = data;
        this.next = null;
    }
}

class LinkedList {
    Node head;

    // Method to insert a node at a specified position
    public void insertAtPos(int position, int data) {
        Node newNode = new Node(data);
        if (position == 1) {
            newNode.next = head;
            head = newNode;
        } else {
            Node temp = head;
            for (int i = 1; i < position - 1 && temp != null; i++) {
                temp = temp.next;
            }
            if (temp == null) {
                System.out.println("Invalid position");
                return;
            }
            newNode.next = temp.next;
            temp.next = newNode;
        }
    }

    // Method to delete a node at a specific position
    public void deleteAtPosition(int position) {
        if (position == 1) {
            head = head.next;
        } else {
            Node temp = head;
            for (int i = 1; i < position - 1 && temp != null; i++) {
                temp = temp.next;
            }
            if (temp == null || temp.next == null) {
                System.out.println("Invalid position");
                return;
            }
            temp.next = temp.next.next;
        }
    }

    // Method to delete the node that occurs after a given node
    public void deleteAfterNode(Node prevNode) {
        if (prevNode == null || prevNode.next == null) {
            System.out.println("Invalid node");
            return;
        }
        prevNode.next = prevNode.next.next;
    }

    // Method to search for a node with a specific value
    public boolean searchNode(int key) {
        Node current = head;
        while (current != null) {
            if (current.data == key) {
                return true;
            }
            current = current.next;
        }
        return false;
    }
}

class Stack {
    Node top;

    // Method to push an element onto the stack
    public void push(int data) {
        Node newNode = new Node(data);
        if (top == null) {
            top = newNode;
        } else {
            newNode.next = top;
            top = newNode;
        }
    }

    // Method to pop an element from the stack
    public int pop() {
        if (top == null) {
            System.out.println("Stack is empty");
            return -1; // or throw an exception
        }
        int poppedValue = top.data;
        top = top.next;
        return poppedValue;
    }

    // Method to peek the top element of the stack
    public int peek() {
        if (top == null) {
            System.out.println("Stack is empty");
            return -1; // or throw an exception
        }
        return top.data;
    }
}

public class Main {
    public static void main(String[] args) {
        LinkedList list = new LinkedList();
        list.insertAtPos(1, 101);
        list.insertAtPos(2, 204);
        list.insertAtPos(3, 306);
        list.insertAtPos(2, 125); // Inserting at position 2

        list.deleteAtPosition(3); // Deleting node at position 3

        Node secondNode = list.head.next;
        list.deleteAfterNode(secondNode); // Deleting node after the second node

        boolean found = list.searchNode(15); // Searching for node with value 15
        System.out.println("Node with value 15 found: " + found);

        Stack stack = new Stack();
        stack.push(5);
        stack.push(10);
        stack.push(15);

        System.out.println("Top element of stack: " + stack.peek());
        System.out.println("Popped element: " + stack.pop());
        System.out.println("Top element of stack after pop: " + stack.peek());
    }
}
