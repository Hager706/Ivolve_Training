# AWS VPC with Public & Private EC2 Instances

##  Objective
This project sets up an **AWS infrastructure** with:
- A **Public Subnet** containing a **Bastion Host (EC2)**
- A **Private Subnet** containing a **Private EC2**
- **SSH access** to the **Private EC2** using **SSH Agent Forwarding** (No key transfer required)
- **Security groups** to enforce access control

---

## 🏗 Architecture Diagram
```
+----------------+           +----------------+
|                |           | Bastion Host   |
| (Local Machine)| --------> | Public EC2     | --------> Private EC2
|                |   SSH     | 10.0.1.41      |   SSH     10.0.2.100
+----------------+           +----------------+
      🔑                  🔑
```

---

## **1️⃣ Create VPC & Subnets**
### **1.1 Create VPC**
- CIDR: `10.0.0.0/16` (allows multiple subnets)
### **1.2 Create Public Subnet**
### **1.3 Create Private Subnet**

---

## **2️⃣ Configure Internet Access**
### **2.1 Create an Internet Gateway**
### **2.2 Create a Route Table for the Public Subnet**

!\[Alt text\](Screen1.png)

---

## **3️⃣ Configure Security Groups**
### **3.1 Create Bastion Host Security Group**

- **Allows SSH from my ip**
!\[Alt text\](Screen2.png)

### **3.2 Create Private EC2 Security Group**

- **Only allows SSH from Bastion Host**
!\[Alt text\](Screen3.png)

---

## **4️⃣ Launch EC2 Instances**
### **4.1 Launch Bastion Host (Public EC2)**

- ✅ **Public IP Assigned** for SSH access
!\[Alt text\](Screen4.png)


### **4.2 Launch Private EC2**

- ❌ **No Public IP** (private access only)
!\[Alt text\](Screen5.png)

---

## **5️⃣ SSH Access via Bastion Host**
### **5.1 Start SSH Agent on local**
```sh
eval "$(ssh-agent -s)"
```

### **5.2 Add Your Private Key to SSH Agent**
```sh
ssh-add ~/.ssh/my-key.pem
```
!\[Alt text\](Screen6.png)

### **5.3 SSH into the Bastion Host (Public EC2)**
```sh
ssh -A -i ~/.ssh/my-key.pem ec2-user@<Bastion_Public_IP>
```

### **5.4 SSH from Bastion Host to Private EC2**
```sh
ssh ec2-user@<Private_EC2_Private_IP>
```
!\[Alt text\](Screen7.png)

- **Done! You're inside the Private EC2 🚀**


---


