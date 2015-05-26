# Nashorn Scripting API Fragment
If you're running AEM 6.0 SP2 with Java 8, you might want to use the new Nashorn JavaScript engine to do cool server-side JS stuff. Unfortunately, you can't -- even though the nashorn.jar is on the system classpath, it is not available to the bundles inside the OSGi container.

This project fixes that.

## Requirements
* AEM 6.0 with service pack 2 (see [Adobe docs](http://docs.adobe.com/docs/en/aem/6-0/release-notes-sp2.html#Include%20the%20service%20pack%20with%20initial%20installation) for installation instructions)
* Java 8 (the version used to build this project doesn't matter, but AEM needs to be running with JRE/JDK 8)

## Build + Deploy

Use Maven to build this project.

To build and deploy to a running instance, run `mvn clean install -P autoInstall` from the project root. By default the host and port are assumed to be `localhost:4502` with user:password as `admin:admin`. These can be changed by appending `-Dcrx.(host|port|user|password)=<correct-value>` as appropriate (e.g. `-Dcrx.port=4503`).

## How does it work?

The build artifact from this project is an OSGi [bundle fragment](http://wiki.osgi.org/wiki/Fragment) which attaches to the system bundle and modifies its `Export-Package` directive to include the Nashorn scripting package.

## Now What?

Installing this fragment only exposes the [Nashorn scripting package](https://docs.oracle.com/javase/8/docs/jdk/api/nashorn/jdk/nashorn/api/scripting/package-summary.html) to the other bundles in your OSGi environment (note that this is *NOT* the same as registering a Sling scripting engine). It is up to you to [write code that uses it](https://docs.oracle.com/javase/8/docs/technotes/guides/scripting/nashorn/intro.html#sthref14).
