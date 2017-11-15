## Two ways of creating your array and adding to your array

We are discussing here the data structure, array. Not the JavaScript Array.

### 1) I initialize the size of the array with some room to grow

```javascript
let largeAlbum = new array(50); 
largeAlbum[0] = 3;
largeAlbum[1] = 8;
largeAlbum[2] = 1;
largeAlbum[3] = 12;
largeAlbum[4] = 5;
```

Now what if I want to add a new picture to the array? No problem.

```javascript
largeAlbum[largeAlbum.length] = 7;
```

### 2) Don't make it any bigger than you need right now

```javascript
let smallAlbum = [3, 8, 1, 12, 5];
```

But to add to it now, you must create a new array:
```javascript
let newAlbum = new array(smallAlbum.length + 1);
let index;
for ( index = 0; i < smallAlbum.length; index++) {
  newAlbum[index] = smallAlbum[index];
}
newAlbum[index+1] = 7;
```

___

### Now what if I want to delete a photo from the album... say the picture 12
```javascript
let myAlbum = [3, 8, 1, 12, 5];
let pictureToDelete = 12;
// first find the picture to delete
let index;
let indexToDelete;
for (index = 0 ; index < myAlbum.length ; index++ ) {
  if(myAlbum[index] === pictureToDelete) {
    indexToDelete = index;
    break;
  }
}         
for (index = indexToDelete; index < myAlbum.length ; index++ ) {
  myAlbum[index] = myAlbum[index+1];
}         
```

Similarly, to add a new picture, say after picture 12, you need to copy all elements from picture 12 onwards over one

This is because the data of an array resides contiguously in memory (side-by-side).
___


## What if we wanted to avoid all of this copying over? ...and avoid this memory restriction?
The reason elements in an array need to be side-by-side, is because we don't have any other property or field to tell us where the next element is. If we pair the data with an additional property called 'next'...

### Let's define our node

```javascript
class Node {
  constructor(value) {
    this.data = value;
    this.next = null;
  }
}
```
### And our linked list

```javascript
class LinkedList {
  constructor(value) {
    this.head = new Node(value);
    this.length = 1;
  }
  
  // functions to edit / manage your linked list
  ...
}
```

## Now what do we need to do to remove picture 12?
```javascript
  remove(valueToDelete) {
    let currentNode = this.head;
    let index = 0;
    let beforeNodeToDelete = null;
    let nodeToDelete = null;

    // the first node is removed
    if (currentNode.data === valueToDelete) {
      this.head = currentNode.next;
      currentNode = null;
      this.length--;
      return;
    }

    beforeNodeToDelete = currentNode;
    // any other node is removed
    while (index <= this.length) {
      if(currentNode.data === valueToDelete) {
        beforeNodeToDelete.next = currentNode.next;
        currentNode = null;
        this.length--;
        break;
      }
      index++;
    }
  }
```

## Positives of linked lists:
+ Fast insertion / deletion
+ Linked lists let you insert elements at the beginning and end of the list is trivial. 
+ If you keep a 'tail' property for the last node, like you 'head' property for the first node, inserting at the end of the list is very trivial.
+ Linked lists also remove the overhead of bothering about the size of the data structure. The size need not to be known in advance.

## Drawbacks:
- Slow lookup: need to iterate through the list to find a specific node
- They do use more memory than arrays because of the pointers

We can also add a 'previous' field to allow traversal in both directions.

For our next data structure, similar to linked lists, we will deal with nodes and pointers again to next nodes...

___

## Trees

Let's look at how this data structure can be defined, and then similarly, we'll compare behaviour using our picture album compared to how we saw it behave with the array and linked list.

### Let's define our Node and Tree
```javascript
class Node {
  constructor(value) {
    this.data = value;
    this.parent = null;
    this.children = [];
  }
}
```

```javascript
class Tree {
  constructor(value) {
    this.root = new Node(value);
  }
  
  // functions to edit / manage the tree
  ...
}
```

## What does a tree traversal look like?

```javascript
  traverse(callback) {
    callback(this.root);

    if (!this.root.children || this.root.children.length < 1) {
      return;
    }
    children.forEach(() => {
      child.traverse(callback);
    });
  }

```

A simple example to traverse the entire tree and print to screen all values:
```javascript
myTree.traverse((node) => console.log(node.data));
```

Your callback can be anything here... a function to return all image type children, a counter function to find the number of images, a function that manipulates certain nodes, etc...


## Why use a tree?

Let's go back to our picture album idea, and consider adding pictures in order, as we select additional pictures to add.

Like in the original array and linked list... let's say we still want the pictures in this order:  3, 8, 1, 12 5.
Realistically, they may not be chosen in that order too though. Let's add them to the tree, sorted, as you select them in this order: 1, 3, 8, 12, 5. 
what does our tree look like?

Now what if we selected them in this order with the array or linked list??
+ If we did that with an array, we'd have to shift pictures over to make room for the new picture everytime we added anywhere but the last position of the array. Lots of copying.
+ With a linked list, we wouldn't have to copy, but we still iterate through the list linearly, find the spot, ajust a few next pointers. 
+ With a tree, no copying or shifting either, but as we iterate, we are looking through a smaller and smaller subset... it might help to visualize with an album of 100 pictures.

We will take a closer look into sorting and efficiency next time.

+ both insertions (and retrievals) of objects take on the average log2N time, where N is the number of objects stored.
+ the tree naturally grows to hold an arbitrary, unlimited number of objects.


### The DOM

What is the DOM?

It’s an interface that allows programs and scripts to dynamically access and update the content, structure, and style of a document.
It's a great example because you have lots of one-to-many relationships.

![simple DOM example](https://snipcademy.com/code/img/tutorials/javascript/dom.svg "Simple DOM")

Because it is so important to quickly access, read, change your DOM tree, on top of being able to traverse the tree, you are also provided with hash tables (dictionaries) of elements by id, to quickly look up specific elements (or nodes) of your tree by index. Hence, why you can use calls like:

```javascript
let object = document.getElementById('myId');
```
or with jQuery:
```javascript
let jQueryObject = $('#myId'); 
```

So when needed, you can also look at combining data structures.
