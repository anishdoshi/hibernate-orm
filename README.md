# Introduction
This is a for of hibernate that applies patches for the following issues into verion 3.3.1-GA:

1. [HHH-1657](https://hibernate.atlassian.net/browse/HHH-1657)
2. [HHH-3662](https://hibernate.atlassian.net/browse/HHH-3662)
3. [HHH-2166](https://hibernate.atlassian.net/browse/HHH-2166)

# Building hibernate 3.3.1 GA
* Install [Maven](http://maven.apache.org/download.cgi).
* Set the proxy settings in your maven settings.xml file. Check [this page](http://maven.apache.org/guides/mini/guide-proxies.html)  on how to set this up.
* Install JDK 1.5, if it isn't installed already.
* Set a property in your maven settings.xml file called JAVA_HOME_5. (NOTE: This step is needed only if your default JDK is above 1.5)
* Make sure that "javac" is in the classpath.
* Set these repositories in your settings.xml

| Repository Name         | URL                                                                |
| ----------------------- |:------------------------------------------------------------------:|
| JBoss Public Repository | http://repository.jboss.org/nexus/content/groups/public/           |
| JBoss Deprecated        | http://repository.jboss.org/nexus/content/repositories/deprecated/ |
| JBoss Releases          | http://repository.jboss.org/nexus/content/repositories/releases/   |
* An example of the maven settings file:

```xml
<settings>
  <proxies>
   <proxy>
      <active>true</active>
      <protocol>http</protocol>
      <host>@PROXY_ADDRESS@</host>
      <port>@PROXY_PORT@</port>
      <!--username>proxyuser</username>
      <password>somepassword</password>
      <nonProxyHosts>www.google.com|*.somewhere.com</nonProxyHosts-->
    </proxy>
  </proxies>
  <profiles>
    <profile>
      <id>compiler</id>
      <properties>
        <JAVA_HOME_5>C:\Program Files\Java\jdk1.5.0_22</JAVA_HOME_5>
      </properties>
    </profile>
	<profile>  
      <id>repos</id>  
      <!-- Here we define the JBoss release and snapshot repos -->  
      <repositories>  
        <repository>  
          <id>jboss</id>  
          <url>http://repository.jboss.org/nexus/content/groups/public/</url>  
          <releases>  
            <enabled>true</enabled>  
            <updatePolicy>never</updatePolicy>  
          </releases>  
          <snapshots>  
            <enabled>true</enabled>  
            <updatePolicy>never</updatePolicy>  
          </snapshots>  
        </repository>
      </repositories>  
      <!-- Here we define the JBoss release and snapshot repos *for plugins* -->  
      <pluginRepositories>  
        <pluginRepository>  
          <id>jboss-plugins</id>  
          <url>http://repository.jboss.org/nexus/content/groups/public/</url>  
          <releases>  
            <enabled>true</enabled>  
            <updatePolicy>never</updatePolicy>  
          </releases>  
          <snapshots>  
            <enabled>true</enabled>  
            <updatePolicy>never</updatePolicy>  
          </snapshots>  
        </pluginRepository>  
      </pluginRepositories>  
    </profile>
    <profile>  
      <id>jboss-deprecated</id>  
      <repositories>  
        <repository>  
          <id>jboss-deprecated</id>  
          <name>JBoss Deprecated</name>  
          <url>http://repository.jboss.org/nexus/content/repositories/deprecated/</url>  
          <layout>default</layout>  
          <releases>  
            <enabled>true</enabled>  
            <updatePolicy>never</updatePolicy>  
          </releases>  
          <snapshots>  
            <enabled>false</enabled>  
          </snapshots>  
        </repository>  
      </repositories>  
    </profile>
    <profile>  
      <id>jboss-releases</id>  
      <repositories>  
        <repository>  
          <id>jboss-releases</id>  
          <name>JBoss Releases</name>  
          <url>http://repository.jboss.org/nexus/content/repositories/releases/</url>  
          <layout>default</layout>  
          <releases>  
            <enabled>true</enabled>  
            <updatePolicy>never</updatePolicy>  
          </releases>  
          <snapshots>  
            <enabled>true</enabled>  
          </snapshots>  
        </repository>  
      </repositories>  
    </profile>
  </profiles>
  <activeProfiles>
    <activeProfile>compiler</activeProfile>
    <activeProfile>repos</activeProfile>
    <activeProfile>jboss-deprecated</activeProfile>
    <activeProfile>jboss-releases</activeProfile>
  </activeProfiles>
</settings>

```
* Checkout 3.3.1-GA using the following git commands:

          git checkout 84af2a9
          git branch <branch_name>

* Run the following command:

          mvn clean package -DdisableDistribution=true

* You will get an error regarding "jbosscache-core" dependency not being able to load. For this, edit the file *<user.dir>/.m2/repository/org/jboss/cache/jbosscache-core/2.1.1.GA/jbosscache-core-2.1.1.GA.pom* file and change the version of "jbosscache-common-parent" to "1.3".
* Run the following command again:

          mvn clean package -DdisableDistribution=true

* The artifacts should be created inside the project folders
