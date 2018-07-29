https://kubernetes.io/blog/2016/08/security-best-practices-kubernetes-deployment/

- Deploy one pod with root filesystem as readonly
```
kubectl apply -f ./kubernetes.yaml
kubectl get pods -l app=myapp
```

- Check pod status
```
## ,-----------
## | bash-3.2$ kubectl get pods -l app=myapp --all-namespaces
## | NAMESPACE   NAME        READY     STATUS                       RESTARTS   AGE
## | my-test     myapp-pod   0/1       CreateContainerConfigError   0          7s
## `-----------

## ,-----------
## | bash-3.2$ kubectl describe pod myapp-pod
## | Name:         myapp-pod
## | Namespace:    my-test
## | Node:         minikube/10.0.2.15
## | Start Time:   Sun, 29 Jul 2018 16:20:26 -0700
## | Labels:       app=myapp
## | Annotations:  kubectl.kubernetes.io/last-applied-configuration={"apiVersion":"v1","kind":"Pod","metadata":{"annotations":{},"labels":{"app":"myapp"},"name":"myapp-pod","namespace":"my-test"},"spec":{"containers":[{...
## | Status:       Pending
## | IP:           172.17.0.19
## | Containers:
## |   myapp-container:
## |     Container ID:  
## |     Image:         busybox
## |     Image ID:      
## |     Port:          <none>
## |     Host Port:     <none>
## |     Command:
## |       sh
## |       -c
## |       echo Hello Kubernetes! && sleep 3600
## |     State:          Waiting
## |       Reason:       CreateContainerConfigError
## |     Ready:          False
## |     Restart Count:  0
## |     Environment:    <none>
## |     Mounts:
## |       /var/run/secrets/kubernetes.io/serviceaccount from default-token-f6npk (ro)
## | Conditions:
## |   Type           Status
## |   Initialized    True 
## |   Ready          False 
## |   PodScheduled   True 
## | Volumes:
## |   default-token-f6npk:
## |     Type:        Secret (a volume populated by a Secret)
## |     SecretName:  default-token-f6npk
## |     Optional:    false
## | QoS Class:       BestEffort
## | Node-Selectors:  <none>
## | Tolerations:     <none>
## | Events:
## |   Type     Reason                 Age               From               Message
## |   ----     ------                 ----              ----               -------
## |   Normal   Scheduled              1m                default-scheduler  Successfully assigned myapp-pod to minikube
## |   Normal   SuccessfulMountVolume  1m                kubelet, minikube  MountVolume.SetUp succeeded for volume "default-token-f6npk"
## |   Normal   Pulling                15s (x6 over 1m)  kubelet, minikube  pulling image "busybox"
## |   Normal   Pulled                 13s (x6 over 1m)  kubelet, minikube  Successfully pulled image "busybox"
## |   Warning  Failed                 13s (x6 over 1m)  kubelet, minikube  Error: container has runAsNonRoot and image will run as root
## `-----------
```
