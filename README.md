# Introduction
This is a for of hibernate that applies patches for the following issues into verion 3.3.1-GA:
1. [HHH-1657](https://hibernate.atlassian.net/browse/HHH-1657)
2. [HHH-3662](https://hibernate.atlassian.net/browse/HHH-3662)
3. [HHH-2166](https://hibernate.atlassian.net/browse/HHH-2166)

# Building hibernate 3.3.1 GA
* Install Maven
* Set the proxy settings in your maven settings.xml file. Check [this page](http://maven.apache.org/guides/mini/guide-proxies.html)  on how to set this up.
* Install JDK 1.5, if it isn't installed already.
* Set a property in your maven settings.xml file called JAVA_HOME_5. (NOTE: This step is needed only if your default JDK is above 1.5)
* Set these repositories in your settings.xml
...| Repository Name         | URL                                                                |
...| ----------------------- |:------------------------------------------------------------------:|
...| JBoss Public Repository | http://repository.jboss.org/nexus/content/groups/public/           |
...| JBoss Deprecated        | http://repository.jboss.org/nexus/content/repositories/deprecated/ |
...| JBoss Releases          | http://repository.jboss.org/nexus/content/repositories/releases/   |
