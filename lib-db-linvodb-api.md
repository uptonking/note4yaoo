---
title: lib-db-linvodb-api
tags: [api, linvodb]
created: 2022-12-23T00:31:25.352Z
modified: 2022-12-23T00:31:34.969Z
---

# lib-db-linvodb-api

# guide

# quickstart

```JS
/** 👇🏻 create a table, like a mongodb collection */
tb = new Model('movie1'); // new Datastore()

// create multiple tables, like a database
// db = {};
// db.users = new Model('path/to/users.db');
// db.movies = new Model('path/to/movies.db');

const movies = [
  { _id: 'id11', title: 'Seven', year: 1995, genres: ['Drama', 'Crime', 'Mystery'] },
  { _id: 'id12', title: 'Fight Club', year: 1999, genres: ['Drama'] },
  { _id: 'id13', title: 'Inception', year: 2010, genres: ['Sci-Fi', 'Action', 'Adventure'] },
  {
    _id: 'id14',
    title: 'Jurassic Park',
    year: 1993,
    genres: ['Sci-Fi', 'Action', 'Adventure'],
  },
  {
    _id: 'id15',
    title: "Schindler's List",
    year: 1993,
    genres: ['Drama', 'History', 'Biography'],
  },
];

let doc1;

// use the .insert to insert one or more documents
tb.insert({ ...movies[0], _id: undefined }, (err, newDoc) => {
  // insert doc with an auto-generated _id
  // The _id of a document, once set, cannot be modified.
  console.log(';; insert-cb1 ', newDoc._id, newDoc);
  doc1 = newDoc;
});
tb.insert(movies, (err, newDocs) => {
  console.log(';; insert-cb2 ', newDocs.length, newDocs)
});

// @deprecated save is like an insert, except it allows saving existing document
tb.save([doc1, { title: 'test movie', year: 2022 }], (err, docs) => {
  // docs[0] is doc1
  // docs[1] is newly-inserted document for test movie 2022, with a _id
});

// find all
tb.find({}, (err, docs) => {
  // If no document is found, docs is equal to []
});
// exact match to find all
tb.find({ title: 'Seven' }, (err, docs) => {
  // only seven
});
tb.find({ title: { $in: ['Seven', 'Inception'] } }, (err, docs) => {
  // seven, inception
});

// tb.update(query, updateRules, options, callback) will update all documents matching query according to the updateRules
tb.update({ _id: 'id12' }, {
    $set: { notes: 'find in imdb' }
  }, {},
  (err, numReplaced) => {

  });

// tb.remove(query, options, callback) will remove all documents matching query according to options
tb.remove({ _id: 'id11' }, {}, (err, numRemoved) => {
  // numRemoved = 1
});

// Schemas are defined as an object of specs for each property. Nested objects are supported.

tb2 = new Model('movie2', {
  schema: {
    title: { type: String }
    notes: { type: String, default: 'sharing' },
    genres: [String]
  }
});



```

 

# api
