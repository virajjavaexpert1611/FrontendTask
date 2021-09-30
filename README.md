Commands to run the html view file with docker

1) To build the docker-image of the html file
    
		docker build -t frontend-task/get-user-name .

2) To run the generated docker-image of the html file
    
		docker run -it -d -p 8080:80 frontend-task/get-user-name

The output will be visible at http://localhost:8080/index.html
