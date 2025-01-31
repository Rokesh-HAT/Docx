# Project Plan: Setup NFS in GCP GKE Cluster

| **Section**     | **Details**                                                                                                                                          |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Driver**      | Teja                                                                                                                                    |
| **Approver**    | Aneesh Poyil                                                                                                                                             |
| **Contributors**| Rokesh                                                                                                                                         |
| **Informed**    | Ponnusamy and Sakthivel                                                                                                                                         |
| **Objective**   | This document outlines different approaches to setting up NFS in a Google Kubernetes Engine (GKE) cluster, along with their pros and cons.           |
| **Key Outcomes**| - Successful deployment of NFS in GKE.<br>- Reliable and scalable storage solution.                                                                 |
| **Status**      |  Pending Approval                                                                                                                |

## 🤔 Problem Statement
Storage persistence is required for stateful applications in a Kubernetes cluster. This document explores different NFS setup approaches in GKE to address scalability, availability, and cost-effectiveness.

## 🔍 Scope

### Must Have:
- Deploy a functioning NFS solution in GKE.
- Provide step-by-step setup instructions.
- Compare different approaches.

### Nice to Have:
- Automated deployment using Helm or Terraform.
- High Availability (HA) configuration.

### Not in Scope:
- Managed storage solutions like Filestore.
- Deep dive into GCP IAM policies.

---

## 📖 Reference Materials
- [GKE Persistent Volumes Documentation](https://cloud.google.com/kubernetes-engine/docs/concepts/persistent-volumes)
- [NFS Subdir External Provisioner](https://github.com/kubernetes-sigs/nfs-subdir-external-provisioner)

---

## Approaches

### 1️⃣ Deploying NFS Server on a GKE Node

**Overview:**

In this approach, you set up a dedicated NFS server on a Google Compute Engine (GCE) instance, mount the storage on a Kubernetes node, and then use Persistent Volumes (PVs) and Persistent Volume Claims (PVCs) within the Google Kubernetes Engine (GKE) cluster to access the NFS server.

**Pros:**
- Lower cost compared to managed solutions.
- Full control over NFS configuration.

**Cons:**
- Manual maintenance required.
- Single point of failure.
- Performance degradation if not properly optimized.

### 2️⃣ Using NFS Subdir External Provisioner

**Overview:**

This approach automates the provisioning of NFS-based persistent volumes by using the nfs-subdir-external-provisioner in combination with Helm charts. This method is often chosen when a Kubernetes cluster needs to dynamically provision storage.

**Pros:**
- Dynamic provisioning of PVs.
- Works with an existing NFS server.

**Cons:**
- Still requires an external NFS server.
- Possible performance overhead.
- Limited visibility and control over storage allocation.

### 3️⃣ Using NFS Operators in GKE

**Overview:**

NFS Operators provide a managed way to handle NFS storage within Kubernetes clusters. These operators automate deployment, scaling, and management of NFS storage, reducing manual effort and improving reliability.

**Pros:**
- Simplifies deployment and management.
- Provides automation for scaling and maintenance.
- Improves reliability and reduces the risk of human error.

**Cons:**
- Requires additional setup and learning curve.
- Limited community support compared to traditional methods.
- Potential compatibility issues with certain Kubernetes versions.

---

## ✅ Conclusion

The choice of approach depends on **cost, scalability, and ease of maintenance**:

- **Deploy NFS on a GCE instance** if cost efficiency and fine-grained control over NFS configuration are your priorities. However, be prepared for **manual management** and potential **single points of failure**.
- **Use an external provisioner** for **dynamic provisioning** of PVs in your GKE cluster, especially if you need an **automated, flexible solution** and are comfortable with an **external NFS server setup**.
- **Use NFS Operators** for a **fully automated and scalable** NFS solution within Kubernetes, minimizing manual effort and improving operational efficiency.

