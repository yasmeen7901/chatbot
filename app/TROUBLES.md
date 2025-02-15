# Troubleshooting Notes for My Kubernetes Project

## 1. Issue: Unable to Create Pods Due to Taint and Toleration
### **Problem:**
Before starting this project, I practiced taints and tolerations on my nodes. Because of that, when I tried to create pods for my project, they weren’t getting scheduled properly.

### **Solution:**
I removed the taints using:
```bash
kubectl taint nodes <node-name> key=value:NoSchedule-
```
After untainting, my pods started running successfully.

---

## 2. Issue: Unable to Access Service Externally
### **Problem:**
Initially, I used **ClusterIP** as my service type. Since ClusterIP only allows internal communication within the cluster, I couldn’t access my application from outside.

### **Solution:**
After deciding to do this project, I was unaware about WebSockets. Then, I researched about it and used it in my project.

I changed the service type from ClusterIP to NodePort and assigned port **30080** to expose it externally:
```yaml
  type: NodePort
  ports:
    - nodePort: 30080
```
After this change, I was able to access my service using:
```bash
http://<node-ip>:30080
```

---

## 3. Issue: Port-Forwarding Not Working Properly
### **Problem:**
When I tried to use port-forwarding to access my application, I wasn’t using the command correctly.

### **Solution:**
I fixed it by running the correct command:
```bash
kubectl port-forward svc/chat-service 8080:80
```
This allowed me to access the application on:
```bash
http://localhost:8080
```

---

## 4. Issue: Not Getting Expected Output in Browser
### **Problem:**
After setting up everything, I expected to see **"Welcome to chat"** in my browser when I accessed the service, but it wasn’t working. The issue was that I was only running the server without setting up proper ingress or a LoadBalancer.

### **Solution:**
Since I didn’t want to use an **Ingress Controller** or a **LoadBalancer** due to cost concerns, I decided to test the connection in the terminal itself using **wscat** instead of the browser.

I installed wscat:
```bash
npm install -g wscat
```
Then, I connected to the WebSocket server using:
```bash
wscat -c ws://<node-ip>:30080
```
Once connected, I was able to send messages to the server and receive the same response back, confirming the connection was working properly.

---

## **Final Thoughts:**
This project taught me a lot about Kubernetes networking, troubleshooting taints, and exposing services properly. The biggest takeaway was understanding that **without ingress or a LoadBalancer, browser access is limited**, but using a terminal-based approach like **wscat** can help verify WebSocket connections effectively.

