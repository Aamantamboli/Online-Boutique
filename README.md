
# Deploy Online Boutique Microservices on AWS EKS

This guide outlines how to deploy the **Online Boutique** microservices application to **AWS Elastic Kubernetes Service (EKS)**. Follow the steps below to set up the necessary infrastructure, deploy the application, and access the frontend.

## Prerequisites

Before starting, make sure you have the following:

### AWS Account:
- Ensure you have an AWS account and the necessary IAM permissions to manage EC2, EKS, and networking resources.

### CLI Tools:
- **AWS CLI**: Install and configure the AWS CLI.
- **kubectl**: Install `kubectl` to interact with your Kubernetes cluster.
- **eksctl**: Install `eksctl` to easily manage EKS clusters.
- **helm**: Install Helm for managing Kubernetes applications.
  
### Docker:
- Install Docker to build container images (if needed).

### Git:
- Install Git to clone the repository.

Clone the Online Boutique repository:

```bash
git clone https://github.com/GoogleCloudPlatform/microservices-demo.git
cd microservices-demo/
```

## 1. Set Up EKS Cluster

### Create the EKS Cluster:
Use `eksctl` to create a new EKS cluster in your preferred region.

```bash
eksctl create cluster \
  --name online-boutique-cluster \
  --region us-east-1 \
  --nodes 3 \
  --node-type t3.medium
```

This will create an EKS cluster with 3 nodes in the `us-east-1` region.

### Verify Cluster Setup:
Check if the cluster is up and running by listing the nodes:

```bash
kubectl get nodes
```

If successful, you should see the nodes in your EKS cluster.

## 2. Deploy Online Boutique to EKS

### Apply Kubernetes Manifests:
Deploy the Online Boutique application to the EKS cluster using the Kubernetes manifests provided in the repository.

```bash
kubectl apply -f ./release/kubernetes-manifests.yaml
```

### Verify Deployment:
Wait for the Pods to reach the "Running" state by checking the pod status:

```bash
kubectl get pods
```

You should see all the Pods with the status `Running`.

## 3. Expose the Frontend Service

### Get External IP for the Frontend Service:
To access the application in your browser, you need to get the external IP of the frontend service.

```bash
kubectl get service frontend-external
```

Look for the `EXTERNAL-IP` column to get the external IP address.

### Access the Application:
Once you have the external IP, you can open the application in your browser by visiting:

```
http://<EXTERNAL-IP>
```

## 4. Clean Up Resources

When you're done with the application, you can delete the EKS cluster and clean up the resources:

```bash
eksctl delete cluster --name online-boutique-cluster --region us-east-1
```

This will remove the EKS cluster and all associated resources.

---

## Additional Resources

- [AWS EKS Documentation](https://docs.aws.amazon.com/eks/latest/userguide/)
- [Kubernetes Documentation](https://kubernetes.io/docs/)
- [Helm Documentation](https://helm.sh/docs/)
- [Online Boutique GitHub Repository](https://github.com/GoogleCloudPlatform/microservices-demo)

---

This `README.md` provides a step-by-step guide for deploying the Online Boutique app to AWS EKS. Make sure you follow all the steps in order, and you should have the application running on your EKS cluster in no time!

