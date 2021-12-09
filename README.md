# Laravel deploy with kubernetes

## Steps

### Edit kube/deployment.yaml 
```
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: laravel
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
docker build -t {Your-dockerhub-username}/{image-name}
</code>
<br>
<br>
<code>
docker login
</code>
<br>
<br>
<code>
docker push {your-dockerhub-username}/{image-name}
</code>
<br>
<br>
<code>
kubectl apply -f kube/deployment.yaml
</code>
<br>
<br>

<code>
kubectl expose deployment laravel --type=NodePort --port=80 
</code>
<br>
<br>
##### If you are using minikube 
<br>
<code>
minikube service --url=true laravel
</code>
<br>
<br>
<code>
http://youripaddress:port
</code>

