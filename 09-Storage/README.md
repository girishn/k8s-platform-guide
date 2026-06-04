# Module 09 — Storage

PV/PVC design, CSI driver selection, stateful workload patterns, backup and snapshots, and storage performance operations.

## Files

| File | Description |
|---|---|
| [storageclass-and-pvc-design.md](storageclass-and-pvc-design.md) | Dynamic provisioning, WaitForFirstConsumer binding mode, reclaim policies, encryption enforcement, PVC quotas per StorageClass |
| [csi-driver-selection.md](csi-driver-selection.md) | EBS (RWO, single-AZ) vs EFS (RWX, multi-AZ) vs S3 (object storage, SDK not CSI mount), access mode decision guide |
| [stateful-workloads.md](stateful-workloads.md) | Managed RDS as golden path, StatefulSet use cases (Kafka, Cassandra, Zookeeper), SPIRE server Aurora MySQL backing, Operator pattern |
| [backup-and-snapshots.md](backup-and-snapshots.md) | VolumeSnapshot API, Velero application-consistent hooks, AWS Backup for EKS, managed RDS PITR, backup validation testing |
| [storage-performance-and-operations.md](storage-performance-and-operations.md) | gp3 vs io2 selection, IOPS bottleneck diagnosis, online PVC resize, StorageClass migration procedure, orphaned PVC monitoring |
