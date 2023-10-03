# Consul-API Exercise
**Please read the following instructions before starting to implement your exercise, you don't want to miss any important instruction.**

### Creating your repository 

Please mirror this git repo using the instructions [here](https://help.github.com/articles/duplicating-a-repository). Then clone it locally. 
(**Please DO NOT fork the repo**)

### Exercise
This exercise includes two main parts:
1. Building a [Consul](https://www.consul.io) server and exposing Consul API
2. Building an API service that exposes some endpoints

### Submitting your solution
You may use one of the following coding languages: Python/Ruby.

The exercise should be delivered as a GitHub repository in your private account, containing:
1. Directory with all the modules of your service (providing a clear directory tree is an advantage).
2. Dockerfile that runs the web framework and copies the code to the container.
3. Vagrantfile that spawns the Consul server.
4. Basic instructions on how to use the Dockerfile and Vagrantfile, and examples for querying the service.

Requirements:
1. The API service that you build should be started by the Dockerfile and should print all logs/output to the container's shell.
2. Use [Vagrant](https://www.vagrantup.com/intro/index.html) & [VirtualBox](https://www.virtualbox.org/) to build your Virtual Machine.
3. `vagrant up` command should also start the Consul agent (it's ok if Consul will not run as a service).
4. Consul UI should be accessible from your laptop's browser.
5. As a sanity check for you Consul environment, make sure that the Consul cluster is functioning well with a known leader.

Nice to have:
1. Pay attention to your code structure and organization in classes, functions and modules. Naming convention will also be taken into consideration.
2. We will be looking at your commit history. A meaningful and instructive commit history is an advantage.
3. Register a Consul service on the VM (using a flat file). If you choose to deploy one, make sure you are able to change its state (critical, healthy, warning).
4. Wrap and run Consul as a service.

### Environment Requirements
- 1 small VM (1 vCPU, 1G memory) running Ubuntu, has Consul server installed.
- A functioning Consul cluster with known leader.
- A Docker container that runs the API application, independently outside the VM. 

### Exercise
1. Create the Consul server VM with proper configuration file.
   The server's API should be accessible from your laptop to move on to the next step.

2. Write a small API service that will expose the following routes:

~~~
GET  /v1/api/consulCluster/status
GET  /v1/api/consulCluster/summary
GET  /v1/api/consulCluster/members
GET  /v1/api/consulCluster/systemInfo
~~~

#### status
This endpoint will sample the Consul server API to see if it is available or not, and will return the result in the following format:
`{"status": 0|1, "message": "<message>"}`

Where:
* Status 0 means down and 1 means up
* Message should indicate when the sampling was successfull or give a relevant error message in case it is down

Bonus:
* If the server is down, include the reason in the message

##### Response example

~~~
{"status": "1", "message": "Consul server is running"}
~~~

#### summary
This endpoint will sample the Consul API to get the following information about the cluster:
 - Number of registered nodes
 - Number of registered services
 - Cluster Leader IP and port
 - The internal protocol version used by Consul

~~~
{
   "registered_nodes": <>,
   "registered_services": <>,
   "leader": <ip:port>,
   "cluster_protocol": <>
 }
~~~

##### Response example

~~~
{
   "registered_nodes": 5,
   "registered_services": 9,
   "leader": "1.2.3.4:8300",
   "cluster_protocol": 3
 }
~~~

#### members
This endpoint will sample the Consul API to get the list of registered nodes in the culster in the following format:

`{"registered_nodes": []}`

##### Response example

~~~
{
  "registered_nodes": [
    "vag1.dc.com",
    "vag2.dc.com"
  ]
}
~~~

#### systemInfo
This endpoint will expose metrics taken from the docker container. Here we wish to see which system metrics you think are relevant when it comes to debugging OS.
The result must include the number of cores and amount of memory that the VM has. Try to come up with at least 5 more system metrics.
Result should be in the following format: 

~~~
{"vCpus": <>, "MemoryGB": <>, <metric3>: <>}
~~~

...and so on
