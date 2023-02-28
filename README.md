# maven-troubleshooting-MNG-7705

## Setup
Run a local copy of nexus
`podman run -d -p 8081:8081 --name nexus docker.io/sonatype/nexus3`

Update your settings file to just be the local host. An example has been supplied.
http://localhost:8081/repository/maven-public/

Populate local nexus with a command like
`mvn -V -f main/pom.xml -s settings.xml dependency:sources  dependency:resolve -Dclassifier=javadoc`
`mvn -V -f branch4/pom.xml -s settings.xml dependency:sources  dependency:resolve -Dclassifier=javadoc`
`mvn -V -f branch5/pom.xml -s settings.xml dependency:sources  dependency:resolve -Dclassifier=javadoc`

Optionally: download the maven version you want like this
`mvn -s settings.xml dependency:unpack -Dartifact=org.apache.maven:apache-maven:3.9.0:zip:bin -DoutputDirectory=.`
If you do this, when the following maven commands would be along the lines of
`./apache-maven-3.9.0/bin/mvn ...`

## To reproduce the issue

Delete your local maven repo
`rm -rf ~/.m2/repository`

In different windows, run the following commands.

TODO
