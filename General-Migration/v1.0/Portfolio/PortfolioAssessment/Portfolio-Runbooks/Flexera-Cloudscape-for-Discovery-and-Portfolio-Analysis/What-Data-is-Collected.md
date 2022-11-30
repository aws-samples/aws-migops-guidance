  

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

  

The following list outlines the specific information sets gathered by the RISC Networks RN150 collecting appliance during an engagement. Data is collected in two distinct phases by the RN150, inventory and performance. For documentation on access requirements please go to 
["How We Collect"](https://documentation.riscnetworks.com/overview/how-we-collect "https://documentation.riscnetworks.com/overview/how-we-collect")

**Network Equipment**
---------------------

### **Inventory**

Hardware Information

*   Serial Number
    
*   Line Cards
    
*   Flash Size
    
*   Memory Size
    
*   Interface Information
    
*   ENTITY-MIB information
    

Software Information

*   Software version
    
*   Flash file list
    

Operational Information

*   Routing Table
    
*   ARP Table
    
*   L2 Forwarding Table
    
*   Neighbor Information (CDP, FDP, LLDP, etc)
    
*   Spanning Tree Topology
    
*   SAN Switch Forwarding Information (WWN Names, etc)
    
*   SCSI Lun Information (FC Switches only)
    
*   Quality of Service Configuration
    
*   Cisco IP SLA Configuration
    
*   Cisco Netflow Configuration
    

### **Performance**

Statistical Information

*   Interface Utilization and Error Statistics
    
*   CPU and Memory Utilization Statistics
    
*   Cisco MQC Statistics
    
*   IP SLA Statistics (TrafficSim)
    
*   Netflow flow information (TrafficWatch)
    

  

**Windows Servers**
-------------------

### **Inventory**

Hardware Information

*   Serial Number (Dell Service Tag, etc)
    
*   Physical Memory
    
*   Physical CPU
    
*   Physical Hard Drive
    
*   HBA Information
    
*   Network Card information
    

Software Information

*   OS Version
    
*   Installed Applications and versions with process ID information
    
*   Windows Services and status
    
*   Logical Disks
    
*   Windows Shares
    
*   HTTP get on port 80
    

Operational Information

*   Windows Event Log information (3 days of Errors and Warnings)
    
*   Citrix Metaframe Server Inventory
    

### **Performance**

*   CPU Performance
    
*   Process specific Performance metrics (CPU, Swap, etc)
    
*   Memory Performance (bytes used / % used )
    
*   Disk (Logical and Physical) performance (I/O per sec, I/O bytes, latency, etc)
    
*   Windows Network Interface Utilization (I/O bytes, etc)
    
*   Windows Process Information
    
*   Windows Netstat Connectivity Information (opt-in only)
    
*   DNS A records and C names where applicable
    

**Linux/Unix Servers**
----------------------

### **Inventory via SNMP & SSH**

Hardware Information

*   Physical Memory
    
*   Physical CPU
    
*   Physical Hard Drive
    
*   Network Interfaces
    

Software Information

*   OS Description
    
*   Installed Applications and versions with process ID information
    
*   Logical Disks
    
*   Filesystems
    
*   HTTP get on port 80
    

### **Inventory via SSH**

*   Operating System
    
*   OS Version
    
*   OS Distribution
    
*   OS Distribution Version
    
*   CPU Architecture
    

### **Performance via SNMP & SSH**

*   CPU Performance
    
*   Memory Performance (bytes used / % used )
    
*   Physical Disk I/O
    
*   Running Processes
    
*   Socket Connectivity Information (uses TCP-MIB via SNMP / prefers RFC 4022 version)
    
*   Network Interface Utilization
    

**VMWare**
----------

### **Inventory**

Hardware Information

*   Server Model
    
*   Network Connectivity
    
*   Physical Memory
    
*   CPU
    
*   Disk Information (size and configuration)
    

Software Information

*   Guest Inventory
    
    *   OS Version
        
    *   ESX Location
        
*   Host Inventory
    
    *   OS Version
        
*   DataStore mapping to hosts and guests
    

Operational Information

*   Virtual Switch configuration
    

### **Performance**

*   CPU Utilization (wait time, ready time, etc)
    
*   Memory Utilization (usage MB, etc)
    
*   Disk Utilization (I/O / sec, bytes/sec, etc)
    
*   Network Utilization (bytes in/out)
    

**Database**
------------

### **Inventory**

Database Information

*   Hostname
    
*   Version
    
*   Schemas Names (sometimes referred to as database names)
    
*   Connectivity
    
*   Table Metadata
    
*   Table Names
    

### **Performance**

*   Connectivity
    
*   Table Names

 **Attachments:** 

