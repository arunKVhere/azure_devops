1. How many ReplicaSets exist on the system?

   ```bash
   kubectl get replicasets
   ```   
   
1. What is the image used to create the pods in the new-replica-set?

   ```
   kubectl describe replicaset
   ```

   ...and look under the containers section --- or --

   ```
   kubectl get rs -o wide
   ```

   ...and look in the `IMAGES` column. Kubernetes accepts `rs` as shorthand for `replicaset`.

1. Delete a pod in the replica set and see how replica set will replace it again. 
   

1. Create a ReplicaSet using the template

   ```
   kubectl create -f replicaset-definition-1.yaml

    apiVersion: apps/v1
    kind: ReplicaSet
    metadata:
      name: myapp-replicaset
      labels:
        app: myapp
        type: front-end
    spec:
     template:
        metadata:
          name: myapp-pod
          labels:
            app: myapp
            type: front-end
        spec:
         containers:
         - name: nginx-container
           image: nginx
     replicas: 3
     selector:
       matchLabels:
        type: front-end

   ```

   Get the apiVersion for replicaset

   ```
   $ kubectl explain replicaset | grep VERSION
   ```

1. Delete the created ReplicaSet

   ```
   kubectl delete replicaset replicaset-1
   ```

1. To edit the replica

   ```
   kubectl edit replicaset new-replica-set
   ```

   Export the RS to a yaml
   
   ```
   kubectl get rs new-replica-set -o yaml > rs.yaml
   kubectl delete rs new-replica-set
   kunectl create -f rs.yaml
   ```

   Scale it 
   ```
   kubectl scale rs new-replica-set --replicas 0
   kubectl scale rs new-replica-set --replicas 4
   ```

   


