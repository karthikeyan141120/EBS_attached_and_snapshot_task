# AWS EC2 and EBS Lab

## Objective

* Launch Linux and Windows EC2 instances
* Install web servers (Apache and IIS)
* Create and attach a 5 GB EBS volume
* Create a snapshot of the volume
* Create a new EBS volume from the snapshot

## Services Used

* Amazon EC2
* Amazon EBS
* VPC
* Security Groups

## Prerequisites

* AWS account
* EC2 key pair
* Default VPC
* Security group allowing:

  * SSH (22)
  * RDP (3389)
  * HTTP (80)

## Steps

### 1. Launch EC2 Instances

**Linux Instance**

* AMI: Amazon Linux 2023
* Instance type: `t2.micro`

**Windows Instance**

* AMI: Windows Server 2022 Base
* Instance type: `t3.medium`

> Ensure both instances have a public IP address.

### 2. Configure Web Servers

**Linux (Apache)**

```bash
sudo dnf install httpd -y
sudo systemctl enable --now httpd
echo "<h1>Linux Web Server Running</h1>" | sudo tee /var/www/html/index.html
```

**Windows (IIS)**

```powershell
Install-WindowsFeature -Name Web-Server -IncludeManagementTools
```

Create `C:\inetpub\wwwroot\index.html` with sample content.

### 3. Create and Attach EBS Volume

* Create a `5 GiB` gp3 EBS volume
* Use the same Availability Zone as the EC2 instance
* Attach the volume to the instance

**Linux**

```bash
sudo mkfs -t xfs /dev/xvdf
sudo mkdir /data
sudo mount /dev/xvdf /data
```

**Windows**

* Open Disk Management
* Initialize the disk
* Create and format a new volume

### 4. Create Snapshot

* Go to **EC2 → Volumes**
* Select the EBS volume
* Choose **Create Snapshot**

### 5. Create Volume from Snapshot

* Go to **EC2 → Snapshots**
* Select the snapshot
* Choose **Create Volume from Snapshot**

## Verification Checklist

* [x] Linux EC2 launched
* [x] Windows EC2 launched
* [x] Web servers accessible
* [x] 5 GB EBS volume created and attached
* [x] Snapshot created
* [x] New volume created from snapshot

## Cleanup

Terminate EC2 instances and delete unused volumes and snapshots to avoid charges.
