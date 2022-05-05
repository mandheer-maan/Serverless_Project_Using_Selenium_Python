# Serverless_Project_Using_Selenium_Python

###  First prepare image using docker
####  Build an image using the follwoing command: (Dockerfile is mentioned below)
```
docker build -t <image-name> <path of the Dockerfile>
```

Dockerfile
```
FROM amazon/aws-sam-cli-build-image-python3.6

RUN yum -y update && \
    yum -y install nano && \
    curl -o- -L https://slss.io/install | VERSION=2.72.2 bash && \
    yum clean all

RUN aws --version && \
    sam --version
```   

###  Run the image that was just built
```
docker run -it <image-name>
```
### Clone the repository

``` 
git clone https://github.com/mandheer-maan/Serverless_Project_Using_Selenium_Python.git
```

### Download Selenium (version: 2.37)
```
pip3 install -t Serverless_Project_Using_Selenium_Python/seleniumLayer/selenium/python/lib/python3.6/site-packages selenium==2.37
```

### Provide the name for Selenium layer and Lambda function 
(Replace ```PROJECT_NAME``` with user-defined name) 
```
sed -i 's/project1/PROJECT_NAME/g' Serverless_Project_Using_Selenium_Python/seleniumLayer/serverless.yaml
sed -i 's/project1/PROJECT_NAME/g' Serverless_Project_Using_Selenium_Python/lambda/serverless.yaml
```

### Configure AWS profile
```
aws configure set aws_access_key_id "AWS_ID";
aws configure set aws_secret_access_key "AWS_ACCESS_KEY";
aws configure set region "us-east-1";
aws configure set output "json";
aws configure set aws_profile "PROFILE_ID";
```

### Prepare chrome related drivers (in .zip file)
```
cd Serverless_Project_Using_Selenium_Python;
chmod +x install.sh;
./install.sh
```

### Deploy Selenium Layers
```
cd seleniumLayer;
serverless deploy 
```


### Deploy Lambda Function
```
cd ../lambda;
serverless deploy 
```

### Start Testing
   - Go to **/lambda** directory  

```
$ serverless invoke --function hello
```

### You should get Response as below

``` json
{
"statusCode": 200,
"body": "Headless Chrome Initialized, Page title Home | Neami    National"
}
```
### Commands Used

```
$ serverless deploy  

$ serverless invoke --function hello
```
---  



## Project Hierarchy
```
── /seleniumLayer/  # lambda layers
  ├── /selenium  lambda layer of selenium lib
  │  └──/python/      # python libs
  │   └── /lib/    
  │     └── /python3.6/*    
  ├── /chromedriver/    # lambda layer of headless Chrome 
  │ ├── /chromedriver   # chrome driver
  │ └── /headless-chromium # headless chrome binary
  └── /serverless.yaml     
── /lambda/            # lambda function
  ├── /handler.py      # source code of lambda function 
  └── /serverless.yaml # serverless config\
  
  ```
  
  ### Extra command : To refresh the terminal state
  ```
  source ~/.bashrc
  ```
- **For Reference go through [this link](https://github.com/yai333/Selenium-UI-testing-with-AWS-Lambda-Layers).** :thumbsup:
