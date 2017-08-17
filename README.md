# kubernetes-exercise

Clone this repo:

```https://github.com/orezi/backup_restore.git```

#Step 1:

Sets up Mediawiki with mysql database running on one docker container.

```$ cd step_1```

**Run:**

```$ docker build -t <image-name>:<tag> .```
```$ docker run -d -p 80:80 <image-name>:<tag>```

- check ```http://localhost``` on the web browser to use mediawiki.

- Insert ```localhost:3306``` as **database host** during installation

- Insert `admin` as username and `pass` as password for database username and password

- Finish Installation

#Step 2.

Sets up Mediawiki using docker-compose on two separate containers that are linked.

```$ cd step_2```

**Run:**

```$ docker-compose up -d --build```

```$ docker ps -a``` ### should show two containers running (mediawiki and mysql)

```docker inspect mysql```  ### to show the ip of the mysql container (note down the IP)

visit ```http://localhost``` 

- Put in the IP address of mysql container from previous step and add port 3306 when asked to specify **database host**

example: 172.xx.x.x:3306

- Use `root` as username and `pass` as password after setting **mediawiki** as **Database name**

- Finish installation


#Step 3:

Sets up mediawiki and mysql using kubernetes.

```$ cd step_3```

- To setup mysql:

```$ kubectl create -f mysql```

- To setup mediawiki:

```$ kubectl create -f mediawiki```

#Step 4:

Sets up prometheus and grafana for monitoring of the kubernetes cluster
```$ cd step_3/step_4```

- To setup prometheus for monitoring of metrics:
```$ kubectl create -f prometheus```

- To setup grafan for visualization of metrics:
``` $ kubectl create -f grafana```

- To setup kube state metrics to expose metrics for prometheus to scrape:
``` $ kubectl create -f kube-state-metrics/kube-system```

#Verify kubernetes setup:

**Minikube setup**

```$ minikube service mediawiki-svc --url``` ###visit the url in the output to see mediawiki site

**OR (kubenetes cluster setup)** 

```$ kubectl describe service mediawiki-svc --url``` ###visit the url in the output to see mediawiki site

```$ kubectl describe service mysql-svc``` ###note the IP listed as endpoint

- Insert the IP noted in previous command as the **database host** during installation

- Insert ```root``` as username and ```pass``` as password during installation

- Finish installation.

**View Prometheus and Grafana dashboards

To get the IP address of the two services:

Prometheus:

- ```minikube service prometheus-svc --url``` or ```kubectl describe service prometheus-svc```

Grafana:
- ```minikube service grafana-svc --url``` or ```kubectl describe service grafana-svc```

**Import Grafana dashboards

- Login to grafana with ```admin``` as username and password

- You can add new dashboards by importing the JSON files located in step_3/step_4/grafana/dashboard-templates









