# Ceph Distributed Storage Cluster Deployer

**Repository Name:** `ceph.distributed.storage.cluster.deployer`

This automation tool deploys and configures a **Ceph distributed storage cluster** across multiple nodes. It handles installation and setup of all key components, including **Ceph Monitors (MONs)**, **OSDs (Object Storage Daemons)**, **MDS (Metadata Server)**, and **Rados Gateway (RGW)**.

Even if you are not familiar with Ceph, this repository provides scripts to bring up a fully functional cluster using a simple configuration file with your node IPs.

---

## What is Ceph?

Ceph is an **open-source distributed storage system** that provides:

* **Object, block, and file storage** in a unified platform
* **High availability and fault tolerance** through replication and CRUSH maps
* **Scalable architecture** - add or remove nodes without downtime
* **Self-healing and self-managing capabilities** to reduce operational overhead

Ceph allows you to turn a cluster of servers into a **highly reliable and elastic storage system**.

---

## Prerequisites

Before running the scripts:

* Ubuntu or Debian-based operating system on all nodes
* Sudo privileges on all nodes in the cluster
* Network connectivity between all cluster nodes
* Ceph repositories and packages installed (the script can handle installation if needed)

---

## Cluster Configuration

The default configuration assumes the following node roles (modify as needed):

* **Admin Node:** `host-192-168-0-6`
* **Ceph Monitor Node:** `host-192-168-0-20`
* **Ceph OSD Nodes:**

  * `host-192-168-0-8`
  * `host-192-168-0-19`
  * `host-192-168-0-4`

You can customize variables such as `USERNAME`, `CLUSTER_NAME`, and node IPs in the configuration file.

---

## How to Use

1. Clone or download the repository:

```bash
git clone <repo_url>
cd ceph.distributed.storage.cluster.deployer
```

2. Customize the configuration:

* Edit hostnames and IP addresses for monitor and OSD nodes
* Set the network range and cluster name

3. Make the main script executable and run it:

```bash
chmod +x ceph_setup.sh
./ceph_setup.sh
```

---

## Script Steps

1. **Initial Setup**

   * Downloads Ceph repository keys
   * Installs `ceph-deploy` and removes conflicting older versions

2. **Cluster Purge (Optional)**

   * Removes any previous Ceph deployments to avoid conflicts

3. **Ceph Installation**

   * Installs required components: `ceph-mon`, `ceph-osd`, `ceph-mgr`, etc.

4. **Cluster Configuration**

   * Configures public network and cluster settings
   * Initializes the monitor node

5. **OSD Creation**

   * Sets up and deploys OSDs on specified nodes

6. **MDS and RGW Setup**

   * Deploys the Metadata Server and Rados Gateway

7. **Additional Monitor Nodes**

   * Adds extra monitor nodes to the cluster if needed

8. **Health Check**

   * Log in to the monitor node to check cluster health after deployment
