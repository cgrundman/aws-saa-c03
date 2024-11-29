# AWS Solution Architect Associate
<img src="https://images.credly.com/images/0e284c3f-5164-4b21-8660-0d84737941bc/twitter_thumb_201604_image.png" width="100" />

Learning materials for AWS Solution Architect Associate Certification (AWS-SAA-C03).

Information on the exam can be found [here](https://aws.amazon.com/certification/certified-solutions-architect-associate/).

Domains of material covered in the exam: 
* Design Resilient Architectures
* Design High-Performing Architectures
* Design Secure Architectures
* Design Cost-Optimized Architectures

## <img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/EC2.png" width="50"/> EC2 - Elastic Compute Cloud

### IP Types

Public IP - IPv4 (common) or IPv6 (IoT), can be observed anywhere in public space

Private IP - Only devices on network can see the IP address

Elastic IP - can change to work when instance is stopped and started (not rebooted)

### Placement Groups

<img src="https://github.com/cgrundman/aws-saa-c03/blob/main/images/cluster_placement_group.jpg" width="300"/>

#### Cluster Placement Group

Use Case: Low latency and fast, mostly for data processing and in bursts

<img src="https://github.com/cgrundman/aws-saa-c03/blob/main/images/spread_placement_group.jpg" width="300"/>

#### Spread Placement Group

Use Case: high availability and reliability, only 7 instances per placement group, used for continuous running applications that need to be available

<img src="https://github.com/cgrundman/aws-saa-c03/blob/main/images/partition_placement_group.png" width="300"/>

#### Partition Placement Group

Use Case: 7 partitions per AZ and 100s of EC2 instances, used for large distributed and replicated workloads 

### <img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/ENI.png" width="50"/> ENI - Elastic Network Interface

<ul>
  <li>component in a VPC that represents a virtual network card</li>
  <li>implemented in same AZ as EC2 instance</li>
  <li>
    can have:
    <ol>
      <li>1 primary IPv4, one or more scondary IPv4</li>
      <li>1 elastic IP (IPv4) per private IP</li>
      <li>1 public IP</li>
      <li>1 or more security groups</li>
      <li>a MAC address</li>
    </ol>
  </li>
</ul>

### EC2 Hibernate

*stop* - data on the disk of the instance is held until start

*terminate* - data on the disk is lost

*hibernate* - in-memory (RAM) is preserved, faster boot time, RAM written onto EBS volume, EBS volume must be encrypted

### EC2 Instance Store

EBS Volumes are network drives with good but limited performance. EC2 is a high-performance hardware disk-like network drive. The instance store features:
<ul>
  <li>Better I/O performance</li>
  <li>Lose storage if they are stopped (ephemeral)</li>
</ul>

Use case: Good buffer, cache, scratch data, temporary content, Risk data loss if hardware fails, backups and replications are admin's responsibility.

### <img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/AMI.png" width="50"/> AMI Overview

Description: AMI's are a customization of an EC2 Insance. AMI's are built for specific regions and can be copied for a specific region. EC2 instances can be launched from:
<ul>
  <li>a public AMI (amazon provided)</li>
  <li>your own AMI</li>
  <li>AWS Marketplace AMS</li>
</ul>

Process:
<ol>
  <li>Start an EC2 instance and customize it.</li>
  <li>Stop the instance.</li>
  <li>Build an AMI - this will also create EBS Snapshots</li>
  <li>Launch instances from other AMI's.</li>
</ol>

<img src="https://github.com/cgrundman/aws-saa-c03/blob/main/images/AMIProcess.png" width="300"/>

## <img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/Auto-Scaling.png" width="50"/> Auto Scaling

### Auto Scaling Groups

Goals:
<ul>
  <li>scale out (add EC2 instances) to match an increased load</li>
  <li>scale in (remove EC2 instances) to match decreased load</li>
  <li>ensure minimum and maximum EC2 instances running</li>
  <li>automatically register as load balancer</li>
  <li>recreate unhealthy instances</li>
</ul>

### ASG Attributes

**Launch Template** - AMI + Instance type, EC2 user data, EBS volumes, security groups, SSH key pair, IAM roles for EC2 instances, network and subnet information, load balancer information

**Min/Max Size**

**Initial Capacity**

### ASG CloudWatch Alarms

Can be used to trigger ASG

### ASG Scaling Policies

<ul>
  <li>
    Dynamic Scaling
    <ul>
      <li>
        Target Tracking Scaling
        <ul>
          <li>simple setup</li>
          <li>ex: avg. ASG CPU to stay around 40%</li>
        </ul>
      </li>
      <li>
        Simple/Step Scaling
        <ul>
          <li>CloudWatch Alarm (CPU > 70%), add 2 units</li>
          <li>CloudWatch Alarm (CPU < 30%), remove 1 unit</li>
        </ul>
      </li>
    </ul>
  </li>
  <li>
    Scheduled Scaling
    <ul>
      <li>anticipate scaling based on known usage patterns</li>
    </ul>
  </li>
  <li>
    Predictive Scaling
    <ul>
      <li>control forecast and schedule scaling ahead</li>
    </ul>
  </li>
</ul>

Metrics to scale on:
<ul>
  <li>CPU Utilization: average CPU utilization across instances</li>
  <li>Request Count Per Target: stable number of requests per instance</li>
  <li>Average network In/Out</li>
  <li>Custom Metric</li>
</ul>

### ASG Scaling Cooldowns

During cooldown, there is no launching new instances or terminating instances to stabilize metrics after stabilize.

## <img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/DynamoDB.png" width="50"/> DynamoDB

## <img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/EBS.png" width="50"/> EBS - Elastic Block Store

### <img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/EBSVolumes.png" width="50"/> EBS Volumes

<ul>
  <li>these are network drives that you can attach to your instances while they can.</li>
  <li>allows EC2 instances to persist data</li>
  <li>mounted to one instance at a time</li>
  <li>bound to specific availability zone</li>
  <li>free under 30GB/month</li>
</ul>

Can be detached and reattached to other instances. Capacity must be provisioned in advance (size in GB and IOPS). Volumes delete upon termination by default for root volumes and off for all other volumes.

### <img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/EBSSnapshots.png" width="50"/> EBS Snapshots

<ul>
  <li>backup of an EBS volume at a point in time</li>
  <li>not necessary to attach volume but recomended</li>
  <li>can copy snapshots across AZ's or regions</li>
</ul>

<img src="https://github.com/cgrundman/aws-saa-c03/blob/main/images/EBSSnapshots.png" width="300"/>

### EBS Snapshot Archive

Snapshots can be moved to an "archive tier" that is 75% cheaper. Takes 24 to 72 hours to restore. 

### Recycle Bin for EBS Snapshots

Can be setup with rules to retain deleted EBS Snapshots to recover from accidental deletion. Rules specify retention time (1 day - 1 year).

### FSR - Fast Snapshot Restore

Forces full initialization of snapshot to have no latency on first use, but is very expensive.

### <img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/EBSVolumeTypes.png" width="50"/> EBS Volume Types

<table>
  <head>
    <tr>
      <td>Type</td>
      <td>Description</td>
    </tr>
  </head>
  <body>
    <tr>
      <td>gp2/gp3 (SSD)</td>
      <td>General purpose SSD vlume that balances price and performance for wide variety of workloads.</td>
    </tr>
    <tr>
      <td>io1/io2 Block Express (SSD)</td>
      <td>Highest performance SSD volume for mission-critical low latency or high throughput workloads.</td>
    </tr>
    <tr>
      <td>stl (HDD)</td>
      <td>Low cost HDD volume designed for frequently accessed throughput-intense workloads.</td>
    </tr>
    <tr>
      <td>sol (HDD)</td>
      <td>Lowest cost HDD volume designed for less frequently accessed workloads.</td>
    </tr>
  </body>
</table>

Characterized by size/throughput/IOPS (I/O Operations per second). Only gp2/gp3 and io1/io2 Block Express can be used as boot volumes.

<table>
  <head>
    <tr>
      <td colspan="4"><h2>Use Cases</h2></td>
    </tr>
    <tr>
      <td colspan="2"><h4>General Purpose SSD</h4></td>
      <td colspan="2"><h4>Provisioned IOPS (PIOPS) SSD</h4></td>
    </tr>
  </head>
  <body>
    <tr>
      <td colspan="2">cost effective storage, low latency</td>
      <td colspan="2">critical business applications with sustained IOPS performance</td>
    </tr>
    <tr>
      <td colspan="2">system boot volumes, virtual desktops, development and test environments</td>
      <td colspan="2">applications that need more than 16,000 IOPS</td>
    </tr>
    <tr>
      <td colspan="2">1GiB - 16GiB</td>
      <td colspan="2">great for database workloads (sensitive to storage performance and consistency)</td>
    </tr>
    <tr>
      <td>gp3</td>
      <td>gp2</td>
      <td>io1 (4GiB - 16GiB)</td>
      <td>io2 Block Express (4GiB - 64GiB)</td>
    </tr>
    <tr>
      <td>baseline: 3000 IOPS / 125MiB/s</td>
      <td>small volumes, burst up to 3000 IOPS</td>
      <td>max PIOPS: 64000 for Nitro EC2 instances and 32000 for other</td>
      <td>sub millisecond latency</td>
    </tr>
    <tr>
      <td>max: 16000 IOPS / 1000 MiB/s independently</td>
      <td>volume and IOPS are linked: max 16000 IOPS</td>
      <td>can increase PIOPS independently from storage size</td>
      <td>max PIOPS: 256000</td>
    </tr>
    <tr>
      <td></td>
      <td>3 IOPS per GB -> means 5334GB have max IOPS</td>
      <td></td>
      <td></td>
    </tr>
  </body>
</table>

### EBS Multi-Attach - (io1/io2 family)

Attach the same EBS volume to multiple EC2 instances in the same AZ. Each instance has full read and write permissions to the high performance volume. Up to 16 EC2 instances at a time and must use a file system that is cluster aware (not XFS, EXT4, etc.).

Use case: achieve higher application availability in clusteres Linux applications that manage concurrent write operations.

### EBS Encryption

Advantages of EBS volumes:
<ul>
  <li>data at rest is encrypted indie the volume</li>
  <li>all data in-flight moving between the instance and the volume is encrypted</li>
  <li>all snapshots are encrypted</li>
  <li>all volumes created from snapshot are encrypted</li>
</ul>

Encryption and decryption are handled transparently (no admin action needed). Encryption has minimal impact on latency. EBS Encryption leverages keys from KMS (AES-256). Copying an unencrypted snapshot allows encryption. Snapshots of encrypted volumes are encrypted.

Process of encrypting an unencrypted volume:
<ol>
  <li>Create EBS Volume and EBS Snapshot of Volume.</li>
  <li>Encrypt the EBS Snapshot (using a copy).</li>
  <li>Create new EBS volume from snapshot.</li>
  <li>Now move encrypted volume to original instance.</li>
</ol>

## <img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/EFS.png" width="50"/> EFS - Elastic File System

EFS is a manages NFS (Network File System) that can be mounted on many EC2 instances. Works with EC2 instances in multiple AZ's. Highliy reliable, scalable, and expensive (3x gp2) - pay per use.

<img src="https://github.com/cgrundman/aws-saa-c03/blob/main/images/EFS.png" width="300"/>

Use case:
<ul>
  <li>Content management, web serving, data sharing, wordpress</li>
  <li>NFSv4.1 protocol</li>
  <li>use security group to control access to EFS</li>
  <li>compatible with Linux based AMI (not Windows)</li>
  <li>encryption as rest using KMS</li>
  <li>POSIX file system</li>
  <li>file system scales automatically, billed by GB (size)</li>
</ul>

### EFS Performance Classes

<table>
  <body>
    <tr>
      <td><b>EFS Scale</b></td>
      <td>1000s of concurrent NFS clients, 10GB/s throughput</td>
    </tr>
    <tr>
      <td></td>
      <td>grow to petabyte scale network file systems, automatically</td>
    </tr>
    <tr>
      <td>Performance Mode</td>
      <td>General Purpose (default) - latency-sensitive use cases (web server, CMS, etc.)</td>
    </tr>
    <tr>
      <td></td>
      <td>Max I/O - higher latency, throughput, highly parallel (big data, media processing)</td>
    </tr>
    <tr>
      <td>Throughput Mode</td>
      <td>Bursting - 1 TB & 50MiB/s and bursts of up to 100MiB/s</td>
    </tr>
    <tr>
      <td></td>
      <td>Provisioned - set your throughput regardless of storage size (ex 1GiB for 1TB)</td>
    </tr>
    <tr>
      <td></td>
      <td>Elastic - automatically scales troughput up or down based on workloads</td>
    </tr>
  </body>
</table>

### EFS Storage Classes

Storage Tiers:
<ul>
  <li><b>standard</b> - frequently accessed files</li>
  <li><b>infrequent access (EFS IA)</b> - cost to retrieve files, lower storage price</li>
  <li><b>archive</b> - rarely accessed data</li>
  <li><b>implement life cycle policies</b> - move files between storage tiers</li>
</ul>

Availability

Standard: Multi AZ, great for production

One Zone: great for development, backup by default, compatible with 1A (EFS One Zone-1A

### EBS vs EFS

<table>
  <head>
    <tr>
      <td><b>EBS</b></td>
      <td><b>EFS</b></td>
    </tr>
  </head>
  <body>
    <tr>
      <td>one instance (except multi-attach io1/io2)</td>
      <td>share files</td>
    </tr>
    <tr>
      <td>are locked at Availability Zone level</td>
      <td>only for Linux Instances (POSIX)</td>
    </tr>
    <tr>
      <td>gp2: IO increases if disk sizes increases</td>
      <td>EFS has higher price point than EBS</td>
    </tr>
    <tr>
      <td>gp3 and io1: can increase IO increasingly</td>
      <td>can leverage storage tiers for cost savings</td>
    </tr>
  </body>
</table>

## <img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/ELB.png" width="50"/> ELB - Elastic Load Balancing

### High Availability and Scalability

**Scalability** - ability of a web application to adapt to greater workloads

**Vertically Scalability** - increasing instance size, common for non-distributed systems

**EC2 vertical scaling** - from t2.nano (0.5GB RAM, 1 CPU) to u-12tb1.metal (12.3TB RAM, 448 CPUs)

**Horizontal Scalability** - increasing instance amount

**EC2 horizontal scaling** - Auto Scaling Group, Load Balancer

**High Availability** - Auto scaling group with multiple AZ, Load balancing with multiple AZ

### Load Balancing

These are servers that forward traffic to multiple servers downstream.

<img src="https://github.com/cgrundman/aws-saa-c03/blob/main/images/ELB.png" width="250"/>

Use case:
<ul>
  <li>Spread load accross multiple downstream servers</li>
  <li>Expose a single point of access (DNS) to application</li>
  <li>Seamlessly handles features downstream</li>
  <li>Do regular health checks</li>
  <li>Provide SSL termination (HTTP) for your websites</li>
  <li>Enforce stickiness with cookies</li>
  <li>Seperate public and private traffic</li>
</ul>

Elastic Load Balacer use case:
<ul>
  <li>managed</li>
  <li>lower setup costs</li>
  <li>integrated with AWS offerings/services</li>
  <ul>
    <li>EC2, EC2 Auto Scaling Group, Amazon ECS</li>
    <li>AWS Certificate Manager (ACM), CoudWatch</li>
    <li>Route 53, AWS WAF, AWS Global Accelerator</li>
  </ul>
</ul>

### Health Checks

Crusial for load balancers. They enable load balancers to know whether instances it forwards traffic to are available. Health checks are performed on port and route (/health is common).

### Load Balancer Types

**Application Load Balancer (v2)** - HTTP, HTTPS, WebSocket

**Network Load Balancer (v2)** - TCP, TLS (secure TCP), UDP

**Gateway Load Balancer** - operates at Network layer - IP Protocol

### <img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/ALB.png" width="50"/> ALB - Application Load Balancer

Application load balancer is layer 7 (HTTP). ALB performs load balancing to multiple HTTP appliances (ex target groups) or applications (ex containers) on the same machine. Supports HTTP, HTTPS and WebSocket and redirects.

Routing tables to different target groups based on:
<ul>
  <li>path URL (example.com/<ins>users</ins> and example.com/<ins>posts</ins>)</li>
  <li>hostname in URL (<ins>one</ins>.example.com and <ins>other</ins>.example.com)</li>
  <li>query string, headers (example.com/users?<ins>id=123&order=false</ins>)</li>
</ul>

### ALB Target Groups

<ul>
  <li>EC2 instances - HTTP</li>
  <li>ECS tasks - HTTP</li>
  <li>Lambda functions - HTTP request is translated into JSON event</li>
  <li>private IP addresses</li>
</ul>

### <img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/NLB.png" width="50"/> NLB - Network Load Balancer

Network load balancer is layer 4 (TCP). NLB forwards TCP and UDP traffic to instances. Supports millions of requests per seconds with ultra-latency. One static IP per AZ and supports assigning Elastic IPs. NLBs are used for extreme performance, TCP or UDP traffic. Not in the AWS free tier.

<img src="https://github.com/cgrundman/aws-saa-c03/blob/main/images/NLB.png" width="300"/>

### NLB Target Groups

<ul>
  <li>EC2 instances</li>
  <li>IP addresses (must e private)</li>
  <li>Application Load Balancer</li>
  <li>Health checks support the TCL, HTTP, and HTTPS protocols</li>
</ul>

### <img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/GLB.png" width="50"/> GLB - Gateway Load Balancer

Deploy, scale, and manage a fleet of 3rd party network appliances in AWS (ex. Firewalls, Intrusion Detection, and Prevention systems, Deep Packet Inspection Systems, payload manipulation. Operates at laver 3 (Network layer, IP sockets). Combines transparent Network Gateway (single entry/exit for all traffic) and load balancer (distributes traffic to virtual appliances). Uses GENEVE protocol on port 6081.

<img src="https://github.com/cgrundman/aws-saa-c03/blob/main/images/GWLB.png" width="250"/>

### GLB Target Groups

<ul>
  <li>EC2 instances</li>
  <li>IP addresses (must e private)</li>
</ul>

### Sticky Sessions (Session Affinity)

Stickiness is directing same client to same instance behind load balancer, can be used in ALB and NLB. Cookies are used for stickiness and have controllable expiration date.

Use case: user can retain user data.

<img src="https://github.com/cgrundman/aws-saa-c03/blob/main/images/StickySessions.jpg" width="300"/>

### Sticky Sessions- Cookie Names

**Application-based Cookies**

Custom cookie - generated by target, can include custom atributes required by application, name specified for each target group (AWSALB, AWSALBAPP, AWSALBTG reserved by ELB)

Application cookie - generated by load balancer, name is AWSALB for ALB

**Duration-based Cookies** - generated by the load balancer, cookie name is AWSALB for ALB, AWSELB for CLB

### ELB Cross-Zone Balancing

<img src="https://github.com/cgrundman/aws-saa-c03/blob/main/images/CrossZoneBalancing.png" width="300"/>

Application load balancer - Cross zone balancing enabled by default, no charges

Network and Gateway Load Balancers - disabled by default, costs $

### SSL/TLS Bases

SSL certificate allows traffic between clients and load balancer to be encrypted in transit (in-flight encryption). SSL refers to secure sockets layer, used to encrypt connections. TLS referes to transport layer security (newer). TLS mainly used, some still use SSL.

Public SSL certificates are issued by Certificate Authorities. SSL certificates have an expiration date. 

### SSL Certificates

<img src="https://github.com/cgrundman/aws-saa-c03/blob/main/images/LoadBalancerSSL.png" width="300"/>

Load balancers use an X.509 certificate (SSL/TLS server certificate). Certificates can be managed using ACM (AWS Certificate Manager). It is possible to create and upload own certificates.

HTTPS Listeners:
<ul>
  <li>must specify a default certificate</li>
  <li>can add list of certificates to support multiple domains</li>
  <li>clients can use SNI to specify the hostname</li>
</ul>

### SNI - Server Name Identification

Solves the proble, of having multiple SSL certificates on one web server. "Newer" protocol client to indicate the hostname target server of initial SSL handshake. Server finds correct certificate, or returns default.

Only works for ALB, NLB, and CloudFront.

### Elastic Load Balancers - SSL Certificates

**Application Load Balancers** - support multiple listeners with multiple SSL certificates, ise SNI to make it work

**Network Load Balancers** - supports multiple listeners with multiple SSL certificates

### Connection Draining

Also called degredation delay, refers to time to complete "in-flight requests" while instance is deregistering or unhealthy. Stops sending new requests to the EC2 instance which is deregistering. Can be set between 1 to 3500 seconds (default 300s) or be disabled. Low values can be set if requests are short.

## <img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/IAM.png" width="50"/> IAM - Identity Access Management

## <img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/Lambda.png" width="50"/> Lambda

## <img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/RDS.png" width="50"/> RDS - Relational Database Service

RDS Overview

Advantages/Disadvantages over using DB on EC2

RDS Auto Scaling

RDS Read Replicas

RDS Multi AZ (disaster recovery)

RDS Single AZ to Multi AZ

RDS Custom

Amazon Aurora

Aurora High Availability and Read Scaling

Amazon DB Cluster

Aurora Custom Endpoints

Aurora Services

Global Aurora

Aurora Machine Learning

## <img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/S3.png" width="50"/> S3 - Simple Storage Service

## <img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/SQS.png" width="50"/> SQS - Simple Queue Service

## <img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/VPC.png" width="50"/> VPC - Virtual Private Cloud

## <img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/CloudFront.png" width="50"/> CloudFront
