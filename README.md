[![Build Status](https://dev.azure.com/vinayasharanappanavar/udacity-cicd/_apis/build/status%2FVinayaMSh.udacity-cicd?branchName=main)](https://dev.azure.com/vinayasharanappanavar/udacity-cicd/_build/latest?definitionId=8&branchName=main)

# Overview

This project is intended as an example/exercise project to test complete CI/CD with Azure pipelines.

The project deploys a Python flask web application in Azure App services

Whenever there is a commit to the repostory, an automatic build is started in GitHub Actions and then is deployed to the App Services

The detailed instructions of how to start and configure the complete pipeline using this repository can be found below in detailed instructions. 

So, lets get started!

## Project Plan
<TODO: Project Plan

* A link to a Trello board for the project
* A link to a spreadsheet that includes the original and final project plan>

## Instructions

<TODO:  
* Architectural Diagram (Shows how key parts of the system work)>

<TODO:  Instructions for running the Python project.  How could a user with no context run this project without asking you for any help.  Include screenshots with explicit steps to create that work. Be sure to at least include the following screenshots:

* Project running on Azure App Service
  -  This project is already deployed and can be accessed with url https://flask-ml-vs-1203.azurewebsites.net/
    ![image](https://github.com/VinayaMSh/udacity-cicd/assets/37274214/0d89fbe5-ce2c-46bf-aded-af84c44f40ca)




## Deploy WebApp

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
  -  Install required dependencies, lint and test the code in the created virtual environment and run the application locally
        ```
        make all

        python app.py
        ```
        ![Screenshot-makeall](https://github.com/VinayaMSh/udacity-cicd/assets/37274214/bcc1feb5-ed9a-4f90-ac4f-0972dae71611)

  -   Once you have the output like below, open a new cloud shell session and execute the make_prediction.sh and it should   display the prediction
       ```
        cd ~/udacity-cicd

        ./make_prediction.sh
        ```
      ![Screenshot-makeorediction](https://github.com/VinayaMSh/udacity-cicd/assets/37274214/3fcad713-678a-47ee-bb39-5e919eaebb5e)


        - When done, exit the virtual environment with exit command

  ### Deploy app in Azure
      
  ```
  az webapp up --sku B1 --name flask-ml-vs-1203 --resource-group udacity-test
  ```
  Give the name of the flask webapp of your choice to the --name parameter 

* Passing tests that are displayed after running the `make all` command from the `Makefile`

* Output of a test run

* Successful deploy of the project in Azure Pipelines.  [Note the official documentation should be referred to and double checked as you setup CI/CD](https://docs.microsoft.com/en-us/azure/devops/pipelines/ecosystems/python-webapp?view=azure-devops).

* Running Azure App Service from Azure Pipelines automatic deployment

* Successful prediction from deployed flask app in Azure Cloud Shell.  [Use this file as a template for the deployed prediction](https://github.com/udacity/nd082-Azure-Cloud-DevOps-Starter-Code/blob/master/C2-AgileDevelopmentwithAzure/project/starter_files/flask-sklearn/make_predict_azure_app.sh).
The output should look similar to this:

```bash
udacity@Azure:~$ ./make_predict_azure_app.sh
Port: 443
{"prediction":[20.35373177134412]}
```

* Output of streamed log files from deployed application

> 

## Enhancements

<TODO: A short description of how to improve the project in the future>

## Demo 

<TODO: Add link Screencast on YouTube>


