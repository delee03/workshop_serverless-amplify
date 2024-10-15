+++
title = "Introduction"
date = 2021
weight = 2
chapter = false
pre = "<b>1. </b>"
+++

#### Overview

In this workshop, you will learn to create a simple **full-stack web application** using **AWS Amplify**. Throughout this workshop, you will **build** and **host** a React application **on AWS**, use Amplify to **add authentication**, **data**, and **a serverless function** to capture the signed-up user's email and save it in the database. Then, you will implement a frontend for your app that **integrates with your cloud resources**.

#### Architect Schema

The following diagram provides a visual representation of the services used in this simple lab and how they are connected. This application uses **AWS Amplify, GraphQL API, AWS Lambda, and Amazon DynamoDB.**

As you go through the workshop, you will learn about the services in detail and find resources that will help you get up to speed with them.

![Architecture Application Schema](/images/workshop-setup/ArchitectureSystem.png?width=90pc)

#### What you will accomplish

**Host**: Build and deploy a React application on the AWS global content delivery network (CDN).  
**Authenticate**: Add authentication to your app to enable sign-in and sign-out functionality.  
**Database**: Integrate a real-time API, database, and a serverless function.  
**Function**: Implement a lambda function that is triggered when a user signs up to the App.

#### Required

**An AWS account:** with administrator permission  
**Nodejs and npm:** Installed on your computer  
**Git & GitHub account:** Foundational knowledge of
**Visual Studio Code:** Installed on your computer  
**If you have a FreeTier Account, that's so great**

{{% notice note%}}
Accounts created within the past 24 hours might not yet have access to the services required for this lab
{{% /notice%}}

#### Main content

1. [Introduction](0-Introdution/)
2. [Create & Deploy a Web Application with ReactJS](1-Create-A-Web-App/)
3. [Build Serverless function with AWS Lamda](2-Build-A-ServerlessFunction-Lamda/)
4. [Create Data Table with DynamoDB](3-Create-Data-Table/)
5. [Link Serverless function to Web Application](4-Link-ServerlessFunction-ToWebApp/)
6. [Add interactivity to web app](5-Add-Interactivity/)
7. [Clean up resources](6-CleanUp/)
 <!-- need to remove parenthesis for path in Hugo 0.88.1 for Windows-->
