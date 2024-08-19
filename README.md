# Kubernetes Deployment
Installing of Kubernetes 
- install kubernates
- Install minikube

# Clone a repository


# Building an image from Dockfile

```
docker build . -t namenge/ip2-Client:v1.0.0
```

# Push the Docker image to a Registry
## Login to the Docker hub
```
docker login
```
## Push the image to register

```
docker push namenge/ip2-Client:v1.0.0
```
# create a namespace to help organize action files
- kubectl create namespace my-ecommerce-app
# Create pod
- apiVersion: v1 specifies the Kubernetes API version being used.
- kind: Pod indicates that you are creating a Pod object.
- metadata contains metadata about the Pod, including its name.
- spec defines the desired state of the Pod.
- containersan array of container objects running inside the Pod. In this case, there is only one container.
- name: crud-backend-app sets the name of the container to "crud-backend-app".
- image: trajendra/crudbackend:latest specifies the Docker image to be used for the container. In this case, it uses the image "trajendra/django-todo" with the "latest" tag.
- ports defines the network ports that the container exposes. In this example, it exposes port 3000.


## Run create pod command after creating yaml file in manifest of kind = pod
 ```
 kubectl apply -f client-pods.yml
 ```
 ```
 kubectl apply -f backend-pods.yml
 ```
 
# Create deployment yaml in the manifest folder
- kind: Defines the type of resource, which is a Deployment in this case.

 - selector: Specifies the labels used to select which Pods are part of this Deployment.

 - matchLabels: Defines the labels that Pods must have to be considered part of the Deployment. In this case, Pods with the label
 - replicas:Defines the desired number of replicas (Pods) to maintain, set to 3 in this example.
 - template:Defines the Pod template used to create the Pods managed by the Deployment.
 - spec: Specifies the specifications for the Pods created from the template.

 # Run the Deployments

 ```
 kubectl apply -f frontent-deployment.yaml 
 ```

 ```
 kubectl apply -f backend-deployment.yaml 
 ```

 ```
 kubectl apply -f mongo-db.yaml 
 ```

# check status 
## Pods
 ```
  kubectl get pods -n=my-ecommerce-app
 ```
 ## Deployments
  ```
  kubectl get deployments -n=my-ecommerce-app
 ```