```
kubectl create ns foo
```

```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.6.4/deploy/static/provider/aws/deploy.yaml
```

```
kubectl apply -f ./k8s
```

Show everything that is listning on port 80:

```
netstat -ano | findstr ":80" | findstr "LISTENING"
```
