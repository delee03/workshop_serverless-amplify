+++
title = "Create & Deploy a Web Application with ReactJS"
date = 2024-10-14T00:38:32+07:00
weight = 3
chapter = false
pre = "<b>2. </b>"
+++

**Content:**

-   [Create a new ReactJS Application](#1-create-a-new-react-application)
-   [Initialize a Github Repository](#2-initialize-a-github-repository)
-   [Install the Amplify packages](#3-install-the-amplify-packages)
-   [Deploy your app with AWS Amplify](#4-deploy-your-app-with-aws-amplify)

#### Create a new ReactJS Application

In this task, you will create a React application and deploy it to the Cloud using AWS Amplify.
AWS Amplify offers a Git-based CI/CD workflow for building, deploying, and hosting single-page web applications or static sites with backends. When connected to a Git repository, Amplify determines the build settings for both the frontend framework and any configured backend resources, and automatically deploys updates with every code commit.

In this task, you will start by creating a new React application and pushing it to a GitHub repository. You will then connect the repository to AWS Amplify web hosting and deploy it to a globally available content delivery network (CDN) hosted on an amplifyapp.com domain.

### 1. Create a new React application

Step 1: Open you file explorer, create a new folder name it <<Your-Project-Amplify>> and open Visual Studio Code with the folder created open terminal in VS Code run the following command to create a new React application using Vite and React:

```bash
npm create vite@latest profilesapp -- --template react
cd profilesapp
npm install
npm run dev

```

![Create a Web Application](/images/workshop-setup/1.1_KhoiTaoDuAn.png?width=full)

Step 2: In the terminal window, select and open the Local link 5173 to view the Vite + React application.

![Create a Web Application](/images/workshop-setup/RunLocalhost.png?width=full)

### 2. Initialize a Github Repository

In this step, you will create a GitHub repository and commit your code to the repository. You will need a GitHub account to complete this step, if you do not have an account, [sign up here](https://github.com/).

{{% notice warning%}}
If you have never used GitHub on your computer, follow [these steps](https://docs.github.com/en/authentication/connecting-to-github-with-ssh) before continue.
{{% /notice%}}

Step 1: Open a new browser tab and navigate to [GitHub at https://github.com](https://github.com/)

Step 2: Sign in to your GitHub account.

Step 3: Click the **+** sign in the top right corner of the page and select **New repository**.

Step 4: In the **Repository name** field, enter `profile_app`.

![Create a Repository with Github](/images/workshop-setup/1.2_CreateRepository.png?width=full)

Step 5:
Open your source code initilized in the previous step, right click on the `profilesapp` and click `Open in Intergrated Terminal`, and run the following commands to initialize a git and push of the application to the new GitHub repository:

![Open Terminal Correctly in VS Code](/images/workshop-setup/1.3_Mo_Dung_TerminalDuAn_CaiAmplify.png?width=full)

{{% notice note%}}
Note: Replace the GitHub URL in the command with your GitHub URL.
{{% /notice%}}

**Run the following commands in the terminal:**

```bash
    git init
    git add .
    git commit -m "first commit"
    git remote add origin https://github.com/<your-username>/profile_app
    git branch -M main

    git push -u origin main
```

### 3. Install the Amplify packages

1. Open a new terminal window, navigate to your app's root folder (profilesapp) open in Intergrated Terminal above by right click on file _package.json_, purpose is navigate correctly to root folder, and run the following command:

![Open Terminal Correctly to Install Amplify in VS Code](/images/workshop-setup/1.3_Mo_Dung_TerminalDuAn_CaiAmplify-Copy.png?width=full)

**Run the following command to install the Amplify CLI:**

```bash
npm create amplify@latest -y

```

2. Running the previous command will scaffold a lightweight Amplify project in the app’s directory.

![Install Successfull Amplify](/images/workshop-setup/1.3_TaiAmplifySuccess.png?width=full)

3. In your terminal window, run the following command to push the changes to GitHub:

```bash
git add .
git commit -m "Add Amplify installed"
git push
```

If you have successfully pushed the changes to GitHub, you will see the following message in the terminal:

![Push Changed filed to Github](/images/workshop-setup/1.3_PushCode.png?width=full)

### 4. Deploy your app with AWS Amplify

1. Sign in to the AWS Management console in a new browser window, and open the AWS Amplify console at [https://console.aws.amazon.com/amplify/](https://console.aws.amazon.com/amplify/).

![Image of AWS Amplify Service](/images/workshop-setup/Amplify_Service.png?width=full)

<!-- ![Install Successfull Amplify](/images/workshop-setup/1.3_TaiAmplifySuccess.png?width=full) -->

2. Choose **Deploy** at the center of the page.

![Image of AWS Amplify Console](/images/workshop-setup/1.4_Deploy_With_Amplify.png?width=full)

3. On the Start building with Amplify page, for Deploy your app, **select GitHub**, and select **Next**.

![Choose Github to Deploy](/images/workshop-setup/1.4_DeployOnGithub1.png?width=full)

4. When prompted, authenticate with GitHub by selecting **Authorize AWS Amplify**.

![Athourize with Github](/images/workshop-setup/1_4_Authorization.png?width=35pc)

5. Select repository you want to deploy on Amplify, authenticate with GitHub by selecting **Only select repositories** (you can choose all repositories, this instance I choose only repositories) and choose **Your project : Profile_app** after that click **Install & Authorize**.

![Athourize with Github](/images/workshop-setup/1_4_SelectRepositoryCreated.png?width=40pc)

6. You will be automatically redirected back to the Amplify console, select **the repository**, **main branch** you want to deploy, and then choose **Next**.
   ![Select Repository Uploaded](/images/workshop-setup/1_4_SelectRepository.png?width=full)

7. Leave the default build settings, and select **Next**.
   ![Default Setting Config](/images/workshop-setup/1_4_ConfigDefault.png?width=full)

8. Review the settings, and select **Save and deploy**

![Review Setting and deploy](/images/workshop-setup/1_4_Review.png?width=full)

**AWS Amplify** will now build your source code and deploy your app at _https://...amplifyapp.com_, and on every git push your deployment instance will be update automatically . It may take up to 5 minutes
to deploy your ReactJS app.

9. Once the build completely, select the **Visit deployed URL** button to see your web app up and running live.

![Deploy Successfull](/images/workshop-setup/1_4_DeploySuccess.png?width=full)

10. You can now view your deployed ReactJS app on the AWS Amplify console.You can view you domain name and the status of the deployment.
    If you see the following screen, **your deployment was successful** and **host** a ReactJS app on AWS Amplify perfectly.

![Deploy Website](/images/workshop-setup/1_4_SuccessfulDeploy1.png?width=full)

**Good job** You have deployed a React application in the AWS Cloud by integrating with GitHub and using AWS Amplify. With AWS Amplify, you can continuously deploy your application in the Cloud and host it on a globally available CDN
