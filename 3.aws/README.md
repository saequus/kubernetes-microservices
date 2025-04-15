# AWS

### AWS EKS

clusterName: `fleetman`
region: `eu-north-1`

Create cluster

~~~bash
eksctl create cluster --name fleetman --nodes-min=3 --node-type=t3.medium
~~~


~~~bash
aws eks --region eu-north-1 update-kubeconfig --name fleetman
~~~

EBS connection setup

~~~bash
eksctl utils associate-iam-oidc-provider --region=eu-north-1 --cluster=fleetman --approve


eksctl create iamserviceaccount --name ebs-csi-controller-sa --namespace kube-system --cluster fleetman --attach-policy-arn arn:aws:iam::aws:policy/service-role/AmazonEBSCSIDriverPolicy --approve  --role-only  --role-name AmazonEKS_EBS_CSI_DriverRole


eksctl create addon --name aws-ebs-csi-driver --cluster fleetman --service-account-role-arn arn:aws:iam::$(aws sts get-caller-identity --query Account --output text):role/AmazonEKS_EBS_CSI_DriverRole --force
~~~


