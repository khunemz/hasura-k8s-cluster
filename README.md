# minikube
make sure that ingress addon is installed
```
minikube addons enable ingress
minikube addons enable ingress-dns
```

# run minikube
```
minikube start --vm-driver=hyperkit
```
# open minikube dashboard
```
minikube dashboard
```

# if you do not want to deploy it to default namespace
```
kubectl create namespace {{namespace}}
```
# firt thing first you need to install postgres
### deployment postgres
#### notice: username / password have to be in `base64`
```
kubectl apply -f deployments/postgres-secrets.yaml
kubectl apply -f deployments/postgres-storage.yaml
kubectl apply -f deployments/postgres.yaml
kubectl apply -f deployments/postgres-service.yaml
```

# make sure everything gets ready
```
kubectl get pods --namespace=labs
kubectl get services --namespace=labs
```

# check pods
```
kubectl get pods --namespace=labs
```
# it would show, for example
```
NAME                        READY   STATUS    RESTARTS      AGE
hasura-547c8f64c5-xqg97     1/1     Running   0             32m
postgres-77f59b67df-6nqdg   1/1     Running   1 (21d ago)   21d
```

# check service
```
kubectl get service --namespace=labs
```

# it would show, for example
```
NAME             TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
hasura-service   LoadBalancer   10.102.83.127   <pending>     80:30708/TCP   26m
postgres         ClusterIP      10.102.214.40   <none>        5432/TCP       21d
```

# exec to pods
```
kubectl exec -it --namespace=labs postgres-{{hash_number_of_pod}} -- /bin/bash
```

# POSTGRES stuff
# psql
```
psql -U $POSTGRES_USER
```

# list of database
```
\d
```

# create database 
```
create database {{database_name}}
```

# use database;
```
\c {{database_name}}
```

# see all tables
```
\dt *.*
```

# to remove all stuff that we had deployed
```
kubectl delete --all {{pod|service|deployment}} --namespace=labs
```

# hasura deployment
#### !!!! you have to change credentials before
```
cd deployments

wget https://raw.githubusercontent.com/hasura/graphql-engine/stable/install-manifests/kubernetes/deployment.yaml
wget https://raw.githubusercontent.com/hasura/graphql-engine/stable/install-manifests/kubernetes/svc.yaml

cd ..
kubectl apply -f deployments/hasura.yaml
kubectl apply -f deployments/hasura-service.yaml
```


# Hasura first run
```
# see hasura ingress
kubectl get ingress --namespace=labs
```

# it would show
```
NAME             CLASS   HOSTS   ADDRESS        PORTS   AGE
hasura-ingress   nginx   *       192.168.64.2   80      5m16s
```

then navigate to the address shown above. In the first run it would ask you about admin secrets which located in hasura deployment file (in this case it located in `hasura.yaml`)


<img width="1440" alt="Screen Shot 2565-06-25 at 09 29 26" src="https://user-images.githubusercontent.com/10510210/175755112-07666eb1-5f5e-4779-9d76-8d1c3565a8a0.png">


<img width="1440" alt="Screen Shot 2565-06-25 at 09 37 37" src="https://user-images.githubusercontent.com/10510210/175755115-bb92806d-c972-456f-addd-fe7bbe36bd68.png">
