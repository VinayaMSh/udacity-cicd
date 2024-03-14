[![Build Status](https://dev.azure.com/vinayasharanappanavar/udacity-cicd/_apis/build/status%2FVinayaMSh.udacity-cicd?branchName=main)](https://dev.azure.com/vinayasharanappanavar/udacity-cicd/_build/latest?definitionId=8&branchName=main)

# Overview

This project is intended as an example/exercise project to test complete CI/CD with Azure pipelines.

The project deploys a Python flask web application in Azure App services

Whenever there is a commit to the repostory, an automatic build is started in GitHub Actions and then is deployed to the App Services

The detailed instructions of how to start and configure the complete pipeline using this repository can be found below in detailed instructions. 

So, lets get started!

## Project Plan

Trello board can be found [here](https://trello.com/invite/b/jOc8RFqQ/ATTIff73aa56ac5ab497ebc567a09ca9f6ccAAD9AD5D/udacity-cicd)
Spreadsheet uploaded in branch in this repo

## Instructions

<TODO:  
* Architectural Diagram (Shows how key parts of the system work)>



* Project running on Azure App Service
  -  This project is already deployed and can be accessed with url https://flask-ml-vs-1203.azurewebsites.net/
    ![image](https://github.com/VinayaMSh/udacity-cicd/assets/37274214/0d89fbe5-ce2c-46bf-aded-af84c44f40ca)




## Instructions for Deploy WebApp

  -  Start by cloning this repository in your Azure Cloud shell
  
  ```
  git clone https://github.com/VinayaMSh/udacity-cicd.git
  ```

  -  Once successfully cloned, go to the repo folder on the shell
     
  ```
  cd ~/udacity-cicd
  ```
  ###  Deploy app locally 

  -  Create virtual environment
        ```
        python3 -m venv ~/.myudacityrepo
        source ~/.myudacityrepo/bin/activate
        ```
  -  Install required dependencies, lint and test the code in the created virtual environment by executing make all command. When it is executed without any errors, run the application locally
        ```
        make all

        python app.py
        ```
        ![Screenshot-makeall](https://github.com/VinayaMSh/udacity-cicd/assets/37274214/bcc1feb5-ed9a-4f90-ac4f-0972dae71611)

  -   Once you have the output like below, open a new cloud shell session and execute the make_prediction.sh and it should display the prediction
       ```
        cd ~/udacity-cicd

        ./make_prediction.sh
        ```
      ![Screenshot-makeorediction](https://github.com/VinayaMSh/udacity-cicd/assets/37274214/3fcad713-678a-47ee-bb39-5e919eaebb5e)


        - When done, exit the virtual environment with exit command

  ### Deploy app in Azure
      
  -  Give the name of the flask webapp of your choice to the --name parameter
  ```
  cd ~/udacity-cicd

  az webapp up --sku B1 --name flask-ml-vs-1203 --resource-group udacity-test
  ```
   
  -  Once the webapp is successfully deployed, one must see similar output on cloud shell
  
  ![Screenshot-az-webapp-up](https://github.com/VinayaMSh/udacity-cicd/assets/37274214/b5e35e08-1e89-4b6d-b116-a8d32ff7ed33)


  -  Tests can be executed either by command `make test` or  `make all` command from the `Makefile`

  
  ![Screenshot-makeall](https://github.com/VinayaMSh/udacity-cicd/assets/37274214/0e02688a-93c5-4410-942b-0311b705e045)

### Setup Azure CICD pieline

  After successful deploy of the project, create Azure Pipeline by following the mentioned documentation.  [Note the official documentation should be referred to and double checked as you setup CI/CD](https://docs.microsoft.com/en-us/azure/devops/pipelines/ecosystems/python-webapp?view=azure-devops).

  After running Azure App Service from Azure Pipelines automatic deployment - the build and deploy part in the pipeline must be executed without any errors
  
  ![Screenshot-AzurePipeline](https://github.com/VinayaMSh/udacity-cicd/assets/37274214/6adab905-4613-405a-8020-8ae12ea38bfa)

  Clicking on the pipeline, shows all the activities done in the pipeline

  ![image](https://github.com/VinayaMSh/udacity-cicd/assets/37274214/a7acaa8c-a6cd-4e60-9660-b82badc78363)


### Successful prediction from deployed flask app in Azure Cloud Shell.
   
   Now, update the url with your webapp url in make_predict_azure_app.sh present in the repository from your cloud shell. Once updated, run the script
  
  ```
  ./make_predict_azure_app.sh
  ```

  Output looks somelike thing

  ![Screenshot-makepredict_azure](https://github.com/VinayaMSh/udacity-cicd/assets/37274214/6902c978-13a3-4217-90cb-0738e848f606)

The output should look similar to this:


### Output of streamed log files from deployed application

  You can see  the logs in the browser with the url https://flask-ml-vs-1203.scm.azurewebsites.net/api/logs/docker
  

  ![Screenshot-webapp-log](https://github.com/VinayaMSh/udacity-cicd/assets/37274214/b3c3de94-e842-4871-b685-69b050c47918)

### Load test with locust

  For testing with locust locally (not on Azure Cloud Shell)

  -  Install locust in your command prompt on Windows machine
    
     ```
      pip install locust

      locust --version
     ```
     
  -  Once installed, copy the locustfile.py from this repository locally and execute the below command

      ```
      locust -f <path to yout loustfile.py> -H https://flask-ml-vs-1203.azurewebsites.net/
     ```
  - Open browser and access  http://localhost:8089
 
    ![Screenshot-locustUI](https://github.com/VinayaMSh/udacity-cicd/assets/37274214/7b118d83-a5b9-43e3-bf02-7d0f64b1113b)

    Try with different inputs , and control the output

    
    ![Screenshot-locustUI-Tabs](https://github.com/VinayaMSh/udacity-cicd/assets/37274214/4e62d35c-d6cf-4c80-8952-69a77e27bd44)

## Enhancements

<TODO: A short description of how to improve the project in the future>

## Demo 

<TODO: Add link Screencast on YouTube>


