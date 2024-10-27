STEPS FOR AKS

Create 3 node pools
coordpool 1 node 16Cores/64GB - Standard_D16as_v4
execpool 2 (Auto Scale to 5) nodes 4Cores/16GB - Standard_D4ds_v4
zkpool 3 node 2Cores/4GB - Standard_B2s
values.yaml values that work with above nodes
coordinator: ALWAYS ALLOCATE n-1 CPU for Coordinator CPU in values.yaml. Leave some memory for OS
  cpu: 15
  memory: 52000
executor: ALWAYS ALLOCATE n-1 CPU for Coordinator CPU in values.yaml. Leave some memory for OS
  cpu: 3
  memory: 12288
  engines: ["default"]
  count: 1
zookeeper: ALWAYS ALLOCATE n-1 CPU for Coordinator CPU in values.yaml. Leave some memory for OS
  cpu: 0.5
  memory: 1024
  count: 3

Create storage account 
Locally-redundant storage (LRS)
StorageV2 (general purpose v2)
Create a Container (Data Storage->Containers) within the storage account "dremio-dist" for distributed storage specified in values.yaml
Get the Access Key (Security+networking->Access keys) for accessing the storage for specifying in values.yaml



kubectl get nodes
kubectl get pods
kubectl get pods -A -o wide

--get storage class always use premium min 100MBS throughput
kubectl get sc 

docker login quay.io

kubectl create secret docker-registry dremio-image-secret \  
  --docker-server=quay.io \  
  --docker-username=kamlesh_dremio \  
  --docker-password=Catanddog1! \  
  --docker-email=kamlesh.sharma@dremio.com


kubectl get secrets


navigate to the charts/dremio_v2 directory
helm list
helm install kamlesh-tam .
kubectl get services dremio-client

kubectl get all
kubectl get pods
kubectl get nodes

kubectl describe pod dremio-master-0

kubectl get pvc
kubectl get pv
kubectl delete PersistentVolumeClaim <pvc-name>
kubectl delete pv <pv-name>

kubectl config get-clusters

--Re-run helm after changes to values.yaml
helm upgrade kamlesh-tam . --wait
or
helm uninstall kamlesh-tam
helm install kamlesh-tam .

# Get a bash shell
$ kubectl exec -it dremio-master-0 -- bash
# Get logs
$ kubectl logs dremio-master-0
# Describe cluster
$ kubectl describe pod dremio-master-0
# Copy files
$ kubectl cp <file-spec-src> <file-spec-dest> -c <specific-container>
$ kubectl cp --help

Cleaning up the cluster


$ az aks delete --name zh-aks --resource-group zh-resourcegroup
Are you sure you want to perform this operation? (y/n): y


$ az group delete --name zh-resourcegroup --yes --no-wait


for pv in $(kubectl get pvc -o name); do kubectl delete $pv; done


$ az aks show --name zh-aks --resource-group zh-resourcegroup

kubectl -n kube-system logs -f deployment/kamlesh-tam

kubectl get hpa -n dremio



kubectl logs <podname> like dremio-executor-0
