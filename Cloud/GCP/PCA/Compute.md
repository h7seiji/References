# Compute Options Tips

## Compute Engine

### GCE is a basic IaaS service, but there are lots of details you’re expected to know

- Differences between PD images / snapshots / VM images.
- How to troubleshoot VM not booting up properly
- Custom image vs public image + startup scripts
- VM price differ between regions
- PDs are network-attach devices and - as such - consume VM bandwidth.
- VM network performance scales with # of vCPUs.

### Machine Type

- Custom machines can be used only for some VM families & up to 224vCPU/896 GB RAM

### Network

- Network bandwidth limited & dependent on vCPU count (up to ~32Gbps for N2s + Tier1 extends further)
- You can expect the best network performance for traffic within the same zone, using internal IP addresses.
- Remember about multi-NIC VMs (up to 8)
- Storage is a network resource! => Network bandwidth shared between network AND disk activity

### Spot VMs

- Ideal for Data processing, image handling, rendering, and media transcoding
- Can also be used in GKE clusters

### Start & Stop

- Startup / shutdown scripts are best-effort only!
- Startup / shutdown scripts are always run by root (Linux) / System (Windows)
- Shutdown scripts are especially useful for:
  - MIGs (to copy back processed data or logs before a VM goes down).
  - Spot / Preemptible VMs, which are much more vulnerable to be stopped.
- Startup / shutdown scripts can be set on VM or project (!!!) level -> will trigger for every VM. VM-level always take precedence (if exists, project-level script is not executed)
- Shutdown scripts have timeouts:
  - 90s for standard instances
  - 30s for Spot / Preemptible instances

### Creation

- Custom images should be centralized and controlled from lifecycle perspective (know what are image families and image states)
- Public / Custom OS image IS NOT the same as “machine image”
- You can create a VM based on all of those options (public / custom OS image, snapshot, existing disk, machine image)
- You can ‘automate’ post-processing with startup script, regardless of how boot disk was created.

### Shielded VMs

- Using Shielded VMs is a best practice in GCP

### Managed Instance Groups (MIG)

- pros & cons of "ready" custom OS images vs public image + startup scripts

### Stateful vs Stateless

- Prefer Stateless. Use Stateful only when necessary:
  - Databases
  - Data processing apps (Kafka etc)
  - Legacy monoliths

### Choosing instance groups

- Unmanaged are used to group EXISTING, different VMs under one “umbrella” and balance traffic to healthy ones only. For example, used in lift&shift migrations.
- You can’t update existing instance template (need to create a new one)
- Know the difference between scale-out and scale-up!

### Updating MIGs

- Know WELL how to rollout new versions to MIGs, incl. canary & rollback strategies

### VM Pricing and cost optimization

- Common pattern for optimization costs for unused PDs: you can create a snapshot, and delete the disk to reduce the maintenance cost of that disk by 35% to 92%.
- For premium OS, you’re billed for license per vCPU per second.
- Bring Your Own License is an option for some OSes
- Use Extended memory to save on OS license costs.

### Persistent Disks

- Use “--no-boot-disk-auto-delete” parameter if you don’t want boot / OS disk to be deleted if a VM gets deleted.
- CMEK and CSEK can be used to encrypt PDs. Have a look at how to use CSEK for a PD.
- Avoid using ext3 filesystems in Linux (poor performance under heavy write loads). Prefer ext4.
- You can share a PD across multiple VMs at the same time in read-only mode.
  - If read-write required, prefer a managed solution such as Filestore or utilize GCS.
- You can share a SSD PD across two N2 VMs at the same time in read-write mode. In Preview as of Q1 ‘23 -> should NOT be covered on the exam.
- To recover from a corrupted disk / Os not booting properly, follow this procedure.
  - On high-level, just attach the corrupted disk as non-boot disk to another VM and troubleshoot.
- For special use-cases (app needs a RAM disk with exceptionally low latency and high throughput and cannot just use the VM memory), you can create a tmpfs filesystem by allocating some VM memory as a RAM disk.
- If needed, you can attach 1-24 local SSDs (ephemeral = data is lost if VM stops; each 375 GB and physically attached to the server that hosts your VM instance). Local SSDs are NOT the same as PD SSDs!!!
