# Stored promises

Stored promises implement the concept of [Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) on top of stored functions.

Promises models shall be modifiable at runtime, i.e. they shall be stored in a CDO repository. 
It is required so ``Promise then(Function resolve, Function reject)`` method could be called on a promise via some invocation mechanism - JAVA API call, REST call, some sort of a message.
A promise shall store the function tuple and return another promise. 

One implementation option is to use 3 functions - resolve, reject, and progress - how it is done in [Q](https://github.com/kriskowal/q).

Promises shall implement additional methods such as ``timeout()``, ``all()``, etc. to allow promise aggregation. 
This would enable reactive parallelized distributed computing to complement stored functions.

Initial prototyping of stored promises was done in [Nasdanika Foundation Server](https://github.com/Nasdanika/server/tree/before-cleanup) promise bundles.  





