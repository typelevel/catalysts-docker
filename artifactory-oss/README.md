# artifactory-oss

This image provides an Artifactory OSS server running in it's own container, but accessible
direct from the host. The server has some repositories pre-configured to run a scala community build
locally; without a local server, the build is _very_ slow.

Note that the steps involving docker usually require root access.

## Download git project


```bash
git clone https://github.com/typelevel/catalysts-docker.git
cd catalysts-docker
```

## Build image


To build an image run:

`docker build -t artifactory-oss artifactory-oss`

## Run image in new container:

```bash
docker run -d --name artifactory-oss -p 8081:8081 artifactory-oss:latest
```

To view in browser

`localhost:8081/artifactory`

This can be stopped and subsequently restarted with:

```bash
docker stop artifactory-oss
docker start artifactory-oss 
```

## Run community build

Download the community build from https://github.com/scala/community-builds and `cd` to the root 
directory.

__TODO__: new cbuild.sh will change this so that one can simply run:

```
./cbuild.sh -v 2.12 -r resolvers/resolvers-catalysts-docker.conf 
```

but for now, in order for the server and the configured repositories,
EITHER

Change `~/.sbt/repositories` (or create) for the community build

```
[repositories]
  local
  CB-maven: http://localhost:8081/artifactory/CB-maven
  typesafe-ivy-releases: http://localhost:8081/artifactory/typesafe-ivy-releases/, [organisation]/[module]/[revision]/[type]s/[artifact](-[classifier]).[ext], bootOnly
  CB-sbt: http://localhost:8081/artifactory/CB-sbt/, [organization]/[module]/(scala_[scalaVersion]/)(sbt_[sbtVersion]/)[revision]/[type]s/[artifact](-[classifier]).[ext]
```

OR

modify `resolvers.conf` locally to;

```
options.resolvers: {
  01: "local"

  02: "CB-maven: http://localhost:8081/artifactory/CB-maven"
  03: "typesafe-ivy-releases: http://localhost:8081/artifactory/typesafe-ivy-releases/, [organisation]/[module]/[revision]/[type]s/[artifact](-[classifier]).[ext], bootOnly"
  04: "CB-sbt: http://localhost:8081/artifactory/CB-sbt/, [organization]/[module]/(scala_[scalaVersion]/)(sbt_[sbtVersion]/)[revision]/[type]s/[artifact](-[classifier]).[ext]"
}
```
# See

- Based on examples from https://github.com/JFrogDev/artifactory-docker-builder/tree/master/examples


