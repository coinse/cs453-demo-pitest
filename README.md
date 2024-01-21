## PITest Hands-on

In this hands-on, we will try applying PITest, a lightweight Java mutation tool, to one of Apache's open source project via the Maven build tool. 

### PITest

[PITest](https://github.com/hcoles/pitest) is a Java mutation tool developed by Henry Coles. What distinguishes PITest from other mutation tools is the fact that it was developed by a practicing software engineer with the aim of actually applying mutation testing to real world projects. As such, PITest maintains a relativly simple set of mutation operators, for the sake of efficiency. On the other hand, it comes with plug-in supports with build tools (such as [Maven](https://maven.apache.org)) as well as an excellent report feature.

### Instructions

1. You should have Jave8+ runtime environment.
2. We will use the [Apache Maven](https://maven.apache.org/install.html) build tool. Install the current version.
3. We will use [Apache Commons Lang3](https://commons.apache.org/proper/commons-lang/) as our target system. Download the current version, and unzip the compressed source files.
4. Inside the lang3 directory, you will find the Maven build congifuration file, named `pom.xml`. Open it.
5. Find `<plugins>` tag in `pom.xml`. Add the following plugin entry inside the `<plugins>`:
```
<plugin>
  <groupId>org.pitest</groupId>
  <artifactId>pitest-maven</artifactId>
  <version>1.12.0</version>
  <dependencies>
    <dependency>
      <groupId>org.pitest</groupId>
      <artifactId>pitest-junit5-plugin</artifactId>
      <version>1.1.1</version>
    </dependency>
  </dependencies>
  <configuration>
    <targetClasses>
      <param>org.apache.commons.lang3.compare.*</param>
    </targetClasses>
    <targetTests>
      <param>org.apache.commons.lang3.compare.*</param>
    </targetTests>
  </configuration>
</plugin>
```
6. Now, execute Maven using the following:
```
$ mvn test-compile org.pitest:pitest-maven:mutationCoverage
```
7. You can check the result by looking at `target/pit-reports`.