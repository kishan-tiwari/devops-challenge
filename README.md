# DevOps Challenge

## What’s the difference between vertical and horizontal scaling?
- In vertical scaling we can increase the cpu or mem of resource instead of adding additional server. But in horizontal scaling, we can add multiple server parallel for handle traffic. Both scaling have there own pros/cons and usecase.

## If we want to execute a predefined script every day at a specific time, how can we achieve that?
- If we are using linux machine then we can use cron job to schedule script every day (example : 0 8 * * *) and if we are using windows machine then we can schedule the script  with windows scheduler

## Provide steps to set up nginx reverse proxy, as well as reasons for it.
- Reason : -
    - Hide identity  of application
    - Run multiple server behind single domain
    - A/B testing
    - Use nginx features like URI based routing/rate limit/user block/request forwarding

- Configure reverse proxy for nodejs app
    - create a virtual host file /etc/nginx/conf.d/example.com.conf
    - nginx -t (for nginx syntax and conf check)
    - systemctl restart nginx (reflect nginx change )
```
server {
    listen 80;
    server_name example.com;

    location / {
        proxy_set_header   X-Forwarded-For $remote_addr;
        proxy_set_header   Host $http_host;
        proxy_pass         http://127.0.0.1:3000;
    }
}
```

## When would you use k8s, and when would you not? Support your answer with an example.
- Why we will use K8s
    - for microservice based application
    - manages multiple pods 
    - service to service communication application
    - for small application
    - horizontal scaling 
    - for stateless application
    - different application stack (nodejs, ruby, python, java etc)

- Why we will not use K8s
    - for large monolith application 
    - for stateful application
    - high resource consumption application
    - vertical scaling

## What is the most common file format to configure and run k8s workloads?
- In k8s we are using YAML for managing k8s workloads.

## What is a k8s pod?
- Pod is smallest unit in k8s which is act like a shell for container. which provide specific ip address/storage/sidecar etc

## What is a k8s ingress resource and what is it used for?
- In k8s ingress act like a security guard which is the first layer of interaction for the upcoming traffic. Its use for exposing application to outside of the world. 

## How to manage environment variables and secrets under k8s.
- We can use k8s secret object for managing environment variables and secret for k8s application.

## From your local terminal, how can you remotely connect to a k8s cluster in the cloud and have full management access?
- we can installed kubectl  binary to interact with kubernetes cluster api. We need to allow specific  user in config/auth for privileges. What users can access in k8s.

## What are the benefits of using IaaC infrastructures like Terraform? Can you briefly describe the flow working with this tool?
- IAC Benefits :-
    - Managing infra in form of source code
    - Better versioning
    - Better consistency
    - Better management
    - Better Compilance

- IAC flow (Terraform)
    - write
    - plan
    - review 
    - apply

## Assuming we have an EC2 t3a.small instance running that is managed with Terraform, the local configuration file is edited and the instance type is changed to t3a large, if the terraform apply command is run, what would happen?
- Terraform shows error that state is not same. Because terraform manages state for infra and if we manually change something then remote state is not match.

## Can you describe what a monitoring system is and expand with some examples on how it can be used and for what reasons/benefits and what’s the difference between metrics  & logs?
- Monitoring system is use to check the health of application or server that its healthy or not.
    - example : if we running an application over ec2 instance then its important to monitor there cpu/mem/disk/nework in/nework out for application high availability. Its just like human health if we didn't care then it can kill human. So we need to check these metrics for better visibilty and sever health.

- Differnce b/w metrics and logs
    - Metrics are usually measured over intervals of time. for example system load for 1min/5min/15min 
    - logs are events which have information about the activity for a specific time period

## How would you open a shell to get into a running container? (what would be the exact command you would run to achieve that)
- docker exec -dit nginx-app bash
    - dit stands for detach interactive tty

## Can you explain the basic differences between relational and non relational DBs, and provide some use cases when one architecture would be better than the other?
- Major differnce b/w relational and non-relational db is the data store structure. In relational db dat store in the form of table and coloumn. But in non-relational db data is store in the form of JSON.

- Both db has better than other. But 
    - if we aware about the data then its good to use relational db
    - if we have predefined schema then use relational db
    
    - if we are not sure about db schema then we can use non-relational db
    - easy horizontal scaling

##  You have ssh access to an Ubuntu or Debian Linux server, the disk is full and you need to clean it up, what would you do and which specific commands should you run?
- df -TH (check volume use percentage)
- cd / && du -sh *   (check which directory taking a lot of resource)

## Assuming you have a Kubernetes workload running a set of microservices in production, the cluster was provisioned with Terraform. The k8s cluster is running under version 1.20. The version 1.21 has been released and we want to upgrade the cluster. What's the best approach you may take to upgrade the cluster without disturbing the entire workload and without any downtime ?
- According to me we need to parallel create a new cluster and test everything with latest k8s version 1.21. Then we need to upgrade k8s component one by one if everything working fine in new cluster with terraform.


