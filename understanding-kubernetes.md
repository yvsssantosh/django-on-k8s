# Understanding Kubernetes.

#### Pods (PO)

A pod is the most basic unit that Kubernetes deals with which generally represents one or more containers that should be controlled as a single application. Usually, pods consist of a main container that satisfies the general purpose of the workload and optionally some helper containers that facilitate closely related tasks.

It is not advised for users should to manage pods themselves, because they do not provide some of the features typically needed in applications (like sophisticated life cycle management and scaling). Instead, users are encouraged to work with higher level objects that use pods or pod templates as base components but implement additional functionality


#### Replication Controllers (RC) & Replica Sets (RS)

A **Replication Controller** ensures that a specified number of pod replicas are running at any one time. In other words, it makes sure that a pod or a homogeneous set of pods are always up and running.

If there are too many pods,the Replication Controller terminates the extra pods. If there are too few, it starts more pods. Unlike manually created pods, the pods maintained by a Replication Controller are automatically replaced if they fail, are deleted, or are terminated. 

A Replication Controller is similar to a process supervisor, but instead of supervising individual processes on a single node, the Replication Controller supervises multiple pods across multiple nodes.

**Replication sets or Replica Sets** are an iteration on the replication controller design with greater flexibility in how the controller identifies the pods it is meant to manage. Replica sets are beginning to replace replication controllers because of their greater replica selection capabilities, but they are not able to do rolling updates to cycle backends to a new version like replication controllers can. Instead, replication sets are meant to be used inside of additional, higher level units that provide that functionality.

Like pods, both replication controllers and replication sets are rarely the units you will work with directly. While they build on the pod design to add horizontal scaling and reliability guarantees, they lack some of the fine grained life cycle management capabilities found in more complex objects.


#### Deployments (DEPLOY)
A Deployment controller provides declarative updates for Pods and ReplicaSets.

You describe a desired state in a Deployment object, and the Deployment controller changes the actual state to the desired state at a controlled rate. You can define Deployments to create new ReplicaSets, or to remove existing Deployments and adopt all their resources with new Deployments.

While deployments built with replica sets may appear to duplicate the functionality offered by replication controllers, deployments solve many of the pain points that existed in the implementation of rolling updates. When updating applications with replication controllers, users are required to submit a plan for a new replication controller that would replace the current controller. When using replication controllers, tasks like tracking history, recovering from network failures during the update, and rolling back bad changes are either difficult or left as the user's responsibility.

Deployments are a high level objects designed to ease the life cycle management of replicated pods. Deployments can be modified easily by changing the configuration and Kubernetes will adjust the replica sets, manage transitions between different application versions, and optionally maintain event history and undo capabilities automatically. Because of these features, deployments will likely be the type of Kubernetes object you work with most frequently.


#### StatefulSets

StatefulSet is the workload API object used to manage stateful applications. It manages the deployment and scaling of a set of Pods, and provides guarantees about the ordering and uniqueness of these Pods.




#### Services (SVC)
A Kubernetes Service is an abstraction which defines a logical set of Pods and a policy by which to access them - sometimes called a micro-service.

For Kubernetes-native applications, Kubernetes offers a simple Endpoints API that is updated whenever the set of Pods in a Service changes. For non-native applications, Kubernetes offers a virtual-IP-based bridge to Services which redirects to the backend Pods
