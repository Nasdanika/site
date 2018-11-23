# Stored functions and proxies

The idea of stored functions is to provide a model/api for functional programming where functions can be configured combined using ``bind()`` method. 
It was inspired by JavaScript functions.

Core concepts:
- A function is something which can be invoked with an array of arguments (an associative array/map is one of options) and either returns value or throws an exception.
- Functions have arity - the number of arguments they accept.
- Functions have ``bind()`` method which allows to bind of some of its parameters to other functions or values. It results in a function with a different arity.
- EMF/OSGi implementation allows to store functions in models using [EMF boxing](emf-boxing.html) and bind function arguments to any boxed values - constants, objects - Maven and bundle, object methods as functions, other functions, OSGi services, context properties and services.

Stored functions were prototyped in different *function* bundles of [Nasdanika Foundation Server](https://github.com/Nasdanika/server/tree/before-cleanup).

Example:

```
Function a = ...; // function with arity 4 - a(w,x,y,z)
Function b = ...; // function with arity 3 - b(x,y,z)
Function c = a.bind(2, b.bind(5));
```

In the above example c has arity 3 - 2 remaining parameters for a and one remaining parameter for b. a is invoked with the result of computation of b.
Function API shall provide bind() flavors which allow to bind parameters in any order and reuse the same argument in several places. 

Bound function (b) definition may be contained in the a definition model or referenced in several ways:
- Model reference.
- URL of function definition resource.
- Bundle/jar name and version to (dynamically) load function resource from and then resource path in bunlde/jar.
- Some kind of a function registry - functions are registered by a logical name and then their "physical" location is resolved at load time.

Functions may also be stored in a CDO repository.

## Function authoring and viewing

Similar to boxed object authoring - model editor and/or web UI. 
In addition to this composite functions may be modeled with a diagram editor, e.g. an editor created with [Eclipse Sirius](https://www.eclipse.org/sirius/). 
While a function is essentially a boxed object diagram-based editing is more natural for functions and tree style editing is more natural for boxed object. 

Both editing styles may be used at the same time:
- Diagrams for binding composite function arguments and context properties to contained functions arguments.
- Trees for building value arguments.      

### Tree mapping

One frequent task in enterprise integration is mapping between complex data structures. 
At development time simple mappings may be done with [Eclipse Nebula Tree Mapper](https://www.eclipse.org/nebula/widgets/treemapper/treemapper.php) or a similar control.
More complex may use a tree editor similar to [Codegen Ecore Web UI editor](https://github.com/nasdanika/codegen-ecore-web-ui) where target tree nodes may be either selected for population or not. 
For selected nodes a value function/expression would be defined on the right by selecting inputs participating in the value building in the checkbox tree of inputs
and then constructing a value expression/function from those inputs. A function/expression may be constructed using different languages supported by the JVM - Java itself, JavaScript, JxPath, ...

At build time the mapping definition will be converted to a composite function. 
Some of such functions may be suitable for a high level of parallelization. E.g. if a data structure is computed by taking inputs from several back-end systems calls to those systems may be performed at the same time.   

## Execution

Execution of stored functions can be easily parallelized and distributed. Parallelization is achieved by using fork-join style of function argument computation. 
E.g. if a function takes several arguments values of those arguments may be computed/loaded in parallel. It some of those arguments are collections then collection
elements also can be computed/loaded in parallel.

Computation distribution is achieved by using fork-join executor which uses a thread pool first and then falls-back to distributed invocation by, for example, making a REST call to a load balancer or sending a message to a work queue. The invocation would contain a unique function identifier and arguments. 
When such an invocation is received the processing node would load function definition, invoke it and return result. 
A distributed call may further break down the function it received and distribute processing. 

## Proxies

Several functions may be bundled together and invoked via a dynamic proxy. Stored proxy would be similar to an object box - specify how to load the proxy class
and also contain an EMap<String,Function>. Functions can be contained or referenced. 

## Summary 

Use of stored functions would allow implementation of parallel and distributed computing in terms familiar to Java developers.
Local execution can be performed sequentially for troubleshooting purposes. 
Java developers would not need to think about how execution shall be parallelized/distributed - it will be done automatically.

With objects passed between functions being EMF boxable executions can be recorded and then analyzed by browsing in a Web UI or an IDE editor - diagram or tree.   
