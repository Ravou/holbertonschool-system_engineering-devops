![Diagram Task 1](diagram/Task_1.png)

## Specifics about the scaled infrastructure

### Added elements and why
- **Additional Web Server(s)**: Added to distribute traffic and increase availability. Allows the infrastructure to handle more users simultaneously and reduces the risk of downtime if a server fails.
- **Load Balancer (HAProxy) cluster**: Added to distribute incoming requests evenly across multiple web servers and provide high availability. Ensures no single web server is overloaded.
- **Separate Application Server**: Isolates application logic from static content serving, improves maintainability, and allows scaling the application layer independently.
- **Separate Database Server(s) (Primary-Replica)**: Isolates data storage, improves performance, enables data replication, and allows read operations to be distributed on replica nodes.
- **Monitoring and security components (optional)**: Added to track system health, detect failures, and enhance security (firewall, SSL/TLS).

### Load Balancer
- **Distribution algorithm**: The load balancer is configured with a **Round Robin** algorithm, which distributes incoming requests sequentially across all available web servers. Each new request goes to the next server in the list, ensuring a roughly even load.
- **Active-Active vs Active-Passive**
  - **Active-Active**: Both load balancers are active and can handle traffic simultaneously. If one fails, the other continues to manage traffic without interruption.
  - **Active-Passive**: Only one load balancer handles traffic at a time. The passive one is on standby and takes over only if the active one fails.
  - **Our setup**: [Specify Active-Active or Active-Passive based on your configuration].

### Database Primary-Replica (Master-Slave) cluster
- **How it works**:  
  The Primary (Master) node handles all write operations and propagates changes to one or more Replica (Slave) nodes. Replica nodes handle read operations to reduce load on the Primary.
- **Difference between Primary and Replica regarding the application**:  
  - **Primary node**: Handles writes (INSERT, UPDATE, DELETE). Critical for maintaining consistent data.  
  - **Replica node**: Handles reads (SELECT) to improve performance. Cannot process writes directly.

---

## Issues with this infrastructure

- **SPOF (Single Point of Failure)**  
  - A single web server, database primary node, or load balancer could cause downtime if it fails.  
- **Security issues**  
  - No firewall: the servers are exposed to the Internet without filtering traffic.  
  - No HTTPS: communication is not encrypted, making it vulnerable to eavesdropping.  
- **No monitoring**  
  - Without monitoring, failures or performance issues may go unnoticed, leading to longer downtime or degraded service.

