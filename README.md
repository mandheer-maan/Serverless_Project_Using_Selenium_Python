# Serverless_Project_Using_Selenium_Python

###  First prepare image using docker
####  Build the image using the follwoing command: (Dockerfile is mentioned below)
```
docker build -t <image-name> <path of the Dockerfile>
```

Dockerfile
```
FROM amazon/aws-sam-cli-build-image-python3.6

RUN yum -y update && \
    yum -y install nano && \
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


## Folder Hierarchy

```
cd Serverless_Project_Using_Selenium_Python/
```

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
  
### First of all Install Selenium library
 - Lambda runtimes include paths in the ```/opt``` directory to ensure that your function code has access to libraries that are included in layers.

 - To include libraries in a layer, place them in ```python/lib/python3.6/site-packages/```

``` bash
# download Selenium 2.37 to layer directory
$ pip3 install -t seleniumLayer/selenium/python/lib/python3.6/site-packages selenium==2.37
```

### Run the below bash script for zipping chromediver and headless-chromium using the below commands

```
chmod +x install.sh

./install.sh
```

``` bash
#!/bin/bash
# download chrome driver
mkdir -p seleniumLayer/chromedriver
cd seleniumLayer/chromedriver
curl -SL https://chromedriver.storage.googleapis.com/2.37/chromedriver_linux64.zip > chromedriver.zip
unzip chromedriver.zip
rm chromedriver.zip
# download chrome binary
curl -SL https://github.com/adieuadieu/serverless-chrome/releases/download/v1.0.0-41/stable-headless-chromium-amazonlinux-2017-03.zip > headless-chromium.zip
unzip headless-chromium.zip
rm headless-chromium.zip

```


### Install serverless command
  - Do this if you don't have serverless in your machine yet

``` bash
npm install -g serverless
```

### Deploy Lambda Layers
   - Go to **/seleniumLayer** directory

```  
$ serverless deploy 
```

### Deploy Lambda Function
   - Go to **/lambda** directory

```  
$ serverless deploy 
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
  
- **For Reference go through [this link](https://github.com/yai333/Selenium-UI-testing-with-AWS-Lambda-Layers).** :thumbsup:
