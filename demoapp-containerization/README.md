# Demoapp Containerization

How to containerize RobotFramework [demoapp](https://bitbucket.org/robotframework/webdemo) in 5 minutes.

**Requirements:**
* For local run: [Python](https://www.python.org/)
* For containerization: [docker-toolbox](https://www.docker.com/products/docker-toolbox)

**Docker Machine Commands:**
Creating a machine (called slave):  
* Without registry: `docker-machine create -d virtualbox slave`
* With registry: `docker-machine create -d virtualbox --engine-insecure-registry $REGISTRY slave`  
* Activate the machine: `eval $(docker-machine env slave)`  
* Deleting the machine: `docker-machine rm -f slave`

**Launch Commands:**
* Run the demoapp directly (without container): `python demoapp/server.py`
* Build into Docker image: `docker build -t demoappimage .`
* Run container: `docker run --name demoappcontainer -d -p 7272:7272 demoappimage`

**Accessing the application:**
When using docker-machine:  
* Get the ip: `docker-machine ip slave`  
* Access with browser: `<ip>:7272`  
When not using docker machine:  
* Access with browser: `localhost:7272`

**Pushing to registry:**  
* Login: `docker login $REGISTRY`  
* Tag the image: `docker tag demoappimage:latest $REGISTRY/<yourname>/demoappimage:latest`  
* Push image to registry: `docker push $REGISTRY/<yourname>/demoappimage:latest`

**Cleanup Commands:**
* Stop the container: `docker stop demoappcontainer`
* Remove the container: `docker rm demoappcontainer`
* Remove the image: `docker rmi demoappimage`
