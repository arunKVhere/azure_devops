
1. How many Deployments exist on the system?

   ```bash
   kubectl get deployments
   ```

1. What is the image used to create the pods in the new deployment?

   ```
   kubectl describe deployment
   ```

   Look under the containers section.

   Another way - run the following and check the `IMAGES` column

   ```
   kubectl get deployment -o wide
   ```
   

1. Create a new Deployment using the deployment-definition-1.yaml file located at /root/.</br>There is an issue with the file, so try to fix it.

   ```
   kubectl create -f deployment-definition-1.yaml

    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: myapp-deployment
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

1. The deployment automatically creates a ReplicaSet and pods. To see it

   ```
   kubectl get replicaset
   ```

   ```
   kubectl get pods
   ```

1. Create a new Deployment with the below attributes using your own deployment definition file.

   Create a deployment definition file in `vi`, e.g. `my-deployment.yaml` with the following

    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      labels:
        app: httpd-frontend
      name: httpd-frontend
    spec:
      replicas: 3
      selector:
        matchLabels:
          app: httpd-frontend
      template:
        metadata:
          labels:
            app: httpd-frontend
        spec:
          containers:
          - image: httpd:2.4-alpine
            name: httpd
    ```

   ```
   kubectl create -f my-deployment.yaml
   ```

   Or we could create it imperatively...

   ```
   kubectl create deployment httpd-frontend --image=httpd:2.4-alpine --replicas=3
   ```


   

