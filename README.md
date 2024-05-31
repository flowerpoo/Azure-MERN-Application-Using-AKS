# Azure-MERN-Application-Using-AKS- deployment

* Clone the git repository
```
https://github.com/UnpredictablePrashant/SampleMERNwithMicroservices
```
* Try to run in local and then create a docker file for each service.
* backend hello service 
```
FROM node:18
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 4200
CMD [ "node","index.js" ]
```
* backend profile service 

```
FROM node:18
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 4201
CMD [ "node","index.js" ]

```
* frontend
```
FROM node:18
WORKDIR /app
COPY package*.json /app
RUN npm install
COPY . /app
EXPOSE 3000
CMD [ "npm","start" ]

```
* create a repository in docker hub and then pushed all the images to docker hub.
```
docker build -t flowerking21/micro_backend_helloservice:latest .
docker build -t flowerking21/micro_backend_profileservice:latest .
docker build -t flowerking21/micro_frontendservice:latest .

docker push flowerking21/micro_backend_helloservice:latest 
docker push flowerking21/micro_backend_profileservice:latest
docker push flowerking21/micro_frontendservice:latest
```

* Create AKS cluster 
```  
Go to Kubernetes service -> Create Kubernetes cluster -> create resource group -> cluster name & availability zones & kubernetes version & Authentication and Authorization -> Node pools (Adjust node size if needed ) -> Networking configure to Azure CNI & DNS name & network policy -> Integrations (create container registery) -> Monitoring Enable container logs -> Tags if needed -> Review and create 
```

* login into your azure account 
```
az login
```
* kubectl command to store credencials in kube config file

```
az aks get-credentials --resource-group aks-group --name micro-cluster1
```

* Deployent 

```
kubectl apply -f deploy.yaml
```
* validation
```
kubectl get pods
kubectl get svc 

```
* make sure your ip address configured with DNS server.

* Everything done well we will get the output as mentioned below 

* profile service 
![alt text](<pic/profile service.PNG>)

* hello service 
![alt text](<pic/hello service.PNG>)

* Frontend service 
![alt text](<pic/react application.PNG>)

Done
Happy Learning !!!!
