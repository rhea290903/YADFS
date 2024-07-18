# Yet Another Distributed File System (YADFS)

YADFS aims to implement a distributed file system capable of storing and managing large amounts of data across multiple machines.

## High-Level Architecture

YADFS consists of data nodes and a name node responsible for storage management and metadata management, respectively, across the network of machines.

### Name Nodes

The Name Node manages metadata about files and directories. It maintains a namespace hierarchy, file-to-block mapping, and information about Data Nodes' health and availability. Key functionalities include:

- Periodic pinging of Data Nodes for availability.
- Handling metadata operations and ensuring namespace resolution.

### Data Nodes

Data Nodes handle the storage and retrieval of data blocks. Key functionalities include:

- Providing APIs for read and write operations on data blocks.
- Implementing replication across Data Nodes to ensure fault tolerance.
- Organizing data into directories and files within the distributed file system.

## Organizing Data in Data Nodes

Files in YADFS are stored as fixed-size blocks distributed across multiple Data Nodes. Each file's metadata is managed by the Name Node, which maps file names to their physical locations in the network.

## Fault Tolerance

YADFS ensures fault tolerance through strategies like data replication, where each data block is replicated across multiple Data Nodes. This redundancy helps in maintaining data availability even in case of Data Node failures.

## Client Interaction and Features

YADFS provides interfaces for interacting with the distributed file system, enabling users to perform various operations:

### Metadata Operations

- Create, delete, move, and copy directories and files.
- List files and directories within a directory.
- Traverse directories to locate specific files or folders.

### DFS Operations

- Upload and download files from the distributed file system.
- Process flows ensure efficient handling of file uploads and downloads, including block splitting, replication, metadata updates, and client acknowledgment.

### Example Process Flows

#### Upload Process Flow

1. **File Splitting**: Divide the file into fixed-size blocks.
2. **Block Creation**: Assign unique identifiers (block IDs) to each block.
3. **Uploading Blocks**: Distribute blocks to appropriate Data Nodes.
4. **Replication**: Create replicas of blocks for fault tolerance.
5. **Metadata Update**: Update file metadata with block locations.
6. **Namespace Resolution**: Determine storage locations for each block.
7. **Client Acknowledgment**: Receive acknowledgments from Data Nodes.

#### Download Process Flow

1. **Client Request**: Initiate request to download a file.
2. **Metadata Retrieval**: Obtain file metadata from Name Node.
3. **Block Location Retrieval**: Determine Data Node locations for blocks.
4. **Data Block Retrieval**: Retrieve blocks from Data Nodes.
5. **Data Transfer**: Transfer blocks to client for reassembly.
6. **Reassembly**: Reconstruct the original file from blocks.
7. **File Completion Check**: Verify successful download.

## Metadata Operation Process Flow

1. **Client Request**: Send operation request to Name Node.
2. **NameNode Verification**: Validate the operation's validity.
3. **Perform Operation**: Execute the operation and update metadata.
4. **Response**: Provide operation status to the client.





