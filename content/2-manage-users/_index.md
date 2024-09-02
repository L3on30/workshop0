+++
title = "Manage user"
date = 2020-05-14T00:38:32+07:00
weight = 2
chapter = false
pre = "<b>2. </b>"
+++


**Content:**
- [Set up Amplify Auth](#set-up-amplify-auth)
- [Set up Amazon Bedrock Model Access](#set-up-amazon-bedrock-model-access)
#### Set up Amplify Auth

1. On your local machine, navigate to the **`ai-generated-recipes/amplify/auth/resource.ts`** file and **update** it with the following code. Then, **save** the file.

   ```typescript
   import { defineAuth } from "@aws-amplify/backend";

   export const auth = defineAuth({
     loginWith: {
       email: {
         verificationEmailStyle: "CODE",
         verificationEmailSubject: "Welcome to the AI-Powered Recipe Generator!",
         verificationEmailBody: (createCode) =>
           `Use this code to confirm your account: ${createCode()}`,
       },
     },
   });

This is an example of the customized verification email:

![Image](/images/2-manage-users/mailcode.png?width=30pc)


#### Set up Amazon Bedrock Model Access

1.  Sign in to the AWS Management console in a new browser window, and **open** the AWS Amazon Bedrock console at [AWS Bedrock](https://console.aws.amazon.com/bedrock/). **Verify** that you are in the **N. Virginia us-east-1 region**, and choose **Get started**.

![Image](/images/2-manage-users/bedrock.png?width=40pc)

2. In the **Foundation models** section, choose the **Claude model**.


![Image](/images/2-manage-users/choosemodel.png?width=30pc)

3. Scroll down to the **Claude models** section, and choose the **Claude 3 Sonnet** tab, and select **Request model access**.

{{% notice note%}}
If you already have access to some models, then the button will display **Manage model access**. 
{{% /notice%}}

![Image](/images/2-manage-users/claude3sonnet.png?width=30pc)

4. In the Base models section, for **Claude 3 Sonnet**, choose **Available to request**, and select **Request model access**.

![Image](/images/2-manage-users/basemodel.png?width=30pc)

5.  On the **Edit model access** page, choose **Next**.

![Image](/images/2-manage-users/checkbasemodel.png?width=30pc)

6.  On the **Review and Submit** page, choose **Submit**.

{{% notice note%}}
If this is the first model you request to access, you have to do one more step that fill in a form that include **Company name** and **purpose** of your project
{{% /notice%}}

![Image](/images/2-manage-users/reviewModel.png?width=30pc)

