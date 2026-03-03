# Project Functionality Overview
This document describes the operational logic and functional features of the Hybrid ISP & Cloud Network Infrastructure. 
The system is designed to provide seamless connectivity, security, and scalability across physical and virtual environments.

## 1. Network Routing & Connectivity (OSPF)
The core of the network uses OSPF (Open Shortest Path First) to ensure dynamic path selection and high availability.
- The network is split into Area 0 (Backbone), Area 10 (Skopje Offices), and Area 20 (Veles Region) to localize traffic and reduce routing overhead.
- Area Border Routers (ABRs) manage the exchange of routing information between the branch offices and the central Data Center.
- The Dijkstra algorithm calculates the shortest path, ensuring that if a link fails, the network automatically reroutes traffic.

  <img width="1001" height="486" alt="LogicaWAN" src="https://github.com/user-attachments/assets/d186fd66-180f-4861-b938-3599045e5020" />

  <img width="1336" height="726" alt="LogicalSkopjeBackbone" src="https://github.com/user-attachments/assets/589c7b9d-5a38-42c8-a506-db3c6daa7ea8" />

## 2. LAN Segmentation & Management
- Within each location, the network is organized for efficiency and security:

<img width="687" height="848" alt="IP-addresses" src="https://github.com/user-attachments/assets/e56678cf-7707-47b3-b09d-02ee7abeb7e2" />

- Automated IP address assignment is configured on routers, including the distribution of the DNS Server IP to all end-clients.
- Traffic is logically separated into VLANs (e.g., IT, Administration, Wireless) to limit broadcast domains.

## 3. Network Security Layers
Security is implemented at both the network edge and the host level:
- Access Control Lists (ACLs) filter traffic based on IP addresses and protocols (e.g., allowing HTTP but blocking SSH for standard users).

  <img width="427" height="353" alt="image" src="https://github.com/user-attachments/assets/a3a6bc56-7912-4c64-b545-8daf92034477" />

- Network Address Translation (NAT) allows hundreds of private devices to access the internet using a single public IP, hiding the internal topology.

  <img width="785" height="423" alt="image" src="https://github.com/user-attachments/assets/8388e3c8-ed4f-47a9-806e-978f551350fe" />


- All wireless access points use WPA2-PSK with AES encryption to secure data transmitted over the air.

  <img width="883" height="723" alt="WPA2-Connection-Wifi" src="https://github.com/user-attachments/assets/cf89ade3-f15e-420b-84d1-51e1b2b54319" />

- End-devices (Laptops/PCs) utilize local firewall rules for an extra layer of protection (Defense in Depth).

  <img width="884" height="727" alt="FirewallConfigOnALaptop" src="https://github.com/user-attachments/assets/bef14c73-d431-49d5-b1dc-34e4f2b7017c" />

  ## 4. DNS & Web Service Hierarchy
  The project simulates a realistic internet browsing experience with an AI generated HTML file:
  
  - Hierarchical DNS Resolution:
    1. Recursive Server (10.0.0.36): Handles initial client requests.
    2. TLD Server (10.0.0.37): Directs the request to the correct domain zone.
    3. Authoritative Server (10.0.0.38): Provides the final IP for search.com.

    <img width="776" height="392" alt="image" src="https://github.com/user-attachments/assets/b7629b3d-6919-42c5-861e-e47d45f064be" />

  - Caching: The Recursive server caches results to speed up future requests.
  - HTTPS (Port 443): Secured web communication using SSL/TLS encryption to protect user data during transit.

    <img width="879" height="692" alt="HTTP-DNS" src="https://github.com/user-attachments/assets/d605ee77-72c9-4af0-9f9f-05fc887ae51e" />

## 5. Cloud SDN & AWS Integration
The project transitions from hardware-dependent networking to Software-Defined Networking (SDN):
- VPC (Virtual Private Cloud): An isolated digital environment in AWS that replicates the Data Center logic in the cloud.

  <img width="737" height="806" alt="CloudSDN" src="https://github.com/user-attachments/assets/ac5c3e15-c3a1-47e0-9236-eb9f688991af" />


- Subnet Partitioning:
  1. Public Subnet: Contains the Internet Gateway and Load Balancer.
  2. Private Subnet: Strictly hosts the application logic (EC2) and Databases, making them invisible to the public internet.
     
- Cloud Security Groups: Unlike static ACLs, Security Groups act as intelligent, stateful firewalls that only allow traffic from the Load Balancer to the Application Server.

  <img width="554" height="344" alt="CloudSG-ALB" src="https://github.com/user-attachments/assets/8eea2d43-79ef-4eed-9aae-2f97987a6a7a" />

  <img width="572" height="398" alt="CloudSG-EC2" src="https://github.com/user-attachments/assets/b483e56d-d70c-44f9-891a-49f9879ae916" />

- Global Delivery: Using S3 and CloudFront (CDN) to serve static content from the nearest "Edge" location to the user, reducing latency.
  
Link to Cloudcraft: https://app.cloudcraft.co/view/1893ea40-6691-433c-bdc1-49f0c579e71d?key=a6596490-1444-483a-a9dc-1d33892ee5d8
