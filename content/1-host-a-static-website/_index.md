+++
title = "Host a Static Website"
date = 2020-05-14T00:38:32+07:00
weight = 1
chapter = false
pre = "<b>1. </b>"
+++


**Content:**
- [Create a new React application](#create-a-new-react-application)
- [Initialize a GitHub repository](#initialize-a-github-repository)
- [Install the Amplify packages](#install-the-amplify-packages)
- [Deploy app with AWS Amplify](#deploy-app-with-aws-amplify)

#### Create a new React application

1. In a new terminal or command line window, run the following command to use **Vite** to create a **React application**:
   ```bash 
   npm create vite@latest ai-recipe-generator -- --template react-ts -y
   cd ai-recipe-generator
   npm install
   npm run dev
   ```
2. In the terminal of **Visual Studio Code**, select and open the Local link to view the **Vite + React** application.

![Image](https://deved-images.nyc3.cdn.digitaloceanspaces.com/CART-69046/gkoFYDe.png?width=30pc)


#### Initialize a GitHub repository

1. In the **Start a new repository** section, make the following selections:

- For **Repository name**, enter **ai-recipe-generator**, and choose the **Public** radio button.
- Then select, **Create a new repository**.

![Image](/images/1-host-a-static-website/repogithub.png?width=20pc)

2. Open a new terminal window, navigate to projects, and run the following commands to initialize a git and push of the application to the new GitHub repo:


**Option 1: Avaiable to authenticate with GitHub using your SSH key**

```bash
git init
git add .
git commit -m "first commit"
git remote add origin git@github.com:<your-username>/<your-repo-name>.git
git branch -M main
git push -u origin main
```


{{% notice note%}}
Replace the **SSH GitHub URL** in the command with **GitHub URL**. 
{{% /notice%}}

**Option 2: If you don't generate an SSH key before**
```bash
git init                                                            
git add .             
git commit -m "first commit"
git remote set-url origin https://github.com/<your-username>/<your-repo-name>
git branch -M main
git push -u origin main
```
#### Install the Amplify packages

1. Open a new terminal window, navigate to your project, and run the following command:
```bash
npm create amplify@latest -y
```
2. In your terminal window, run the following command to push the changes to GitHub:
```bash
git add .
git commit -m 'installing amplify'
git push origin main
```

#### Deploy app with AWS Amplify

1. Sign in to the AWS Management console in a new browser window, and open the AWS Amplify console at **[AWS Amplify](https://console.aws.amazon.com/amplify/apps)**.
2. Choose **Create new app**.

![Image](/images/1-host-a-static-website/createnewapp.png?width=45pc)

3. On the **Start building with Amplify** page, for **Deploy your app**, select **GitHub**, and select **Next**.

![Image](/images/1-host-a-static-website/startbuilding.png?width=40pc)

4. When prompted, **authenticate** with GitHub. You will be automatically redirected back to the Amplify console. Choose the **repository** and **main branch** you created earlier. Then select **Next**.

![Image](/images/1-host-a-static-website/addrepo.png?width=40pc)

5. Leave the default **build settings**, and select **Next**.

![Image](/images/1-host-a-static-website/appsetting.png?width=30pc)

6. Review the inputs selected, and choose **Save and deploy**.

![Image](/images/1-host-a-static-website/repodetail.png?width=30pc)

7. Once the build completes, select the **Visit deployed URL** button to see your web app up and running live. 
AWS Amplify will now build your source code and deploy your app at **https://...amplifyapp.com**

![Image](/images/1-host-a-static-website/ai-recipe.png?width=30pc)
