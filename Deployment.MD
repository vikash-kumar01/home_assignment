###  deployment.yml 
       kind: Deployment
       apiVersion: apps/v1
       metadata:
         name: mrdevops
      spec:
        replicas: 2
        selector:      # tells the controller which pods to watch/belong to
           matchLabels:
              app: mrdevops
       template:
          metadata:
            labels:
              app: mrdevops
          spec:
             containers:
              - name: mrdevops
                image: vikashashoke/pipeline-demo
                imagePullPolicy: Always
                ports:
                  - containerPort: 80
                  
                  
### Deploy deployments on Minikube

        kubectl apply -f deployment.yml                  ## it'll create the deployments
        
        
### To List all the Objects we deployed using deployment.yml
        
        kubectl get all                                  ## To list all the objects we've deployed
        
