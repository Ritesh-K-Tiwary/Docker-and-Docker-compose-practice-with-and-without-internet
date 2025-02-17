# Docker-and-Docker-compose-practice-with-and-without-internet

Setting up Docker and Docker Compose in two scenarios:  

1. **With Internet (Online Installation)** – Using official repositories.  
2. **Without Internet (Offline Installation)** – Downloading and transferring required files manually.  

---

## **1️⃣ Online Installation (With Internet)**  

### **Step 1: Uninstall Old Versions (If Any)**  
```bash
sudo apt remove docker docker-engine docker.io containerd runc
```

### **Step 2: Update and Install Required Dependencies**  
```bash
sudo apt update
sudo apt install -y ca-certificates curl gnupg lsb-release
```

### **Step 3: Add Docker’s Official GPG Key**  
```bash
sudo mkdir -m 0755 -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo tee /etc/apt/keyrings/docker.asc > /dev/null
```

### **Step 4: Add Docker Repository**  
```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### **Step 5: Install Docker Engine & Docker Compose**  
```bash
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose docker-compose-plugin
```

### **Step 6: Start & Enable Docker**  
```bash
sudo systemctl start docker
sudo systemctl enable docker
```

### **Step 7: Verify Installation**  
```bash
docker --version
docker-compose --version
```
Run a test container:
```bash
sudo docker run hello-world
```

---

## **2️⃣ Offline Installation (Without Internet)**  
If your target machine has no internet access, you need to download packages on a different machine and transfer them manually.

### **Step 1: Download Docker Packages**
On an internet-connected machine, run:
```bash
mkdir docker-offline && cd docker-offline
apt download docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-compose
```
This will download all required `.deb` packages.

### **Step 2: Transfer to Target Machine**
Copy the `docker-offline` folder to the machine without internet using USB, SCP, or other means.

### **Step 3: Install Docker Manually**
On the offline machine, navigate to the copied folder:
```bash
cd /path/to/docker-offline
sudo dpkg -i *.deb
```
If any dependencies are missing, you may need to manually download and transfer them as well.

### **Step 4: Start Docker Service**
```bash
sudo systemctl start docker
sudo systemctl enable docker
```

### **Step 5: Verify Installation**
```bash
docker --version
docker-compose --version
```

---

Now, Docker and Docker Compose should be installed! Let me know if you need further assistance. 🚀
