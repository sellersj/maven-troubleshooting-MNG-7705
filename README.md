# maven-troubleshooting-MNG-7705

## Setup
Run a local copy of nexus
`podman run -d -p 8081:8081 --name nexus docker.io/sonatype/nexus3`

Update your settings file to just be the local host. An example has been supplied.
http://localhost:8081/repository/maven-public/

Populate local nexus with a command like
```
mvn -V -s settings.xml dependency:sources  dependency:resolve -Dclassifier=javadoc -f main/pom.xml
mvn -V -s settings.xml dependency:sources  dependency:resolve -Dclassifier=javadoc -f branch4/pom.xml
mvn -V -s settings.xml dependency:sources  dependency:resolve -Dclassifier=javadoc -f branch5/pom.xml
```

Optionally: download the maven version you want like this
`mvn -s settings.xml dependency:unpack -Dartifact=org.apache.maven:apache-maven:3.9.0:zip:bin -DoutputDirectory=target`
If you do this, when the following maven commands would be along the lines of
`./target/apache-maven-3.9.0/bin/mvn ...`

## To reproduce the issue

Delete your local maven repo
`rm -rf ~/.m2/repository`

In different windows, run the following commands.

```
strace -f -tt -e trace=file ./target/apache-maven-3.9.0/bin/mvn -s settings.xml dependency:sources  dependency:resolve -Dclassifier=javadoc -f main/pom.xml
strace -f -tt -e trace=file ./target/apache-maven-3.9.0/bin/mvn -s settings.xml dependency:sources  dependency:resolve -Dclassifier=javadoc -f branch4/pom.xml
strace -f -tt -e trace=file ./target/apache-maven-3.9.0/bin/mvn -s settings.xml dependency:sources  dependency:resolve -Dclassifier=javadoc -f branch5/pom.xml
```
