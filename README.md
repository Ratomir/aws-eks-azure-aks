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
| Control plane <br />high availability options   | [Resilience in Amazon EKS](https://docs.aws.amazon.com/eks/latest/userguide/disaster-recovery-resiliency.html)     | (Spread between AZ)[https://learn.microsoft.com/en-us/azure/aks/availability-zones]    |
| SLA   | June 2018     | [Details](https://azure.microsoft.com/en-in/support/legal/sla/kubernetes-service/v1_1/) <br /> 99.95%    |
| Original GA release date   | June 2018     | June 2018    |
| Original GA release date   | June 2018     | June 2018    |
| Original GA release date   | June 2018     | June 2018    |
| Original GA release date   | June 2018     | June 2018    |
| Original GA release date   | June 2018     | June 2018    |


