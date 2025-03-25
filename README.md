** EKS CLUSTER MANAGEMENT USING TERRAFORM ** 

This repository is to setup Custom VPC, and setup EKS Cluster in the Custom VPC in AWS Environment


**VPC (vpc.tf):**

```
1. Using the file vpc.tf file , the vpc, subnets both private and public would be created.
2. It will create Internet Gateway and attach to VPC
3. It will create the NAT gateway in public subnet, which will be used by worker nodes in private subnets
4. We will then create two route tables, one for public subnet and one for private subnet. 
```

**EKS Control Plane (eks.tf):**

```
1. With the help of eks.tf, we will create the eks control plane, which includes few of the configuration details such as kubernetes version, vpc details, end point access details etc. 
2. We also create the IAM role and few policies required for EKS Control plane node
3. We will attach the IAM Role to the EKS control plane, this is provided by role_arn in eks cluster resource itself.
```

**EKS Worker Nodes (eks-private-ng.tf):**

```
1. With the help of eks-private-ng.tf , it would create a node group  and the desired size of nodes we define for the size of cluster.
2. It also creates a role and attaches 3 policies which are required for EKS worker node groups which are mandatory, and the fourth policy is related to Autoscaling, which is used by Cluster Austoscaler, as we would also autoscale the cluster as per our requirement with the help of the CA.
3. It will create a config file with your cluster configuration which got created under .kube directory which resides in your home directory. This file generation is mandatory to be present in order to authenticate to cluster and also do other tasks which would be done inside the EKS cluster. 
```

**EKS Addons (eks-addons.tf):**

```
 There are few addons which would be installed on eks cluster, as per your needs you can add any other addons if required.

 ALB Ingress controller (Alb-controller-iam-role-policy.tf): 

 It will install ingress controller once cluster is setup and config file is generated. This ingress controller would be helpful for Ingress resources to provision ALB. 
```

**Cluster Autoscaler IAM Role:**

```
This tf file would create required IAM Role and policies for Cluster autoscaler to work properly.
```
