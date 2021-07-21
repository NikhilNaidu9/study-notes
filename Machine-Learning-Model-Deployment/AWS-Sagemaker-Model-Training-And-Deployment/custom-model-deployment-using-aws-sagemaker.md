# Custom Model Deployment Using AWS Sagemaker

## Steps
1. Create a bucket where we can store the model 
1. Upload the model to the bucket
1. Then write the `predictor.py` for running the model which will be hosted using flask
1. It will have to two ENDPOINTS which will will `/ping` and `/invocations`
1. `/ping` is responsible for checking that container is ready to take inference request at invocation point
1. `/invocations` will recieve `POST` requet and respond according to the format specified in the algorithm
1. To make the model REST API, we will be needing flask, which is a WSGI(Web Server Gateway Interface) application framework, Gunicorn the WSGI server, and nginx the reverse-proxy and load balancer.
1. Then we need to bundle all the config files and serving script into a container 
1. We bundle all the files using `DockerFile` 
1. `DockerFile` consist of information like the distribution it will be using, the commands of software installation that it will run in the container, file directories of the container
1. After writing a `DockerFile` we build it using the `docker build` 
1. After building it locally we will push it to the `Elastic Container Registry` 
1. Before pushing it to registry we have to configure the aws CLI with our credentials
1. `aws configure` - adding credentials from the account
1. `aws ecr get-login --no-include-email` 
1. Create a repository in the `ecr` using frontend
1. Start the docker daemon
1. `docker tag hello-world:latest aws_account_id.dkr.ecr.us-east-1.amazonaws.com/hello-world:latest` - tag the image to push to the registry
1. `docker push aws_account_id.dkr.ecr.us-east-1.amazonaws.com/hello-world:latest` - This will push it to the registry
1. Now after push the image to the registry we create a model using frontend
1. After this create a endpoint configuration using the frontend
1. Then create a endpoint using existing endpoint configuration     
1. This is where the problem occurs, it takes a lot of time to create a endpoint and then it fails 
1. Problem was that the code was edited in the Windows system and it was executing in the Linux system so both have different line endings 
1. Problem is solved by using a tool `dos2unix` on all the files which transforms the file endings like how it is required in Linux systems
1. Sometimes the login credentials expires, we need to login again with the credentials using aws cli 
1. After this create a `Lambda` function which will invoke the model 
1. Function should have a python environment 
1. Then add a trigger called `API Gateway` 
1. Select the REST API option while creating it
1. Add the code in lambda function to execute the request 
1. Then in the API Gateway add the `POST` method which will be configured to trigger the lambda function 
1. Then we write small script in the sagemaker notebook instance to pass the input and get the output from the endpoint  

# Reference 
Tutorial Used  
https://medium.com/analytics-vidhya/deploy-your-own-model-with-aws-sagemaker-55b4234be4a

Getting Started with AWS ECR CLI  
https://docs.aws.amazon.com/AmazonECR/latest/userguide/getting-started-cli.html

# Errors
/usr/bin/env: 'python3\r': No such file or directory
https://askubuntu.com/questions/896860/usr-bin-env-python3-r-no-such-file-or-directory 
