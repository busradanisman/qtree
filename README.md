qtree - a simple JavaScript quadtree
=====

`qtree` is a minimal quadtree implementation that supports simple `put` and `get` operations on objects having a `x, y` position and `w, h` dimension. 

Installation
---

```
npm install qtree
```

Should also work in all browsers as is. `qtree` has no dependencies.

Usage
---

Create a quadtree by giving it some bounds, e.g. x, y, width and height

```javascript
var QuadTree = require('qtree');
var qt = QuadTree(0, 0, 100, 100);
```

You can also give `QuadTree` some options, the only option currently is the maximum number of children in a quadtree node until it is subdivided:

```javascript
var qt = QuadTree(0, 0, 100, 100, { maxchildren: 25 }); // defaults to 25
```

Put objects into the quadtree by using `put`. The objects can be anything as long as they have `x, y, w, h` properties as numbers indicating the bounding area of that object:

```javascript
qt.put({x: 5, y: 5, w: 0, h: 0, string: 'test'});
```

Iterate over the objects by giving an area and a callback:

```javascript
qt.get({x:0, y: 0, w: 10, h: 10}, function(obj) {
    // obj == {x: 5, y: 5, w: 0, h: 0, string: 'test'}
});	     
```

Iterating over objects continues until all of them have been iterated, or the callback function returns `false`.

You can also give a buffer threshold, indicating that you want to iterate over all objects in the area expanded by the threshold to all directions:

```javascript
qt.get({x:0, y: 0, w: 4, h: 4}, 2, function(obj) {
    // obj == {x: 5, y: 5, w: 0, h: 0, string: 'test'}
});	     
```

Alternatively, you can also iterate over all objects that are close to a line segment. The line segment is defined by having `x, y, dx, dy, dist` properties:

```javascript
qt.get({x: 0, y: 0, dx: 1, dy: 1}, 1, function(obj) {
    // obj == {x: 5, y: 5, w: 0, h: 0, string: 'test'}
});
```

Please note it is assumed that `dx, dy` are a 2-d vector normalized to the length of 1. The `dist` property of the object tells the length of the line segment to this direction. If `dist` is undefined or negative, it is assumed to be an infinite line instead of a line segment.

You can also use a buffer threshold when iterating based on a line segment.

License
---

(The MIT License)

Copyright (c) 2013 Antti Saarinen &lt;antti.p.saarinen@gmail.com&gt;

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the 'Software'), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.