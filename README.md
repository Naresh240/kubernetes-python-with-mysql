# python-with-mysql-database

# Pre-Requisites
    Docker
    EKS-Cluster
    ALB Ingress Controller
# Build Docker image using below command
    docker build -t naresh240/python-app:latest .
# Push Docker image to remote place
    docker login
    docker push naresh240/python-app:latest
# Encode PASSWORD of mysql using following command
    echo -n "admin123" | base64
# Deploy mysql using below command
    kubectl apply -f kubernetes/mysql/
# Connect to mysql pod
    kubectl exec -it <pod-name> -- /bin/bash
# Connect to mysql
    mysql -u naresh -p
  Provide password for mysql
# Connect to mysqldb
    use mysqldb
# Create "employee" table in mysqldb
    CREATE TABLE IF NOT EXISTS employee(empno VARCHAR(20),empname VARCHAR(20),salary VARCHAR(20));
    commit;
# Create Confing Map for identifing hostname of mysql server
    kubectl create configmap hostname-config --from-literal=mysql_host=$(kubectl get svc mysql-service -o jsonpath="{.spec.clusterIP}")
# Deploy python Application
    kubectl apply -f kubernetes/
# Check output of application using ingress
  ````PUT data using insertemployee````
  
  http://6fa5d906-default-pythoning-b984-74873513.us-east-1.elb.amazonaws.com/insertemployee
  
  ![image](https://user-images.githubusercontent.com/58024415/122684358-90809900-d222-11eb-97f9-662a324d2ee5.png)   
  
  ````GET data using listofemployees````
  http://6fa5d906-default-pythoning-b984-74873513.us-east-1.elb.amazonaws.com/listofemployees
  
  ![image](https://user-images.githubusercontent.com/58024415/122684493-46e47e00-d223-11eb-8ae2-2722347317f7.png)

    
