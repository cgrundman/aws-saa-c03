# AWS Solution Architect Associate
<img src="https://images.credly.com/images/0e284c3f-5164-4b21-8660-0d84737941bc/twitter_thumb_201604_image.png" width="100" />

Learning materials for AWS Solution Architect Associate Certification (AWS-SAA-C03).

Information on the exam can be found [here](https://aws.amazon.com/certification/certified-solutions-architect-associate/).

Domains of material covered in the exam: 
* Design Resilient Architectures
* Design High-Performing Architectures
* Design Secure Architectures
* Design Cost-Optimized Architectures

<table>
<!--     <thead>
        <tr>
            <th>Icon</th>
            <th>Name</th>
            <th>Description</th>
        </tr>
    </thead> -->
    <tbody>
        <tr>
            <td colspan=1><img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/EC2.png" width="50"/></td>
            <td colspan=2><h2>EC2 - Elastic Compute Cloud</h2></td>
        </tr>
        <tr>
            <td></td>
            <td><h4>Placement Groups</h4></td>
        <tr>
            <td></td>
            <td><h5>Cluster Placement Group</h5></td>
            <td><img src="https://github.com/cgrundman/aws-saa-c03/blob/main/images/cluster_placement_group.jpg" width="300"/></td>
        </tr>
        <tr>
            <td></td>
            <td><h5>Description:</h5></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td><h5>Use Case:</h5></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td><h5>Spread Placement Group</h5></td>
            <td><img src="https://github.com/cgrundman/aws-saa-c03/blob/main/images/spread_placement_group.jpg" width="300"/></td>
        </tr>
        <tr>
            <td></td>
            <td><h5>Description:</h5></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td><h4>Use Case:</h4></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td><h4>Partition Placement Group</h4></td>
            <td><img src="https://github.com/cgrundman/aws-saa-c03/blob/main/images/partition_placement_group.png" width="300"/></td>
        </tr>
        <tr>
            <td></td>
            <td><h4>Description:</h4></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td><h4>Use Case:</h4></td>
            <td></td>
        </tr>
        <tr>
            <td colspan=1><img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/Auto-Scaling.png" width="50"/></td>
            <td colspan=2><h2>Auto-Scaling</h2></td>
        </tr>
        <tr>
            <td colspan=1><img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/DynamoDB.png" width="50"/></td>
            <td colspan=2><h2>DynamoDB</h2></td>
        </tr>
        <tr>
            <td colspan=1><img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/EBS.png" width="50"/></td>
            <td colspan=2><h2>EBS - Elastic Block Store</h2></td>
        </tr>
        <tr>
            <td></td>
            <td><h4>ELB Snapshots</h4></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td><h4>ELB Encryption</h4></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td><h4>ELB Volume Types</h4></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td><h4>AMI Overview</h4></td>
            <td></td>
        </tr>
        <tr>
            <td colspan=1><img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/EFS.png" width="50"/></td>
            <td colspan=2><h2>EFS - Elastic File System</h2></td>
        </tr>
        <tr>
            <td colspan=1><img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/ELB.png" width="50"/></td>
            <td colspan=2><h2>ELB - Elastic Load Balancing</h2></td>
        </tr>
        <tr>
            <td colspan=1><img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/IAM.png" width="50"/></td>
            <td colspan=2><h2>IAM - Identity Access Management</h2></td>
        </tr>
        <tr>
            <td colspan=1><img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/Lambda.png" width="50"/></td>
            <td colspan=2><h2>Lambda</h2></td>
        </tr>
        <tr>
            <td colspan=1><img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/RDS.png" width="50"/></td>
            <td colspan=2><h2>RDS - Relational Database Service</h2></td>
        </tr>
        <tr>
            <td colspan=1><img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/S3.png" width="50"/></td>
            <td colspan=2><h2>S3 - Simple Storage Service</h2></td>
        </tr>
        <tr>
            <td colspan=1><img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/SQS.png" width="50"/></td>
            <td colspan=2><h2>SQS - Simple Queue Service</h2></td>
        </tr>
        <tr>
            <td colspan=1><img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/VPC.png" width="50"/></td>
            <td colspan=2><h2>VPC - Virtual Private Cloud</h2></td>
        </tr>
        <tr>
            <td colspan=1><img src="https://github.com/cgrundman/aws-saa-c03/blob/main/icons/CloudFront.png" width="50"/></td>
            <td colspan=2><h2>CloudFront</h2></td>
        </tr>
    </tbody>
</table>

## EC2 - Elastic Compute Cloud
private vs public vs elastic IP
placement groups
elastic network interfaces - ENI
EC2 Hibernate
EC2 Instance storage
EBS Volumes
EBS Snapshots
EBS Snapshot Archive
Recycle Bin for EBS Snapshots
Fast Snapshot Restore
A

