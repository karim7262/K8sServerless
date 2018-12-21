# Mongo DB

## Install MongoDB

We can use the helm chart again with the following:

```
helm install stable/mongodb --name fonkdb --set service.type=LoadBalancer,persistence.enabled=false,usePassword=false
```

Obviously we would put a password in real life to this but for our application and simplicity we'll leave that out for now.  

We've also put the service type as loadbalancer so we can test it.  Normally you would leave it as `clusterIP` type as you don't want people accessing the database directly outside your cluster.  We do this for testing purposes!

Make sure its deployed:

```
kubectl get pods,services -l app=mongodb
```

The output is:

```
NAME                                 READY     STATUS              RESTARTS   AGE
pod/fonkdb-mongodb-c474fff64-r54tz   0/1       ContainerCreating   0          2m

NAME                     TYPE           CLUSTER-IP       EXTERNAL-IP     PORT(S)           AGE
service/fonkdb-mongodb   LoadBalancer   10.107.150.119   10.93.140.132   27017:30943/TCP   2m
```

We now have access to our database!  

To delete this we could run `helm delete --purge fonkdb`

## Testing MongoDB

In this section we will explore some of the ways MongoDB works and how we can do quieries. 