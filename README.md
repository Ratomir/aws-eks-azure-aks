# init2022

| Feature      | Amazon EKS     | Azure AKS     |
| :---         |     :---:      |          :---: |
| Original GA release date   | June 2018     | June 2018    |
| [CNCF Kubernetes Conformance](https://www.cncf.io/certification/software-conformance/)     | :heavy_check_mark:       | :heavy_check_mark:      |
| Automatically <br />control-plane upgrade process   | :x:     | :x: <br /> [In development](https://azure.microsoft.com/en-us/updates/aks-cluster-auto-upgrade/)    |
| Manually <br />control-plane upgrade process   | [Update](https://docs.aws.amazon.com/eks/latest/userguide/update-cluster.html)  <br /> kube-proxy, coredns, AWS VPC CNI   | [Update](https://learn.microsoft.com/en-us/azure/aks/upgrade-cluster?tabs=azure-cli)  <br /> quota limits  |
| Node upgrade process   | Drain and replace nodes     | Drain and replace nodes    |
| Node OS - Managed  | [Linux](https://docs.aws.amazon.com/eks/latest/userguide/eks-linux-ami-versions.html) <br /> [Bottlerocket](https://docs.aws.amazon.com/eks/latest/userguide/eks-optimized-ami-bottlerocket.html) <br /> [Windows](https://docs.aws.amazon.com/eks/latest/userguide/eks-ami-versions-windows.html)  | Ubuntu 18, 22.04 <br /> Windows 2022    |
| Container runtime   | [containerd](https://aws.amazon.com/blogs/containers/amazon-eks-1-21-released/)     | [containerd](https://learn.microsoft.com/en-us/azure/aks/cluster-configuration)    |
| Control plane <br />high availability options   | [Resilience in Amazon EKS](https://docs.aws.amazon.com/eks/latest/userguide/disaster-recovery-resiliency.html)     | [Spread between AZ](https://learn.microsoft.com/en-us/azure/aks/availability-zones)    |
| SLA   | June 2018     | [Details](https://azure.microsoft.com/en-in/support/legal/sla/kubernetes-service/v1_1/) <br /> 99.95%    |
| Pricing   | [Price](https://aws.amazon.com/eks/pricing/) <br /> [Fargate](https://aws.amazon.com/fargate/pricing/) (based on the vCPU and memory) <br /> [Outputs](https://aws.amazon.com/outposts/rack/pricing/) $0.10 per hour    | [Price](https://azure.microsoft.com/en-ca/pricing/details/kubernetes-service/) SLA 0.10$ per cluster <br /> [Virtual nodes](https://azure.microsoft.com/en-us/pricing/details/container-instances/)    |
| GPU   | Optimized [image](https://docs.aws.amazon.com/eks/latest/userguide/eks-optimized-ami.html#gpu-ami)<br /> [GPU setup](https://docs.aws.amazon.com/deep-learning-containers/latest/devguide/deep-learning-containers-eks-setup.html#deep-learning-containers-eks-setup-gpu-clusters)   | [NVIDIA GPU Cluster](https://learn.microsoft.com/en-us/azure/aks/gpu-cluster)<br /> [GPU vm offers](https://learn.microsoft.com/en-us/azure/virtual-machines/sizes-gpu)    |
| Control plane <br /> log collection   | [Cloud watch](https://docs.aws.amazon.com/eks/latest/userguide/control-plane-logs.html)     | Log Analytics [Diagnostics table](https://learn.microsoft.com/en-us/azure/azure-monitor/containers/container-insights-log-query#resource-logs)    |
| Container metrics   | [Container Insights metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Container-Insights-metrics-EKS.html)     | [Container insights](https://learn.microsoft.com/en-us/azure/azure-monitor/containers/container-insights-overview) |
| Node health monitoring   | [GitHub issue](https://github.com/aws/containers-roadmap/issues/928) [AWS](https://aws.amazon.com/premiumsupport/knowledge-center/eks-node-status-ready/)    | [Auto-repair](https://learn.microsoft.com/en-us/azure/aks/node-auto-repair)    |


