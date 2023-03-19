```
kubectl create ns study
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

```
kubectl config set-credentials pod-deployment-viewer --token=$(kubectl describe secret -n study $(kubectl get secret -n study | grep pod-deployment-viewer-account | awk '{print $1}') | grep token: | awk '{print $2}')
kubectl config set-context pod-deployment-viewer-context --user=pod-deployment-viewer --namespace=study
kubectl config use-context pod-deployment-viewer-context
```

```
<!-- Set the credentials -->
kubectl config set-credentials pod-deployment-viewer --token=$(kubectl describe secret -n study $(kubectl get secret -n study | Select-String "pod-deployment-viewer-account" | ForEach-Object { $_.Line.Split(' ', [StringSplitOptions]::RemoveEmptyEntries)[0] }) | Select-String "token:" | ForEach-Object { $_.Line.Split(':      ')[1] })

<!-- Set the context -->
kubectl config set-context pod-deployment-viewer-context --user=pod-deployment-viewer --namespace=study

<!-- Set the cluster -->
kubectl config set-context pod-deployment-viewer-context --cluster=docker-desktop --user=pod-deployment-viewer --namespace=study

<!-- Use the context -->
kubectl config use-context pod-deployment-viewer-context

<!-- Reset the credentials -->
kubectl config set-context docker-desktop --user=docker-desktop --namespace=study
kubectl config use-context docker-desktop
```

Troubleshooting

- Ingress werkt niet:
  - luistert er niets op poort 80

- Inloggen werkt niet met het account pod-deployment-viewer
  - kijk naar de kubeconfig of deze goed staat en of er een token in zit
