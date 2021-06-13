# Assignment 1 DevOps
Name: Heshan Mapa

Student Number: s3661741

## Stonk Inc
Stonk Inc currently faces an issue:
1. Wanting to start Kubernetes to be able to host their application

Continuing to help them as their DevOps Practitioner, I will help them with:
1. Setting up a Kubernetes to host their application
2. Expand on the CI build to automatically deploy the Kubernetes cluster
3. Using SaaS tools to reduce the learning curve for their own Development team.

## Dependencies
### Terraform
* Need to download and install terraform for linux through their website located at https://www.terraform.io/downloads.html
* Follow their simple install instructions to correctly install Terraform
* Validating Terraform in a terminal shell `terraform --version`

### Github
* As this project is on github, installing git and being able to clone the project to be able to configure to the company's needs.

### CircleCi
* We are using CircleCi for their Continuous Integration Building
* Being able to connect directly with the github repo, being able to build and test the application after every push.
* Access to the pipeline can be found when logging in to the developer's account at https://circleci.com

## Step-by-Step Solution
### Setting up a private repo in GitHub
First, we need to make another private repository on GitHub where we will work on the project. We will be ensuring we are using proper branching by using the GitHub Flow method, where all the new features we will be adding will be added and developed on feature branches and then merged into the main branch through the usage of Pull Requests which can then be later reviewed by the DevOp Practitioner (this case being me).
![github repo](https://i.imgur.com/AtnxFO6.png)

### Continuous Integration Building
We then have to set up intergration between CircleCi and the GitHub repo as we have done previously.
![circleci](https://i.imgur.com/NwJOSgU.png)

### Deployment Instructions
* Access the makefile in the root folder, and initiate the following commands.
`make bootstrap`
* Navigate to the .circleci folder and go through the CI config.yaml and update the bucket details
* Navigate to the infra folder, in the makefile update the bucket details.
* Deploy the kubernetes cluster using KOPS
```
make kube-create-cluster
make kube-secret
make kube-deploy-cluster
make kube-config
```
* Validate that everything is running with the following command

`kube-validate`

### Helm Chart
* Helm Charts are used to combine the Kubernetes YAML manifests into a singular package which can then be deployed into our Kubernetes clusters

### Deploying non-production environment
* A non-production environment typically means that the application development and staging is not used for production purposes. So the application and constantly be previewed in a non-live fashion to developers to help with testing. It's not made for customers/consumers
* In the config.yml file, I made a new command to deploy the the test (non-production environment). It's creating it in its own test environment so we can have multiple running at the same time. Essentially one for testing, and another for production

### Deploying Production Environment

## Screenshots
### Deployment of non-production (test) environment
![todo-test](https://i.imgur.com/3DRjlN9.png)

### Deployment of production (prod) environment
![todo-prod](https://i.imgur.com/omGLGGK.png)

### Smoke tests
* Test
![smoke-test](https://i.imgur.com/8F3ksv8.png)

* Prod
![smoke-prod]()

### Kubernetes Namespace
![namespace](https://i.imgur.com/9m5OlRV.png)

### Production on hold (requiring approval)
![approval](https://i.imgur.com/PxA64MY.png)
![approval2](https://i.imgur.com/CaJyMoQ.png)
![approval3](https://i.imgur.com/PzYaPXs.png)

### logging and monitoring with cloudwatch
![logging](https://i.imgur.com/zxKXlfg.png)

### Screenshot of TODO app logs in CLoudWatch
![cloudwatch](https://i.imgur.com/MIjKxUn.png)
![cloudwatch2](https://i.imgur.com/w7JudC9.png)

# Simple Todo App with MongoDB, Express.js and Node.js
The ToDo app uses the following technologies and javascript libraries:
* MongoDB
* Express.js
* Node.js
* express-handlebars
* method-override
* connect-flash
* express-session
* mongoose
* bcryptjs
* passport
* docker & docker-compose

## What are the features?
You can register with your email address, and you can create ToDo items. You can list ToDos, edit and delete them. 

# How to use
First install the depdencies by running the following from the root directory:
```
npm install --prefix src/
```

To run this application locally you need to have an insatnce of MongoDB running. A docker-compose file has been provided in the root director that will run an insatnce of MongoDB in docker. TO start the MongoDB from the root direction run the following command:

```
docker-compose up -d
```

Then to start the application issue the following command from the root directory:
```
npm run start --prefix src/
```

The application can then be accessed through the browser of your choise on the following:

```
localhost:5000
```
## Container
A Dockerfile has been provided for the application if you wish to run it in docker. To build the image, issue the following commands:

```
cd src/
docker build . -t todoapp:latest
```

## Terraform

### Bootstrap
A set of bootstrap templates have been provided that will provision a DynamoDB Table, S3 Bucket & Option Group for DocumentDB & ECR in AWS. To set these up, ensure your AWS Programmatic credentials are set in your console and execute the following command from the root directory

```
make bootstrap
```

### To instantiate and destroy your TF Infra:

To instantiate your infra in AWS, ensure your AWS Programattic credentials are set and execute the following command from the root infra directory:

```
make up -e ENV=<environment_name>
```

Where environment_name is the name of the environment that you wish to manage.

To destroy the infra already deployed in AWS, ensure your AWS Programattic credentials are set and execute the following command from the root directory:

```
make down -e ENV=<environment_name>
```

## Testing

Basic testing has been included as part of this application. This includes unit testing (Models Only), Integration Testing & E2E Testing.

### Linting:
Basic Linting is performed across the code base. To run linting, execute the following commands from the root directory:

```
npm run test-lint --prefix src/
```

### Unit Testing
Unit Tetsing is performed on the models for each object stored in MongoDB, they will vdaliate the model and ensure that required data is entered. To execute unit testing execute the following commands from the root directory:

```
npm run test-unit --prefix src/
```

### Integration Testing
Integration testing is included to ensure the applicaiton can talk to the MongoDB Backend and create a user, redirect to the correct page, login as a user and register a new task. 

Note: MongoDB needs to be running locally for testing to work (This can be done by spinning up the mongodb docker container).

To perform integration testing execute the following commands from the root directory:

```
npm run test-integration --prefix src/
```


###### This project is licensed under the MIT Open Source License
