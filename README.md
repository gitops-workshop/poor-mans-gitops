# Poor Man's GitOps

Build and install the agent:

```
docker build -t my-agent:v1 agent
kubectl -n default apply -f agent/install.yaml
```

Wait for the agent to apply your manifests:

```
watch kubectl -n default get all
```

<!--
### Publish Agent

```
docker tag my-agent:v1 alexcollinsintuit/agent:v1
docker push alexcollinsintuit/agent:v1
```
-->

### Clean Up

```
kubectl -n default delete -f agent/install.yaml
kubectl -n default delete pod my-app
```
