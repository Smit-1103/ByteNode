# ByteNode - IPFS Distributed Storage System

ByteNode is a Django-based distributed file storage system that leverages IPFS (InterPlanetary File System) to provide reliable, redundant, and fault-tolerant file storage. The system intelligently chunks files and distributes them across multiple IPFS nodes, ensuring high availability and data integrity.

## Key Features

- **User Authentication**: Secure user registration and login system
- **Intelligent File Chunking**: Files are automatically split into manageable 1MB chunks
- **Distributed Storage**: Each chunk is stored across multiple IPFS nodes for redundancy
- **Fault Tolerance**: Files remain fully retrievable even if multiple storage nodes fail
- **Automatic Rebalancing**: System monitors and redistributes chunks to maintain optimal load balance
- **Health Monitoring**: Self-healing capabilities detect and repair storage issues
- **REST API**: Complete API for programmatic integration
- **Admin Dashboard**: Comprehensive system monitoring and management interface

## Admin Capabilities

Administrators have access to powerful management tools:

1. **Django Admin Interface**: Enhanced admin views for Files, Chunks, Nodes, and Distributions
2. **Custom Dashboard**: Visual monitoring of system health and performance metrics
3. **Health Check**: Manual and scheduled system integrity verification
4. **Node Management**: Test connections, monitor performance, and manage IPFS nodes

## Automated Maintenance

ByteNode includes built-in maintenance features to ensure system health:

```bash
# Check system health without making changes
python manage.py check_system_health --dry-run

# Check system health and automatically fix issues
python manage.py check_system_health
```

## Technical Implementation

- Files are split into 1MB chunks for optimized storage
- Each chunk is stored on IPFS with a unique hash
- Multiple copies of each chunk are distributed across the network
- The system intelligently monitors node health and redistributes chunks as needed
- Load balancing prevents any single node from becoming overwhelmed

## Getting Started

For detailed setup instructions, please refer to the [Setup Guide](setup.md).

## License

MIT License
