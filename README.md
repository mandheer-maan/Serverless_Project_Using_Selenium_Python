# Serverless_Project_Using_Selenium_Python

---

## Folder Hierarchy

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
  
### First of all Run bash script for zipping chromediver and headless-chromium

``` bash
#!/bin/sh
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
