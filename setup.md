# ByteNode Storage - Setup Guide

This document provides step-by-step instructions to set up and run the ByteNode Storage project, a distributed file storage system built with Django and IPFS.

## Prerequisites

Before starting, ensure you have the following installed on your system:

- Python 3.8 or higher
- pip (Python package manager)
- IPFS daemon (for distributed file storage)
- Git (for cloning the repository)

## Installation Steps

### 1. Clone the Repository

```bash
git clone https://github.com/Smit-1103/ByteNode.git
cd byteNode
```

### 2. Create and Activate a Virtual Environment

```bash
# On Windows
python -m venv venv
venv\Scripts\activate

# On macOS/Linux
python3 -m venv venv
source venv/bin/activate
```

### 3. Install Required Dependencies

```bash
pip install -r requirements.txt
```

If the requirements.txt file is not available, install the following packages:

```bash
pip install django==5.1.4
pip install requests
pip install django-cors-headers
pip install djangorestframework
pip install django-jazzmin
```

### 4. Set Up IPFS

#### Install IPFS
Follow the official IPFS installation guide at https://docs.ipfs.tech/install/

#### Initialize and Start IPFS Daemon
```bash
ipfs init
ipfs daemon
```

This will start the IPFS daemon which is required for the ByteNode Storage system to interact with the IPFS network.

### 5. Database Setup

```bash
# Apply migrations
python manage.py migrate

# Create a superuser (admin)
python manage.py createsuperuser
```

### 6. Run the Development Server

```bash
python manage.py runserver
```

The application should now be running at http://127.0.0.1:8000/

## System Configuration

### Setting Up Nodes

Before you can use the system, you need to set up at least one IPFS node:

1. Log in as an admin user
2. Navigate to the Admin Dashboard
3. Add a new node with the following details:
   - Name: A descriptive name for the node
   - IPFS ID: The ID of your IPFS node (run `ipfs id` to get this)
   - IP: The IP address of the node (use 127.0.0.1 for local development)
   - Port: The API port of the IPFS node (default is 5001)

### System Health Check

You can run a system health check to ensure all nodes are functioning correctly:

```bash
python manage.py check_system_health
```

Add the `--dry-run` flag to report issues without fixing them:

```bash
python manage.py check_system_health --dry-run
```

## Advanced Node Management

### Running Multiple IPFS Nodes on Local System

For testing or development purposes, you can run multiple IPFS nodes on the same machine by specifying different IPFS paths:

```bash
# Initialize an additional IPFS node with a custom path
IPFS_PATH=~/.ipfs2 ipfs init
IPFS_PATH=~/.ipfs3 ipfs init

# Run additional IPFS daemons (run each in a separate terminal)
IPFS_PATH=~/.ipfs2 ipfs daemon
IPFS_PATH=~/.ipfs3 ipfs daemon
```

Each node will have its own identity and can be added to your ByteNode system as a separate storage node. This is useful for testing the distributed storage capabilities locally.

### Manual Load Balancing

In emergency situations where you need to manually adjust the load distribution across nodes:

```bash
# Update node loads to rebalance the system
python manage.py update_node_loads
```

This command recalculates the load on each node and redistributes chunks for optimal performance. Use this command when:
- A node is experiencing unusually high load
- You've added new nodes and want to accelerate redistribution
- System performance is degraded due to imbalanced storage

## Using ByteNode Storage

### User Registration and Login

1. Navigate to http://127.0.0.1:8000/
2. Click on "Register" to create a new account
3. Log in with your credentials

### Uploading Files

1. Click on "Upload" in the navigation bar
2. Select a file from your computer
3. Click "Upload"

The system will:
- Split the file into chunks
- Distribute these chunks across available IPFS nodes
- Store metadata about the file and its chunks in the database

### Managing Files

1. Click on "My Files" to see all your uploaded files
2. For each file, you can:
   - Download the file
   - View file details (including chunk distribution)
   - Delete the file

### Admin Dashboard

If you're logged in as an admin user, you can access the Admin Dashboard to:
- Monitor node health
- View system statistics
- Manage file distributions
- Test node connectivity

## Architecture Overview

ByteNode Storage consists of the following key components:

1. **Django Web Application**: Provides the user interface and API endpoints
2. **IPFS Network**: Stores and retrieves file chunks
3. **Database**: Stores metadata about files, chunks, and nodes

### Fault-Tolerant Design

A critical feature of ByteNode is its robust fault-tolerance mechanism:

- Each file is split into multiple chunks
- **Every chunk is stored across different nodes** - ensuring no single node contains all chunks of any file
- The system maintains multiple copies of each chunk on different nodes
- If any node becomes unavailable or corrupted, the system can still retrieve all file chunks from alternative nodes
- This intelligent distribution ensures 100% file availability even when multiple nodes fail
- The system automatically detects node failures and redistributes chunks to maintain redundancy

This advanced fault-tolerance is what sets ByteNode apart from traditional storage systems. You can lose access to multiple nodes and still retrieve your files completely intact.

### Key Models

- **File**: Represents a file uploaded by a user
- **FileChunk**: Represents a chunk of a file
- **Node**: Represents a node in the IPFS network
- **ChunkDistribution**: Tracks which chunks are stored on which nodes

### File Distribution Process

When a file is uploaded:
1. The file is split into chunks
2. Each chunk is uploaded to IPFS
3. The system distributes chunks across multiple nodes for redundancy
4. Metadata about the file and its chunks is stored in the database

When a file is downloaded:
1. The system retrieves the file's metadata
2. It fetches each chunk from the optimal node
3. The chunks are reassembled into the original file
4. The file is verified using its checksum

## Troubleshooting

### IPFS Connection Issues

If you encounter IPFS connection issues:
1. Ensure the IPFS daemon is running
2. Check that the node configuration (IP and port) is correct
3. Verify that your firewall allows connections to the IPFS ports

### Node Health

If nodes are not functioning correctly:
1. Run the system health check: `python manage.py check_system_health`
2. Check the node's status in the Admin Dashboard
3. Verify that the IPFS daemon is running on the node

### Load Balancing Issues

If you're experiencing performance problems due to uneven load distribution:
1. Check node load statistics in the Admin Dashboard
2. Run `python manage.py update_node_loads` to manually trigger rebalancing
3. Consider adding more nodes if the overall system load is consistently high

## Contributing

To contribute to ByteNode Storage:
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## License

MIT License
