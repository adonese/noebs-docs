# Noebs installation

Noebs can be self hosted too as well as our usual managed solution. 


### Recommended requiremnts

Noebs and its supporting infra runs the best in *NIX platforms. While other platforms can be used, there are hard requirements for Redis. Noebs relies on redis (in-memory database) to provide extreme performance under heavy workloads. This turns out to be very beneficial and helped us a lot in our design.

#### EBS and CBOS integations

For clients how insists on self hosting noebs, EBS integation process is a must. We provide a standard VM that was tested and already in production to help our clients with EBS integrations. 

#### Infra

Below is the set of recommended set up to get noebs up and running. While noebs _can_ run on Windows servers, at least Redis must be run in a Linux instance. Databases are configurable and are up to the org to chose which DB they like. The current base installation of noebs comes with SQLite and relies heavily on Redis for user facing apis.

| noebs api server | db server | redis server* |
|--------------|----------------|-------------|
| Linux (Ubuntu 20.04) | Linux (Ubuntu 20.04) | Linux (Ubuntu 20.04) |
| 2 CPUs | 2 CPUs | 2 CPUs |
| 2 GB RAM | 4 GB RAM | 4 GB RAM |

!!! Note
    _We use Redis for performance reasons_

#### Docker 

noebs can also be deployed as a docker instance. 

##### Installation

- Download noebs source code
- cd to noebs root directory (E.g., $HOME/src/noebs)
- docker build -t noebs . # -t for giving it a name
- docker run -it -p 8080:8080 noebs:latest

Now, noebs is running under http://localhost:8080/. Consult the api for getting up and running with noebs.

!!! note
    There are requirements for running noebs under docker

    - Redis should be used in a dedicated server
    - We recommend to use a SQL server (postgres) instead of SQLite


### Important notes

???+ tldr
    - noebs runs on every platform (windows, Linux or Mac). Noebs compiles into true native machine code and can be run virtually in every platform
    - the curren setup doesn't consider load balancing, redis failover or any redunancy steps.
