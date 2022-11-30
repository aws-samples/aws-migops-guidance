page

  

|    |    |    |    |
| --- | --- | --- | --- |

  

* * *

[[_TOC_]]

Cluster Breakdown
-----------------

As you build out the VMware on Cloud infrastructure, below table provides a template to record various data points.

*   **Cluster Name:** This is the name of the cluster that is used by the cluster to identify the business workloads migrated into the VMC cluster
*   **VMC Cluster Name:** This would be the cluster name that is in VMC
*   **Number of VMs:** The number of VMs that would belong to the specific cluster
*   **vCPUs:** The number of virtual CPU sockets (or) cores
*   **Memory:** The total RAM allocated to all the virtual machines in TB
*   **Storage:** Total amount of storage required by all the virtual machines in a specific cluster in TB
*   **Node type:** Denotes the type of node. Current options include: i3 and r5 nodes, i3EN nodes - future option
*   **Hosts by CPU:** Identifies the number of nodes that would be required based on the number of CPU cores required for each cluster
*   **Hosts by RAM:** Identifies the number of nodes that would be required based on the RAM total for each cluster
*   **Hosts by Storage:** Identifies the number of nodes that would be required based on the total TBs required for each cluster
*   **N+1 host requirement:** This column picks the highest of among all the "Hosts by" columns and adds 1 additional node to that total to account for possible addition of few virtual machines in the future

  

| **Cluster Name** | **VMC Cluster Name** | **Number of VMs** | **vCPUs** |   **Memory (TB)**   | **Storage (TB)** | **Node Type** | **Hosts by CPU** | **Hosts by RAM** | **Hosts by Storage** | **N+1 Hosts Requirement** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| VDI | Cluster-1 |     |     |     |     |     |     |     |     |     |
| DevUAT | Cluster-2 |     |     |     |     |     |     |     |     |     |
| Prod-App1 | Cluster-3 |     |     |     |     |     |     |     |     |     |
| Prod-App2 | Cluster-4 |     |     |     |     |     |     |     |     |     |
| Prod-BizCrit1 | Cluster-5 |     |     |     |     |     |     |     |     |     |
| Prod04 | Cluster-6 |     |     |     |     |     |     |     |     |     |
| Prod05-nonCrit1 | Cluster-7 |     |     |     |     |     |     |     |     |     |
| Prod06 | Cluster-8 |     |     |     |     |     |     |     |     |     |
| **Total** |     |     |     |     |     |     |     |     |     |     |

  

Cluster workload breakdown
--------------------------

This table provides a high level summary of the various clusters and their respective workloads

*   **Workload type:** This denotes the environment of applications that reside each of the clusters
*   **VMs:** This is the total number of VMs for each environment
*   **Memory:** This is the total of the RAM usage measured in TB
*   **Storage:** This is the total storage requirement for all the applications in a specific environment
*   **i3 nodes by CPU:** Identifies the number of nodes that would be required based on the number of CPU cores required
*   **i3 nods by RAM:** Identifies the number of nodes that would be required based on the RAM total for each workload
*   **i3 nodes by storage:** Identifies the number of nodes that would be required based on the total TBs required
*   **Hosts required:** Total number of hosts required to host all the machines of a specific workload
*   **Nodes per cluster:** Total number of hosts per cluster
*   **Total Cluster:** Total number of clusters required for each workload

  

| **Workload Type** | **VMs** | **vCPU** | **Memory   ** | **Storage   ** | **Hosts by CPU** | **Hosts by RAM** | **Hosts by Storage** | **Hosts Required** | **Nodes Per Cluster** | **Total Clusters** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Development |     |     |     |     |     |     |     |     |     |     |
| Production |     |     |     |     |     |     |     |     |     |     |
| **Total** |     |     |     |     |     |     |     |     |     |     |

 **Attachments:** 

