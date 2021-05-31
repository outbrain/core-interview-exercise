# Consul Lab Exercise
Please read the following instructions before starting to implement your exercise, you don't want to miss any important instruction.

### Creating your repository 

Please mirror this git repo using the instructions [here](https://help.github.com/articles/duplicating-a-repository). Then clone it locally. 
(**Please DO NOT fork the repo**)

### Submitting your solution
The solutin should be delivered in a new branch in **YOUR DUPLICATED REPO**.

In Outbrain's cloud platform group we embraced automation as one of our values.
To be able to test our automation and changes before they are applyed in production, we use [Vagrant](https://www.vagrantup.com/intro/index.html) & [VirtualBox](https://www.virtualbox.org/) as our local virtual environment installed on our laptops.

We use [Consul](https://www.consul.io/docs/index.html) as our service discovery platform. All of our services rely on Consul to communicate with one another, so each change must be tested and reviewed on a test environment that mimics production, before deploying the change.
Your assignment is to build such a test environment.

### Environment components:
2 small VMs (1 vCPU, 1G memory):
 - 1 VM installed with Consul server (Ubuntu)
 - 1 VM installed with Apache server + Consul agent (Ubuntu)

### Environment requirements:
 - The VMs should be able to communicate with one another.
 - Consul should run as a service.
 - Consul service UI should be accessible from your laptop's browser.
 - Apache should listen on port 8080 and serve a test page.
 - Both Consul agents (the one on the Apache server and the one on the Consul server) should appear in the output of 'consul members' command.
 - Both Consul agents should be registered to the same datacenter/cluster.
 - Create and register a Consul service in the Apache VM that has a specific health check configured (there are few ways to register a service in consul, register using flat file).

### Environment Validation:
 - `consul members` command outputs both Consul agents.
 - You are able to curl Consul on localhost to get the list of services registered on the local machine.
 - Stopping Apache changes the status of the service registered on the Apache VM (Verify using UI & API).

### Assignment submission:
The exercise should be delivered as a GitHub repository in your private account, containing a Vagrantfile and all necessary files required to build the environment.
To test your assignment, we should be able to simply run 'vagrant up' and the environment will be deployed as stated above.
