## Load Balancer Endpoint
http://a7fc107d6227e435bbdcb554906f0fb6-1219523202.us-east-1.elb.amazonaws.com/

## Authors

- [@nampt97](https://www.github.com/nampt97)

## Badges


### CircleCI Status
[![<CircleCI>](https://circleci.com/gh/nampt97/udacity-devops-capstone.svg?style=svg)](https://github.com/nampt97/udacity-devops-capstone)

### License
[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](https://choosealicense.com/licenses/mit/)

# Udacity Capstone Project

In this project you will apply the skills and knowledge which were developed throughout the Cloud DevOps Nanodegree program. These include:

* Working in AWS
* Using Circle CI to implement Continuous Integration and Continuous Deployment
* Building pipelines
* Working with CloudFormation to deploy clusters/infrastructure
* Building Docker containers in pipelines
* Building Kubernetes clusters

## Project Scope

## Environment Variables

To run this project, you will need to add the following environment variables to your CircleCI environment variables

* `AWS_DEFAULT_REGION`
* `AWS_ACCESS_KEY_ID`
* `AWS_SECRET_ACCESS_KEY`
* `AWS_DEFAULT_REGION`
* `DOCKER_HUB_PASSWORD`
* `DOCKER_HUB_USERNAME`

## Folder structure

| File | Description |
| ---- | ----------- |
| `.circleci/config.yml` | CircleCI configuration |
| `cloudformation` | CloudFormation yaml templates for creating infrastructure |
| `cloudformation/network.yml` | Create network VPC |
| `cloudformation/network-params.json` | Create network VPC params |
| `cloudformation/eks-cluster.yml` | Create EKS cluster |
| `cloudformation/eks-cluster-params.json` | Create EKS cluster params |
| `cloudformation/aws-eks-nodegroup.yml` | Create EKS nodes group |
| `cloudformation/amazon-eks-nodegroup-params.json` | Create EKS nodes group params |
| `kubernetes` | Kubernetes resource files |
| `kubernetes/deployment.yml` | Kubernetes deployment declaration |
| `kubernetes/loadbalancer.yml` | Kubernetes loadbalancer declaration |
| `kubernetes/aws-authen-cm.yml` | Kubernetes configmap declaration |
| `app.py` | main application to answer request |
| `Dockerfile` | Dockerfile to build image|
| `make_prediction.sh` | API call to make prediction |
| `Makefile` | Build file of the project |
| `requirements.txt` | Python required libraries |
| `scripts/run-docker.sh` | Shell script to run docker container |
| `scripts/run-kubernetes.sh` | Shell script to deploy docker container |
| `scripts/.create-cluster.sh` | Shell script to manually create EKS cluster |
| `scripts/create-kubeconfig.sh` | Shell script to create kubeconfig |
| `scripts/create-stack.sh` | Shell script to create AWS CloudFormation stack|
| `scripts/update-stack.sh` | Shell script to update AWS CloudFormation stack|
| `scripts/delete-stack.sh` | Shell script to delete AWS CloudFormation stack|
| `scripts/upload-docker.sh` | Shell script for uploading docker image to dockerhub repository |

## Run Steps For Cloud Deployment
* Create a DockerHub public repository
* Run chmod 700 for each Shell scrip in `./scripts` folder
* Run `./create-stack.sh capstone network.yml network-params.json` to create VPC infrastructure
* Run `./create-stack.sh capstone-eks eks-cluster.yml eks-cluster-params.json` to create EKS cluster
* Run `./create-stack.sh capstone-nodegroup aws-eks-nodegroup.yml amazon-eks-nodegroup-params.json` to create EKS nodes group
* Run `aws eks list-clusters --profile udacity` to see output like below
`{
    "clusters": [
        "CapstoneEKS-0J5F5Y6TBD53"
    ]
}` to get cluster name

* Replace cluster name to the line `123: cluster-name: CapstoneEKS-0J5F5Y6TBD53` in `./circleci/config.yml`.
* Configure CircleCI project for the github repository
* Done!

* Some kubectl commands to check k8s resources
```bash
    # See ndoes in cluster
    kubectl get nodes
    # See running pods
    kubectl get pods
    # See services
    kubectl get services
    # View logs of a pod (when checking incoming request)
    kubectl logs <POD_NAME>
    # Port forward to forward a port in pod to host port (format: <HOST_PORT><POD_PORT>)
    kubectl port-forward <HOST_PORT><POD_PORT>
```
## Run Steps For Manual Deployment
* Run `./scripts/create-cluster.sh`
* Run `./scripts/create-kubeconfig.sh`
* Run `./scripts/run-docker.sh`
* Run `./scripts/run-kubernetes.sh`

Remember to replace names of DockerHub repository & cluster name to the script file before you run.

