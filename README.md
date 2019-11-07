# Poor Man's GitOps

Build and install the agent:

```
docker build -t poor-mans-gitops:v1 agent
k apply -f agent/install.yaml
```

Wait for the agent to apply your manifests:

```
watch kubectl get all
```

You should see:

```
NAME                                READY   STATUS      RESTARTS   AGE
pod/gitops-agent-1571704560-dckfs   0/1     Completed   0          2m23s
pod/hello-world                     1/1     Running     0          2m21s

NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   17d

NAME                                COMPLETIONS   DURATION   AGE
job.batch/gitops-agent-1571704560   1/1           3s         2m23s

NAME                         SCHEDULE      SUSPEND   ACTIVE   LAST SCHEDULE   AGE
cronjob.batch/gitops-agent   */3 * * * *   False     0        2m27s           3m55s
```

### Clean Up

```
k delete -f agent/install.yaml
k delete pod hello-world --force --grace-period=0
```
