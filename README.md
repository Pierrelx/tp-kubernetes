# tp-kubernetes


### Secret
Mysql root : _root_

Actualiser le mysql-secret.yaml
`
kubectl get secret mysql-secret -o yaml >> mysql-secret.yaml
`
Actualiser le mysql-secret.yaml
`
kubectl create secret generic mysql-secret --from-literal=password=motdepasse
`