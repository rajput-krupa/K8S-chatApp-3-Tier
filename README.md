![image](https://github.com/user-attachments/assets/574d5635-78b7-49fb-80af-1734c1637db8)

## This project demonstrates a 3-tier chat application deployed on Kubernetes (Minikube).
The architecture consists of:
- Frontend: React or web client
- Backend: Flask/Node.js API
- Database: MongoDB
  
Each component runs in separate deployments, with persistent storage for MongoDB, exposed via services, and managed in a dedicated namespace. Docker images are pushed to Docker Hub for easy deployment.

## 🔹 Step 1: Clone the Git Repository
```bash
git clone https://github.com/rajput-krupa/K8S-chatApp-3-Tier
cd K8S-chatApp-3-Tier/k8s
```
## 🔹 Step 2: Build and Push Backend Docker Image (krupa/chatapp-backend:latest)
```bash
docker build -t krupa/chatapp-backend:latest .
docker push krupa/chatapp-backend:latest
```
## 🔹 Step 3: Build and Push Frontend Docker Image (krupa/chatapp-frontend:latest)
```bash
docker build -t krupa/chatapp-frontend:latest .
docker push krupa/chatapp-frontend:latest
```
## 🔹 Step 4: Pull MongoDB Docker Image (mongo:latest)
```bash
docker pull mongo:latest
```
## 🔹 Step 5: Create Kubernetes Namespace (chat-app)
```bash
kubectl apply -f namespace.yml
kubectl get ns
```
## 🔹 Step 6: Deploy Backend Deployment
```bash
kubectl apply -f backend-deployment.yml
```
## 🔹 Step 7: Deploy MongoDB Deployment
```bash
kubectl apply -f mongodb-deployment.yml
```
## 🔹 Step 8: Configure Persistent Volume and Persistent Volume Claim for MongoDB
```bash
kubectl apply -f mongodb-pv-pvc.yml
```
## 🔹 Step 9: Verify Pods in Namespace
```bash
kubectl get pods -n chat-app
```
## 🔹 Step 10: Create Services for Frontend, Backend, and MongoDB
```bash
kubectl apply -f frontend-service.yml
kubectl apply -f backend-service.yml
kubectl apply -f mongodb-service.yml
```
## 🔹 Step 11: Run Backend via Port Forwarding
```bash
kubectl port-forward service/backend -n chat-app 5001:5001
```
## 🔹 Step 12: Run Frontend via Port Forwarding
```bash
sudo -E kubectl port-forward service/frontend -n chat-app 80:80
```
## 🔹 Step 13: Enable Ingress and Access Application via Minikube
```bash
minikube addons enable ingress
kubectl get svc -n ingress-nginx
kubectl port-forward svc/ingress-nginx-controller
```


