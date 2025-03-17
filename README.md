# ByteNode - IPFS Distributed Storage System

ByteNode is a Django-based distributed file storage system that leverages IPFS (InterPlanetary File System) to provide reliable, redundant, and fault-tolerant file storage. The system intelligently chunks files and distributes them across multiple IPFS nodes, ensuring high availability and data integrity.

---

## Fulfilled Requirements

1. **User Authentication**:  
   - Implemented secure user registration and login with Django’s authentication framework.
   - Users can reset passwords, manage profiles, and have role-based permissions.

2. **File Chunking**:  
   - Files are split into 1MB chunks automatically.
   - Large files can be uploaded and downloaded efficiently without timeout issues.

3. **Redundant IPFS Storage**:  
   - Multiple copies of each file chunk are stored across several IPFS nodes.
   - Ensures data availability even if some nodes go offline.

4. **Fault Tolerance & Health Checks**:  
   - Built-in commands (`check_system_health`) detect and repair missing chunks.
   - The system automatically redistributes chunks if a node fails.

5. **Automatic Rebalancing**:  
   - Prevents single-node overload by intelligently distributing file chunks.
   - Monitors IPFS node health for proactive load balancing.

6. **Monitoring & Self-Healing**:  
   - Regularly scheduled checks maintain data integrity.
   - Admin dashboard provides insights into system performance and node status.

7. **REST API & Admin Dashboard**:  
   - Full-featured REST API for integration with external services.
   - Custom Django admin views and a dedicated dashboard for node management, file/chunk tracking, and health monitoring.

---

## Key Features

- **User Authentication**: Secure user registration and login system.  
  Manage user access and permissions using Django’s robust authentication framework.

- **Intelligent File Chunking**: Files are automatically split into manageable 1MB chunks.  
  This design ensures efficient upload and download speeds, even for very large files.

- **Distributed Storage**: Each chunk is stored across multiple IPFS nodes for redundancy.  
  This distribution ensures data remains accessible even if one or more nodes are unavailable.

- **Fault Tolerance**: Files remain fully retrievable even if multiple storage nodes fail.  
  IPFS node failures are handled gracefully, with automated re-allocation of file chunks.

- **Automatic Rebalancing**: The system monitors and redistributes chunks to maintain optimal load balance.  
  Load balancing helps prevent any single node from becoming a bottleneck.

- **Health Monitoring**: Self-healing capabilities detect and repair storage issues.  
  Regularly scheduled checks ensure data integrity and system reliability.

- **REST API**: A complete API for programmatic integration.  
  Integrate ByteNode seamlessly into third-party applications or internal automation pipelines.

- **Admin Dashboard**: A comprehensive system monitoring and management interface.  
  Administrators can quickly view system status, check logs, and manage resources.

---
## Screenshots

Below is a table with some sample screenshots to give you a quick visual overview of ByteNode’s interface and features.
Replace the screenshot paths and descriptions with your own to suit your actual setup.
| Screenshot                                                                                                      | Description                                                                                                                                                         |
|-----------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ![Image](https://github.com/user-attachments/assets/1a619667-28f3-4781-9214-b7b6d1474286)                       | **Login Page**<br>Users can sign in with their credentials. This page leverages Django’s authentication system for secure access.                                   |
| ![Image](https://github.com/user-attachments/assets/fa70beb1-7afc-4fc7-9761-a3026bb64cca)                       | **Admin Dashboard**<br>Admins can monitor system status, view statistics, and manage core configurations.                                                           |
| ![Image](https://github.com/user-attachments/assets/9c5126cd-85c5-46cf-a86a-a96cd8d94d47)                       | **File Management**<br>View, upload, and manage files. Displays chunk details and metadata for easy tracking.                                                       |
| ![Image](https://github.com/user-attachments/assets/aeea33d5-91a7-431e-a99a-2d5d090d2033)                       | **Node Management**<br>Oversee all connected IPFS nodes, check their status, and configure settings as needed for optimal performance.                             |
| ![Image](https://github.com/user-attachments/assets/fa70beb1-7afc-4fc7-9761-a3026bb64cca)                       | **Health Check**<br>Run manual or scheduled integrity checks. This ensures all file chunks are available and nodes are functioning properly.                        |
| ![Image](https://github.com/user-attachments/assets/ed1fdc69-07d9-4b90-bd17-3d1e4c64fb3e)                       | **Chunk Distribution**<br>Visual representation of how file chunks are distributed across multiple IPFS nodes for redundancy and fault tolerance.                  |
| ![Image](https://github.com/user-attachments/assets/123e2dec-566b-4460-bb43-e8bfec81c942)                       | **Load Balancing**<br>Automatic rebalancing helps distribute chunks to ensure no single node becomes overloaded.                                                   |
| ![Image](https://github.com/user-attachments/assets/a30a1964-54a3-45f1-acaf-9ae42c804408)                       | **Node Diagnose**<br>Users can add, remove, or check their nodes here.                                                                                             |
| ![Image](https://github.com/user-attachments/assets/6156303f-9c57-4657-b079-88737e089243)                       | **Upload File**<br>Users can upload any files from their local machine. The file will be divided into chunks and distributed to different nodes for redundancy.    |


## Demo Video

For a hands-on walkthrough of ByteNode’s features and usage, check out the **[Demo Video](https://github.com/user-attachments/assets/9388e4e9-8c8a-447b-a070-9605086e7e5a)**.  
This video covers:
- Installation & setup
- File upload and chunk distribution
- Monitoring system health
- Troubleshooting common issues

---
## Admin Capabilities

Administrators have access to powerful management tools that streamline maintenance and ensure system reliability:

1. **Django Admin Interface**  
   - Enhanced admin views for Files, Chunks, Nodes, and Distributions.
   - Easily review which chunks are stored on which nodes, and manage user access or file metadata.

2. **Custom Dashboard**  
   - Visual monitoring of system health and performance metrics, including node status, chunk distribution statistics, and storage capacity usage.

3. **Health Check**  
   - Offers both manual and scheduled system integrity verification.
   - Admins can trigger health checks on-demand or rely on automated schedules.

4. **Node Management**  
   - Manage IPFS nodes by testing connections, monitoring performance, and configuring node settings.
   - If a node becomes unreliable, the system can redistribute chunks accordingly.

---

For instructions on how to set up and start this project, please refer to our 
[Setup Instructions](setup.md).

## Automated Maintenance

ByteNode includes built-in maintenance commands to ensure system health:

```bash
# Check system health without making changes
python manage.py check_system_health --dry-run

# Check system health and automatically fix issues
python manage.py check_system_health
