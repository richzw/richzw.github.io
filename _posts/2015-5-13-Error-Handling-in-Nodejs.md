---
layout: post
title: Error Handling in Nodejs
---

You should also be familiar with the three main ways to deliver an error in Node.js:

-  For synchronous code, if an error happens, return the error (or `throw` the error as an exception)

```javascript
// Define divider as a syncrhonous function
var divideSync = function(x,y) {
    // if error condition?
    if ( y === 0 ) {
        // "throw" the error safely by returning it
        return new Error("Can't divide by zero")
    }
    else {
        // no error occured, continue on
        return x/y
    }
}

// Divide 4/2
var result = divideSync(4,2)
// did an error occur?
if ( result instanceof Error ) {
    // handle the error safely
    console.log('4/2=err', result)
}
else {
    // no error occured, continue on
    console.log('4/2='+result)
}

// Divide 4/0
result = divideSync(4,0)
// did an error occur?
if ( result instanceof Error ) {
    // handle the error safely
    console.log('4/0=err', result)
}
else {
    // no error occured, continue on
    console.log('4/0='+result)
}
```

- pass the error to a callback, a function provided specifically for handling errors and the results of asynchronous operations. The first argument of the callback is err, if an error happens err is the error. If an error doesn't happen then err is null. Any other arguments follow the err argument.

```javascript
var divide = function(x,y,next) {
    // if error condition?
    if ( y === 0 ) {
        // "throw" the error safely by calling the completion callback
        // with the first argument being the error
        next(new Error("Can't divide by zero"))
    }
    else {
        // no error occured, continue on
        next(null, x/y)
    }
}

divide(4,2,function(err,result){
    // did an error occur?
    if ( err ) {
        // handle the error safely
        console.log('4/2=err', err)
    }
    else {
        // no error occured, continue on
        console.log('4/2='+result)
    }
})

divide(4,0,function(err,result){
    // did an error occur?
    if ( err ) {
        // handle the error safely
        console.log('4/0=err', err)
    }
    else {
        // no error occured, continue on
        console.log('4/0='+result)
    }
})
```

- emit an `error` event on an EventEmitter

```javascript
// Definite our Divider Event Emitter
var events = require('events')
var Divider = function(){
    events.EventEmitter.call(this)
}
require('util').inherits(Divider, events.EventEmitter)

// Add the divide function
Divider.prototype.divide = function(x,y){
    // if error condition?
    if ( y === 0 ) {
        // "throw" the error safely by emitting it
        var err = new Error("Can't divide by zero")
        this.emit('error', err)
    }
    else {
        // no error occured, continue on
        this.emit('divided', x, y, x/y)
    }

    // Chain
    return this;
}

// Create our divider and listen for errors
var divider = new Divider()
divider.on('error', function(err){
    // handle the error safely
    console.log(err)
})
divider.on('divided', function(x,y,result){
    console.log(x+'/'+y+'='+result)
})

// Divide
divider.divide(4,2).divide(4,0)
```


Ref:

- [http://stackoverflow.com/questions/7310521/node-js-best-practice-exception-handling](http://stackoverflow.com/questions/7310521/node-js-best-practice-exception-handling)
- [https://www.joyent.com/developers/node/design/errors](https://www.joyent.com/developers/node/design/errors)
