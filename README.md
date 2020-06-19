# tp-kubernetes


### Secret
Mysql root : _root_

Actualiser le mysql-secret.yaml

`kubectl get secret mysql-secret -o yaml >> mysql-secret.yaml`
Créer le mysql-secret
`kubectl create secret generic mysql-secret --from-literal=password=motdepasse`

### Accéder aux conteneurs avec minikube

`minikube dashboard`

`minikube service <leservice> -n <namespace>`

