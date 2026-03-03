# isp-architecture-ospf-cloud-security

## 🚀Key Architectures and Technologies
The project is divided into two primary environments:
- On-Premise ISP Infrastructure: Simulated in Cisco Packet Tracer, focusing on physical connectivity, routing, and local services.
- Cloud Infrastructure: Designed in Cloudcraft and partially implemented in AWS, focusing on scalability, SDN, and global delivery.

## 📂 Overview
This project simulates an ISP network connecting:
- Skopje (Core / Area 0)
- Skopje Offices (Area 10)
- Veles Regional Network (Area 20)

And Cloud Environment (AWS VPC):
- Public Subnet - Hosts the Application Load Balancer (ALB) and Bastion hosts
- Private Subnet - Secure Layer for the Application server (search.com)


## 💎 Features
Traditional network:
- OSPF Multi-Area
- VLAN segmentation
- Inter-VLAN routing
- NAT (PAT)
- ACL security rules
- WPA2 Security
- DHCP & DNS
- WAN link between Skopje and Veles

Cloud Networking:
- VPC (Virtual Private Cloud)
- SDN Logic
- Security Groups
- Route 53
- IGW (Internet Gateway)
- S3 and CloudFront

## 🧪 How to Test the Traditional Network
Open the .pkt file in Cisco Packet Tracer and:
- Ping between areas
- Test OSPF routes
- Check NAT translations
