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
## Install serverless command
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
  
---  
  
- **For Reference go through [this link](https://github.com/yai333/Selenium-UI-testing-with-AWS-Lambda-Layers).** :thumbsup:
