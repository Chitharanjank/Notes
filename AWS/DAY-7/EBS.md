# EBS

## What is AWS EBS?
Amazon Elastic Block Store (EBS) is a block-level storage service provided by AWS.
It is primarily used to store data for EC2 instances (Virtual Servers) in AWS. EBS volumes can be attached to EC2 instances to provide persistent storage, meaning the data remains even if the EC2 instance is stopped or terminated.

## Key Concepts
EBS Volumes: These are virtual disks that you attach to EC2 instances. They appear as block devices, similar to hard drives, but they reside in the cloud.

Persistence: Data stored in EBS volumes remains intact after you stop or terminate your EC2 instance (unlike instance store volumes, which are temporary).

Snapshots: You can create backups of EBS volumes using snapshots, which can be stored in Amazon S3. Snapshots allow you to restore the data or create new volumes from them.

Performance: EBS provides various volume types that vary in performance, including General Purpose SSD (gp2, gp3), Provisioned IOPS SSD (io1, io2), and Magnetic (st1, sc1).

## Volume Types
General Purpose SSD (gp2/gp3): Good for most workloads, like boot volumes and small-to-medium databases.

Provisioned IOPS SSD (io1/io2): High-performance volumes for workloads that require low latency and high throughput (e.g., large databases).

Throughput Optimized HDD (st1): Designed for workloads with large, sequential I/O, such as big data or log processing.

Cold HDD (sc1): Ideal for infrequently accessed data like backups.

Magnetic (standard): Older, lower-cost option. Rarely used now in modern environments.

## How to Create and Attach an EBS Volume
### Create a Volume

Go to the EC2 dashboard in AWS Management Console.

Select Volumes from the sidebar, then click Create Volume.

Choose the volume type, size, and availability zone (must match the EC2 instance's zone).

### Attach the Volume

Select the created volume, click Actions, and select Attach Volume.
Select the instance to attach it to and assign a device name (e.g., /dev/sdf).
Mount the Volume (after attachment)

### Log into the EC2 instance and mount the volume on the operating system

### Create a Mount Point
   
     mkdir <mount_point-name>

### 1. TEMPORARY MOUNT

###### Check is there any data in the Volume

        file -s <dev_name>

 - If the output is data, it means the volume does not have a file system (or it's empty).
 - If it shows something like ext4 or xfs, then it means the volume already has a file system.
       
If the volume is empty or unformatted, you'll need to format it with a file system. 
This step is necessary if ```file -s <dev_name>``` shows data as the output.
       
        mkfs -t ext4 <dev_name>

##### Mount the volume 

        mount <dev_name> <mount_point_name>

### 2. PERM MOUNT

 - Before mounting make sure to convert it to linux file system only if volume is empty
 
To mount the secondary EBS volume permanently, so it remains mounted even after an EC2 restart, you need to add an entry in the /etc/fstab file.

#### Create a Backup of /etc/fstab
It’s always good practice to make a backup of important configuration files before making changes to them. This allows you to restore the original file if something goes wrong.

     cp /etc/fstab /etc/fstab.back

#### Add entry infstab

    <dev_name> <mounting_point> <file-system>  defaults,nofail   0  0

Here’s what each part means:
/dev/nvme1n1: The device name for the EBS volume.

/mnt/my-ebs: The mount point where the volume will be mounted.

ext4: The file system type (this could be xfs or another file system depending on what you formatted the EBS volume with).

defaults: The default mount options.

nofail: This ensures that the system will not fail to boot if the volume is not available (e.g., if the volume is not attached).
0 0: These values are used by dump and fsck utilities for backup and file system checks, respectively. Most of the time, you'll use 0 0 for non-root file systems.



##### Refresh

After adding the entry to /etc/fstab, you can use the mount -a command to apply the changes and mount all file systems listed in the /etc/fstab file

        mount -a

### Unmount
for unmounting ypu can use
         umount <dev_name>

# Architecture
![My Image](/Images/EBS.jpg)
