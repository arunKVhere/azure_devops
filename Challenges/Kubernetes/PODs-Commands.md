1. How many pods exist on the system?

   ```bash
   kubectl get pods
   ```
   
1. Create a new pod with the nginx image.

   ```bash
   kubectl run nginx --image=nginx
   ```

1. How many pods are created now?

   ```bash
   kubectl get pods
   ```

   ```bash
   kubectl get pods --no-headers | wc -l
   ```

   * `--no-headers` should be obvious - output only the details.
   * `wc` is the word count program. `-l` tells it to count lines instead, and it will count the lines emitted by `kubectl`
   
1. What is the image used to create the new pods?

    ```bash
    kubectl describe pod nginx | grep image
    ```
    
1. Which nodes are these pods placed on?

    ```bash
    kubectl get pods -o wide
    ```

1. How many containers are part of the pod webapp?

   ```bash
   kubectl describe pod nginx
   ```

   Look under the `Containers` section. Note there is `nginx`


1. What is the state of the container agentx in the pod nginx?

   ```bash
   kubectl describe pod nginx
   ```

   Examine the `State:` field for the `nginx` container.

1. Create a new pod with the name redis and with the image redis123.</br>Use a pod-definition YAML file.

   To create the pod definition YAML file:

   `--dry-run=client` tells `kubectl` to test without actually doing anything. `-o yaml` says "Output what you would send to API server to the console", which we then redirect into the named file.

   ```bash
   kubectl run redis --image=redis123 --dry-run=client -o yaml > redis.yaml
   ```

   And now use the YAML you created to deploy the pod.

   ```bash
   kubectl create -f redis.yaml
   ```

1. Now change the image on this pod to redis.</br>Once done, the pod should be in a running state.

   There are three ways this can be done!

   1. Method 1</br>
      Edit your manifest file created in last question

      ```bash
      vi redis.yaml
      ```

      Fix the image name in the redis.yaml to `redis`, save and exit.

      Apply the edited yaml

      ```bash
      kubectl apply -f redis.yaml
      ```

   1. Method 2</br>
      Edit the running pod directly (note not all fields can be edited this way)

      ```
      kubectl edit pod redis
      ```

      This will bring the pod YAML up in `vi`. Edit it as per method 1. When you eixt `vi` the change will be immediately applied. If you make a mistake, you will be dropped back into `vi`

   1. Method 3</br>
      Patch the image directly. For this you need to know the `name` of the container in the pod, as we assign the new image to that name, as in `container_image_name=new_image`

      ```bash
      kubectl set image pod/redis redis=redis
      ```

   
