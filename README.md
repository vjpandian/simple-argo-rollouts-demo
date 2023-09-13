# simple-argo-rollouts-demo

### Prerequisites:

- Install `argo-rollouts` from the docs [page](https://argo-rollouts.readthedocs.io/en/stable/installation/)
```
chmod +x ./kubectl-argo-rollouts-darwin-amd64
sudo mv ./kubectl-argo-rollouts-darwin-amd64 /usr/local/bin/kubectl-argo-rollouts
kubectl argo rollouts version
```
- Create a namespace and install the `argo-rollouts` controller:
```
kubectl create namespace argo-rollouts
kubectl apply -n argo-rollouts -f https://github.com/argoproj/argo-rollouts/releases/latest/download/install.yaml
```


