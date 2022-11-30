  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

  

The RN150 is a CentOS/Linux Virtual Appliance. It is deployed on VMware ESX or ESXi Server (Hardware Ver. 8), VMware Player, or VMware Workstation.

### Resource Default Requirements

*   8 GB of RAM (minimum 4 GB)
    
*   2 vCPUs (minimum 1 vCPU)
    
*   50 GB Hard drive (Thin Provisioned)
    
*   Internet Access (TCP Port 443 outbound) to the following:
    
    *   [**orchestration.riscnetworks.com**](http://orchestration.riscnetworks.com) ( 34.192.184.110, 34.192.195.90 )
        
    *   [**initial.riscnetworks.com**](http://initial.riscnetworks.com) ( 34.192.43.78, 34.192.198.28)
        
    *   [**dataup.riscnetworks.com**](http://dataup.riscnetworks.com) ( 34.192.12.37, 34.192.197.132 )
        
    *   [**app1.riscnetworks.com**](http://app1.riscnetworks.com) (34.192.198.73 )
        
    *   **Backup & Growth** (34.192.99.153, 34.192.185.36)
        

### Communication Protocols

The RN150 uses the following protocols (ports) to access the network. These protocols/ports should be permitted between the RN150 and all local resources (servers, routers, etc) to be included in the discovery.

  

|   Protocol   |   Port   |   Source   |   Destination   |   Usage   |
| --- | --- | --- | --- | --- |
|   TCP   |   443   |   RN150   |   Internet   |   For communication from the RN150 to the RISC Networks Cloud Orchestration layer   |
|   ICMP   |   —   |   RN150   |   Local Networks   |   By the RN150 for base discovery for available devices   |
|   TCP   |   135   |   RN150   |   Local Networks   |   By the RN150 to obtain WMI information from Windows hosts discovered   |
|   TCP   |   1024-65535   |   RN150   |   Local Networks   |   RPC Dynamic Port Allocation used for WMI communication.   |
|   TCP   |   80   |   RN150   |   Local Networks   |   By the RN150 to obtain HTTP   |
|   UDP   |   161   |   RN150   |   Local Networks   |   Used for gathering SNMP information from devices on the Network   |
|   TCP   |   443   |   RN150   |   Local Networks   |   Used for gathering VMware guest information directly from vCenter.   |
|   TCP   |   22   |   RN150   |   Local Networks   |   By the RN150 to collect from Linux/UNIX servers over the SSH protocol   |
|   TCP   |   \*   |   RN150   |   Local Networks   |   Collection from Linux/UNIX servers via SSH user supplied non-standard TCP ports   |
|   TCP   |   445   |   RN150   |   Local Networks   |   SMB over TCP/IP used for application socket collection   |
|   TCP   |   139   |   RN150   |   Local Networks   |   SMB over NetBIOS used for application socket collection   |
|   TCP   |   8443   |   RN150   |   Local Networks   |   Used for discovering Tomcat and Cisco UC servers\*   |
|   TCP   |   62078   |   RN150   |   Local Networks   |   Used for discovering Apple products (iPhone) – iTunes sync over air port   |
|   TCP   |   22   |   RN150   |   Local Networks   |   For command line discovery of Cisco Switches and Routers   |
|   TCP   |   1433\*\*   |   RN150   |   Local Networks   |   For MSSQL database collection only   |
|   TCP   |   1521\*\*   |   RN150   |   Local Networks   |   For Oracle database collection only   |
|   TCP   |   3306\*\*   |   RN150   |   Local Networks   |   For MySQL database collection only   |

  

\*\* or other non-standard ports as required for database connectivity

### Required Credentials and Parameters

*   IP Subnets that the client would like to scan
    
    *   These can be added at the time the RN150 is deployed.
        
    *   Subnets can be manually entered or a routing table can be used to populate the list via SNMP
        
*   Windows Domain Administrator or Local Administrator (workgroup servers only) credentials
    
    *   Needed for WMI access
        
*   SSH user account with sudo privileges
    
    *   password or key-based authentication
        
    *   [additional details](https://documentation.riscnetworks.com/overview/how-we-collect/ssh-collection-module)
        
*   SNMP Read Only Credentials
    
    *   Needed for Linux/Unix Servers where not using SSH and should include the following MIBs:
        
        *   Host-Resources-MIB
            
        *   UCD-MIB
            
        *   IF-MIB
            
        *   TCP-MIB
            
        *   UCD-DISKIO-MIB
            
    *   Needed for Network Devices
        
    *   Supports v1/v2/v3
        
*   VMware credentials
    
    *   Read only access to vCenter or root access to ESX hosts directly
        
*   Database credentials
    
    *   IP/SIDs of database hosts
        
    *   [additional details](https://documentation.riscnetworks.com/overview/how-we-collect/database-module)

 **Attachments:** 

