
## Table of contents
- [Speed comparison](#speed-comparison)
- [Limits](#limits)
- [Max pods per node](#max-pods-per-node)
  * [AKS](#aks)
  * [EKS](#eks)
- [Security](#security)
- [Container Registry](#container-registry)
- [Stack overflow Trends](#stack-overflow-trends-link)
- [Azure Kubernetes useful links](#azure-kubernetes-useful-links)
  * [AKS for EKS proffesionals](#aks-for-eks-proffesionals)
- [EKS useful links](#eks-useful-links)
- [Storage IO Performance](#storage-io-performance)
- [AKS VM Banchmarks](#aks-vm-banchmarks)
- [EKS Scalling Containers on AWS](#eks-scalling-containers-on-aws)
  * [Developer integration](#developer-integration)
- [EKS vs AKS, architecture design, side-by-side](#eks-vs-aks-architecture-design-side-by-side)

## Global features
| Feature      | Amazon EKS     | Azure AKS     |
| :---         |     :---:      |          :---: |
| Original GA release date   | June 2018     | June 2018    |
| [CNCF Kubernetes Conformance](https://www.cncf.io/certification/software-conformance/)     | :heavy_check_mark:       | :heavy_check_mark:      |
| Runs on | Public <br /> [In government](https://docs.aws.amazon.com/govcloud-us/latest/UserGuide/govcloud-eks.html) | Public <br /> [In government](https://azure.microsoft.com/en-us/explore/global-infrastructure/government/) |
| Compliant |  HIPAA, ISO, PCI DSS, and SOC |  HIPAA, ISO, PCI DSS, and SOC |
| Newer Kubernetes version | :steam_locomotive: | Is faster :bullettrain_side: |
| Automatically <br />control-plane upgrade process   | :x:     | :x: <br /> [In development](https://azure.microsoft.com/en-us/updates/aks-cluster-auto-upgrade/) <br />  [Offical doc](https://learn.microsoft.com/en-us/azure/aks/auto-upgrade-cluster)   |
| Manually <br />control-plane upgrade process   | [Update](https://docs.aws.amazon.com/eks/latest/userguide/update-cluster.html)  <br /> kube-proxy, coredns, AWS VPC CNI   | [Update](https://learn.microsoft.com/en-us/azure/aks/upgrade-cluster?tabs=azure-cli)  <br /> quota limits  |
| Node upgrade process   | Drain and replace nodes     | Drain and replace nodes    |
| Node OS - Managed  | [Linux](https://docs.aws.amazon.com/eks/latest/userguide/eks-linux-ami-versions.html) <br /> [Bottlerocket](https://docs.aws.amazon.com/eks/latest/userguide/eks-optimized-ami-bottlerocket.html) <br /> [Windows](https://docs.aws.amazon.com/eks/latest/userguide/eks-ami-versions-windows.html)  | Ubuntu 18, 22.04 <br /> Windows 2022    |
| Container runtime   | [containerd](https://aws.amazon.com/blogs/containers/amazon-eks-1-21-released/)     | [containerd](https://learn.microsoft.com/en-us/azure/aks/cluster-configuration)    |
| Control plane <br />high availability options   | [Resilience in Amazon EKS](https://docs.aws.amazon.com/eks/latest/userguide/disaster-recovery-resiliency.html)     | [Spread between AZ](https://learn.microsoft.com/en-us/azure/aks/availability-zones)    |
| SLA   | [99.5% by default](https://aws.amazon.com/eks/sla/)     | [99.9%](https://azure.microsoft.com/en-in/support/legal/sla/kubernetes-service/v1_1/) <br /> With more AZ to 99.95%    |
| Pricing   | [Price](https://aws.amazon.com/eks/pricing/) <br /> [Fargate](https://aws.amazon.com/fargate/pricing/) (based on the vCPU and memory) <br /> [Outputs](https://aws.amazon.com/outposts/rack/pricing/) $0.10 per hour    | [Price](https://azure.microsoft.com/en-ca/pricing/details/kubernetes-service/) SLA 0.10$ per cluster <br /> [Virtual nodes](https://azure.microsoft.com/en-us/pricing/details/container-instances/)    |
| GPU   | Optimized [image](https://docs.aws.amazon.com/eks/latest/userguide/eks-optimized-ami.html#gpu-ami)<br /> [GPU setup](https://docs.aws.amazon.com/deep-learning-containers/latest/devguide/deep-learning-containers-eks-setup.html#deep-learning-containers-eks-setup-gpu-clusters)   | [NVIDIA GPU Cluster](https://learn.microsoft.com/en-us/azure/aks/gpu-cluster)<br /> [GPU vm offers](https://learn.microsoft.com/en-us/azure/virtual-machines/sizes-gpu)    |
| Control plane <br /> log collection   | [Cloud watch](https://docs.aws.amazon.com/eks/latest/userguide/control-plane-logs.html)     | Log Analytics [Diagnostics table](https://learn.microsoft.com/en-us/azure/azure-monitor/containers/container-insights-log-query#resource-logs)    |
| Container metrics   | [Container Insights metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Container-Insights-metrics-EKS.html) <br /> [Quick start](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Container-Insights-setup-EKS-quickstart.html)     | [Container insights](https://learn.microsoft.com/en-us/azure/azure-monitor/containers/container-insights-overview) |
| Node health monitoring   | [GitHub issue](https://github.com/aws/containers-roadmap/issues/928) [AWS](https://aws.amazon.com/premiumsupport/knowledge-center/eks-node-status-ready/)    | [Auto-repair](https://learn.microsoft.com/en-us/azure/aks/node-auto-repair)    |
| Cluster-autoscaler <br /> [Leader election](https://en.wikipedia.org/wiki/Leader_election) | [EKS](https://docs.aws.amazon.com/eks/latest/userguide/autoscaling.html) <br />  | [AKS](https://learn.microsoft.com/en-us/azure/aks/cluster-autoscaler) |


## Speed comparison
Please, take a look of the :movie_camera: [video](https://www.youtube.com/watch?v=goZFUy4uHVg&t=859s&ab_channel=DevOpsToolkit) from the [DevOps Toolkit YouYube channel](https://www.youtube.com/c/DevOpsToolkit). In the video you can find comparison between four k8s providers, EKS, AKS, GKE and Linode. :relaxed:

## Limits
| Name      | Amazon EKS     | Azure AKS     | Notes |
| :---         |     :---:      |          :---: | :---  |
| Limits | Limits are per account | Limits per subscription | |
| Offical link | [EKS](https://docs.aws.amazon.com/eks/latest/userguide/service-quotas.html) <br /> [Fargate throttling quotas](https://docs.aws.amazon.com/AmazonECS/latest/userguide/throttling.html) | [AKS](https://learn.microsoft.com/en-us/azure/aks/quotas-skus-regions) | [Token bucket](https://en.wikipedia.org/wiki/Token_bucket) |
| Max clusters | Per region 100| Per subscription 5000 | Adjustable |
| Max node pools/groups| 30 | 100 | EKS uses node groups <br /> AKS uses node pools |
| Max nodes per node pool/group | 450 | 1000(per cluster) | |
| Max nodes per cluster | :rocket: 13 500 :rocket: | Virtual Machine Availability Sets and Basic Load Balancer SKU 100 <br /> Virtual Machine Scale Sets and Standard Load Balancer SKU 1000 (across all node pools)| |

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
| Network policy | [CNI and Calico](https://docs.aws.amazon.com/eks/latest/userguide/calico.html) | [Azure NPM(Network Policy Manager) and <br /> Calico](https://learn.microsoft.com/en-us/azure/aks/use-network-policies#create-an-aks-cluster-and-enable-network-policy) | |
| Pod Security Policy | **Depricated** <br /> [Gatekeeper](https://aws.amazon.com/blogs/containers/using-gatekeeper-as-a-drop-in-pod-security-policy-replacement-in-amazon-eks/) <br /> [PAC policy as code](https://aws.github.io/aws-eks-best-practices/security/docs/pods/#pod-security-standards-pss-and-pod-security-admission-psa) | **Depricated** <br /> [Azure Policy](https://learn.microsoft.com/en-us/azure/aks/use-azure-policy) <br /> [Workload Identity](https://azure.github.io/azure-workload-identity/docs/) | [Pod Security Standard](https://kubernetes.io/docs/concepts/security/pod-security-standards/) <br /> [Pod Security Admission](https://kubernetes.io/docs/concepts/security/pod-security-admission/) |
| Private cluster | Public by default <br /> [guide](https://docs.aws.amazon.com/eks/latest/userguide/cluster-endpoint.html) | Public by default <br /> Private cluster, DNS zone, endpoint <br /> [guide](https://learn.microsoft.com/en-us/azure/aks/private-clusters) | |
| Firewall for cluster Kubernetes API | [CIDR](https://docs.aws.amazon.com/eks/latest/userguide/cluster-endpoint.html) | [CIDR](https://learn.microsoft.com/en-us/azure/firewall/protect-azure-kubernetes-service) | |

## Container Registry
| Name      | Amazon ECR    | Azure ACR    | Notes |
| :---         |     :---:      |          :---: | :---  |
| Image formats | [Formats](https://docs.aws.amazon.com/AmazonECR/latest/userguide/image-manifest-formats.html) | [Formats](https://learn.microsoft.com/en-us/azure/container-registry/container-registry-image-formats) | |
| Access | IAM <br /> [Repository level](https://docs.aws.amazon.com/AmazonECR/latest/userguide/security_iam_id-based-policy-examples.html) <br /> Public by default <br /> [VPC endpoint](https://docs.aws.amazon.com/AmazonECR/latest/userguide/vpc-endpoints.html) | RBAC <br /> [Repository level](https://learn.microsoft.com/en-us/azure/container-registry/container-registry-repository-scoped-permissions) <br /> Public by default <br /> [VNET endpoint](https://learn.microsoft.com/en-us/azure/container-registry/container-registry-vnet) | |
| Supports immutable image tags | [Image tag mutability](https://docs.aws.amazon.com/AmazonECR/latest/userguide/image-tag-mutability.html) | [Container image lock](https://learn.microsoft.com/en-us/azure/container-registry/container-registry-image-lock) | |
| SLA | [99.9%](https://aws.amazon.com/ecr/sla/) | [99.9%](https://azure.microsoft.com/en-us/support/legal/sla/container-registry/v1_1/) | |
| Geo-Redundancy | [Yes](https://aws.amazon.com/blogs/containers/cross-region-replication-in-amazon-ecr-has-landed/) | [Premium tier](https://learn.microsoft.com/en-us/azure/container-registry/container-registry-geo-replication)| |
| Image signing | [Free](https://docs.aws.amazon.com/AmazonECR/latest/userguide/image-scanning.html) | [Azure Defender](https://docs.aws.amazon.com/AmazonECR/latest/userguide/image-scanning.html) | |

## Stack overflow Trends [link](https://insights.stackoverflow.com/trends?tags=amazon-eks%2Cazure-aks)
![image](https://user-images.githubusercontent.com/8688494/191298183-67ce4490-73f7-4364-ad0b-fbc2e103f253.png)

## Azure Kubernetes useful links
- [AKS Construction helper](https://azure.github.io/AKS-Construction/)
- [AKS changelog](https://github.com/Azure/AKS/blob/master/CHANGELOG.md)
- [Release stuts](https://releases.aks.azure.com/webpage/index.html#tabeuro)
- [AKS Azure policy reference](https://learn.microsoft.com/en-us/azure/aks/policy-reference)
- [Image cleaner](https://learn.microsoft.com/en-us/azure/aks/image-cleaner?tabs=azure-cli)
- [Threat matrix for Kubernetes](https://www.microsoft.com/security/blog/2021/03/23/secure-containerized-environments-with-updated-threat-matrix-for-kubernetes/)
- [VM selector tool](https://azure.microsoft.com/en-us/pricing/vm-selector/)
- [Instance calculator](https://learnk8s.io/kubernetes-instance-calculator)

### AKS for EKS proffesionals
Amazing series of blogs for EKS proffesionals https://learn.microsoft.com/en-us/azure/architecture/aws-professional/eks-to-aks/

## EKS useful links
- [EKS best practices](https://github.com/aws/aws-eks-best-practices)
- [EKS workshop](https://www.eksworkshop.com/)
- [Instance calculator](https://learnk8s.io/kubernetes-instance-calculator)


## Storage IO Performance
Really good blog about storage performance with Azure Kubernetes Cluster, File Storage and Disk, but probably the same concpet may be applied on the EKS. Take a shoot https://www.feval.ca/posts/k8s-io/.

## AKS VM Banchmarks
- [Linux VM Banchmark](https://learn.microsoft.com/en-us/azure/virtual-machines/linux/compute-benchmark-scores)
- [Windows VM Banchmark](https://learn.microsoft.com/en-us/azure/virtual-machines/windows/compute-benchmark-scores)

## EKS Scalling Containers on AWS
At the moment, there is no better blog, test, or whatever on the Internet about containers and scale performance then https://www.vladionescu.me/. You need :four::five: minutes to walk trought the post. https://www.vladionescu.me/posts/scaling-containers-on-aws-in-2022/ Enjoy! 

### Developer integration
I believe that AKS has better integration with developer tools, at first with Visual Studio Code and Visual Studio. Yes, they are Microsoft's tools and it is something expected. You can deploy a container to a cluster from IDE.
From oposite side, it is not something that AWS doesn't want in the eco-system but it's not primary focus.
Still, it is maintainable at the both cases, anyway you should use CI/CD concept and tools.

## EKS vs AKS, architecture design, side-by-side
![image](https://user-images.githubusercontent.com/8688494/191537957-01567773-aef8-4897-90f3-57beaa94ab62.png)


