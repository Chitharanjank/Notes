#  Amazon EC2 (Elastic Compute Cloud)
Amazon EC2 is a cloud-based virtual server that allows you to run applications without maintaining physical hardware.

You can launch different types of instances based on your needs (CPU, RAM, storage, etc.).

EC2 instances are scalable, meaning you can increase or decrease resources as required.

Instances are billed on a pay-as-you-go model.

## EC2 Instance Types

### 1️ General Purpose (T, M Series) – Like a Normal Laptop 💻

Used for everyday tasks like hosting websites, small applications, and databases.
Example: T3, M5
Real-Life Example: A regular laptop used for watching YouTube, browsing, and working on MS Office.

#### 2️ Compute Optimized (C Series) – Like a Gaming PC 🎮

Used for tasks that need high CPU power, like gaming servers and data processing.
Example: C5, C6g
Real-Life Example: A gaming PC that runs games smoothly because of its powerful processor.

#### 3️ Memory Optimized (R, X Series) – Like a Supercomputer 🧠

Used for tasks that need a lot of RAM, like big databases and real-time analytics.
Example: R5, X1e
Real-Life Example: A supercomputer used for complex scientific research.

#### 4️ Storage Optimized (I, D Series) – Like a Hard Drive 🛢️

Used when you need very fast disk storage, like big data processing and log analysis.
Example: I3, D2
Real-Life Example: A high-speed SSD (Solid State Drive) that stores and retrieves data super fast.


#### 5 High-Performance Computing (HPC) – Like a NASA Supercomputer 🚀

Used for scientific calculations like weather prediction and space simulations.
Example: Hpc6a
Real-Life Example: A NASA supercomputer that calculates the path of planets.

#### 6. Accelerated Computing (P, G, Inf Series) – Like a Graphics Workstation (GPU-Powered)

These instances come with GPUs (Graphics Processing Units) for tasks that need parallel processing, like AI/ML training, and 3D rendering.

Examples: P3, G5, Inf1
Real-Life Example: A high-end graphics workstation that renders 3D animations, trains AI models, or processes high-resolution videos super fast.

###### How to Choose the Right Instance Type?
If you need a normal, balanced server, go for General Purpose (T, M).

If you need more speed, go for Compute Optimized (C).

If you need a lot of memory, go for Memory Optimized (R, X).

If you need fast storage, go for Storage Optimized (I, D).

If you need supercomputing, go for HPC (Hpc).

## EC2 Key Pair
A Key Pair (Public & Private Key) is used to securely connect to EC2 instances.

AWS stores the Public Key, and you download the Private Key (.pem file).

You use this key with SSH to log in:

```ssh -i <your-key.pem> ec2-user@your-instance-ip```

Losing the private key means you cannot access the instance.

## What is EC2 Tenancy?
EC2 tenancy determines how an Amazon EC2 instance is hosted on physical servers. It defines whether the instance runs on shared or dedicated hardware.

## Types of EC2 Tenancy

### 1. Shared Tenancy (Default)
Most cost-effective option.
Instances run on shared physical servers with other AWS customers.
Suitable for most workloads unless there are strict compliance or security requirements.

### 2. Dedicated Instance
Runs on hardware dedicated to a single AWS account.
May share hardware with other instances from the same account.
Provides some isolation but not full control over the underlying host.
More expensive than shared tenancy.

### 3. Dedicated Host
Provides an entire physical server dedicated to a single AWS account.
Full control over instance placement on the host.
Required for some licensing and compliance requirements (e.g., BYOL – Bring Your Own License).
More expensive than Dedicated Instances.
