# kubernetes-microservices

Exercises from course Kubernetes Microservices by Richard Chesterwood.

Tested on MacOS Sequoia in 2025.


## Comments

If you're using MacOS, expect that specifying type: NodePort should expose your app automatically on `<Minikube IP>:<NodePort>`. It usually does — but on MacOS, there's a special situation that explains why it doesn't just work.

On MacOS, Minikube doesn't run Kubernetes natively on your host machine — it uses a virtual machine (VM) or a container runtime like Docker.

That means:

* The Kubernetes cluster (and its nodes) live inside a VM or container.

* So, the NodePort only binds inside the VM, not to your Mac’s network interface.

As a result:

* Trying to access `http://<minikube-ip>:<nodePort>` from your Mac might fail.

* You have to use `minikube service` or `kubectl port-forward` to tunnel traffic from your host into the cluster.

I open multiple terminals shells and run commands separately in each:

~~~bash
kubectl port-forward svc/fleetman-queue 30010:8161
kubectl port-forward svc/fleetman-webapp 30081:8080
~~~

another approach with `service`:
~~~bash
minikube service fleetman-webapp
~~~


