# docs-gha-self-hosted-runner-pool-k8s
Simple deployment for spinning up a pool of self-hosted runners for a given repo in K8s

1. Create a K8s Secret with your GH PAT as follows:

```
kubectl create secret generic access-token \
    --from-literal=ACCESS_TOKEN='your-gh-pat'
```
2. Set the number of runners you want in your pool. 

```
spec:
  selector:
    matchLabels:
      api: gha-runner
  replicas: <integer-goes-here> # example: 10
```

2. Update the `REPO_URL` env var in `gha-self-hosted-deployment` for your chosen repository.

```
- name: REPO_URL
    value: <your-repo-url> # example: https://github.com/jvincent-mongodb/docs-gha-self-hosted-runner-pool-k8s
```

3. Deploy the runners to K8s

```
kubectl apply -f gha-self-hosted-deployment.yaml
```
