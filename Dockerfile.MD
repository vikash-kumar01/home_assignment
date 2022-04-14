### Dockerfile

    FROM maven as build
    WORKDIR /app
    COPY . .
    RUN mvn install


    FROM openjdk:11.0
    WORKDIR /app
    COPY --from=build /app/target
    EXPOSE 9090
    CMD ["java","-jar","/app.jar"]
    
    
### Building Docker Image from Docker file
    
    docker image build -t sringbootapp .
    docker image tag sringbootapp vikashashoke/sringbootapp:1.0              # Version 1.0 (Optionl for version maintaining i did & pushed to dockerHUb for Kubernetes)
    docker image tag sringbootapp vikashashoke/sringbootapp:latest           # Version 1.0 Latest version
    


### Pushing Docker Images to DockerHub

    docker image push vikashashoke/sringbootapp:1.0          # Docker login needed before pushing the image
    docker image push vikashashoke/sringbootapp:latest
    
### Running docker image Exposing port 9090

    docker container run -itd --name  myspringbootapplication -p 9090:9090 vikashashoke/sringbootapp:latest /bin/bash         #Running container in detached mode
    




