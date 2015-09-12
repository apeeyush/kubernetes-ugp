# Getting started with Kubernetes

## Starting the cluster locally
    hack/local-up-cluster.sh

## Creating single pod
    kubectl create -f ./hello-world.yaml
    kubectl get pods
    kubectl logs hello-world
    kubectl delete pod hello-world
    kubectl delete pods/hello-world

## Creating replication controller
    kubectl create -f ./nginx-rc.yaml
    kubectl get rc
    kubectl delete rc my-nginx
    kubectl get pods -L app
    kubectl get rc my-nginx -L app
    kubectl get rc my-nginx -o template --template="{{.spec.selector}}" # To view selectors

## To check pod IPs
    kubectl get pods -l app=nginx -o json | grep podIP

## To describe a service
    cluster/kubectl.sh describe svc nginxsvc

## To get all endpoints
    cluster/kubectl.sh get ep

## Kubectl exec
    # To print pod environment variables
    kubectl exec my-nginx-6isf4 -- printenv
    # To ls on a pod
    kubectl exec <podname> ls /

## To scale the number of replicas
    cluster/kubectl.sh scale rc my-nginx --replicas=2
