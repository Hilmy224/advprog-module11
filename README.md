 
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

## ==Reflection 2 Rolling Update & Kubernetes Manifest Fil ==

1. What is the difference between Rolling Update and Recreate deployment strategy?
+ Rolling Update:
+ The rolling update strategy updates pods gradually by creating new pods and incrementally replacing the old ones. This ensures that there is no downtime, as the application remains available throughout the update process. Each new pod is created and becomes ready before the old pod is terminated, providing a seamless transition to the new version.

+ Recreate:
+ The recreate deployment strategy, on the other hand, stops all the existing pods before starting new ones. This means there is a complete downtime period where the application is unavailable while the old pods are being deleted and new pods are being created. This strategy might be simpler and quicker for certain updates but comes at the cost of application availability.
2. Try deploying the Spring Petclinic REST using Recreate deployment strategy and document your attempt.
Forgot to Screenshot and my laptop ran out of battery

3. Prepare different manifest files for executing Recreate deployment strategy.
+ the file is `recreatedeployment.yaml`
4. What do you think are the benefits of using Kubernetes manifest files? Recall your experience in deploying the app manually and compare it to your experience when deploying the same app by applying the manifest files (i.e., invoking `kubectl apply-f` command) to the cluster.

Benefits:

+ Consistency: Manifest files ensure consistent deployment configurations, reducing the risk of human error. Each deployment is defined in a YAML file, which can be version-controlled and shared among team members.
+ Efficiency: Deploying applications via manifest files is more efficient. You only need to run kubectl apply -f <file.yaml>, which simplifies and speeds up the deployment process compared to manual methods.
+ Scalability: Manifest files allow for easy scalability. You can update the number of replicas or other configurations in the YAML file and reapply it.
+ Repeatability: Using manifest files makes it easy to reproduce the environment setup, as all configurations are documented and can be re-applied at any time.

+ So deploying manually involves several steps, such as creating and configuring resources individually, which is time-consuming and prone to errors. With manifest files, the entire deployment process is streamlined into a single command, ensuring that all configurations are applied uniformly and efficiently. This method also enhances collaboration, as configurations can be reviewed and managed through version control systems.