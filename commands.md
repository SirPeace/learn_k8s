# kubectl commands list

This is the list of cubectl commands that I learned from this [course](https://youtube.com/watch?v=X48VuDVv0do).

Of course you can find their better explanation in the documentation or in the cli itself, but it just helps me remember them better and to check what I have tried out already and what I haven't yet.

## get

```
$ kubectl get <component>
```

Get K8s components. \<component> may be one of the following:

- **services**
- **pods**
- **nodes**
- **replicaset**

### Examples

```
$ kubectl get deployments
NAME               READY   UP-TO-DATE   AVAILABLE   AGE
nginx-deployment   1/1     1            1           10s

$ kubectl get pods
NAME                                READY   STATUS    RESTARTS   AGE
nginx-deployment-56d5bf5669-vdtz8   1/1     Running   0          14s
```

## create

```
$ kubectl create <component>
```

Create a K8s component. \<component> may be one of the following:

- **deployment**

### Examples

```
$ kubectl create deployment nginx-deployment --image=nginx:alpine
deployment.apps/nginx-deployment created
```

## edit

```
$ kubectl edit <component> <name>
```

Edit a K8s component. \<component> may be one of the following:

- **deployment**

### Examples

```
$ kubectl edit deployment nginx-deployment
GNU nano 5.9
# Please edit the object below. Lines beginning with a '#' will be ignored,
# and an empty file will abort the edit. If an error occurs while saving this file will be
# reopened with the relevant failures.
#
apiVersion: apps/v1
kind: Deployment
metadata:
annotations:
    deployment.kubernetes.io/revision: "1"
creationTimestamp: "2021-11-30T11:16:38Z"
generation: 1
labels:
    app: nginx-deployment
name: nginx-deployment
namespace: default
resourceVersion: "1663"
uid: 12ed6c3b-0e91-4f75-8901-de60c72772d8
...
```

## logs

```
$ kubectl logs <pod-name>
```

Get logs of the specified pod.

### Examples

```
$ kubectl logs nginx-deployment-67979c989-65sgr
2021/11/30 11:16:48 [notice] 1#1: nginx/1.20.2
2021/11/30 11:16:48 [notice] 1#1: built by gcc 10.3.1 20210424 (Alpine 10.3.1_git20210424)
2021/11/30 11:16:48 [notice] 1#1: OS: Linux 5.10.16.3-microsoft-standard-WSL2
2021/11/30 11:16:48 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2021/11/30 11:16:48 [notice] 1#1: start worker processes
2021/11/30 11:16:48 [notice] 1#1: start worker process 33
2021/11/30 11:16:48 [notice] 1#1: start worker process 34
2021/11/30 11:16:48 [notice] 1#1: start worker process 35
2021/11/30 11:16:48 [notice] 1#1: start worker process 36
2021/11/30 11:16:48 [notice] 1#1: start worker process 37
2021/11/30 11:16:48 [notice] 1#1: start worker process 38
2021/11/30 11:16:48 [notice] 1#1: start worker process 39
2021/11/30 11:16:48 [notice] 1#1: start worker process 40
```

## describe

```
$ kubectl describe <component> <name>
```

Get additional information about the specified component. \<component> may be one of the following:

- **pod**
- **deployment**

### Examples

```
$ kubectl describe pod nginx-deployment-67979c989-65sgr
Name:         nginx-deployment-56d5bf5669-vdtz8
Namespace:    default
Priority:     0
Node:         minikube/192.168.49.2
Start Time:   Tue, 30 Nov 2021 14:38:53 +0300
Labels:       app=nginx-deployment
              pod-template-hash=56d5bf5669
Annotations:  <none>
Status:       Running
IP:           172.17.0.3
...
```

## exec

```
$ kubectl exec <pod-name> -- <command>
```

Execute the shell command in the pod container.

### Examples

```
$ kubectl exec -it nginx-deployment-67979c989-65sgr -- sh
/ # ls -l
total 72
drwxr-xr-x    2 root     root          4096 Nov 12 09:18 bin
drwxr-xr-x    5 root     root           360 Nov 30 11:38 dev
drwxr-xr-x    1 root     root          4096 Nov 16 18:22 docker-entrypoint.d
-rwxrwxr-x    1 root     root          1202 Nov 16 18:22 docker-entrypoint.sh
drwxr-xr-x    1 root     root          4096 Nov 30 11:38 etc
drwxr-xr-x    2 root     root          4096 Nov 12 09:18 home
drwxr-xr-x    1 root     root          4096 Nov 12 09:18 lib
drwxr-xr-x    5 root     root          4096 Nov 12 09:18 media
drwxr-xr-x    2 root     root          4096 Nov 12 09:18 mnt
drwxr-xr-x    2 root     root          4096 Nov 12 09:18 opt
dr-xr-xr-x  281 root     root             0 Nov 30 11:38 proc
drwx------    1 root     root          4096 Nov 30 11:50 root
drwxr-xr-x    1 root     root          4096 Nov 30 11:38 run
drwxr-xr-x    2 root     root          4096 Nov 12 09:18 sbin
drwxr-xr-x    2 root     root          4096 Nov 12 09:18 srv
dr-xr-xr-x   11 root     root             0 Nov 30 11:38 sys
drwxrwxrwt    1 root     root          4096 Nov 16 18:22 tmp
drwxr-xr-x    1 root     root          4096 Nov 12 09:18 usr
drwxr-xr-x    1 root     root          4096 Nov 12 09:18 var
```

## delete

```
$ kubectl delete <component> <name>
```

Delete the specified K8s component. \<component> may be one of the following:

- **deployment**

### Examples

```
$ kubectl delete deployment nginx-deployment
deployment.apps "nginx-deployment" deleted

$ kubectl delete -f mongo-deployment.yml
deployment.apps "database" deleted
```

## apply

```
$ kubectl apply -f <filepath>
```

Create or update deployment based on the specified configuration file.

### Examples

```
$ kubectl apply -f nginx-deployment.yml
deployment.apps/nginx-deployment created
$ kubectl apply -f nginx-deployment.yml
deployment.apps/nginx-deployment configured
```
