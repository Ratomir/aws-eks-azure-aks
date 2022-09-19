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



## Speed comparison
Please, take a look of the :movie_camera: [video](https://www.youtube.com/watch?v=goZFUy4uHVg&t=859s&ab_channel=DevOpsToolkit) from the [DevOps Toolkit YouYube channel](https://www.youtube.com/c/DevOpsToolkit). In the video you can find comparison between four k8s providers, EKS, AKS, GKE and Linode. :relaxed:

## Limits
| Name      | Amazon EKS     | Azure AKS     | Notes |
| :---         |     :---:      |          :---: | :---  |
| Offical link | [EKS](https://docs.aws.amazon.com/eks/latest/userguide/service-quotas.html) <br /> [Fargate throttling quotas](https://docs.aws.amazon.com/AmazonECS/latest/userguide/throttling.html) | [AKS](https://learn.microsoft.com/en-us/azure/aks/quotas-skus-regions) | [Token bucket](https://en.wikipedia.org/wiki/Token_bucket) |
| Max clusters | Per region 100| Per subscription 5000 | Adjustable |
| Max node pools/groups| 30 | 100 | EKS uses node groups <br /> AKS uses node pools |
| Max nodes per node pool/group | 450 | (per cluster) | |
| Max nodes per cluster | :rocket: 13 500 :rocket: | Virtual Machine Availability Sets and Basic Load Balancer SKU 100 <br /> Virtual Machine Scale Sets and Standard Load Balancer SKU 1000 (across all node pools)| |
| Max pods | | [Basic networking](https://learn.microsoft.com/en-us/azure/aks/concepts-network#kubenet-basic-networking) with Kubenet | |

## Max pods per node
### AKS
With [Basic networking](https://learn.microsoft.com/en-us/azure/aks/concepts-network#kubenet-basic-networking) with Kubenet 
- Maximum: 250
- Azure CLI default: 110
- Azure Resource Manager template default: 110
- Azure portal deployment default: 30

Advanced networking with [Azure Container Networking Interface](https://learn.microsoft.com/en-us/azure/aks/concepts-network#azure-cni-advanced-networking)
- Maximum: 250
- Default: 30

### EKS
Depends of the EC2 instance size and Elastic Network Interfaces (ENI) of an image
The formula
```math
N * (M-1) + 2
```
- N is the number of Elastic Network Interfaces (ENI) of the instance type
- M is the number of IP addresses per ENI

All calculations from [AWS frequently updated](https://github.com/awslabs/amazon-eks-ami/blob/master/files/eni-max-pods.txt).

## Security
| Name      | Amazon EKS     | Azure AKS     | Notes |
| :---         |     :---:      |          :---: | :---  |
| Network plugin/CNI | [VPC CNI](https://docs.aws.amazon.com/eks/latest/userguide/pod-networking.html) | [Azure CNI](https://learn.microsoft.com/en-us/azure/aks/configure-azure-cni) <br /> [Plugin GitHub](https://github.com/Azure/azure-container-networking) | - [EKS CNI Proposal](https://github.com/aws/amazon-vpc-cni-k8s/blob/master/docs/cni-proposal.md) <br /> [amazon-vpc-cni-k8s](https://github.com/aws/amazon-vpc-cni-k8s) |
| RBAC | [IAM](https://docs.aws.amazon.com/eks/latest/userguide/add-user-role.html) aws-auth ConfigMap | [Azure Active Directory](https://learn.microsoft.com/en-us/azure/aks/azure-ad-rbac) <br /> [Roles](https://learn.microsoft.com/en-us/azure/aks/azure-ad-rbac#create-the-aks-cluster-resources-for-sres) :arrow_right: Permissions :arrow_right: [role bindings](https://learn.microsoft.com/en-us/azure/aks/azure-ad-rbac#create-the-aks-cluster-resources-for-sres)| [k8s Using RBAC Authorization](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#default-roles-and-role-bindings) |
