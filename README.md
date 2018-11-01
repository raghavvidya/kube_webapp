Let you use Kubernetes(v1.11.0) to quickly build a lmap usage environment.

The LAMP contains the following four operating environments.

Linux or Ubuntu
Apache
MySQL
PHP

Build MYSQL
=============
change the folder to mysql.

Use this command to create a secret password
kubectl create secret generic mysql-pass --from-file=password.txt
Create a deploy and service for mysql server.

```sh
   kubectl apply -f mysql.yaml
```

# Check those service and pod
```
kubectl get pod
NAME                                 READY     STATUS    RESTARTS   AGE
my-php7-server-888f47968-twt8x       1/1       Running   0          2d
```
```
kubectl get svc
NAME               CLUSTER-IP       EXTERNAL-IP    PORT(S)    AGE
mysql-service      192.10.20.152   <none>         3306/TCP   2d
```

# Build PHP7-Apache2
change the folder to php7-apache2.

Create a deploy and service for php7-apache2 server.
```
kubectl apply -f php7-apache2.yaml
```

Check those service and pod
```
kubectl get pod
NAME                              READY     STATUS    RESTARTS   AGE
my-php7-server-888f47968-twt8x   1/1       Running   0          1d
```
```
kubectl get svc
NAME               CLUSTER-IP       EXTERNAL-IP    PORT(S)    AGE
my-php7-server     192.20.10.15     192.11.24.21   80/TCP     1h
```

# Scale up/down application
Scale up the deployment
```
kubectl get deploy
NAME              DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
my-php7-server    1         1         1            0           8h
wordpress-mysql   1         1         1            0           8h
```

```
kubectl scale deploy my-php7-server --replicas=3
deployment.extensions/my-php7-server scaled
```

```
kubectl get deploy
NAME              DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
my-php7-server    3         3         3            0           8h
wordpress-mysql   1         1         1            0           8h
````
Scale down the deployment

```
kubectl scale deploy my-php7-server --replicas=2
deployment.extensions/my-php7-server scaled
```

```
 kubectl get deploy
NAME              DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
my-php7-server    2         2         2            0           8h
wordpress-mysql   1         1         1            0           9h
```

# Check your browser
browse 192.11.24.21 can see that connect the database success.
