## clj-docker-client [![Build Status](https://travis-ci.org/lispyclouds/clj-docker-client.svg?branch=master)](https://travis-ci.org/lispyclouds/clj-docker-client)

[![License: GPL v3](https://img.shields.io/badge/license-GPL%20v3-blue.svg?style=flat-square)](http://www.gnu.org/licenses/gpl-3.0)
[![Clojars Project](https://img.shields.io/clojars/v/lispyclouds/clj-docker-client.svg?style=flat-square)](https://clojars.org/lispyclouds/clj-docker-client)

An idiomatic Clojure Docker client based on the excellent JVM [client](https://github.com/spotify/docker-client) by Spotify.

### Why not use the Spotify lib directly?
The Spotify lib though being excellent, has Java style varag method calls,
non-standard variable passing and undocumented behaviour. This eases out these 
things and to make an idiomatic, clojure friendly API to Docker.   

This is a work in progress and aims to be fully compliant and up to date with the Docker API changes. 

### Installation
Leiningen/Boot
```clojure
[lispyclouds/clj-docker-client "0.1.4"]
```

Clojure CLI/deps.edn
```clojure
{lispyclouds/clj-docker-client {:mvn/version "0.1.4"}}
```

Gradle
```groovy
compile 'lispyclouds:clj-docker-client:0.1.4'
```

Maven
```xml
<dependency>
  <groupId>lispyclouds</groupId>
  <artifactId>clj-docker-client</artifactId>
  <version>0.1.4</version>
</dependency>
```

### Requirements
- Clojure 1.9+
- JDK 1.8+

### Usage

```clojure
(require '[clj-docker-client.core :as docker])
```

#### Creating a connection to the Local Docker daemon
```clojure
(def conn (docker/connect))
```

#### Ping the Docker server
```clojure
(docker/ping conn)
```

### Image Handling

#### Pulling the `busybox:musl` image
```clojure
(docker/pull conn "busybox:musl")
```

#### Building an image from a Dockerfile
```clojure
(docker/build conn "full path to directory containing a Dockerfile")
```

#### Pushing an image
```clojure
(docker/push conn "image id or <repo>:<tag>")
```

#### Removing an image
```clojure
(docker/image-rm conn "image id or <repo>:<tag>")
```

#### Listing all available images
```clojure
(docker/image-ls conn)
```

### Container Handling

#### Creating a container with the `busybox:musl` image, a command and a env var
```clojure
(docker/create conn "busybox:musl" "echo hello" {:env "testing"})
```

#### Listing all available containers
```clojure
(docker/ps conn) ; Only running containers
(docker/ps conn true) ; All containers
```

#### Starting a container
```clojure
(docker/start conn "name or id")
```

#### Stopping a container
```clojure
(docker/stop conn "name or id")
```

#### Killing a container
```clojure
(docker/kill conn "name or id")
```

#### Removing a container
```clojure
(docker/rm conn "id or name") ; Remove non-running container
(docker/rm conn "id or name" true) ; Force remove non-running container
```
