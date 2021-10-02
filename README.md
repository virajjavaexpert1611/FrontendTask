# Guide
Commands to run the html view file with docker

1. To build the docker-image of the html file

        docker build -t viraj/fe-get-user-name .

2. To run the generated docker-image of the html file

        docker run -it -d -p 8080:80 viraj/fe-get-user-name

3. The output will be visible at http://localhost:8080/index.html

4.  Before building docker image, deploy Backend service and get its URL and update same into index.html file, 

        url: "http://localhost:8081/get-user",
        
        Change http://localhost:8081 to service URL on which be-app is running.

5. Helm chart is added into fe directory.

6. To deploy helm chart,
    
      helm upgrade -i fe-app fe/ --values fe/values.yaml

7. To access service from browser, 

        export NODE_PORT=$(kubectl get --namespace demo -o jsonpath="{.spec.ports[0].nodePort}" services fe-app)
        export NODE_IP=$(kubectl get nodes --namespace demo -o jsonpath="{.items[0].status.addresses[0].address}")
        echo http://$NODE_IP:$NODE_PORT


# Notes:-
1. Update docker image reference and tag in values.yaml file,

        image:
          repository: viraj/fe-get-user-name            ==> Update docker image
          pullPolicy: IfNotPresent
          # Overrides the image tag whose default is the chart appVersion.
          tag: "v3"                        ==> Update tag

2. Update service type and port according to app configuration if required,

          service:
            type: NodePort           
            port: 80

        ## service type can be change to clusterIP if required.


3. Enable HPA if required,
      
        autoscaling:
          enabled: false
          minReplicas: 1
          maxReplicas: 100

        set above enabled: true and replicacounts


