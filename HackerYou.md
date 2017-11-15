## Two ways of creating your array and adding to your array

### 1) I initialize the size of the array with some room to grow

```javascript
var albumMaxSize = new array(10); 
albumMaxSize[0] = '23';
albumMaxSize[1] = '13';
albumMaxSize[2] = '14';
albumMaxSize[3] = '12';
albumMaxSize[4] = '21';
```

Now what if I want to add a new picture to the array? No problem.

```javascript
albumMaxSize[length] = '44';
```

### 2) Don't make it any bigger than you need right now

```javascript
var albumMinSize = ['23', '13', '14', '12', '21'];
```

But to add to it now, you must create a new array:
```javascript
var newAlbum = new array(album.length + 1);
for ( int i = 0; i < album.length; i++) {
  newAlbum[i] = album[i];
}
newAlbum[++i] = '34';
```

___

### Now what if I want to delete a photo from the album... say the picture at position 4
```javascript
var indexToDelete = 4;
var newAlbum[10];
for (int i = indexToDelete - 1 ; c < length - 1 ; i++ ) {
  array[i] = array[i+1];
}         
```

Similarly, to add a new picture, say at position 3, you need to copy all elements from position 3 onwards over one

___


## What if we wanted to avoid all of this copying over?
The reason elements in an array need to be side-by-side, is because we don't have any other property or field to tell us where the next element is. If we pair the data with an additional property called 'next'...

### Let's define our node

```javascript
var Node = function Node(value) {
  this.data = value;
  this.next = null;
};
```
### And our linked list

```javascript
var SinglyList = function SinglyList(value) {
  var _this = this;
  
  this.head = new Node(value);
  this.length = 0;
  
  ...
}
```

## Now what do we need to do to remove a node / picture from position 4?
```javascript
  this.remove = function (position) {
    let currentNode = this.head;
    let count = 0;
    let beforeNodeToDelete = null;
    let nodeToDelete = null;

    // the first node is removed
    if (position === 1) {
      this.head = currentNode.next;
      currentNode = null;
      this._length--;
      return;
    }

    // any other node is removed
    while (count < position) {
      beforeNodeToDelete = currentNode;
      nodeToDelete = currentNode.next;
      count++;
    }

    beforeNodeToDelete.next = nodeToDelete.next;
    nodeToDelete = null;
    this._length--;
  }
```

## Positives of linked lists:
+ Fast insertion / deletion
+ Linked lists let you insert elements at the beginning and end of the list in O(1) time. 
+ Linked lists also remove the overhead of bothering about the size of the data structure. The size need not to be known in advance.

## Drawbacks:
- Slow lookup: need to iterate through the list to find a specific node
- They do use more memory than arrays because of the pointers

We can also add a 'previous' field to allow traversal in both directions, and a 'tail' property to our Linked List implementation to keep track of the last element of the list if needed.


For our next data structure, similar to linked lists, we will deal with nodes and pointers again to next nodes...

___

## Trees

The example we will use to discuss trees is the DOM. What is the DOM?

It’s an interface that allows programs and scripts to dynamically access and update the content, structure, and style of a document.
It's a great example because you have lots of one-to-many relationships.

![simple DOM example](https://snipcademy.com/code/img/tutorials/javascript/dom.svg "Simple DOM")


### Let's define our Node and Tree
```javascript
var Node = function Node(value) {
  this.data = value;
  this.parent = null;
  this.children = [];
};
```

```javascript
var Tree = function Tree(value) {
  var _this = this;

  this.root = new Node(value);
  this.length = 0;
};
```

## What does a tree traversal look like?

```javascript
  this.traverse = function (callback) {
    callback(_this);

    if (!_this.children) {
      return;
    }
    for (var i = 0; i < _this.children.length; i++) {
      var child = _this.children[i];
      child.traverse(callback);
    }
  };
};
```

Your callback can be anything here... a function to return all image type children, a counter function to find the number of images, a function that manipulates certain nodes, etc...


Because it is so important to quickly access, read, change your DOM tree, on top of being able to traverse the tree, you are also provided with hash tables (dictionaries) of elements by id, to quickly look up specific elements (or nodes) of your tree by index. Hence, why you can use calls like:

```javascript
let object = document.getElementById('myId');
```
or with jQuery:
```javascript
let jQueryObject = $('#myId'); 
```

So when needed, you can also look at combining data structures.

## Why use a tree?

Let's go back to our original picture album problem and add items dynamically to the tree...

+ both insertions (and retrievals) of objects take on the average log2N time, where N is the number of objects stored.
+ the tree naturally grows to hold an arbitrary, unlimited number of objects.
