gridfstore
==========

Mongoose with GridFS.  
GridFS is convenient way to store files and it allows all mongodb features like clusters and sharding.
This library is intended to help GridFS usage with nodejs and mongoose. It allows efficient way to store data, 
e.g. on the fly gzipped before storing and when gzipped data is read back gzip can be extracted on the fly.

[![Build Status](https://travis-ci.org/jupe/gridfstore.png?branch=master)](https://travis-ci.org/jupe/gridfstore)

Installation
------------
```
npm install gridfstore
```

Documentation
-------------
```
/*
  register schema
*/
gridfstore.register('collection', myschema);

/*
  store arguments:
  data                      -> string|buffer|readstream
  options: { gzip: true }   -> gzip input data before store gridfs
*/
gridfstore.store( metadata, data, [options,] callback)

/* mongoose model */
gridfstore.model   
/*
  read arguments:
  uuid                                    -> store generate uuid as filename
  options: { 
    gunzip: Boolean,                      -> gunzip output data before call callback (default: false)
    method: String   ('sync'|'async')     -> get as sync or asyncronously (stream)  (default: sync)
  }
*/
gridfstore.read( uuid, [options,] callback)
```

Usage
-----
```
var mongoose  = require('mongoose'),
   gridfstore = require('../lib/gridfstore');
   
var mymeta = {
  title: {type: String},
  owner: {type: String}
}

gridfstore.register('test', mymeta);

gridfstore.store( {filename: 'test1.txt', title: 'example', owner: 'jva'}, 
                  'this is file content',
                  function(error, meta){
    //meta == whole metadata from gridfs
});

```
