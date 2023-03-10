# Kubernetes Perfdash

Kubernetes Perfdash (performance dashboard) is a web UI that collects and displays
performance metrics. Performance metrics are created based on performance test
results for different nodes numbers, platform types and platform versions.

Perfdash is available at http://perf-dash.k8s.io/

## Supported metrics

* Responsiveness
* Resources
* PodStartup
* TestPhaseTimer
* RequestCount
* RequestCountByClient

Metrics above are available for all kinds of tests divided into load and density subtypes.

## Application server

Application server runs as a deployment on kubernetes cluster. It is hosted on
*mungegithub* cluster in *k8s-mungegithub* project.

## How to deploy new version of perf-dash.k8s.io

* Increment TAG in the `Makefile` (for example: 2.10 -> 2.11)
* Modify the perfdash image version in the `deployment.yaml` to be the same as the
  one specified in the `Makefile`
* Submit a PR, get required approvals and wait until it's merged
* Run `make push` to push new image to container registry
* Refer to [perf-dash.k8s.io/README.md](https://github.com/kubernetes/k8s.io/blob/main/perf-dash.k8s.io/README.md) for the deploy instructions
  
  Note: Since 2020-04-21, perf-dash.k8s.io is hosted in the public **aaa** (sic!) cluster. 
  Instructions on connecting to **aaa** cluster can be found [here](https://github.com/kubernetes/k8s.io/blob/main/running-in-community-clusters.md#access-the-cluster). 

## Application images

Images are stored in *gcr.io/k8s-testimages* project container registry.


## Local development

To test your changes locally, execute `make run`. It will build the binary and
start perfdash website at <http://localhost:8080>. Note that it might take a
short while for perfdash to start since it needs to fetch the job artifacts first.

You can alter startup parameters (like number of jobs for which history is fetched)
by editing the makefile.
