# docker-catalysts

To build

`docker build -t artifactory-oss artifactory-oss`

To run:

`docker run -d --name artifactory-oss -p 8081:8081 artifactory:latest`

To view in browser

`localhost:8081/artifactory`

Changes to `~/.sbt/repositories` for the community build

```
[repositories]
  local
  CB-maven: http://localhost:8081/artifactory/CB-maven
  typesafe-ivy-releases: http://localhost:8081/artifactory/typesafe-ivy-releases/, [organisation]/[module]/[revision]/[type]s/[artifact](-[classifier]).[ext], bootOnly
  CB-sbt: http://localhost:8081/artifactory/CB-sbt/, [organization]/[module]/(scala_[scalaVersion]/)(sbt_[sbtVersion]/)[revision]/[type]s/[artifact](-[classifier]).[ext]
```

# See

- Based on examples from https://github.com/JFrogDev/artifactory-docker-builder/tree/master/examples
- https://gitter.im/InTheNow/catalysts

