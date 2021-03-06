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

Oh oh...
But to add to it now, you must create a new array:
```javascript
let newAlbum = new array(smallAlbum.length + 1);
let index;
for ( index = 0; i < smallAlbum.length; index++) {
  newAlbum[index] = smallAlbum[index];
}
newAlbum[index+1] = 7;
```

The point is, hopefully, you've predefined your array big enough for your needs.

___

### Now what if I want to delete a photo from the album... say the picture 12
```javascript
let myAlbum = [3, 8, 1, 12, 5];
let pictureToDelete = 12;
let index;
let indexToDelete;

// first find the picture to delete
for (index = 0 ; index < myAlbum.length ; index++ ) {
  if(myAlbum[index] === pictureToDelete) {
    indexToDelete = index;
    break;
  }
}

// now we can overwrite it, shifting all elements over by one
for (index = indexToDelete; index < myAlbum.length ; index++ ) {
  myAlbum[index] = myAlbum[index+1];
}         
```

Similarly, to add a new picture, say after picture 12, you need to copy all elements from picture 12 onwards over one. So much copying, sigh... what if we had to copy much larger elements... yikes!

This is because the data of an array resides contiguously in memory (side-by-side).
___


## What if we wanted to avoid all of this copying over? ...and avoid this memory restriction?

Let's pair our data with a second property... one that tells us where the next element is. Then they wouldn't need to be side-by-side like in an array... they could reside anywhere in memory! Sweet!

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

Here's the code, but let me draw it out...

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

Inserting happens in a similar fashion too.

## Positives of linked lists:
+ Fast insertion / deletion **(no copying of other elements!)**
+ Linked lists let you insert elements at the **beginning of the list** fast ...aka O(1)  ...i.e. same time regardless of size
+ If you keep a **'tail' property** for the last node, like you 'head' property for the first node, inserting at the end of the list is also fast ...O(1).
+ Linked lists also remove the overhead of bothering about the size of the data structure. **The size need not to be known in advance.**

## Drawbacks:
- Slow lookup: need to iterate through the list to find a specific node
- They do use more memory than arrays because of the pointers

### Note
We can also add a **'previous' property** to allow traversal in both directions.

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

Of all of the wonderful things we want to do with a tree, we first would need a way to traverse it (visit every node). 

## What does a tree traversal look like?

Here's an example with recursion and callbacks...

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

What is actually happening in the background, the callback commands are stored in a stack to *remember* what to do *later*... 


## Why use a tree?

Let's go back to our picture album idea, and consider adding pictures in order, as we select additional pictures to add.

Like in the original array and linked list... let's say we still want the pictures in this order:  3, 8, 1, 12 5.
Realistically, they may not be chosen in that order too though. Let's add them to the tree, sorted, as you select them in this order: 1, 3, 8, 12, 5. 
what does our tree look like?

Now what if we selected them in this order with the array or linked list??
+ If we did that with an array, we'd have to shift pictures over to make room for the new picture EVERYTIME we added anywhere but the last position of the array. Lots of copying. NO THANKS!
+ With a linked list, we wouldn't have to copy, but we still iterate through the list linearly, find the spot, ajust a few next pointers. 
+ With a tree, no copying or shifting either, but as we iterate, we are looking through a smaller and smaller subset... it might help to visualize with an album of 100 pictures.

We will take a closer look into sorting and efficiency next time.

+ both insertions (and retrievals) of objects take on the average log2N time, where N is the number of objects stored...
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
