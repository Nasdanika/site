# Dynamic bundles

The concept of dynamic bundles is nothing new - use OGSi load bundle (low level) or P2 to dynamically load bundles into OSGi runtime. 
It can be used similarly to the [Maven classloader service](maven-classloader-service.html) - to dynamically load bundles and execute some code once the bundles are loaded. 

Instead of Maven coordinates this service would take installable unit ID and version. The service will use the artifact registry to authorize load and lookup repository URL to load from. 

Instead of returning a classloader it would simply return or complete the future - loaded bundles will be accessible through the bundle context.  

https://github.com/Nasdanika/server/tree/master/org.nasdanika.provisioning can be used as a starting point for implementation.

Dynamic bundles approach is more powerful than Maven class loading. However, it requires developers to be familiar with OSGi bundles development, and this skill is harder to come by than Maven. 

Both approaches may be used at the same time. In particular, dynamic bundles may be used for loading [EMF boxed objects](emf-boxing.html) including [stored functions and proxies](stored-functions-and-proxies).