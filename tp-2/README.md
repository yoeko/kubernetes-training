# Kubernetes training

# Create a pod

## Create pod.yml file

## Initialize pod
kubectl apply -f pod.yml

```yml
apiVersion: v1
kind: Pod
metadata: 
  name: simple-webapp-color
  labels:
    app: web
spec:
  containers:
  - name: web
    image: mmumshad/simple-webapp-color
    ports:
      - containerPort: 8080
    env:
      - name: APP_COLOR
        value: red

```

## Check pods
kubectl get po
kubectl describe po

## Expose the pod to external (the pod contain a container which is listening on port 8080)
kubectl port-forward simple-webapp-color 8080:8080 --address 0.0.0.0

## Delete pod
kubectl delete -f pod.yml

## Create a nginx-deployment.yml file
```yml
apiVersion: apps/v1
kind: Deployment
metadata: 
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 2
  strategy: 
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name:  nginx
        image:  nginx:1.18.0
        ports:
        - containerPort: 80
```

## Init deployment
kubectl get deploy

## Check deployment
kubectl get replicaset -o wide



## run kube pod by command line
kubectl run --image=mmumshad/simple-webapp-color \
--env="APP_COLOR=red" \
--restart=Never \
simple-webapp-color


## run kube deployment by command line
kubectl create deployment --image=nginx:1.18.0 nginx-deployment


## scale deployment 
kubectl scale --replicas=2 deployment/nginx-deployment

## change deployment based image
kubectl set image deployment/nginx-deployment nginx=nginx
