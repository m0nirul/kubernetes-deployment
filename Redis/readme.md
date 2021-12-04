# Installing redis in a kubernetes cluster
## 1. Validate the yaml files
Please check namespace, name and api versions
## 2. Create Configmap, statefulset 
Run the following command
`kubectl apply -f redis-sts.yml`

## 3. Create Service 
Run the following command
`kubectl apply -f redis-svc.yml`

## 4. Deploy redis as cluster
`kubectl -n <namespace>  exec -it redis-cluster-0 -- redis-cli --cluster create --cluster-replicas 1 $(kubectl -n <namespace> get pods -l app=redis-cluster -o jsonpath='{range.items[*]}{.status.podIP}:6379 ')`

