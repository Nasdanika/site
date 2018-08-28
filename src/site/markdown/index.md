# Nasdanika


## Principles

* Effective knowledge elicitation, retention, and dissemination:
    * Capturing of knowledge in documented models.
    * Web-based documentation system serving models documentation and visualizations. 
* Working at a high level of abstraction by leveraging [model-driven development](articles/mdd.html).
* Elimination of repetitive tasks through code generation and metadata-driven logic.

## Target audience

A full stack [T-shaped](https://en.wikipedia.org/wiki/T-shaped_skills) Java developer, an innovator, leveraging visual and declarative techniques provided by Eclipse and Nasdanika tools to collaborate with and delegate to other technologists, not necessarily developers, and technically minded business people to test ideas and build prototypes and applications together.

Visual/declarative approach to software development heightens the level of abstraction and reduces the amount of hand-coding, sometimes just to a few lines of code or no code in simple cases. 
By doing so it increases the pool of developers, the speed of application and innovation delivery, and the rate of success because people build applications for themselves and their teams and as such have a good understanding of the requirements.

## Products

### Server-side

* [HTML](../html/index.html) - Java bindings for HTML, Bootstrap, Font Awesome, KnockoutJS and AngularJS. This bundle provides a fluent API for building HTML/Bootstrap code. It allows the developer to stay in Java IDE and leverage code assist and other features of Eclipse IDE and Java language. For example, this bundle makes it easy to build "polymorphic Web UI's" where base UI is built by the foundation classes and customized as needed by sub-classes.
* [Foundation Server](../server/org.nasdanika.repository/index.html) - An [Equinox](http://www.eclipse.org/equinox/)/[OSGi](https://www.osgi.org/developer/what-is-osgi/)-based framework for domain-driven development of web applications. Server contains a number of bundles some of them are listed below.
    * [CDO](../server/org.nasdanika.cdo/index.html) - [EMF CDO Model Repositiory](https://eclipse.org/cdo/documentation/) provides transparent persistence for EMF Ecore models, i.e. all you need to persist a model is to generate CDO code from it, CDO takes care of the rest. Nasdanika CDO bundles provide several OSGi components for building CDO applications and several CDO contexts.  
        * [Security](../server/org.nasdanika.cdo.security/index.html) - provides classes and interfaces for implementing application-level security.  
        * [Web](../server/org.nasdanika.cdo.web/index.html) - CDO Web provides contexts which merge HTTP request context with CDO View or Transaction context, so requests are executed in a context of CDO view/transaction with security checks and read or write locks applied. This bundle also contains routes for dispatching HTTP requests to specific objects in the repository, i.e. repository objects can have their unique base URL and a number of sub-urls for different operations on the object.
            * [Doc](../server/org.nasdanika.cdo.web.doc/index.html) - Documentation bundle serves CDO models and OSGi components documentation including visualizations of CDO models as UML class diagrams and OSGi components wiring as component diagrams. With this bundle you can show your stakeholders how your system actually works. This bundle also serves hand-crafted documentation, [user stories models](../server/org.nasdanika.story/index.html) documentation with visualizations as use case and activity diagrams, and WebTest test results with slideshows of captured screenshots, so people can explore different flows in the system.
    * [Web](../server/org.nasdanika.web/index.html) - this bundle contains the Nasdanika HTTP handling framework, which is buit on the Servlet API and uses the concept of routes (inpspired by [ExpressJS](https://expressjs.com/). There are three types of routes - root routes, object routes matching object class and executed in the context of an object, and EObject routes matching EClass name and namespace URI and executed in the context of EObject and, typically, CDOView or CDOTransaction. 

### Code generation

* [Config](../config/index.html) - provides a model and an editor for creating hierarchical configurations.
* [Codegen](../codegen/index.html) - Code generation Ecore/CDO model and editor. The model provides classes which can generate Eclipse project, file, Java compilation unit (with merging of generated code with existing), etc.  
* [Codegen Ecore](../codegen-ecore/index.html) - Code generation from EMF Ecore models. The Nasdanika Ecore code generation editor allows to select generation targets and then select model elements for which the code should be generated. E.g. you may have a model with dozens of classes and hundreds of features and operations, but generate Web UI classes just for a couple of classes and a dozen of features. 
* [Codegen Ecore Web UI](../codegen-ecore-web-ui/index.html) - Generators and templates for generating rendereres, routes,  and resource bundles from selected EClasses and their features and operations.
* [Workspace Wizard](../workspace-wizard/index.html) - Wizards to generate modeling project workspace and NFS-based application workspace. These wizards generate Maven/Tycho projects to produce an Eclipse product and P2 repository for the application.

### Knowledge management

* [Help](../help/index.html) provides:
    * The primary toc for other Nasdanika help toc's to link to.
    * Markdown content producer which converts intercepts *.md.html help resource requests, finds corresponding *.md files and converts them to HTML on the fly.
    * Markdown processor extensions.
* [Docgen](../docgen/index.html) - Documentation generation framework.
* [Docgen Ecore](../docgen-ecore/index.html) - Documentation generator for Ecore models - static HTML and Eclipse help.

### Eclipse UI

* [Presentation](../presentation/index.html) - features classes and extension points related to the Eclipse UI presentation such as SWT, JFace, and EMF editors.

### UX

* [Story](../story/index.html) - User story model and editor. User story models can be used for capturing descriptions of software features from an end-user perspective. Results of automated tests executed by WebTest can be linked to user stories scenarios documentation by the CDO Web Doc bundle. 
* [WebTest](../webtest/index.html) - Web/mobile UI testing framework built on [JUnit](http://junit.org/junit4/) and [Selenium WebDriver](http://www.seleniumhq.org/projects/webdriver/). Nasdanika WebTest encourages abstraction of tests from the low-level UI manipulation logic using the "Application UI Driver" which contains Actors and Pages. WebTest records test execution flow in a model and captures screenshots during execution. The model can then be served by the [org.nasdanika.cdo.web.doc](../server/org.nasdanika.cdo.web.doc/index.html) bundle. WebTest supports "sketched" execution where you may not have a UI yet, only sketches, and can already write the UI driver and tests and run them. See [Tests with sketches](https://server-side-java-development-for-innovators.books.nasdanika.org/chapter-2-automated-ui-tests/tests/sketches/) chapter in the "Server-side Java Development for Innovators" book (see below).
* [WebTest Model](../webtest-model/index.html) - Ecore/CDO model for storing results of Web UI tests.


### Dependencies

* [Maven OSGi](https://github.com/Nasdanika/maven-osgi) - Maven dependencies wrapped into OSGi bundles with [Reficio p2 maven plugin](https://github.com/reficio/p2-maven-plugin).
* [Third-party](../third-party/index.html) - Third party dependencies which cannot be added with the Maven OSGi product. 

## Eclipse packages

* [Nasdanika Tool Suite](../tools/index.html) - An extension of the [Eclipse Modeling Tools](https://www.eclipse.org/downloads/packages/eclipse-modeling-tools/photon) package with additional features and plugins.

## Composite repository

``https://www.nasdanika.org/products/site/repository``

## Documentation

* [Model-Driven Development](articles/mdd.html).
* [Server-side Java Development for Innovators](https://server-side-java-development-for-innovators.books.nasdanika.org/).

