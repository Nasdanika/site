# Maven classloader service

The idea is to have an OSGi service which builds classloaders for a requested Maven artifact version. Its interface might look like:

```
public interface MavenClassloader {

	ClassLoader getClassloader(String groupId, String artifactId, String version, ClassLoader parent) throws ...;

}
```

Classloaders constructed in such a way would contain the requested artifact jar and all its dependencies. 
The implementation may use [Apache Artifact Resolver](https://maven.apache.org/resolver/) to download artifacts to a local repository and construct classloaders.

Because downloading may be time consuming the service may also provide asynchronous API's, e.g.:

```
CompletableFuture getClassloader(String groupId, String artifactId, String version, ClassLoader parent) throws ...;
```

Some flavors of those methods may be:

- No parent classloader attributes - the calling bundle classloader is used by default.
- ``createNew`` parameter - creates a new classloader for each call - high level of isolation at the cost of additional garbage collection.
- Take IProgressMonitor parameter to monitor download process.

 Implementation service may:
 
 - Take repository directory configuration parameter. Use bundle data directory by default.
 - Take repository|ies URL parameter.
 - Take parameters specifying security configuration/policies - which artifacts to trust - e.g. by jar signature and/or by Maven coordinates. For example trust only particular artifact groups. 
 - Have a list of artifacts and versions to pre-load on startup.
 
 One possible option for the two last bullets is there is a registry of artifacts which are allowed to be loaded by the Maven classloader service. The service takes a
URL of this registry as configuration parameter, reads the registry on startup and starts background jobs to pre-load registry artifacts - maybe not all of them, but those marked with "preload" flag. 
 
The service may also call the registry as part of getClassLoader() invocation to authorize loading of a particular artifact.   
 
The service may soft-reference cache classloaders keyed by group id, artifact id, version, and parent classloader. Parent classloader in the key may also be a soft reference. 
 
The goal of this service is to enable server-less lambda-like execution of Java code which is explained in more details in other roadmap articles.
 
One example would be - a Java developer who wants their code to be executed on a particular event, e.g. completion of some task by a user. 
The Java developer doesn't want to host their own (micro)service - too much overhead. They create a Maven artifact with a class to invoked on event and 
publish the artifact to a repository. Then they may register the artifact in the registry of allowed artifacts - there might be some approval process. 
Or, publishing the artifact to a specific repository may include approval steps, so the fact of the artifact being in the repository might be enough to trust it.
Once the artifact is made available for the Maven classloader service it may be registered for event listening by, say, a REST call which specifies Maven coordinates, class name and possibly method name to pass event to - this way the class does not have to implement a particular interface and static methods can be used.
The rest call may also specify initialization parameters. More about it in [EMF/CDO boxing](emf-boxing.html).           

## Artifact registry

The registry may be implemented and loaded in a variety of ways with some options listed below:

### Delivery

* REST endpoint to be called by loading services for authorization and repository URL lookup.
* Registry model resource loaded from URL.
* Registry resources stored in a bundle:
    * Static - registry entries are fixed at build time.
    * Dynamic - use P2 and Nasdanika provisioning or something similar to automatically download bundle updates.
    
### Authoring

* Web UI.
* IDE - text file or specialized edit plug-in.    