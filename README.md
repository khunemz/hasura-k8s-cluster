# minikube
make sure that ingress addon is installed
```
minikube addons enable ingress
minikube addons enable ingress-dns
```

# postgress
```
kubectl apply -f deployments/postgres-secrets.yaml
kubectl apply -f deployments/postgres-storage.yaml
kubectl apply -f deployments/postgres.yaml
kubectl apply -f deployments/postgres-service.yaml

kubectl get pods --namespace=labs
kubectl get services --namespace=labs

# check pods
kubectl get pods --namespace=labs
kubectl get service --namespace=labs

# exec to pods
kubectl exec -it --namespace=labs postgres-{{hass}} -- /bin/bash

# psql

psql -U $POSTGRES_USER

# remove
kubectl delete --all {{pod|service|deployment}} --namespace=labs
```

# hasura
```
cd deployments

wget https://raw.githubusercontent.com/hasura/graphql-engine/stable/install-manifests/kubernetes/deployment.yaml
wget https://raw.githubusercontent.com/hasura/graphql-engine/stable/install-manifests/kubernetes/svc.yaml

cd ..

kubectl apply -f deployments/hasura.yaml
kubectl apply -f deployments/hasura-service.yaml

# dashboard stuff
kubectl get ingress --namespace=labs

# it would show

NAME             CLASS   HOSTS   ADDRESS        PORTS   AGE
hasura-ingress   nginx   *       192.168.64.2   80      5m16s

# then navigate to the address shown above

# in the first run it would ask you about admin secrets which located in hasura deployment file (in this case it located in `hasura.yaml`)
```



# Hasura first run
``
// 1) see hasura ingress

```


## screen shot

<img width="1440" alt="Screen Shot 2565-06-25 at 09 29 26" src="https://user-images.githubusercontent.com/10510210/175755112-07666eb1-5f5e-4779-9d76-8d1c3565a8a0.png">


<img width="1440" alt="Screen Shot 2565-06-25 at 09 37 37" src="https://user-images.githubusercontent.com/10510210/175755115-bb92806d-c972-456f-addd-fe7bbe36bd68.png">

