###  deployment.yml 
       kind: Deployment
       apiVersion: apps/v1
       metadata:
         name: mydeployment
      spec:
        replicas: 2
        selector:      # tells the controller which pods to watch/belong to
           matchLabels:
              app: myspringbootapp
       template:
          metadata:
            labels:
              app: myspringbootapp
          spec:
             containers:
              - name: myspringbootapp
                image: vikashashoke/pipeline-demo
                imagePullPolicy: Always
                ports:
                  - containerPort: 80
                  
                  
### Deploy deployments on Minikube

        kubectl apply -f deployment.yml                  ## it'll create the deployments
        
        
### To List all the Objects we deployed using deployment.yml
        
        kubectl get all                                  ## To list all the objects we've deployed
        


### (Optional) Not Mentioned in the task but Exposing the Service Using nodeport to check


### Service.yml

    apiVersion: v1
    kind: Service
    metadata:  
      name: my-nodeport-service
    spec:
     selector:    
        app: myspringbootapp
     type: NodePort
     ports:  
      - name: http
        port: 80
        targetPort: 80
        nodePort: 30036
        protocol: TCP
        
### Applying the service.yml

      kubectl apply -f service.yml
      
### List the services
       
       kubectl get svc
       
### To Accesss the Spring boot Application 
 
        host_ip:nodeport    (host_ip:30036)
