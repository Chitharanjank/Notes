# AWS Auto Scaling 

## 1. What is Auto Scaling?
- **Auto Scaling** automatically **adds** or **removes** resources based on demand.
- Helps optimize **performance, availability, and cost**.
- Works with **EC2 instances, ECS services, DynamoDB, Aurora, and more**.

---

## 3. Benefits of Auto Scaling
✅ **High Availability**: Ensures the required number of instances are always running.  
✅ **Cost Optimization**: Removes **idle instances**, reducing AWS costs.  
✅ **Performance Improvement**: Adds instances when traffic increases.  
✅ **Fault Tolerance**: Replaces **unhealthy** instances automatically.  

---

## 4. How Auto Scaling Works
1. **Create an Auto Scaling Group (ASG)**
   - Defines the **minimum, maximum, and desired number of instances**.
   - Spreads instances across **multiple Availability Zones (AZs)**.

2. **Attach a Load Balancer (Optional)**
   - Distributes traffic among healthy instances.
   - Works with **ALB, NLB, or CLB**.

3. **Define Scaling Policies**
   - Sets conditions for adding/removing instances.

4. **Monitor and Adjust**
   - Uses **Amazon CloudWatch** for monitoring.

---

## 6. Auto Scaling Components

| Component | Description |
|-----------|-------------|
| **Launch Template** | Defines EC2 instance settings (AMI, instance type, security groups, key pairs). |
| **Auto Scaling Group (ASG)** | Manages EC2 instances across Availability Zones. |
| **Scaling Policies** | Define when and how scaling happens. |
| **Health Checks** | AWS checks instance health and replaces failed instances. |
| **Load Balancer (Optional)** | Distributes traffic to healthy instances. |

---

## 7. Configuring EC2 Auto Scaling

1. **Create a Launch Template**  
   - Go to EC2 Console → **Launch Templates** → Create a template.  
   - Choose **AMI, instance type, key pair, security group**.

2. **Create an Auto Scaling Group (ASG)**  
   - Go to **EC2 Auto Scaling** → Create ASG.  
   - Attach the **Launch Template**.  
   - Set **minimum, maximum, and desired instances**.  
   - Select **Availability Zones (AZs)**.

3. **Set Scaling Policies**   
   - Example: Keep **CPU utilization at 50%**.

4. **Attach Load Balancer (Optional)**  
   - Distributes traffic among instances.  
   - Recommended for **high-traffic applications**.

5. **Review and Create**  
   - AWS starts managing instances based on policies.

---

## 8. Monitoring Auto Scaling

🔹 **Amazon CloudWatch**  
   - Monitors **CPU usage, memory, network traffic, and requests per second**.  
   - Can trigger alarms to **scale up/down**.

🔹 **AWS Auto Scaling Dashboard**  
   - Shows **scaling activities, instance health, and policy status**.

🔹 **AWS CloudTrail**  
   - Logs all **Auto Scaling API calls** for auditing.

---

## 10. Auto Scaling vs Load Balancer

| Feature | Auto Scaling | Load Balancer |
|---------|-------------|--------------|
| **Purpose** | Adds/removes instances | Distributes traffic |
| **Component Managed** | EC2 Instances | Incoming Requests |
| **Scaling Type** | Vertical (instance count) | Horizontal (traffic routing) |
| **Example** | Adds instances when CPU > 70% | Routes traffic to healthy instances |

---