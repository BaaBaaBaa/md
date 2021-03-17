```javascript
const pending = 'pending';
const resolved = 'resolved';
const rejected = 'rejected';

function myPromise(fn) {
    const that = this;
    that.state = pending;
    that.value = null;
    that.resolvedCallBacks = [];
    that.rejectedCallBacks = [];
    // 待完善 resolve 和 reject 函数
  	// 待完善执行 fn 函数
}
```

```javascript
const pending = 'pending';
const resolved = 'resolved';
const rejected = 'rejected';

function myPromise(fn) {
    const that = this;
    that.state = pending;
    that.value = null;
    that.resolvedCallBacks = [];
    that.rejectedCallBacks = [];
    
    try {
        fn(resolve, reject);
    } catch(e) {
        reject(e);
    }
    
    function resolve(value) {
        if(that.state === pending) {
            that.state = resolved;
            that.value = value;
            that.resolvedCallbacks.map(cb => cb(that.value))
        }
    }
    
    function reject(value) {
        if(that.state === pending) {
            that.state = rejected;
            that.value = value;
            that.rejectedCallbacks.map(cb => cb(that.value))
        }
    }
    
}
```

```javascript
myPromise.prototype.then = function(onFulfilled, onRejected) {
    const that = this;
    onFulfilled = typeof onFulfilled === 'function' ? onFulFilled : v => v;
    onRejected = typeof onRejected === 'function' ? onReject : r => { throw r };
    
    if(that.state === pending) {
        that.resolvedCallbacks.push(onFulfilled);
        that.rejectedCallbacks.push(onRejected);
    }
    if(that.state === resolved) {
        onFulfilled(that.value);
    }
    if(that.state === rejected) {
        onFulfilled(that.value);
    }
}
```

