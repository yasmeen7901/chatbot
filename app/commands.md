 A list of all the commands used for  **Real-Time Chat** project:


### **1️⃣ Project Setup**
```bash
mkdir real-time-chat && cd real-time-chat
touch server.js package.json Dockerfile deployment.yaml service.yaml hpa.yaml
npm init -y
npm install ws
```

---

### **2️⃣ Docker Image Creation**
```bash
docker build -t real-time-chat .
docker run -d -p 8080:8080 real-time-chat
docker ps
docker tag real-time-chat <your-dockerhub-username>/real-time-chat:latest
docker push <your-dockerhub-username>/real-time-chat:latest
```

---

### **3️⃣ Kubernetes Deployment**
```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl apply -f hpa.yaml
kubectl get pods
kubectl get services
kubectl get hpa
kubectl port-forward service/real-time-chat-service 8080:8080
```

---

### **4️⃣ Scaling & Monitoring**
```bash
kubectl scale deployment real-time-chat-deployment --replicas=5
kubectl get pods --watch
kubectl logs <pod-name>
```

---

### **5️⃣ Cleanup**
```bash
kubectl delete -f deployment.yaml
kubectl delete -f service.yaml
kubectl delete -f hpa.yaml
```

**6️⃣ RUN**

wscat -c ws://<EXTERNAL-IP>:8080



---

That's it! 🚀
