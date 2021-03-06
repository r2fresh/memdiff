BDD style memory leak hunting tool. See [example/simple.js](#example)

![](https://dl.dropbox.com/s/dh69myarcqjkm6i/memdiff.png?token_hash=AAHxKG2CeksLu7V6HWCy_zr9TQLhoVfQXNFh3pMv9ujVbw)

## Install

```bash
$ npm install -g memdiff
```

Requires Node v0.8.x

## Usage

```bash
$ memdiff --help
```

<a name="example"></a>
## Example Module

```js
// example/simple.js
function SimpleClass(){}

var leaks = [];

describe('SimpleClass', function(){

  it('is leaking', function(){
    leaks.push(new SimpleClass);
  });


  it('is not leaking', function(){
    new SimpleClass;
  });

});
```

<a name="api"></a>
## API

```js
var memdiff = require('memdiff');

function SimpleClass(){}

var leaks = [];

function leaking(){
  leaks.push(new SimpleClass);
}

memdiff(leaking, function(result){ // or memdiff({ fn: leaking, duration: 15, times: 9999, interval: 1 ....
  console.log('leaking: ', result.size);
});
```
