![Diagram Task 3](diagram/Task_3.png)

## Additional elements and why they are added

- **Additional Web Servers**  
  - Added to **distribute traffic** among multiple servers, increase availability, and allow horizontal scaling.  
  - Reduces the risk of downtime if one web server fails.

- **Load Balancer (HAProxy) cluster**  
  - Added to **distribute requests evenly** across all web servers and provide high availability.  
  - Ensures no single web server becomes a bottleneck or point of failure.

- **Separate Application Server**  
  - Added to **isolate the application logic** from static content serving.  
  - Improves maintainability, security, and allows scaling the application layer independently from the web server.

- **Separate Database Server(s)**  
  - Added to **store and manage data** separately from the web and application layers.  
  - Allows a Primary-Replica (Master-Slave) setup to distribute read operations and improve performance.  
  - Provides data redundancy and reduces the risk of data loss.

