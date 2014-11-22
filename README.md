pants-path
==========

[![License](http://img.shields.io/badge/license-MIT-red.svg?style=flat-square)](https://github.com/xinix-technology/pants-path/blob/master/LICENSE)
[![Bower](http://img.shields.io/bower/v/xinix-technology/pants-path.svg?style=flat-square)](https://github.com/xinix-technology/pants-path)

Pustaka pembantu pants ini dapat digunakan untuk memberikan kemampuan data container pada aplikasi tanpa mengotori namespace global. Data pada containernya dapat diakses melalui string path tertentu seperti `user.name.first_name`.

Meski berprefix pants, pants-path dapat digunakan secara standalone tanpa menggunakan pants.

## Instalasi menggunakan bower

```bash
bower install xinix-technology/pants-path --save
```

##  API

pants-path memuat DUA kegunaan:

1. Pustaka mengakses data pada container context
2. Pustaka mengakses path

### Context

Sebuah object yang memegang kendali akses terhadap sebuah root data (object yang ingin diakses datanya). Object ini diinstansiasi melalui fungsi `pants.path()`

#### pants.path(opt object: rootData): Context

Fungsi pants.path() membutuhkan argument #1 rootData secara opsional, jika diberikan akan mengembalikan nilai berupa context baru dengan root data yang telah diberikan. Namun jika argument #1 tidak ada, maka fungsi akan mengembalikan nilai berupa singleton default context (sebuah context yang akan dikembalikan selalu untuk setiap pemanggilan fungsi tanpa argument #1.
Contoh:

```javascript
// root data to be specified for context later
var myRootData = {
  'somenamespace': {
    'somedata': 'this is data'
  }
};

// create new context with myRootData object as root data
var context = pants.path(myRootData);
var data = context.get('somenamespace.somedata'); // data === myRootData.somenamespace.somedata

var anotherContext = pants.path(myRootData); // context !== anotherContext

// get default context
var defaultContext = pants.path();
defaultContext.set('hello.world', 'hello world!');

var anotherCallOfContext = pants.path(); // defaultContext === anotherCallOfContext
console.assert(anotherCallOfContext.get('hello.world'));  // === 'hello world!'
```

#### Context#set(string: pathString, data)

Mengeset sebuah data ke dalam context pada path tertentu.

#### Context#get(string: pathString)

Mengambil sebuah data dari dalam context pada path tertentu.

### Path

Sebuah object untuk manipulasi object dengan path tertentu dalam bentuk string. Object ini diinstansiasi melalui fungsi `pants.path.get()`

#### pants.path.get()

Fungsi pants.path.get() membutuhkan argument #1 sebagai path dalam bentuk string.
Contoh:

```javascript
var path = pants.path.get('canonical.data.tree');
```

#### Path#get(object: rootData): var

Mengembalikan var yang berada pada path tertentu dalam root data.

#### Path#set(object: rootData, var: value): boolean

Mengeset sebuah nilai dalam root data pada path tertentu.
