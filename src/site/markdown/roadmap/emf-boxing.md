# EMF boxing

The idea of EMF boxing is that Java objects are "boxed" into an EMF model. This idea is similar to serialization with the difference that boxed/serialized model may be
created by means other than building an actual object and then serializing it into a model.

A first stub at this idea was taken in Nasdanika boxing model - https://github.com/Nasdanika/server/tree/before-cleanup/org.nasdanika.cdo.boxing

Some enhancements to the above model:
* Object boxes may leverage Maven class loading service and dynamic bundles. Object box may have two subclasses - Maven object and bundle object each with attributes to load object classes from respective maven/bundle classloaders.
* Classloader of an Object being serialized may be inspected and object box class and its attributes may be inferred. It should be relatively easy to do for classes loaded by bundles. Maven class loading service may return a subclass of URL classloader explicitly specifying maven coordinates.
* In addition to BundleContext and OSGi services boxes there may be context boxes, i.e. boxes retrieving their values from a context object provided during unboxing - e.g. a property by its name or a "service" by its class.

Different use cases:

* Boxed objects may be created via an editor or web ui.
* Boxed objects may be stored in XML resources or in a CDO repository.
* Box models may reference each other.
* They can be delivered in bundles or plain jars, including dynamic delivery with Dynamic bundles and Maven class loading service. 
* Boxed objects may be instantiated, viewed and edited in an IDE editor and/or web UI. Also an HTML report may be generated from a boxed model.
* Also boxed objects may be used for remote service invocation. Dynamic class loading from Maven and OSGi bundles makes it more powerful than other remoting approaches. E.g. some long-running service may be invoked with a callback object passed to it. 

EMF boxing is a foundation for stored functions and promises.   

       

