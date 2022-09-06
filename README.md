[![hudeyfa](https://circleci.com/gh/hudeyfa/operationalizing-ml-microservice-api.svg?style=svg)](https://app.circleci.com/pipelines/github/hudeyfa/operationalizing-ml-microservice-api)

## Project Overview

In this project, I worked on operationalizing a Machine Learning Microservice API.  

I was given a pre-trained, sklearn model that has been trained to predict housing prices in Boston according to several features, such as average rooms in a home and data about highway access, teacher-to-pupil ratios, and so on. You can read more about the data, which was initially taken from Kaggle, on [the data source site](https://www.kaggle.com/c/boston-housing). This project tests one’s ability to operationalize a Python flask app—in a provided file, app.py—that serves out predictions (inference) about housing prices through API calls. This project could be extended to any pre-trained machine learning model, such as those for image recognition and data labeling.

### Project Tasks

The project goal is to operationalize this working, machine learning microservice using [Kubernetes](https://kubernetes.io/), which is an open-source system for automating the management of containerized applications. In this project you will:
* Test your project code using linting
* Complete a Dockerfile to containerize this application
* Deploy your containerized application using Docker and make a prediction
* Improve the log statements in the source code for this application
* Configure Kubernetes and create a Kubernetes cluster
* Deploy a container using Kubernetes and make a prediction
* Upload a complete Github repo with CircleCI to indicate that your code has been tested

You can find a detailed [project rubric, here](https://review.udacity.com/#!/rubrics/2576/view).

**The final implementation of the project will showcase your abilities to operationalize production microservices.**

---

## Setup the Environment

1. Create a virtual environment and activate it
```python
python3 -m venv ~/.devops
source ~/.devops/bin/activate
```
2. Run `make install` to install the necessary dependencies
3. Install Hadolint for linting Dockerfile
```shell
sudo  wget -O /bin/hadolint https://github.com/hadolint/hadolint/releases/download/v1.16.3/hadolint-Linux-x86_64
sudo chmod +x /bin/hadolint
```
4. Type `make lint` to run lint checks on the project code.   
All requirements should be satisfied, and you should see a printed statement that rates your code
```shell
------------------------------------
Your code has been rated at 10.00/10
```
5. Install and configure Docker
6. Install and configure Kubernete Cluster, Minikube.
> To run a Kubernetes cluster locally, for testing and project purposes, you need the Kubernetes package, Minikube. Thorough installation instructions can be found [here](https://minikube.sigs.k8s.io/docs/start/).

### Project Files

- **.circleci**: Contains CircleCI configuration file.
- **model_data**: Machine learning model related data
- **output_txt_files**: Files that contain application’s log output
- **app.py**: The main application file.
- **requirements.txt**: Contains a list of project’s dependencies.
- **Makefile**: Includes commands for installing dependencies, testing and linting project source code.
- **Dockerfile**: Contains instructions that Docker uses to build and assemble a container image.
- **run_docker.sh**: Builds and runs a given docker image.
- **upload_docker.sh**: Deploys an image to docker hub.
- **run_kubernetes.sh**: Runs the app in Kubernetes cluster.
- **make_prediction.sh**: Sends some input data to the containerized app. Used to test the app locally.

### Running the Application

#### Three modes:

1. Standalone:  `python app.py`
2. Run in Docker:  `./run_docker.sh`
3. Run in Kubernetes:  
In order to run in Kubernetes, first upload the built image to docker hub. This will make it accessible to a Kubernets cluster
   - First run `./upload_docker.sh` to upload the docker image
   - Then run `./run_kubernetes.sh` to run the uploaded docker image in Kubernetes

### Making Predictions
To make a prediction, you have to keep the application running and perform the following steps:
1. Open a separate tab or terminal window.
2. In this new window, navigate to the main project directory.
3. Execute `./make_prediction.sh`  
This shell script is responsible for sending some input data to your containerized application via the appropriate port.  
In the prediction window, you should see the value of the prediction:
```JSON
 {
  "prediction": [
    20.35373177134412
  ]
}
 ```

### Reference
- [Dockerfile best practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
- [Minikube tutorial](https://kubernetes.io/docs/tutorials/hello-minikube/)
- [Kubernetes](https://kubernetes.io/)
- [Hadolint](https://github.com/hadolint/hadolint/)
