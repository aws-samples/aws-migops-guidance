  

[[_TOC_]]

Data analysis involves several steps depending on the desired outcomes. ModelizeIT does not produce cost/business case information and needs to be utilized in conjunction with a tool such as MPA to produce pricing-related data. An export to MPA requires just a few clicks and details are provided below.

**Important**: The analysis server must be restarted to include new data collected since the last restart. To restart the analysis server, go to [https://example.aws.modelizeit.com/.custmrG/](https://saas19.aws.modelizeit.com/.abbdapG/) making sure the "G" is at the end and replacing with your instance url, then click on "Reload".

  

Inventory Analysis
------------------

The Capacity Plan report lists all the servers and metadata related to the servers in a single report. The capacity plan data can be exported into a CSV for additional filtering/analysis or for ingest into tools such as the CloudEndure Migration Factory. Selecting Statistics (pie-chart icon) on any given view provides summary-level information about the content on that view and in the case of the Capacity Plan, the entire inventory as in the screenshot below.

 ![](/.attachments/DK-Portfolio/Screen%20Shot%202020-09-19%20at%209.46.49%20AM.png)

  

Licensing Analysis
------------------

ModelizeIT provides reports for analyzing Oracle as well as SQLServer under the Software Licenses section of the Home Page. These reports provide inventory as well as consumption data for the hosts in addition to the feature set of functionality or versions of the software packages being used on the hosts. Oracle database options and packs are mapped to CPU pools via the hypervisors.

 ![](/.attachments/DK-Portfolio/Picture1.png)

  

Application Grouping, Naming, and Metadata
------------------------------------------

Selecting “Unknown Apps” and the “Identify” icon on the left control panel groups all the hosts inventoried into application groups based on communication data that was collected and analyzed by the tool. Naming the unknown applications with meaningful names can be done in a couple of different ways.

 ![](/.attachments/DK-Portfolio/Picture2.png)

  

### Bulk Application Name Ingest

If quality CMDB data for app to server mapping is available, it can be bulk-ingested into the tool. Tooling and capabilities to ingest this data is constantly evolving, so please check their documentation for the latest/best format to ingest the data. Essentially a CSV file with the application, its metadata, and the servers it “contains” can be ingested and reflected it the tool. It's currently best to create a master file of this data and ingest it at one time through a Gatherer processing job.

To bulk ingest applications, create a file of the following format and save it as a TAB delimited .txt file. Note: there should not be a header row, just all data. 

| SERVERNAME | APPNAME |   ENVIRONMENT   |
| --- | --- | --- |

Then you will run the python script agains this file using the following command changing the red text to what you named the file above. This assumes you have a working version of python (check with `python --version`) and that both files are in the present working directory. You can download the script by clicking on it. 

`python   < DELIMITEDFILENAME.txt > APPLICATION.csv`

Then you will upload this to the gather server (e.g. [https://saas19.aws.modelizeit.com/.custmrG/](https://saas19.aws.modelizeit.com/.abbdapG/) making sure the "G" is at the end and replacing with your instance url). 

-  Click "Manage Jobs" -  Click "Add"  -  Select "Upload Manually Collected Files" (under "Type") -  In "Parameters" select the file you want to upload (APPLICATION.csv) -  Click "Upload" -  Click "Dashboard" -  Click "Reload"

### Additional Application Metadata

Additional application metadata fields can be added by editing the “Application” class through the above ingest file process. Typical fields could include Scope, Criticality, Disposition, etc. This is done by adding additional columns to the APPLICATION.csv file. 

### Individual Application Edit

Any application can be individually edited by viewing it in the browser and then using the “Edit” option from the left control panel. The membership of the stack can also be edited by adding/removing the server membership as appropriate. The “clone” option is an efficient method to copy application information to separate out “PROD” environments into other environments such as “DEV” and “TEST” etc.

There are special "keywords" for environments that result in specific treatment of the application in ModelizeIT. These are case sensitive. 

*   "IT" - Infrastructure application (e.g. Active Directory, Monitoring, backups, etc.)
*   "OOS" - Out of Scope
*   "USER" - User subnetwork/workstations

It can often be useful to name IP ranges to help consolidate lists of IPs on architecture diagram. To do this, create a new "Business App" (via + button on left nav), name the network segment (e.g. "Usernet"), set the environment to "USER", and contains to the CIDR block (e.g. 172.1.122.0/24). Once you have done this, all IPs within the stated range will appear as a single icon on the architecture diagrams. 

Exporting Data
--------------

ModelizeIT makes it easy to export data to other tools commonly utilized by implementation teams. The “Custom Query” option within the tool allows you to select the class of object and the type of export required including CSV zip (for ingestion into data analysis tools) as well as image objects (as in the case of architecture diagrams that can be inserted into CMDB tools or Confluence or similar wiki pages). In addition to the custom exports listed and available from the documentation, we have partnered with their team to create a couple of custom exports.

### Exporting results of page

The content of every page visible in Modelize IT can be exported to CSV format. To do this rename the page from .html to .csv in the browser and this will download the entire content of the page.

### CloudEndure Migration Factory

The “Capacity Plan” export has been modified to include as much or all of the data required for ingest into the Migration Factory. The sizing recommendation for both “like-for-like” as well as a “right-sized” server as well as additional data such as IP address, host name, etc. can be utilized by the factory to create the target environment.

### MPA Export

As noted earlier, data from the tool needs to be exported into MPA or a similar tool for TCO/cost analysis. The “Batch Reports” option provides a detailed export of server inventory information that should be a click-through ingest into the MPA tool.

  

Custom Reports
--------------

Often it is desired to have specific included or excluded in the data analysis. It is possible in ModelizeIT to create custom views, to do so click on the custom button
 ![](/.attachments/DK-Portfolio/Screenshot%202021-10-04%20at%2019.06.32.png)
, this will allow creation of new report.

An important example of this is to see servers architecture with ports. This is specially useful when trying to understand the server connectivity importance. To do so choose the following setting in the custom report page:

| Setting  | Value |
| --- | --- |
| View type | Topology |
| Output format | html |
| Profile | "Create a new name for this" |
| Show |   Show IP address for servers  Describe connections   |
| Show Apps, AFFs, WAVEs, DCs, ZONEs |   Show objects of the same class  Show APPLICATIONs   |
| Filter out | <None> |
| Paper, layout and colors |   Use the same color for the whole object group  Optimize output for printing on paper  Spend more time on layout optimization    |

  

Architecture Diagrams
---------------------

Reference ModelizeIT's online documentation for explanation of the [architecture diagrams](https://www.modelizeit.com/documentation/RejuvenApptor-Legend.html).

 **Attachments:** 


[Picture1.png](/.attachments/DK-Portfolio/Picture1.png)

[Picture2.png](/.attachments/DK-Portfolio/Picture2.png)

[Screen%20Shot%202020-09-19%20at%209.46.49%20AM.png](/.attachments/DK-Portfolio/Screen%20Shot%202020-09-19%20at%209.46.49%20AM.png)

[Screenshot%202021-10-04%20at%2019.06.32.png](/.attachments/DK-Portfolio/Screenshot%202021-10-04%20at%2019.06.32.png)

[image-20200921-194052.png](/.attachments/DK-Portfolio/image-20200921-194052.png)

[tsv2apps.py](/.attachments/DK-Portfolio/tsv2apps.py)
