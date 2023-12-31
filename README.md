# simple-argo-rollouts-demo

A simplified version of the official argo rollouts [demo](https://github.com/argoproj/rollouts-demo).

![Rollouts UI](https://github.com/vjpandian/simple-argo-rollouts-demo/blob/6b456929d328f9a5356e862099c5c0707739f6e3/Rollouts-Demo.gif)

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

### Deploying the rollout

- Run the command below to deploy the initial services
  
```
kubectl apply -f . -n argo-rollouts
```

- You can watch the rollout in a terminal window by running the command below:

```
kubectl argo rollouts -n argo-rollouts get rollout rollouts-demo --watch
```

- View the deployed service by performing a port-forward

```
kubectl port-forward service/rollout-bluegreen-active 8080:80 -n argo-rollouts
```

You can now view the currently deployed version at http://localhost:8080

### Updating a rollout

```
  kubectl argo rollouts -n argo-rollouts set image rollouts-demo \
  rollouts-demo=argoproj/rollouts-demo:yellow
```

This will set the image tag to be deployed in case you choose to promote to a newer version `yellow`

### Expose the preview service to a different port

```
kubectl port-forward service/rollout-bluegreen-preview 8081:80 -n argo-rollouts
```

You can now view the currently deployed version at http://localhost:8081 and confirm that this is a version that you'd like to rollout to prod or not.

### Promoting a rollout

```
kubectl argo rollouts -n argo-rollouts promote rollouts-demo
```

Once a rollout is promoted, only the active service will be available.
