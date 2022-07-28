---
title : "Configure Event Generator"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---

#### Configure Event Generator

{{% notice info %}}
Throughout the lab, we will use the same **EventGeneratorConfigurationUrl** of the **Output** stack.
{{% /notice %}}

1. Right click on the **EventGeneratorConfigurationUrl**.
  + Click **Open link in new tab**.
  
![SQS](/images/2/0000.png?featherlight=false&width=90pc)

2. We use **EventGeneratorConfigurationUrl** of **Output** stack just created.

   - Select **CONFIGURE COGNITO USER POOL**

![SQS](/images/2/0001.png?featherlight=false&width=90pc)

3. Make configuration

   - CognitoPassword
   - CognitoUsername
   - Then select **Configure**

![SQS](/images/2/0002.png?featherlight=false&width=90pc)

{{% notice note %}}
If the user information is incorrect, you may have copied an extra space at the end of the CognitoPassword information.
{{% /notice %}}