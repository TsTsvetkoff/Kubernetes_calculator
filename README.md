# Python Socket Programming with Kubernetes

This project demonstrates how to use Python's socket programming capabilities to create a server-client architecture, where the server can handle multiple clients. The server and clients are each deployed as separate pods in a Kubernetes cluster. 
The server is a simple calculator that can perform addition operations of two positive numbers. The clients can connect to the server and send requests to perform these operations. Each client and server run in their own Kubernetes pod, allowing for scalability and management through Kubernetes.

## Prerequisites
- Docker Desktop with Kubernetes enabled

## How to Run
!!! **This project is meant for local execution only** !!!

To run the server-client architecture, follow these steps:

1. Ensure you have a running Kubernetes cluster. You can use Docker Desktop with Kubernetes enabled.
2. Apply the Kubernetes configuration files. This will create the necessary deployments, services, and roles for the server and clients.

That command is needed only once for configuration.
```bash
kubectl apply -f=clusterrole.yaml -f=clusterrolebinding.yaml
```

That command makes the needed deployments and starts the service.
```bash
kubectl apply -f=k8s_deployment_server.yaml -f=k8s_deployment_client.yaml
```

3. Once the deployments are up and running, you can check the status of your pods:
```bash
kubectl get pods
```
Example output
```bash
NAME                                  READY   STATUS    RESTARTS   AGE
client1-deployment-b569768b9-tcd27    1/1     Running   0          6m14s
client2-deployment-5b76868f44-9tnl7   1/1     Running   0          6m14s
server-deployment-bf864957b-ldcn7     1/1     Running   0          6m14s
```
4. To interact with a client, you can attach to the running container in the pod -
via docker desktop or terminal in interactive mode.

```bash
kubectl exec -it <client-pod>  -- /bin/bash
```
```bash
Example
kubectl exec -it client1-deployment-b569768b9-tcd27  -- /bin/bash
```

5. Run the client file in the client container:

Note: Kubernetes doesn't natively support running containers in fully interactive mode
```bash
python client.py 
```

You can also utilize the second client to test the server's ability to handle multiple clients plus ability to monitor the server's logs.
Also you can delete client pods and review how kubernetes will automatically recreate them.

![k8s_demo.png](k8s_demo.png)

6. Enjoy the server-client architecture!
7. To stop the created pods execute:
```bash
kubectl delete -f=k8s_deployment_server.yaml -f=k8s_deployment_client.yaml 
```
