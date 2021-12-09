# Laravel deploy with kubernetes

## Steps

<code>
docker build -t {Your-dockerhub-username}/{image-name}
</code>
<code>
docker login
</code>
<code>
docker push {your-dockerhub-username}/{image-name}
</code>

edit kube/deployment.yaml 
```
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: laravel
    role: rolling-update
  name: laravel
spec:
  replicas: 4
  selector:
    matchLabels:
      app: laravel
  template:
    metadata:
      labels:
        app: laravel
    spec:
      containers:
      - image: {your-dockerhub-username}/{image-name}
        imagePullPolicy: Always
        name: laravel

```
<code>
kubectl apply -f kube/deployment.yaml
</code>

<code>
kubectl expose deployment laravel --type=NodePort --port=80 
</code>

if you are using minikube 

<code>
minikube service --url=true laravel
</code>

<code>
http://youripaddress:port
</code>

