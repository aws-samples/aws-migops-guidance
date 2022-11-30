  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

* * *

This solution should only be considered after ruling out using AWS SSO for console and CLI federation.

Introduction
============

This runbook is part of an AWS Runbook series meant to provide the foundation for a customer’s AWS Operational Knowledge Base. This guide provides the descriptions and methods for federating access from an organization's existing identities in AD via ADFS to their AWS Accounts. 

Using this Runbook
==================

Each customer environment is unique, so this runbook should be revised to include any existing customer specific processes. The runbooks in this series are also published in Word format but are more valuable when incorporated into a Knowledge Management System that supports linking and indexing.

Purpose
=======

These instructions are meant for customers that plan to use the standard number of AWS Accounts defined in the Landing Zone reference implementation which includes ~7 AWS accounts (master, consolidated logging, shared services, dev, test, prod, and sandbox). Customers that require a large number of accounts and/or a large number of administrators with multiple roles per account will need to use an alternate pattern to ensure that SAML assertion requests do not exceed the maximum size. These instructions assume that the customer already has an active ADFS setup. This is the case for customers that have already migrated to Office365 and/or other SaaS based applications.

Collect Required Information
============================

|   **Name**   |   **Value**   |
| --- | --- |
|   ADFS Login URL   |   [https://sts.acme.com/adfs/ls/IdpInitiatedSignOn.aspx?loginToRp=urn:amazon:webservices](https://sts.acme.com/adfs/ls/IdpInitiatedSignOn.aspx?loginToRp=urn:amazon:webservices+)   |
| ADFS Prod Login URL |     |
|   AWS Account IDs Matrix   |   Complete the AWS Account matrix located on the following page: Landing Zone Account Design   |
|   User to Role Matrix   |   Complete the User to Role matrix located on the following page: Landing Zone IAM Roles Design   |

Configure AWS as a Trusted Relying Party  
 ADFS SAML Claims Setup  
Next, we need to tell AD FS that it should offer authentication services for AWS. The SAML configuration for doing so is known as a _relying party_.  
To start, choose the **Start menu**, type **ad fs**, and choose **AD FS Management**.  
 ![](/.attachments/DK-LandingZone-ControlTower/worddav81822fd08883c1c5b2725b40ca4f0056.png)
  
Choose **Add Relying Party Trust** to start the **Add Relying Party Trust Wizard**.  
 ![](/.attachments/DK-LandingZone-ControlTower/worddavc4727d69a0f2883a01aea7cc3ef42ecc.png)
  
Choose **Start** to begin. Then, on **Select Data Source**, type the following URL for the AWS SAML metadata, and then choose **Next**. [https://signin.aws.amazon.com/static/saml-metadata.xml](https://signin.aws.amazon.com/static/saml-metadata.xml)  
 ![](/.attachments/DK-LandingZone-ControlTower/worddav263d72c33bdad28c34cff8093481efb1.png)

SAML federations use metadata documents to maintain information about the public keys and certificates that each party utilizes. At run time, each member of the federation can then use this information to validate that the cryptographic elements of the distributed transactions come from the expected actors and haven't been tampered with. Since these metadata documents do not contain any sensitive cryptographic material, AWS publishes federation metadata at [https://signin.aws.amazon.com/static/saml-metadata.xml](https://signin.aws.amazon.com/static/saml-metadata.xml+)

  
Accept the defaults for **Specify Display Name**, **Configure Multi-factor Authentication Now?**, and **Choose Issuance Authorization Rules** by choosing **Next** three times. Choose **Close** on the **Finish** page to complete the **Add Relying Party Trust Wizard**.  
 ![](/.attachments/DK-LandingZone-ControlTower/worddavd3d94017e489772c4b43dd983f79abaf.png)

Configure claim rules for the AWS relying party
-----------------------------------------------

In a SAML federation, the IdP can pass various attributes about the user, the authentication method, or other points of context to the service provider (in this case AWS) in the form of SAML attributes. In order for SAML federation for AWS to function properly, [several attributes](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers_create_saml_assertions.html) are required. In AD FS, **Claim Rules** are used to assemble these required attributes using a combination of Active Directory lookups, simple transformations, and regular expression based custom rules. You will configure a total of **four claim rules**.  
The **Edit Claim Rules** window should be already open, if not, you can re-open it from **Relying Party Trusts**, by choosing [signin.aws.amazon.com](http://signin.aws.amazon.com/), and then choosing **Edit Claim rules** as shown in the following screenshot.  
 ![](/.attachments/DK-LandingZone-ControlTower/worddav1a654cab0051793d6bbf7bae24e823c0.png)
  
Choose **Add Rule...** to configure the first rule, and then choose **Transform an incoming claim**. Finally, choose **Next**.  
 ![](/.attachments/DK-LandingZone-ControlTower/worddav7fcd133233cf40d27caefc20340d3314.png)
  
On the **Configure Claim Rule** page, type the following settings, and choose **OK**, as shown in the following screenshot.

|   **Configuration Element**   |   **Value**   |
| --- | --- |
|   Claim rule name   |   Name ID   |
|   Incoming claim type   |   Windows account name   |
|   Outgoing claim type   |   Name ID   |
|   Outgoing name ID format   |   Persistent Identifier   |

   
 ![](/.attachments/DK-LandingZone-ControlTower/worddavc586eb24cde90445c056a48551ab6d15.png)
  
   
Choose **Add Rule** to configure the second rule, and then choose **Send LDAP Attributes as Claims**. Finally, choose **Next**.  
 ![](/.attachments/DK-LandingZone-ControlTower/worddavdd8e0de9e7c983bfe4e094583d28b3a0.png)
  
On the **Configure Claim Rule** page, type the following settings, and choose **OK**, as shown in the following screenshot.

|   **Configuration Element**   |   **Value**   |
| --- | --- |
|   Claim rule name   |   RoleSessionName   |
|   Attribute store   |   Active Directory   |
|   LDAP Attribute   |   SAM-Account-Name   |
|   Outgoing Claim Type   |   [https://aws.amazon.com/SAML/Attributes/RoleSessionName](https://aws.amazon.com/SAML/Attributes/RoleSessionName)   |

 ![](/.attachments/DK-LandingZone-ControlTower/worddavc720642e92490d89c12cc4bd4fb27a7e.png)
  
Choose **Add Rule** to configure the third rule, and then choose **Send claims using a custom rule**. Finally, choose **Next**.  
 ![](/.attachments/DK-LandingZone-ControlTower/worddav98bd3d7a798398f3dbea16bffe0b2901.png)

n the **Claim rule name** box, type **Get AD Groups**. In the **Custom rule** box, enter the following, and then choose **OK**.

 add(store = "Active Directory", types = ("http://temp/variable"), query = ";tokenGroups;{0}", param = c.Value);\]\]>

  
This custom rule uses a script in the claim rule language that retrieves all the groups the authenticated user is a member of and places them into a temporary claim named [{+}](http://temp/variable)[http://temp/variable+](http://temp/variable+). Think of this as a variable you can access later.  
**Note**: Ensure that there isn't any trailing whitespace, as this may cause unexpected results.  
 ![](/.attachments/DK-LandingZone-ControlTower/worddavb48e179844952cb622c3e8b272ae9540.png)
  
Choose **Add Rule** to configure the fourth and final rule. Then choose **Send claims using a custom rule**, and choose **Next**.  
 ![](/.attachments/DK-LandingZone-ControlTower/worddav98bd3d7a798398f3dbea16bffe0b2901.png)
  
In the **Claim rule name** box, type **Roles**. In the **Custom rule** box, enter the following, and then choose **OK**.

  

issue(Type = "https://aws.amazon.com/SAML/Attributes/Role", Value = RegExReplace(c.Value, "AWS-(\[^d\]{12})-(\\w\*)", "arn:aws:iam::$1:saml-provider/ADFS,arn:aws:iam::$1:role/ADFS-$2")); This custom rule uses regular expressions to transform each of the group memberships of the form AWS-\- into in the IAM role ARN, IAM federation provider ARN form AWS expects. It does so by matching the first pattern match (\\d{12}) to $1 and the second pattern match (\\w\*) to $2 for each entry in the temp variable.\]\]>

  
This custom rule uses regular expressions to transform each of the group memberships of the form **AWS-<Account Number>-<Role Name>** into in the IAM role ARN, IAM federation provider ARN form AWS expects. It does so by matching the first pattern match (\\d{12}) to $1 and the second pattern match (\\w\*) to $2 for each entry in the temp variable.  
This attribute makes better sense later in the exercise when you see it in action. For now, the key takeaway is that you are defining the resulting value for the AWS Role attribute in a dynamic way (by mapping group memberships) instead of a static way (by explicitly defining ARNs). This dynamic resolution allows the IdP configuration to scale to support virtually **any number** of AWS accounts and any number of IAM roles without further configuration.

Ensure that there isn't any trailing whitespace, as this may cause unexpected results.

  
 ![](/.attachments/DK-LandingZone-ControlTower/worddav471c568b0e313c9d60fdc4b1f54c31e2.png)
  
  
Choose **OK** to complete the **Edit Claim Rules** wizard.  
 ![](/.attachments/DK-LandingZone-ControlTower/worddavf7740c8573bba0486e1e23e49db126d8.png)

Create AD Groups for Each Role & Account 
=========================================

1.  For each AWS Account, capture the following information that will be needed to complete the federation setup. 
    1.  Account ID 
    2.  Staff that will be granted access to each role 
2.  Create one AD group for each of the roles that you want to grant access to on the target AWS Account. The default roles are: (see **Landing Zone IAM Roles Design**) 
    1.  Admin 
        1.  AWS-<Account Number>-Admin 
    2.  PowerUser 
        1.  AWS-<Account Number>-PowerUser 
    3.  ReadOnly 
        1.  AWS-<Account Number>-ReadOnly 
3.  Add the identified users to the AD Groups 

Understanding the AWS-<Account Number>-<Role Name> naming convention
--------------------------------------------------------------------

In the preceding section, we utilized a naming convention of AWS-<Account Number>-<Role Name> for the groups stored in Active Directory. To understand why this was chosen, we must first consider several aspects of how AWS environments are commonly segregated:

*   Most AWS customers use **multiple AWS accounts**. These accounts are organized using common dimensions (e.g. line of business, environment, application, etc) that are often combined. For example, one account might be used for Finance-Prod while another might be used for HR-NonProd.
*   Most AWS customers apply permissions based on the **organizational role** of the user. For example, an organization might have roles such as 'Developer,''ProductionSupport,''Engineering,' or 'Security.'
*   Most users have access only to a **subset** of their organization's AWS accounts. For example, if a developer is writing applications for the Finance department they will have access to the Finance-\* set of accounts, but not to the HR-\* set of accounts.
*   To apply **separation of duties**, most users have different roles in different accounts. For example, an individual may have a relatively powerful role (e.g. PowerUser) in a non-production account where they perform development work, but a more constrained role (e.g. ReadOnly) in a production account where they mainly access log files for debugging purposes.

The AWS-<Account Number>-<Role Name> naming convention was specifically formulated to provide a **best practice pattern** for group naming that was able to account for all the aspects identified above. While the specific set of dimensions an organization may choose to use for account segmentation or the specific set of named roles an organization may define will certainly vary from one organization to the next, this standard works in all known cases. We highly encourage you to use this pattern within your organization, as it has been proven across a large number of customer implementations at scale.

Configure Master Account 
=========================

Login to the Master AWS account using an IAM account with Admin permissions
---------------------------------------------------------------------------

1.  [https://My\_AWS\_Account\_ID.signin.aws.amazon.com/console/](https://My_AWS_Account_ID.signin.aws.amazon.com/console/+)

Customize the AWS account sign-in URL
-------------------------------------

This will enable the name of the account to show up on the ADFS federation page. 

1.  Go to IAM Service Dashboard
     ![](/.attachments/DK-LandingZone-ControlTower/image2017-11-12_10-13-24.png)
    
2.  Under IAM users sign-in link: select **Customize** 
     ![](/.attachments/DK-LandingZone-ControlTower/image2017-11-12_10-23-37.png)
    
3.  Type in the name of the Alias (e.g. acme-master, acme-sharedservices, acme-security, acme-dev, etc.)
     ![](/.attachments/DK-LandingZone-ControlTower/image2017-11-12_10-27-0.png)
    

Configure the IAM Identity Provider
-----------------------------------

This must be manually executed for each Landing Zone account due to CloudFormation not currently supporting the creation and management of IAM Identity Providers.  
This set of instructions covers configuring AWS to trust the authentication and authorization information it provides. During this process, you will provide AWS with the SAML metadata from your ADFS installation, which details all of the encryption and signing certificates that ADFS will use. This exchange provides the pre-established cryptographic trust needed for AWS to utilize the assertions generated by ADFS.   
To start this process, we need to configure an IAM Identity Provider within the AWS console. 

1.  Download IdP metadata 
    1.  [https://sts.acme.com/FederationMetadata/2007-06/FederationMetadata.xml](https://sts.acme.com/FederationMetadata/2007-06/FederationMetadata.xml)
2.  Go to IAM Service Dashboard
3.  Select **Idetity providers** from the left pane and then choose **Create Provider**.
     ![](/.attachments/DK-LandingZone-ControlTower/image2017-11-12_10-35-51.png)
    
4.  Enter the following values to configure the provider, and choose **Next Step**.
    
    |   Provider Type    |   SAML    |
    | --- | --- |
    |   Provider Name    |   ADFS    |
    |   Metadata Document    |   Browse to file downloaded in previous step.    |
    
     ![](/.attachments/DK-LandingZone-ControlTower/image2017-11-12_10-41-38.png)
    
5.  Verify the information is correct and then choose **Create** to create the identity provider. 
    
     ![](/.attachments/DK-LandingZone-ControlTower/image2017-11-12_10-42-17.png)
     
6.  The banner at the top of the screen provides confirmation that your identity provider was successfully created. 
     ![](/.attachments/DK-LandingZone-ControlTower/image2017-11-12_10-54-19.png)
    

Create AWS IAM Roles for IdP access 
------------------------------------

This should be automated via the IAM CF Template for each Landing Zone account. [http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-iam-role.html](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-iam-role.html+)

  
In our final step before initial testing, we need to create a set of IAM roles that correspond one to one to the directory groups we populated earlier in the exercise. These roles will be named such that their resulting ARNs will match the regular expression transformation we configured in AD FS earlier. 

1.  Go to IAM in the AWS Console
2.  Select **Roles** from the left pane and then choose **Create role**.
     ![](/.attachments/DK-LandingZone-ControlTower/image2017-11-12_10-15-22.png)
    
3.  Select **SAML 2.0 federation** under **Select type of trusted entity**. 
     ![](/.attachments/DK-LandingZone-ControlTower/image2017-11-12_10-18-7.png)
    
4.  Set the **SAML provider** to **ADFS** using the drop-down list menu. This configuration defines the specific federation provider that provides authentication and authorization into the role. 
5.  Review the role trust policy (no changes required) and choose **Next Step** to continue. 
6.  Select "Allow programmatic and AWS Management Console Access
     ![](/.attachments/DK-LandingZone-ControlTower/image2017-11-12_10-59-58.png)
    
7.  Choose **Next: Permissions**
8.  Select the **_ReadOnlyAccess_** policy. 
    1.  **Note:** The policy that you attach here specifically controls the AWS actions that the federated user is authorized to perform.
     ![](/.attachments/DK-LandingZone-ControlTower/image2017-11-12_10-6-50.png)
    
9.  Set the Role Name to **ADFS-ReadOnly**. 
     ![](/.attachments/DK-LandingZone-ControlTower/image2017-11-12_11-7-48.png)
    
10.  Finally, repeat the entire sequence of the preceding steps for the following two additional roles.
    1.  **ADFS-PowerUser (Policy: PowerUserAccess)** 
    2.  **ADFS-Admin (Policy: AdministratorAccess)** 

Configure Other Landing Zone Accounts
=====================================

Execute the following steps on each of the remaining Landing Zone accounts. 

1.  Login to the Master AWS account using Federated Login
    1.  [https://sts.acme.com/adfs/ls/IdpInitiatedSignOn.aspx?loginToRp=urn:amazon:webservices](https://sts.acme.com/adfs/ls/IdpInitiatedSignOn.aspx?loginToRp=urn:amazon:webservices+)
2.  Switch Role to the target AWS Account by clicking on the following and selecting Switch Role. 
    1.   Fill in the form using the following information: 
        1.  Account ID 
        2.  Role: OrganizationAccountAccessRole (this is the role created in each account that has been added to an AWS Organization)
3.  Customize the AWS account sign-in URL (See instructions above)
4.  Configure the IAM Identity Provider (See instructions above)
5.  Create AWS IAM Roles for IdP access (See instructions above)
6.  Test federating to the account via all defined roles
    1.  [https://sts.acme.com/adfs/ls/IdpInitiatedSignOn.aspx?loginToRp=urn:amazon:webservices](https://sts.acme.com/adfs/ls/IdpInitiatedSignOn.aspx?loginToRp=urn:amazon:webservices+)

Troubleshoot SAML Assertion Errors
==================================

Use a SAML Playground/diagnostics tool to troubleshoot SAML assertion errors.

Federated CLI Setup for Administrators that have a Windows Workstation
======================================================================

Setup the AWS Tools for Windows PowerShell
------------------------------------------

Follow the instructions on the following page. [http://docs.aws.amazon.com/powershell/latest/userguide/pstools-getting-set-up.html](http://docs.aws.amazon.com/powershell/latest/userguide/pstools-getting-set-up.html+)  
Information on managing profiles can be found here.  [http://docs.aws.amazon.com/powershell/latest/userguide/specifying-your-aws-credentials.html](http://docs.aws.amazon.com/powershell/latest/userguide/specifying-your-aws-credentials.html+)

Copy and Modify the following PowerShell Script
-----------------------------------------------

/adfs/ls/IdpInitiatedSignOn.aspx?loginToRp=urn:amazon:webservices" $epName = Set-AWSSamlEndpoint -Endpoint $endpoint -StoreAs ADFS -AuthenticationType Negotiate Set-AWSSamlRoleProfile -StoreAs IWA -EndpointName $epName Get-AWSPowerShellVersion Set-AWSCredentials -ProfileName IWA Set-DefaultAWSRegion -Region us-east-1 Get-S3Bucket\]\]>

  

/adfs/ls/IdpInitiatedSignOn.aspx?loginToRp=urn:amazon:webservices" $credential = Get-Credential -Message "Enter the domain credentials for the endpoint" $epName = Set-AWSSamlEndpoint -Endpoint $endpoint -StoreAs ADFS -AuthenticationType Negotiate Set-AWSSamlRoleProfile -EndpointName $epName -NetworkCredential $credential -StoreAs IWA Set-AWSCredentials -ProfileName IWA Set-DefaultAWSRegion -Region us-east-1 Get-S3Bucket \]\]>

  

/adfs/ls/IdpInitiatedSignOn.aspx?loginToRp=urn:amazon:webservices" $credential = Get-Credential -Message "Enter the domain credentials for the endpoint" $epName = Set-AWSSamlEndpoint -Endpoint $endpoint -StoreAs ADFS -AuthenticationType Negotiate $epName | Set-AWSSamlRoleProfile -NetworkCredential $credential \` -PrincipalARN "arn:aws:iam::012345678912:saml-provider/ADFS" \` -RoleARN "arn:aws:iam::012345678912:role/ADFS-ReadOnly" \` -StoreAs IWA Set-AWSCredentials -ProfileName IWA Set-DefaultAWSRegion -Region us-east-1 Get-S3Bucket \]\]>

Federated CLI Setup for Administrators that have an OSX or Linux Workstation
============================================================================

Install AWS CLI
---------------

OSX

[http://docs.aws.amazon.com/cli/latest/userguide/cli-install-macos.html](http://docs.aws.amazon.com/cli/latest/userguide/cli-install-macos.html)

LInux

[http://docs.aws.amazon.com/cli/latest/userguide/awscli-install-linux.html](http://docs.aws.amazon.com/cli/latest/userguide/awscli-install-linux.html)

Copy and Modify one of the following Python Scripts
---------------------------------------------------

### Python 3.x

/adfs/ls/IdpInitiatedSignOn.aspx?loginToRp=urn:amazon:webservices' # Uncomment to enable low level debugging #logging.basicConfig(level=logging.DEBUG) ########################################################################## # Get the federated credentials from the user print ('') username = input("Username: ") password = getpass.getpass() print ('') # Initiate session handler session = requests.Session() # Programmatically get the SAML assertion # Opens the initial IdP url and follows all of the HTTP302 redirects, and # gets the resulting login page formresponse = session.get(idpentryurl, verify=sslverification) # Capture the idpauthformsubmiturl, which is the final url after all the 302s idpauthformsubmiturl = formresponse.url # Parse the response and extract all the necessary values # in order to build a dictionary of all of the form values the IdP expects formsoup = BeautifulSoup(formresponse.text, 'html5lib') payload = {} for inputtag in formsoup.find\_all(re.compile('(INPUT|input)')): name = inputtag.get('name','') value = inputtag.get('value','') if "user" in name.lower(): #Make an educated guess that this is the right field for the username payload\[name\] = username elif "email" in name.lower(): #Some IdPs also label the username field as 'email' payload\[name\] = username elif "pass" in name.lower(): #Make an educated guess that this is the right field for the password payload\[name\] = password else: #Simply populate the parameter with the existing value (picks up hidden fields in the login form) payload\[name\] = value # Debug the parameter payload if needed # Use with caution since this will print sensitive output to the screen #print (payload) # Some IdPs don't explicitly set a form action, but if one is set we should # build the idpauthformsubmiturl by combining the scheme and hostname # from the entry url with the form action target # If the action tag doesn't exist, we just stick with the # idpauthformsubmiturl above for inputtag in formsoup.find\_all(re.compile('(FORM|form)')): action = inputtag.get('action') loginid = inputtag.get('id') if (action and loginid == "loginForm"): parsedurl = urlparse(idpentryurl) idpauthformsubmiturl = parsedurl.scheme + "://" + parsedurl.netloc + action # Performs the submission of the IdP login form with the above post data response = session.post( idpauthformsubmiturl, data=payload, verify=sslverification) # Debug the response if needed #print (response.text) # Overwrite and delete the credential variables, just for safety username = '##############################################' password = '##############################################' del username del password # Decode the response and extract the SAML assertion soup = BeautifulSoup(response.text, 'html5lib') assertion = '' # Look for the SAMLResponse attribute of the input tag (determined by # analyzing the debug print lines above) for inputtag in soup.find\_all('input'): if(inputtag.get('name') == 'SAMLResponse'): #print(inputtag.get('value')) assertion = inputtag.get('value') # Better error handling is required for production use. if (assertion == ''): #TODO: Insert valid error checking/handling print ('Response did not contain a valid SAML assertion') sys.exit(0) # Debug only # print(base64.b64decode(assertion)) # Parse the returned assertion and extract the authorized roles awsroles = \[\] root = ET.fromstring(base64.b64decode(assertion)) for saml2attribute in root.iter('{urn:oasis:names:tc:SAML:2.0:assertion}Attribute'): if (saml2attribute.get('Name') == 'https://aws.amazon.com/SAML/Attributes/Role'): for saml2attributevalue in saml2attribute.iter('{urn:oasis:names:tc:SAML:2.0:assertion}AttributeValue'): awsroles.append(saml2attributevalue.text) # Note the format of the attribute value should be role\_arn,principal\_arn # but lots of blogs list it as principal\_arn,role\_arn so let's reverse # them if needed for awsrole in awsroles: chunks = awsrole.split(',') if'saml-provider' in chunks\[0\]: newawsrole = chunks\[1\] + ',' + chunks\[0\] index = awsroles.index(awsrole) awsroles.insert(index, newawsrole) awsroles.remove(awsrole) # If I have more than one role, ask the user which one they want, # otherwise just proceed print ("") if len(awsroles) > 1: i = 0 print ("Please choose the role you would like to assume:") for awsrole in awsroles: print ('\[', i, '\]: ', awsrole.split(',')\[0\]) i += 1 selectedroleindex = input ("Selection: ") # Basic sanity check of input if int(selectedroleindex) > (len(awsroles) - 1): print ('You selected an invalid role index, please try again') sys.exit(0) role\_arn = awsroles\[int(selectedroleindex)\].split(',')\[0\] principal\_arn = awsroles\[int(selectedroleindex)\].split(',')\[1\] else: role\_arn = awsroles\[0\].split(',')\[0\] principal\_arn = awsroles\[0\].split(',')\[1\] # Use the AWS STS token to list all of the S3 buckets session = boto3.client('sts', region\_name=region) # Use the assertion to get an AWS STS token using Assume Role with SAML token = session.assume\_role\_with\_saml(RoleArn=role\_arn, PrincipalArn=principal\_arn, SAMLAssertion=assertion) # Write the AWS STS token into the AWS credential file home = expanduser("~") filename = home + awsconfigfile # Read in the existing config file config = configparser.RawConfigParser() config.read(filename) # Put the credentials into a saml specific section instead of clobbering # the default credentials if not config.has\_section('saml'): config.add\_section('saml') config.set('saml', 'output', outputformat) config.set('saml', 'region', region) config.set('saml', 'aws\_access\_key\_id', token\['Credentials'\]\['AccessKeyId'\]) config.set('saml', 'aws\_secret\_access\_key', token\['Credentials'\]\['SecretAccessKey'\]) config.set('saml', 'aws\_session\_token', token\['Credentials'\]\['SessionToken'\]) # Write the updated config file with open(filename, 'w+') as configfile: config.write(configfile) # Give the user some basic info as to what has just happened print ('\\n\\n----------------------------------------------------------------') print ('Your new access key pair has been stored in the AWS configuration file {0} under the saml profile.'.format(filename)) print ('Note that it will expire at {0}.'.format(token\['Credentials'\]\['Expiration'\])) print ('After this time, you may safely rerun this script to refresh your access key pair.') print ('To use this credential, call the AWS CLI with the --profile option (e.g. aws --profile saml ec2 describe-instances).') print ('----------------------------------------------------------------\\n\\n') # Use the AWS STS token to list all of the S3 buckets s3conn = boto3.client('s3', aws\_access\_key\_id=token\['Credentials'\]\['AccessKeyId'\], aws\_secret\_access\_key=token\['Credentials'\]\['SecretAccessKey'\], aws\_session\_token=token\['Credentials'\]\['SessionToken'\]) buckets = s3conn.list\_buckets() #for debug #print(buckets) print ("") print ('Simple API example listing all s3 buckets:') for bucket in buckets\["Buckets"\]: print (bucket\['Name'\]) print ("")\]\]>

### Python 2.x

 1: i = 0 print "Please choose the role you would like to assume:" for awsrole in awsroles: print '\[', i, '\]: ', awsrole.split(',')\[0\] i += 1 print "Selection: ", selectedroleindex = raw\_input() # Basic sanity check of input if int(selectedroleindex) > (len(awsroles) - 1): print 'You selected an invalid role index, please try again' sys.exit(0) role\_arn = awsroles\[int(selectedroleindex)\].split(',')\[0\] principal\_arn = awsroles\[int(selectedroleindex)\].split(',')\[1\] else: role\_arn = awsroles\[0\].split(',')\[0\] principal\_arn = awsroles\[0\].split(',')\[1\] # Use the assertion to get an AWS STS token using Assume Role with SAML conn = boto.sts.connect\_to\_region(region) token = conn.assume\_role\_with\_saml(role\_arn, principal\_arn, assertion) # Write the AWS STS token into the AWS credential file home = expanduser("~") filename = home + awsconfigfile # Read in the existing config file config = ConfigParser.RawConfigParser() config.read(filename) # Put the credentials into a saml specific section instead of clobbering # the default credentials if not config.has\_section('saml'): config.add\_section('saml') config.set('saml', 'output', outputformat) config.set('saml', 'region', region) config.set('saml', 'aws\_access\_key\_id', token.credentials.access\_key) config.set('saml', 'aws\_secret\_access\_key', token.credentials.secret\_key) config.set('saml', 'aws\_session\_token', token.credentials.session\_token) # Write the updated config file with open(filename, 'w+') as configfile: config.write(configfile) # Give the user some basic info as to what has just happened print '\\n\\n----------------------------------------------------------------' print 'Your new access key pair has been stored in the AWS configuration file {0} under the saml profile.'.format(filename) print 'Note that it will expire at {0}.'.format(token.credentials.expiration) print 'After this time, you may safely rerun this script to refresh your access key pair.' print 'To use this credential, call the AWS CLI with the --profile option (e.g. aws --profile saml ec2 describe-instances).' print '----------------------------------------------------------------\\n\\n' # Use the AWS STS token to list all of the S3 buckets s3conn = boto.s3.connect\_to\_region(region, aws\_access\_key\_id=token.credentials.access\_key, aws\_secret\_access\_key=token.credentials.secret\_key, security\_token=token.credentials.session\_token) buckets = s3conn.get\_all\_buckets() print 'Simple API example listing all S3 buckets:' print(buckets) \]\]>

  

References
==========

SEC306: Choose Your Own SAML Adventure
--------------------------------------

[http://federationworkshopreinvent2016.s3-website-us-east-1.amazonaws.com/labguides/adfshour1/labguide-adfshour1.html](http://federationworkshopreinvent2016.s3-website-us-east-1.amazonaws.com/labguides/adfshour1/labguide-adfshour1.html)

Federating to a Single AWS Account
----------------------------------

[https://aws.amazon.com/blogs/security/enabling-federation-to-aws-using-windows-active-directory-adfs-and-saml-2-0/](https://aws.amazon.com/blogs/security/enabling-federation-to-aws-using-windows-active-directory-adfs-and-saml-2-0/)

Federating to Multiple AWS Accounts
-----------------------------------

[https://aws.amazon.com/blogs/security/how-to-set-up-sso-to-the-aws-management-console-for-multiple-accounts-by-using-ad-fs-and-saml-2-0/](https://aws.amazon.com/blogs/security/how-to-set-up-sso-to-the-aws-management-console-for-multiple-accounts-by-using-ad-fs-and-saml-2-0/)

PowerShell Scripts from the Multiple AWS Accounts article
---------------------------------------------------------

[https://s3.amazonaws.com/awsiammedia/public/sample/ADFSMultiAccount/AWS.ADFS.PowerShell.zip](https://s3.amazonaws.com/awsiammedia/public/sample/ADFSMultiAccount/AWS.ADFS.PowerShell.zip)

 **Attachments:** 


[image2017-11-12_10-13-24.png](/.attachments/DK-LandingZone-ControlTower/image2017-11-12_10-13-24.png)

[image2017-11-12_10-15-22.png](/.attachments/DK-LandingZone-ControlTower/image2017-11-12_10-15-22.png)

[image2017-11-12_10-18-7.png](/.attachments/DK-LandingZone-ControlTower/image2017-11-12_10-18-7.png)

[image2017-11-12_10-23-37.png](/.attachments/DK-LandingZone-ControlTower/image2017-11-12_10-23-37.png)

[image2017-11-12_10-27-0.png](/.attachments/DK-LandingZone-ControlTower/image2017-11-12_10-27-0.png)

[image2017-11-12_10-35-51.png](/.attachments/DK-LandingZone-ControlTower/image2017-11-12_10-35-51.png)

[image2017-11-12_10-37-46.png](/.attachments/DK-LandingZone-ControlTower/image2017-11-12_10-37-46.png)

[image2017-11-12_10-4-5.png](/.attachments/DK-LandingZone-ControlTower/image2017-11-12_10-4-5.png)

[image2017-11-12_10-41-38.png](/.attachments/DK-LandingZone-ControlTower/image2017-11-12_10-41-38.png)

[image2017-11-12_10-42-17.png](/.attachments/DK-LandingZone-ControlTower/image2017-11-12_10-42-17.png)

[image2017-11-12_10-54-19.png](/.attachments/DK-LandingZone-ControlTower/image2017-11-12_10-54-19.png)

[image2017-11-12_10-59-58.png](/.attachments/DK-LandingZone-ControlTower/image2017-11-12_10-59-58.png)

[image2017-11-12_10-6-50.png](/.attachments/DK-LandingZone-ControlTower/image2017-11-12_10-6-50.png)

[image2017-11-12_11-7-48.png](/.attachments/DK-LandingZone-ControlTower/image2017-11-12_11-7-48.png)

[worddav1a654cab0051793d6bbf7bae24e823c0.png](/.attachments/DK-LandingZone-ControlTower/worddav1a654cab0051793d6bbf7bae24e823c0.png)

[worddav263d72c33bdad28c34cff8093481efb1.png](/.attachments/DK-LandingZone-ControlTower/worddav263d72c33bdad28c34cff8093481efb1.png)

[worddav471c568b0e313c9d60fdc4b1f54c31e2.png](/.attachments/DK-LandingZone-ControlTower/worddav471c568b0e313c9d60fdc4b1f54c31e2.png)

[worddav7fcd133233cf40d27caefc20340d3314.png](/.attachments/DK-LandingZone-ControlTower/worddav7fcd133233cf40d27caefc20340d3314.png)

[worddav81822fd08883c1c5b2725b40ca4f0056.png](/.attachments/DK-LandingZone-ControlTower/worddav81822fd08883c1c5b2725b40ca4f0056.png)

[worddav98bd3d7a798398f3dbea16bffe0b2901.png](/.attachments/DK-LandingZone-ControlTower/worddav98bd3d7a798398f3dbea16bffe0b2901.png)

[worddavb48e179844952cb622c3e8b272ae9540.png](/.attachments/DK-LandingZone-ControlTower/worddavb48e179844952cb622c3e8b272ae9540.png)

[worddavc4727d69a0f2883a01aea7cc3ef42ecc.png](/.attachments/DK-LandingZone-ControlTower/worddavc4727d69a0f2883a01aea7cc3ef42ecc.png)

[worddavc586eb24cde90445c056a48551ab6d15.png](/.attachments/DK-LandingZone-ControlTower/worddavc586eb24cde90445c056a48551ab6d15.png)

[worddavc720642e92490d89c12cc4bd4fb27a7e.png](/.attachments/DK-LandingZone-ControlTower/worddavc720642e92490d89c12cc4bd4fb27a7e.png)

[worddavd3d94017e489772c4b43dd983f79abaf.png](/.attachments/DK-LandingZone-ControlTower/worddavd3d94017e489772c4b43dd983f79abaf.png)

[worddavdd8e0de9e7c983bfe4e094583d28b3a0.png](/.attachments/DK-LandingZone-ControlTower/worddavdd8e0de9e7c983bfe4e094583d28b3a0.png)

[worddavf7740c8573bba0486e1e23e49db126d8.png](/.attachments/DK-LandingZone-ControlTower/worddavf7740c8573bba0486e1e23e49db126d8.png)
