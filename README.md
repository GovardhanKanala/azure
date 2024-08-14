# azure monitoring usefull quaries 

## 1. Monitor Node CPU Usage
This query checks the CPU usage on AKS nodes.

```kusto
KubeNodeInventory
| where TimeGenerated > ago(5m)
| where ClusterName == "your-cluster-name"
| summarize AllocatedCpu=avg(CpuAllocatedNanoCores), AllocatableCpu=avg(CpuAllocatableNanoCores) by Computer
| extend CpuUsagePercentage = (AllocatedCpu / AllocatableCpu) * 100
| where CpuUsagePercentage > 80 // Alert when CPU usage exceeds 80%
```

```
KubePodInventory
| where TimeGenerated > ago(5m)
| where ClusterName == "your-cluster-name"
| summarize AvgMemoryUsage=avg(MemoryUsageBytes) by Name, Namespace
| where AvgMemoryUsage > 2000000000 // Example threshold: 2 GB
```
