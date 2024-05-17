 
## == Reflection 1 Minikube==
 1. Compare the application logs before and after you exposed it as a Service.
 Try to open the app several times while the proxy into the Service is running.
 What do you see in the logs? Does the number of logs increase each time you open the app?

 + Before Exposing as a Service:
When you check the application logs before exposing it as a Service, you'll typically see logs related to the initialization of the application, such as messages indicating that the HTTP and UDP servers have started and are listening on a specific port (e.g., port 8080).

+ After Exposing as a Service:
After exposing the application as a Service and accessing it multiple times via the proxy, you'll notice additional log entries. Specifically, each time you open or refresh the application in the web browser, the logs will show new HTTP GET requests. This indicates that the application is receiving and processing these requests.

+ So Yes, the number of logs increases each time you open or refresh the app. Each user interaction (like refreshing the page) generates a new HTTP request, which is logged by the application. This is useful for monitoring how often the application is accessed and can help in diagnosing issues or understanding usage patterns.

2. Notice that there are two versions of `kubectl get` invocation during this tutorial section.
 13 The first does not have any option, while the latter has `-n` option with value set to `kube-system`. What is the purpose of the `-n` option and why did the output not list the pods/services that you explicitly created

+ Without -n Option:
The kubectl get command without any options lists the resources (pods, services, etc.) in the default namespace. This is the namespace where the custom resources are created unless specified otherwise.

+ With -n Option :
The -n option stands for "namespace." In Kubernetes, namespaces are used to organize and separate resources within a cluster. When you use kubectl get -n kube-system, it specifically targets the kube-system namespace, which contains system-critical pods and services managed by Kubernetes itself (e.g., CoreDNS, kube-proxy).

+ The reason the output does not list the pods/services you explicitly created when using the -n kube-system option is that the resources are likely in a different namespace (probably the default namespace). The -n option restricts the scope of the kubectl get command to the specified namespace, so it won't show resources in other namespaces.

