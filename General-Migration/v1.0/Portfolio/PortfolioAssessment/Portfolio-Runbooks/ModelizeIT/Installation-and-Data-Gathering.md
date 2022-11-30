[[_TOC_]]

  

Typical installation steps are documented below. Detailed documentation can be found on the modelizeIT website located [here](https://www.modelizeit.com/documentation/toc.html).

Project configuration and initiation
------------------------------------

With the execution of a PO to modelizeIT, they will provide you links to the remote Gatherer and Rejuvenaptor(processing engine). These links follow the format:

Gatherer: https://saas19.aws.modelizeit.com/<<Customer>>**G**

Rejuvenaptor: https://saas19.aws.modelizeit.com/<<Customer>>**R**

They will also provide you with a link to the software download for a Linux or Windows installation of the local (On-Prem) Gatherer. Deploying multiple local gatherers is ideal for highly segmented environments.

ModelizeIT license is validated by the Analysis server or, if network access is not permitted, can be bound to the specific on-prem host.

Installation of Gatherer Servers
--------------------------------

### Pre-requisites

The following pre-requisites should be full filled before starting the installation.

-  Server for Installation of Gatherer server. (Windows 2019, 2 vCPUs and 8GB of RAM are recommended) with 50MB of free disk space per in-scope server (Target server) -  Chrome browser is installed on the Gatherer server (will work with other browsers but can have small issues). -  User with Admin privileges on the Gatherer server (usually domain Admin) -  List of Target servers with OS type (Windows, Linux, Unix, etc.) -  User with Administrator rights to execute local commands on Windows Target servers -  Root user or user that is allowed to execute commands via sudo \* on Linux Target servers -  If the Target server list has Windows 2000 or Windows 2003 workloads then SMB v1 must be enabled. -  Ports to be open -  Gatherer to ModelizeIT (SaaS) server: 443 -  Gatherer server to Windows Target Server: 139,445 -  Gatherer server to Linux Target Server: 22 or other ssh port -  Antivirus exceptions -  Gatherer server: allow "C:\\modelizeIT\\lib\\Gatherer.exe" and  "C:\\modelizeIT\\lib\\plink.exe" -  On Windows Target servers: Allow %WINDOWS%\\ADG-discover.exe, %WINDOWS%\\ADG-discover.js and "Application Data Gatherer Service" -  tar.exe is available on the Gatherer server. (if not then install 7zip and create a tar.exe file in the C:\\Windows with content pointing to the 7Zip such as "C:\\Program Files\\7Zip\\7za.exe" a %1 %2 >NUL )

If needed, you can reference sample data collection files (.out) for [Windows](https://www.modelizeit.com/documentation/examples/ADG-SCEX01-1606220853.out.zip), [Linux](https://www.modelizeit.com/documentation/examples/ADG-ip-10-0-0-129-1609030220.out.zip), and [Solaris](https://www.modelizeit.com/documentation/examples/ADG-sun26-2103172306.out.zip). 

### Installation Steps

| Install Steps |
| --- |
|   Login to the Gatherer server and download the Installation file.   |
|   Unzip the installer to c:\\ , the folder should look like c:\\modelizeIT\\bin folder with 3 executables   ![](/.attachments/DK-Portfolio/Screenshot%202021-08-09%20at%2008.19.56.png)  |
| Ensure to provide access to the folder and all the folders underneath it. |
|   Open Cmd as Admin, navigate to the C:\\modelizeIT\\bin folder and run InstallRegKey.cmd script.  (If prompted then select Yes, not prompted the first time)   ![](/.attachments/DK-Portfolio/Screenshot%202021-08-09%20at%2008.21.56.png)  |
|   In the same location C:\\modelizeIT\\bin run the Gatherer-UI.cmd script   ![](/.attachments/DK-Portfolio/Screenshot%202021-08-09%20at%2008.24.27.png)    |
| Verify in the Cmd that the port used is 8880 and then open  localhost:8880 in Chrome |
| Login with the default user and password, provided by ModelizeIT. The user name is case sensitive. |
| The user will be logged in to the UI User page and prompted to change the default password. |
| Thereafter logout and login again with the new password. |
|   Additional users can be created by clicking on the top right section.   ![](/.attachments/DK-Portfolio/Screenshot%202021-08-09%20at%2008.38.01.png)  It is recommended to add Superusers for the users administering the system. Additional users will require a valid and working email (where MFA code will be sent).  The default user can be deleted, once the Superusers have been created.      |
| In case of unexpected behaviour observe the CMD running Gatherer-UI.cmd where the errors will be logged. |

### Testing connection to Target servers

It is recommended to test the connectivity to the Target servers before proceeding to execution of data collector scripts.

  

| Test Steps |
| --- |
| Ensure that Gatherer-UI cmd is running, and then login to the Gatherer UI (localhost:8880). When logging in, a MFA will be sent to email. This MFA is valid for 7 days, so you will need to keep the email or otherwise remember the code. |
|   You will be logged in to the Application Data Gathering Job Manager page. On this page click on Add button for jobs and then Edit Targets Icon to create a new Target List   ![](/.attachments/DK-Portfolio/Screenshot%202021-08-09%20at%2009.35.32.png)    |
|   Create a new Target List with a valid Name and hostnames or IP addresses for Contents. Multiple hostnames/IP addresses can be added with comma separations or as new lines. Click Submit and go back to Jobs Page.  Note: the first time you do this, keep the number of servers small (2 - 5) to expedite the tests. You will create individual target lists based on OS (i.e. a Windows list, a Linux list, etc.). Target lists should also be limited to ~100 servers to expedite troubleshooting.    ![](/.attachments/DK-Portfolio/Screenshot%202021-08-09%20at%2009.39.32.png)    |
|   Click on the edit icon to create Parameters used to connect to the Target list created earlier.   ![](/.attachments/DK-Portfolio/Screenshot%202021-08-09%20at%2009.45.46.png)    |
|   The Parameter are the secret credential that will be used to connect to the Target Servers. Click Submit and then return to Jobs Page.  Parameters are not needed for windows server discovery if the logged in user on the gatherer has administrative permissions to the targets.   Parameters are always needed for Linux and Unix discovery.  If the ssh credentials require a .ppk/.pem file it can be stored in C:\\modelizeIT\\data\\localhost\\SECRETS\\_secret\_name_.ppk where "secret\_name" matches what you enter in the UI.    ![](/.attachments/DK-Portfolio/Screenshot%202021-08-09%20at%2009.49.43.png)    |
|   Open a new CMD and ensure that c:/modelizeIT/bin/Gatherer-JobRunner.cmd is running in the CMD.  To simplify discovery, this should be run as a domain admin user so credentials are not needed for Windows servers.  If you see any error messages the license may not have been validated, ensure the gatherer has network access to the SaaS server or update.modelizeIT.com to validate the license.    |
|   Log back to the browser localhost:8880 and create a Job of Type: "Test connectivity" with the defined Target list and the Parameters.  ![](/.attachments/DK-Portfolio/Screenshot%202021-08-09%20at%2009.50.56.png)      |
| Wait till the job completes and then review the result. You might have to refresh the page to get the latest Status. Once the status is Finished, view the LOG to see the results. |

### Data Gathering

| Install Steps |
| --- |
| Ensure that Gatherer-UI cmd and Gatherer-JobRunner are running, and then login to the Gatherer UI (localhost:8880).   |
|   Create a new job of the Type: Application Data Gathering and using the Targets and Parameters used for connectivity testing.  ![](/.attachments/DK-Portfolio/Screenshot%202021-08-18%20at%2000.08.05.png)      |
|   Choose Schedule Now and click Submit. Wait till the job completes and then review the result. You might have to refresh the page to get the latest Status.  Once the status is STARTED you can view the Log to see the results or if there were any errors connecting to servers.   ![](/.attachments/DK-Portfolio/Screenshot%202021-08-18%20at%2000.12.28.png)    |
|   In case of error messages in Logs refer to : [https://www.modelizeit.com/documentation/ADC-Messages.html](https://www.modelizeit.com/documentation/ADC-Messages.html) to get more details.  The job will run and stop in 7 days by default.   |

  

### Auto Upload to Gatherer SaaS server

| Install Steps |
| --- |
|   Logon to SaaS Analysis server (RejuvenApptor) and create an "Upload only" user.    ![](/.attachments/DK-Portfolio/Screenshot%202021-08-18%20at%2016.48.18.png)    |
|   Log back on to the On premise "Gatherer server" and switch to Dashboard and click on Parameters to create a new Secret Key.   ![](/.attachments/DK-Portfolio/Screenshot%202021-08-19%20at%2010.56.05.png)    |
|   Create a new Secrets of the type "BASIC" and with the username and password of the Upload Only user created earlier in SaaS Analysis server.   ![](/.attachments/DK-Portfolio/Screenshot%202021-08-19%20at%2011.20.36.png)    |
|   Open the Gatherer-JobRunner.cmd (usually located in C:\\modelizeIT\\bin\\Gatherer-Jobrunner.cmd) and add additional parameter with the Secret Key created in the previous step and the SaaS Gatherer link.  (The SaaS gatherer link is ending with G instead of R)  \--upload <Secret Key>@[https://example.modelizeIT.com/.12345G](https://example.modelizeIT.com/.12345G)  Add the maximum number of threads that will be uploading files to the SaaS App  \--run-parser 4   ![](/.attachments/DK-Portfolio/Screenshot%202021-08-19%20at%2012.00.47.png)  Save and restart the Gatherer-JobRunner.cmd     |

  

### Uploading manually collected data

In some instances it is not possible to reach the servers through the Gatherer server and then the scripts for data collection need to be run manually on those Target machines. The scripts to run on the target machines will be supplied by ModelizeIT based on the operating system.

**Linux Install**

| Install Steps |
| --- |
| Identify a directory with at least 100MB available for temp and output files (usually less than 5MB is necessary but up to 100MB may be required for some servers). This directory can be an NFS-mount. cd to this directory.  |
| Put the following script <ADG-discover.bin> on this location |
| chmod +x <ADG-discover.bin> |
| run "nohup <ADG-discover.bin> &" |
| After 7 days (default 7, can be changed if needed) an output file will be generated in the current directory called <ADG-hostname-timestamp.out> |
| Zip the file and then move it to a server or local terminal where internet access is available. |
|   Logon to the SaaS Gatherer server  ([https://example.modelizeIT.com/.12345G](https://example.modelizeIT.com/.12345G)) and create a job of type "Upload manually collected files". Select the file or multiple files and click "Upload"   ![](/.attachments/DK-Portfolio/Screenshot%202021-08-19%20at%2015.31.45.png)    |
| It is also possible to configure the Gatherer installed on the on-premise server to send the output files automatically. If so configured then the output files should be placed in the location specified in the configuration and then the file will be uploaded automatically. (location example: C:\\modelizeIT\\data\\localhost\\UPLOADS\\news\\) |
| It is possible to kill the script (by restarting the server or manually). The partial outputted files can still be uploaded. |

  

**Windows Install**

| Install Steps |
| --- |
| Identify a directory with at least 100MB available for temp and output files (usually less than 5MB is necessary but up to 100MB may be required for some servers).  |
| Place the script for discovery <ADG-discover.exe> on the directory and run the script as Administrator. Do not logout of the server. |
| After 7 days (default 7, can be changed if needed) an output file will be generated in the current directory called <ADG-hostname-timestamp.out> |
| Zip the file and then move it to a server or local terminal where internet access is available. |
|   Logon to the SaaS Gatherer server  ([https://example.modelizeIT.com/.12345G](https://example.modelizeIT.com/.12345G)) and create a job of type "Upload manually collected files". Select the file or multiple files and click "Upload"   ![](/.attachments/DK-Portfolio/Screenshot%202021-08-19%20at%2015.31.45.png)    |
| It is also possible to configure the Gatherer installed on the on-premise server to send the output files automatically. If so configured then the output files should be placed in the location specified in the configuration and then the file will be uploaded automatically. (location example: C:\\modelizeIT\\data\\localhost\\UPLOADS\\news\\) |
| It is possible to kill the script (by logging out or restarting the server or manually). The partial outputted files can still be uploaded. |

  

**VMware Inventory**

| Hypervisor Inventory Ingestion |
| --- |
| Use RVTools to export to .xls |
| Manually upload the .xls to the analysis server via a manual file upload job. Reference [ModelizeIT documentation](https://www.modelizeit.com/documentation/ADC-Upload-OUT.html). |

  

**Other Imports Available**

ModelizeIT can also accept load balancer configuration information. See the online documentation for [F5 load balancers](https://www.modelizeit.com/documentation/ADC-from-F5.html) as well as [NetScaler Load Balancers](https://www.modelizeit.com/documentation/ADC-from-NS.html).

 **Attachments:** 


[Screenshot%202021-08-09%20at%2008.19.56.png](/.attachments/DK-Portfolio/Screenshot%202021-08-09%20at%2008.19.56.png)

[Screenshot%202021-08-09%20at%2008.21.56.png](/.attachments/DK-Portfolio/Screenshot%202021-08-09%20at%2008.21.56.png)

[Screenshot%202021-08-09%20at%2008.24.27.png](/.attachments/DK-Portfolio/Screenshot%202021-08-09%20at%2008.24.27.png)

[Screenshot%202021-08-09%20at%2008.38.01.png](/.attachments/DK-Portfolio/Screenshot%202021-08-09%20at%2008.38.01.png)

[Screenshot%202021-08-09%20at%2009.31.08.png](/.attachments/DK-Portfolio/Screenshot%202021-08-09%20at%2009.31.08.png)

[Screenshot%202021-08-09%20at%2009.35.32.png](/.attachments/DK-Portfolio/Screenshot%202021-08-09%20at%2009.35.32.png)

[Screenshot%202021-08-09%20at%2009.39.32.png](/.attachments/DK-Portfolio/Screenshot%202021-08-09%20at%2009.39.32.png)

[Screenshot%202021-08-09%20at%2009.45.46.png](/.attachments/DK-Portfolio/Screenshot%202021-08-09%20at%2009.45.46.png)

[Screenshot%202021-08-09%20at%2009.49.43.png](/.attachments/DK-Portfolio/Screenshot%202021-08-09%20at%2009.49.43.png)

[Screenshot%202021-08-09%20at%2009.50.56.png](/.attachments/DK-Portfolio/Screenshot%202021-08-09%20at%2009.50.56.png)

[Screenshot%202021-08-18%20at%2000.08.05.png](/.attachments/DK-Portfolio/Screenshot%202021-08-18%20at%2000.08.05.png)

[Screenshot%202021-08-18%20at%2000.12.28.png](/.attachments/DK-Portfolio/Screenshot%202021-08-18%20at%2000.12.28.png)

[Screenshot%202021-08-18%20at%2016.48.18.png](/.attachments/DK-Portfolio/Screenshot%202021-08-18%20at%2016.48.18.png)

[Screenshot%202021-08-19%20at%2010.56.05.png](/.attachments/DK-Portfolio/Screenshot%202021-08-19%20at%2010.56.05.png)

[Screenshot%202021-08-19%20at%2011.20.36.png](/.attachments/DK-Portfolio/Screenshot%202021-08-19%20at%2011.20.36.png)

[Screenshot%202021-08-19%20at%2012.00.47.png](/.attachments/DK-Portfolio/Screenshot%202021-08-19%20at%2012.00.47.png)

[Screenshot%202021-08-19%20at%2015.30.58.png](/.attachments/DK-Portfolio/Screenshot%202021-08-19%20at%2015.30.58.png)

[Screenshot%202021-08-19%20at%2015.31.26.png](/.attachments/DK-Portfolio/Screenshot%202021-08-19%20at%2015.31.26.png)

[Screenshot%202021-08-19%20at%2015.31.45.png](/.attachments/DK-Portfolio/Screenshot%202021-08-19%20at%2015.31.45.png)
