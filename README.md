# faiss-node
This package is in a very early stage of development.

## Installation

```sh
$ npm install faiss-node
```

## Usage

```javascript
const { IndexFlatL2 } = require('faiss-node');

const dimension = 2;
const index = new IndexFlatL2(dimension);

console.log(index.getDimension()); // 2
console.log(index.isTrained()); // true
console.log(index.ntotal()); // 0

// inserting data into index.
index.add([1, 0]);
index.add([1, 2]);
index.add([1, 3]);
index.add([1, 1]);

console.log(index.ntotal()); // 4

const results = index.search([1, 0], 4);
console.log(results.labels); // [ 0, 3, 1, 2 ]
console.log(results.distances); // [ 0, 1, 4, 9 ]

// Save index
const fname = 'faiss.index';
index.write(fname);

// Load saved index
const index_loaded = IndexFlatL2.read(fname);
console.log(index_loaded.getDimension()); //2
console.log(index_loaded.ntotal()); //4
const results1 = index_loaded.search([1, 1], 4);
console.log(results1.labels); // [ 3, 0, 1, 2 ]
console.log(results1.distances); // [ 0, 1, 1, 4 ]
```