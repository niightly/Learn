# ES6 Iterations - Some examples

### A simple reduce
Use a reducer when you need to combine data from multiple sources into one entity.

```js
const posts = [
  {id: 1, upVotes: 2},
  {id: 2, upVotes: 89},
  {id: 3, upVotes: 1}
];
const totalUpvotes = posts.reduce((totalUpvotes, currentPost) =>     
  totalUpvotes + currentPost.upvotes, // reducer function
  0 // initial accumulator value
);
// now totalUpvotes = 92
```

### A simple map
Use a map for processing streams like data (examples array). It helps me to think of it as a transformation that will be applied to all the elements of a stream (array).

```js
const integers = [1, 2, 3, 4, 6, 7];
const twoXIntegers = integers.map(i => i*2);
// twoXIntegers are now [2, 4, 6, 8, 12, 14]
```

### A simple find
This helps pin point elements inside an array (stream like data structure).

```js
const posts = [
  {id: '1', title: 'Title 1'},
  {id: 2, title: 'Title 2'}
];
// find the title of post whose id is 1
const title = posts.find(p => p.id === 1).title;
```

### A simple filter
Filter creates views of array like data structures.

```js
const integers = [1, 2, 3, 4, 6, 7];
const evenIntegers = integers.filter(i => i%2 === 0);
// evenIntegers are [2, 4, 6]
```

### A Map / Reduce combined
```js
const posts = [
  {id: 1, upVotes: 2},
  {id: 2, upVotes: 89},
  {id: 3, upVotes: 1}
];
const reducePost = posts.reduce((array, post) => {
  if (post.upVotes < 3) { array.push(post) }
  return array
},[]);
/* now reducePost = [
  {id: 1, upVotes: 2},
  {id: 3, upVotes: 1}
]
```

### Adding an element to an array
Useful while creating infinite scroll ui (there is an example further below which uses real world array of objects).

```js
const books = ['Positioning by Trout', 'War by Green'];
const newBooks = [...books, 'HWFIF by Carnegie'];
// newBooks are now ['Positioning by Trout', 'War by Green', 'HWFIF // by Carnegie']
```

### Creating a view on top of an array
Useful when there is a need to remove something from a list, example a user deleted an item from the cart.

```js
const myId = 6;
const userIds = [1, 5, 7, 3, 6];
const allButMe = userIds.filter(id => id !== myId);
// allButMe is [1, 5, 7, 3]
```

### Adding an element to an array of objects
Nice to use when you want to update a property on the fly

```js
const books = [];
const newBook = {title: 'Alice in wonderland', id: 1};
const updatedBooks = [...books, newBook];
The books variable here might also be undefined. It doesn’t matter, the spread operator will still work.
```

### Adding a key value pair to an object
Nice to use when you want to add a property on the fly

```js
const user = {name: 'Shivek Khurana'};
const updatedUser = {...user, age: 23};
```

### Adding a key value pair with dynamic key
Nice to use when you want to add a dynamic property on the fly

```js
const dynamicKey = 'wearsSpectacles';
const user = {name: 'Shivek Khurana'};
const updatedUser = {...user, [dynamicKey]: true};
// updatedUser is {name: 'Shivek Khurana', wearsSpectacles: true}
```

### Find and replace key value pair in array of objects:
Amazing isn't it?

```js
const posts = [
  {id: '1', title: 'Title 1'},
  {id: 2, title: 'Title 2'}
];
const updatedPosts = posts.map(p => p.id !== 1 ?
  p : {...p, {title: 'Updated Title 1'}}
);
/*
updatedPosts is now 
[
  {id: '1', title: 'Updated Title 1'},
  {id: 2, title: 'Title 2'}
];
*/
```

### Find an element inside an array of objects
No more for and stuff like that, one line and everything is solved

```js
const posts = [
  {id: 1, title: 'Title 1'},
  {id: 2, title: 'Title 2'}
];
const postInQuestion = posts.find(p => p.id === 2);
// postInQuestion now holds {id: 2, title: 'Title 2'}
```

### Delete a key value pair inside an object
Looks gly, but is useful

```js
const user = {name: 'Shivek Khurana', age: 23, password: 'SantaCl@use'};
const userWithoutPassword = Object.keys(user)
  .filter(key => key !== 'password')
  .map(key => {[key]: user[key]})
  .reduce((accumulator, current) => 
    ({...accumulator, ...current}),
    {}
  )
;
// userWithoutPassword becomes {name: 'Shivek Khurana', age: 23}
```

### Encode an object into query string
You’ll hardly need this specific use case, but it might help you create something.

```js
const params = {color: 'red', minPrice: 8000, maxPrice: 10000};
const query = '?' + Object.keys(params)
  .map(k =>   
    encodeURIComponent(k) + '=' + encodeURIComponent(params[k])
  )
  .join('&')
;
// encodeURIComponent encodes special characters like spaces, hashes 
// query is now "color=red&minPrice=8000&maxPrice=10000"
```

### Find index of element in an array of objects
No more for and stuff like that, one line and everything is solved

```js
const posts = [
  {id: 13, title: 'Title 221'},
  {id: 5, title: 'Title 102'},
  {id: 131, title: 'Title 18'},
  {id: 55, title: 'Title 234'}
];
// to find index of element with id 131
const requiredIndex = posts.map(p => p.id).indexOf(131);
```

With all this data structure power, I hope your code will become more precise, crisp and maintainable. When a new dev joins the team (and doesn’t understands this sorcery, show them this post).

> Most part of this page came from Shivek Khurana, thank you man.