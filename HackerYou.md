Two ways of creating your array and adding to it

1) I initialize the size of the array with a good guess of what I'll need

```javascript
var albumMaxSize = new array(10); 
albumMaxSize[0] = '23';
albumMaxSize[1] = '13';
albumMaxSize[2] = '14';
albumMaxSize[3] = '12';
albumMaxSize[4] = '21';
```
Now what if I want to add a new picture to the array:
```javascript
albumMaxSize[length] = '44';
```

2) Don't make it any bigger than you think you might need

```javascript
var albumMinSize = ['23', '13', '14', '12', '21'];
```

How about for the albumMinSize array:
```javascript
var newAlbum = new array(album.length + 1);
for ( int i = 0; i < album.length; i++) {
  newAlbum[i] = album[i];
}
newAlbum[++i] = '34';
```

Now what if I want to delete a photo from the album... say the picture at position 4
```javascript
var indexToDelete = 4;
var newAlbum[10];
for (int i = indexToDelete - 1 ; c < length - 1 ; i++ ) {
  array[i] = array[i+1];
}         
```

What if we wanted to avoid all of this copying over?
The reason elements in an array need to be side-by-side, is because we don't have any other property or field to tell us where the next element is. If we pair the data with an additional property called 'next'...

Let's define our node

```javascript
function Node(data) {
    this.data = data;
    this.next = null;
}
```
And our linked list

```javascript
function SinglyList() {
    this._length = 0;
    this.head = null;
}
```

```javascript
// simplified to only perform delete and not return the deleted node
SinglyList.prototype.remove = function(position) {
  var currentNode = this.head,
    length = this._length,
    count = 0,
    beforeNodeToDelete = null,
    nodeToDelete = null,
    
  // edge case handling
  ...
 
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
 
  return;
};
```

+ Fast insertion / deletion
+ Linked lists let you insert elements at the beginning and end of the list in O(1) time. 
+ Linked lists also remove the overhead of bothering about the size of the data structure. The size need not to be known in advance.
- Slow lookup: Drawback: O(n) complexity in finding a specific node
- They do use more memory than arrays because of the pointers
- They are read in order


Trees



```javascript
function Node(data) {
    this.data = data;
    this.parent = null;
    this.children = [];
}
```

```javascript
function Tree(data) {
    var node = new Node(data);
    this._root = node;
}
```
```javascript
```
```javascript
```
```javascript
```
```javascript
```
```javascript
```
```javascript
```
```javascript
```
```javascript
```
    
