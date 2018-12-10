# stateful-applications
[Tutorial](https://kubernetes.io/docs/tutorials/stateful-application/mysql-wordpress-persistent-volume/#create-persistentvolumeclaims-and-persistentvolumes)
Deploying WordPress app and MySQL containers.

## Commands:
```bash
$ kubectl create secret generic mysql-pass --from-literal=password=Ch@ng3M3!
secret/mysql-pass created
rwibawa@PLSLAPTOP-02742:~/workspace_k8s/stateful-applications$ kubectl get secrets
NAME                  TYPE                                  DATA      AGE
mysql-pass            Opaque                                1         9s

$ kubectl create -f mysql-deployment.yaml
$ kubectl get pvc
NAME             STATUS    VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
mysql-pv-claim   Bound     pvc-ee706685-fc24-11e8-af98-08d0f8f11711   20Gi       RWO            standard       17s

$ kubectl create -f wordpress-deployment.yaml
$ kubectl get pvc
NAME             STATUS    VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
mysql-pv-claim   Bound     pvc-ee706685-fc24-11e8-af98-08d0f8f11711   20Gi       RWO            standard       5m
wp-pv-claim      Bound     pvc-a653a316-fc25-11e8-af98-08d0f8f11711   20Gi       RWO            standard       49s

$ kubectl get services wordpress
NAME        TYPE           CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
wordpress   LoadBalancer   10.98.4.227   <pending>     80:31717/TCP   3m
```
## Clean up
```bash
$ kubectl delete secret mysql-pass

$ kubectl delete deployment -l app=wordpress
$ kubectl delete service -l app=wordpress

$ kubectl delete pvc -l app=wordpress
```
