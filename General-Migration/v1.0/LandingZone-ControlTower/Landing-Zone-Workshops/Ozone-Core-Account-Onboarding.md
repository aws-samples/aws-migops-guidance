Related Artifacts
=================

*   **Landing Zone Ozone - Launch Parameters**
    

* * *

Create an AWS Account
=====================

AMS multi-account landing zone requires the provisioning of a new Amazon Web Services (AWS) account to act as the Master Account in the AMS multi-account landing zone environment. To create an AWS account, follow these step-by-step instructions: [How do I create and activate a new Amazon Web Services account?](http://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/)

The simple steps are: Go to [Create Account](https://aws.amazon.com/resources/create-account/), and click **Sign Up Now** and, on the page that opens, click **Create a new AWS account**. Follow the on-screen instructions, which include receiving a phone call and entering a PIN using your phone keypad. You'll also need to enter a credit card. AMS uses this account as the master/payer account for your new multi-account landing zone.

**Note:** Do not link your new account to an existing master/payer account.

Ensure that you have set up an AWS Organization; for information, see [What Is AWS Organizations?](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_introduction.html).

**Important**  
It is very important that you ensure that an **email address** (a distribution list, not an individual's email address) and **phone number** are associated with the account so that you receive responses to potential security incidents. The phone number and email address for the account cannot be changed without resetting the account password, which is a significant undertaking for an AMS root account. To ensure that these values are stable, _it is critical to select contact information not associated with individuals_, which can change. Choose an email alias that can point to a group. Follow this same best practice in selecting a phone number: choose a number that can point to a group or to a number owned by the company and not an individual. 

Create an IAM Role for AMS to Access Your Account
=================================================

Now that you've successfully created your new AWS account, the next step in the process is to allow AMS access to the new account to create and configure your AMS environment, and for ongoing change and provisioning requests to be fulfilled. For details, see [Delegate Access Across AWS Accounts Using IAM Roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/tutorial_cross-account-with-roles.html).

AWS Identity and Access Management (IAM) is a web service that helps you securely control access to AWS resources for your users. You use IAM to control who can use your AWS resources (authentication) and what resources they can use and in what ways (authorization).

Activate IAM Access to the AWS Console
--------------------------------------

1.  Sign in to the AWS Management Console with your root account credentials (the email and password that you used to create your AWS account). Do not sign in with other IAM credentials. The AWS Management Console home page opens.
    
2.  In the top navigation bar, open the drop-down menu for your account name, and then choose **My Account**. The Billing home page opens.
    
3.  Scroll down to IAM User Access -> Billing Information, and choose Edit. An Activate IAM access area opens.
    
4.  Select the check box and then choose **Update**. You can now use IAM policies to control which pages a user can access.
    

Create an IAM Role for AMS to Use
---------------------------------

1.  Use the following JSON file that contains the IAM role AMS uses for creating infrastructure.
    
2.   Sign in to the AWS Management Console and open the AWS CloudFormation console at [https://console.aws.amazon.com/cloudformation](https://console.aws.amazon.com/cloudformation/).
    
     ![](/.attachments/DK-LandingZone-ControlTower/image-20200807-155048.png)
    
3.  Choose **Create Stack**. You see the following page.
    
     ![](/.attachments/DK-LandingZone-ControlTower/image-20200807-155100.png)
    
4.  Choose **Upload a template file**, upload the JSON or YAML file of the IAM role, and then choose **Next**. You see the following page.
    
     ![](/.attachments/DK-LandingZone-ControlTower/image-20200807-155127.png)
    
5.  Enter **ams-onboarding-role** into the **Stack name** section and continue scrolling down and selecting next until you reach this page.
    
     ![](/.attachments/DK-LandingZone-ControlTower/image-20200807-155151.png)
    
6.  Make sure the check box is selected and then select **Create Stack**.
    
7.  Make sure the stack was created successfully.
    

Document Launch Parameters
==========================

Conduct a workshop session to review and collect the required Launch Parameters

**Landing Zone Ozone - Launch Parameters**

 **Attachments:** 


[image-20200807-155048.png](/.attachments/DK-LandingZone-ControlTower/image-20200807-155048.png)

[image-20200807-155100.png](/.attachments/DK-LandingZone-ControlTower/image-20200807-155100.png)

[image-20200807-155127.png](/.attachments/DK-LandingZone-ControlTower/image-20200807-155127.png)

[image-20200807-155151.png](/.attachments/DK-LandingZone-ControlTower/image-20200807-155151.png)
