1. Create a new service to access the web application using the service-definition-1.yaml file.

    ```
    vi service-definition-1.yaml
    ```
    
    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
     name: myapp-service
    spec:
     type: NodePort
     ports:
     - targetPort: 80
       port: 80
       nodePort: 30008
     selector:
       app: myapp
       type: front-end
    ```
    

    Fill in the values as directed, save and exit.

    ```
    kubectl create -f service-definition-1.yaml
    ```
    
1. How many Services exist on the system and check the TYPE, EndPoint of the service?

    ```
    kubectl get services
    ```
    
1. What is the targetPort configured on the kubernetes service?

    ```
    kubectl describe service | grep TargetPort
    ```
    

1. How many labels are configured on the kubernetes service?

    ```
    kubectl describe service
    ```

    ...and look for labels.

    --- OR ---

    ```
    kubectl get service --show-labels
    ```        

1.  Try to access the application via the UI
