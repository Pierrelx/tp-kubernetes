# tp-kubernetes

  
  

### Secret

Mysql root : _root_

  Créer le mysql-secret

`kubectl create secret generic mysql-secret --from-literal=password=motdepasse`

Actualiser le mysql-secret.yaml  

`kubectl get secret mysql-secret -o yaml >> mysql-secret.yaml`

  

### Accéder aux conteneurs avec minikube

  

`minikube dashboard`

  

`minikube service <leservice> -n <namespace>`

### Setup de rook
[Source](https://github.com/rook/rook/blob/master/Documentation/ceph-quickstart.md)

création de l'infra de base
`kubectl create -f https://raw.githubusercontent.com/rook/rook/master/cluster/examples/kubernetes/ceph/common.yaml`

création de l'opérator
`kubectl create -f https://raw.githubusercontent.com/rook/rook/master/cluster/examples/kubernetes/ceph/operator.yaml`

**Vérifier avec `kubectl -n rook-ceph get pod` que *rook-ceph-operator* est en état `Running` avant de continuer**
...
création du cluster rook ceph
 `kubectl create -f https://raw.githubusercontent.com/rook/rook/master/cluster/examples/kubernetes/ceph/cluster.yaml`
 
 création de la toolbox (pour vérifier le fonctionnement de cluster)
`kubectl create -f https://raw.githubusercontent.com/rook/rook/master/cluster/examples/kubernetes/ceph/toolbox.yaml`

Attendre avec `kubectl -n rook-ceph get pod -l "app=rook-ceph-tools"` que la toolbox passe en état `Running`
...
passer en bash dans la toolbox
`kubectl -n rook-ceph exec -it $(kubectl 
-n rook-ceph get pod -l "app=rook-ceph-tools" -o jsonpath='{.items[0].metadata.name}') bash`

> -   All mons should be in quorum
> -   A mgr should be active
> -   At least one OSD should be active
> -   If the health is not `HEALTH_OK`, the warnings or errors should be investigated
> 
> >**$** ceph status 
> > 	cluster:  
> > 		id:     a0452c76-30d9-4c1a-a948-5d8405f19a7c 
> > 		health: HEALTH_OK
> >
>  > services:  
>  > 	mon: 3 daemons, quorum a,b,c (age 3m)  
>  > 	mgr: a(active, since 2m)  
>  > 	osd: 3 osds: 3 up (since 1m), 3 in (since 1m) ...

