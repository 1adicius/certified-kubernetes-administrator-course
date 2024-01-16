# Mock Exam 1

  #### Solution to the Mock Exam 1

  1. Deploy a pod named nginx-pod using the nginx:alpine image.

     <details>
       
         k run nginx-pod --image=nginx:alpine
     </details>

  2. Deploy a messaging pod using the redis:alpine image with the labels set to tier=msg.

     <details>
     
     ```
     k run messaging --image=redis:alpine --labels=tier=msg
     ```
     </details>

 
  3. Create a namespace named apx-x9984574.
     
     <details>

     ```
     k create ns apx-x9984574
     ```
     </details>

  4. Get the list of nodes in JSON format and store it in a file at /opt/outputs/nodes-z3444kd9.json.

     <details>

     ```
     kubectl get nodes -o json > /opt/outputs/nodes-z3444kd9.json
     ```
     </details>

  5. Create a service messaging-service to expose the messaging application within the cluster on port 6379.

     <details>

     ```
     kubectl expose pod messaging --port=6379 --name messaging-service
     ```
     </details>

  6. Create a deployment named hr-web-app using the image kodekloud/webapp-color with 2 replicas.

     <details>

      ```
      apiVersion: apps/v1
      kind: Deployment
      metadata:
        creationTimestamp: null
        labels:
          app: hr-web-app
        name: hr-web-app
      spec:
        replicas: 2
        selector:
          matchLabels:
            app: hr-web-app
        strategy: {}
        template:
          metadata:
            creationTimestamp: null
            labels:
              app: hr-web-app
          spec:
            containers:
            - image: kodekloud/webapp-color
              name: webapp-color
              resources: {}
      status: {}
      ```
      
      In v1.19, we can add `--replicas` flag with `kubectl create deployment` command:
      ```
      kubectl create deployment hr-web-app --image=kodekloud/webapp-color --replicas=2
      ```
     </details>

  7. Create a static pod named static-busybox on the controlplane node that uses the busybox image and the command sleep 1000.

     <details>

         k run static-busybox --image busybox --dry-run=client -o yaml --command -- sleep 1000 > static-busybox.yaml
    
      move the file to `/etc/kubernetes/manifests`
             
         mv static-busybox.yaml /etc/kubernetes/manifests/
    
      manifest file should look like this:
         
                 apiVersion: v1
                 kind: Pod
                 metadata:
                   creationTimestamp: null
                   labels:
                     run: static-busybox
                   name: static-busybox
                 spec:
                   containers:
                   - command:
                     - sleep
                     - "1000"
                     image: busybox
                     name: static-busybox
                     resources: {}
                   dnsPolicy: ClusterFirst
                   restartPolicy: Always
                 status: {}
         
  </details>

  8. Create a POD in the `finance` namespace named temp-bus with the image redis:alpine.

     <details>

     ```
     k run temp-bus --image=redis:alpine -n finance
     ```
     </details>

  9. A new application orange is deployed. There is something wrong with it. Identify and fix the issue.

       <details>
  
       ```
       kubectl describe pod orange
       ```
  
       Export the running pod using below command and correct the spelling of the command **`sleeeep`** to **`sleep`** 
  
       ```
       kubectl get pod orange -o yaml > orange.yaml
       ```
     
       Delete the running Orange pod and recreate the pod using command.
       
       ```
       k replace -f orange.yaml --force
       ```
       </details>

  10. Expose the hr-web-app as service hr-web-app-service application on port 30082 on the nodes on the cluster.

      <details>
        
          k expose deploy hr-web-app --name=hr-web-app-service --type NodePort --port 8080
        go to the svc and edit the `nodePort: 30082`

          k edit svc hr-web-app-service
      </details>

  12. Use JSON PATH query to retrieve the osImages of all the nodes and store it in a file /opt/outputs/nodes_os_x43kj56.txt.

      <details>

      ``` 
      kubectl get nodes -o jsonpath='{.items[*].status.nodeInfo.osImage}' > /opt/outputs/nodes_os_x43kj56.txt
      ```
      </details>

  13. Create a Persistent Volume with the given specification: -
      <br>Volume name: pv-analytics</br>
      <br>Storage: 100Mi</br>
      <br>Access mode: ReadWriteMany</br>
      <br>Host path: /pv/data-analytics</br>

      <details>
     
       ```
       apiVersion: v1
       kind: PersistentVolume
       metadata:
         name: pv-analytics
       spec:
         capacity:
           storage: 100Mi
         volumeMode: Filesystem
         accessModes:
           - ReadWriteMany
         hostPath:
             path: /pv/data-analytics
       ```
       </details>
       
