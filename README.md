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
