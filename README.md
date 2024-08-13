# azure monitoring usefull quaries 

## 1. Monitor Node CPU Usage
This query checks the CPU usage on AKS nodes.

```kusto
KubeNodeInventory
| where TimeGenerated > ago(5m)
| where ClusterName == "your-cluster-name"
| summarize AvgCpuUsage=avg(CpuUsageNanoCores) by Computer
| where AvgCpuUsage > 800000000 // Example threshold: 800m CPU
```

