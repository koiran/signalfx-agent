<!--- GENERATED BY gomplate from scripts/docs/templates/monitor-page.md.tmpl --->

# vsphere

Monitor Type: `vsphere` ([Source](https://github.com/signalfx/signalfx-agent/tree/master/pkg/monitors/vsphere))

**Accepts Endpoints**: **Yes**

**Multiple Instances Allowed**: Yes

## Overview

A VMware vSphere deployment includes physical hosts, ESXi hypervisors, virtual machines, and vCenter Server.
This monitor reports metrics for a vSphere deployment by logging into a vCenter Server and periodically
retrieving data about the deployment and its real time performance data.

When this monitor starts up, it logs into vCenter Server and traverses the inventory, gathering and caching all of
the hosts and virtual machines, and their available metrics.

Then it periodically queries the vCenter for the performance data for those metrics. It does so at a rate of
once every 20 seconds, the interval at which vCenter makes real-time performance data avaialable.

Because the 20 second interval for real-time metrics is fixed by vSphere, this monitor runs every 20 seconds,
regardless of the IntervalSeconds value in the agent config.

It also refreshes, at a configurable interval, the cache of hosts, virtual machines, and metrics. By default,
it does this every 60 seconds, but this interval can be changed by updating the configuration field
`InventoryRefreshInterval`.

Compatibility:
This monitor uses VMware's govmomi SDK, which is built for and tested against vCenter 6.0, 6.5 and 6.7.
It may work with versions 5.5 and 5.1, but neither are officially supported.

Sample YAML configuration:
```yaml
monitors:
  - type: vsphere
    host: "172.16.248.140"
    username: "administrator@vsphere.local"
    password: "S3cr3t"
    insecureSkipVerify: true
```


## Configuration

To activate this monitor in the Smart Agent, add the following to your
agent config:

```
monitors:  # All monitor config goes under this key
 - type: vsphere
   ...  # Additional config
```

**For a list of monitor options that are common to all monitors, see [Common
Configuration](../monitor-config.md#common-configuration).**


| Config option | Required | Type | Description |
| --- | --- | --- | --- |
| `host` | no | `string` |  |
| `port` | no | `integer` |  (**default:** `0`) |
| `username` | no | `string` | The vSphere username |
| `password` | no | `string` | The vSphere password |
| `insecureSkipVerify` | no | `bool` | Whether we verify the server's certificate chain and host name (**default:** `false`) |
| `inventoryRefreshInterval` | no | `int64` | How often to reload the inventory and inventory metrics (**default:** `60s`) |
| `tlsCACertPath` | no | `string` | Path to the ca file |
| `tlsClientCertificatePath` | no | `string` | Configure client certs. Both tlsClientKeyPath and tlsClientCertificatePath must be present. The files must contain PEM encoded data. Path to the client certificate |
| `tlsClientKeyPath` | no | `string` | Path to the keyfile |


## Metrics

These are the metrics available for this monitor.
Metrics that are categorized as
[container/host](https://docs.signalfx.com/en/latest/admin-guide/usage.html#about-custom-bundled-and-high-resolution-metrics)
(*default*) are ***in bold and italics*** in the list below.


#### Group cpu
All of the following metrics are part of the `cpu` metric group. All of
the non-default metrics below can be turned on by adding `cpu` to the
monitor config option `extraGroups`:
 - `vsphere.cpu_core_utilization_percent` (*gauge*)<br>    CPU utilization of the corresponding core as a percentage during the interval.
 - `vsphere.cpu_costop_ms` (*counter*)<br>    Time the virtual machine is ready to run, but is unable to run due to co-scheduling constraints.
 - `vsphere.cpu_demand_entitlement_ratio_percent` (*gauge*)<br>    CPU resource entitlement to CPU demand ratio.
 - `vsphere.cpu_demand_mhz` (*counter*)<br>    The amount of CPU resources a virtual machine would use if there were no CPU contention or CPU limit.
 - `vsphere.cpu_entitlement_mhz` (*gauge*)<br>    CPU resources devoted by the ESXi scheduler.
 - `vsphere.cpu_idle_ms` (*counter*)<br>    Total time that the CPU spent in an idle state.
 - `vsphere.cpu_maxlimited_ms` (*counter*)<br>    Time the virtual machine is ready to run, but is not running because it has reached its maximum CPU limit setting.
 - `vsphere.cpu_overlap_ms` (*counter*)<br>    Time the virtual machine was interrupted to perform system services on behalf of itself or other virtual machines.
 - `vsphere.cpu_readiness_percent` (*gauge*)<br>    Percentage of time that the virtual machine was ready, but could not get scheduled to run on the physical CPU.
 - `vsphere.cpu_ready_ms` (*counter*)<br>    Time that the virtual machine was ready, but could not get scheduled to run on the physical CPU during last measurement interval. CPU ready time is dependent on the number of virtual machines on the host and their CPU loads.
 - `vsphere.cpu_reservedCapacity_mhz` (*gauge*)<br>    Total CPU capacity reserved by virtual machines.
 - `vsphere.cpu_run_ms` (*counter*)<br>    Time the virtual machine is scheduled to run
 - `vsphere.cpu_swapwait_ms` (*gauge*)<br>    CPU time spent waiting for swap-in.
 - `vsphere.cpu_system_ms` (*counter*)<br>    Amount of time spent on system processes on each virtual CPU in the virtual machine.
 - `vsphere.cpu_totalCapacity_mhz` (*gauge*)<br>    Total CPU capacity reserved by and available for virtual machines
 - `vsphere.cpu_usage_percent` (*gauge*)<br>    CPU usage as a percentage during the interval.
 - `vsphere.cpu_usagemhz` (*gauge*)<br>    CPU usage, as measured in megahertz, during the interval.
 - `vsphere.cpu_used_percent` (*counter*)<br>    Time accounted to the virtual machine.
 - `vsphere.cpu_utilization_percent` (*gauge*)<br>    CPU utilization as a percentage during the interval. CPU usage and CPU utilization might be different due to power management technologies or hyper-threading.
 - `vsphere.cpu_wait_ms` (*counter*)<br>    Total CPU time spent in wait state. The wait total includes time spent the CPU Idle, CPU Swap Wait, and CPU I/O Wait states.
 - `vsphere_cpu_latency_percent` (*gauge*)<br>    Percent of time the virtual machine is unable to run because it is contending for access to the physical CPU(s).

#### Group datastore
All of the following metrics are part of the `datastore` metric group. All of
the non-default metrics below can be turned on by adding `datastore` to the
monitor config option `extraGroups`:
 - `vsphere.datastore.datastore_read_load_metric` (*gauge*)<br>    Storage DRS datastore metric for read workload model.
 - `vsphere.datastore.datastore_vmobserved_latency_ms` (*gauge*)<br>    The average datastore latency as seen by virtual machines.
 - `vsphere.datastore.datastore_write_load_metric` (*gauge*)<br>    Storage DRS datastore metric for write workload model.
 - `vsphere.datastore.max_total_latency_ms` (*gauge*)<br>    Highest latency value across all datastores used by the host.
 - `vsphere.datastore.read_kbs` (*gauge*)<br>    Rate of reading data from the datastore (kilobytes per second)
 - `vsphere.datastore.size_normalized_datastore_latency_ms` (*gauge*)<br>    Storage I/O Control size-normalized I/O latency.
 - `vsphere.datastore.total_read_latency_ms` (*gauge*)<br>    Average amount of time for a read operation from the vsphere.datastore. Total latency = kernel latency + device latency.
 - `vsphere.datastore.total_write_latency_ms` (*gauge*)<br>    Average amount of time for a write operation to the vsphere.datastore. Total latency = kernel latency + device latency.
 - `vsphere.datastore.write_kbs` (*gauge*)<br>    Rate of writing data to the datastore.
 - `vsphere.datastore_datastoreIops` (*gauge*)<br>    Average amount of time for an I/O operation to the datastore or LUN across all ESX hosts accessing it.

#### Group disk
All of the following metrics are part of the `disk` metric group. All of
the non-default metrics below can be turned on by adding `disk` to the
monitor config option `extraGroups`:
 - `vsphere.disk.bus_resets` (*counter*)<br>    Number of SCSI-bus reset commands issued during the collection interval.
 - `vsphere.disk.commands` (*counter*)<br>    Number of SCSI commands issued during the collection interval.
 - `vsphere.disk.commands_aborted` (*counter*)<br>    Number of SCSI commands aborted during the collection interval.
 - `vsphere.disk.commands_averaged` (*gauge*)<br>    Average number of SCSI commands issued per second during the collection interval.
 - `vsphere.disk.device_latency_ms` (*gauge*)<br>    Average amount of time, in milliseconds, to complete a SCSI command from the physical device.
 - `vsphere.disk.device_read_latency_ms` (*gauge*)<br>    Average amount of time, in milliseconds, to read from the physical device.
 - `vsphere.disk.device_write_latency_ms` (*gauge*)<br>    Average amount of time, in milliseconds, to write to the physical device.
 - `vsphere.disk.kernel_latency_ms` (*gauge*)<br>    Average amount of time, in milliseconds, spent by VMkernel to process each SCSI command.
 - `vsphere.disk.kernel_read_latency_ms` (*gauge*)<br>    Average amount of time, in milliseconds, spent by VMkernel to process each SCSI read command.
 - `vsphere.disk.kernel_write_latency_ms` (*gauge*)<br>    Average amount of time, in milliseconds, spent by VMkernel to process each SCSI write command.
 - `vsphere.disk.max_queue_depth` (*gauge*)<br>    Maximum queue depth.
 - `vsphere.disk.max_total_latency_ms` (*gauge*)<br>    Highest latency value across all disks used by the host.
 - `vsphere.disk.number_read` (*counter*)<br>    Number of disk reads during the collection interval.
 - `vsphere.disk.number_read_averaged` (*gauge*)<br>    Average number of read commands issued per second to the datastore during the collection interval.
 - `vsphere.disk.number_write` (*counter*)<br>    Number of disk writes during the collection interval.
 - `vsphere.disk.number_write_averaged` (*gauge*)<br>    Average number of write commands issued per second to the datastore during the collection interval.
 - `vsphere.disk.queue_latency_ms` (*gauge*)<br>    Average amount of time spent in the VMkernel queue, per SCSI command, during the collection interval.
 - `vsphere.disk.queue_read_latency_ms` (*gauge*)<br>    Average amount of time spent in the VMkernel queue, per SCSI read command, during the collection interval.
 - `vsphere.disk.queue_write_latency_ms` (*gauge*)<br>    Average amount of time spent in the VMkernel queue, per SCSI write command, during the collection interval.
 - `vsphere.disk.read_kbs` (*gauge*)<br>    Average number of kilobytes read from the disk each second during the collection interval.
 - `vsphere.disk.total_latency_ms` (*gauge*)<br>    Average amount of time taken during the collection interval to process a SCSI command issued by the guest OS to the virtual machine.
 - `vsphere.disk.total_read_latency_ms` (*gauge*)<br>    Average amount of time taken during the collection interval to process a SCSI read command issued from the guest OS to the virtual machine.
 - `vsphere.disk.total_write_latency_ms` (*gauge*)<br>    Average amount of time taken during the collection interval to process a SCSI write command issued by the guest OS to the virtual machine.
 - `vsphere.disk.usage_kbs` (*gauge*)<br>    Aggregated disk I/O rate.
 - `vsphere.disk.write_kbs` (*gauge*)<br>    Average number of kilobytes written to disk each second during the collection interval.

#### Group hbr
All of the following metrics are part of the `hbr` metric group. All of
the non-default metrics below can be turned on by adding `hbr` to the
monitor config option `extraGroups`:
 - `vsphere.hbr.hbr_net_rx_kbs` (*gauge*)<br>    Kilobytes per second of outgoing host-based replication network traffic (for this virtual machine or host).
 - `vsphere.hbr.hbr_net_tx_kbs` (*gauge*)<br>    Average amount of data transmitted per second.
 - `vsphere.hbr.hbr_num_vms` (*gauge*)<br>    Number of powered-on virtual machines running on this host that currently have host-based replication protection enabled.

#### Group mem
All of the following metrics are part of the `mem` metric group. All of
the non-default metrics below can be turned on by adding `mem` to the
monitor config option `extraGroups`:
 - `vsphere.mem.active_kb` (*gauge*)<br>    Amount of memory that is actively used, as estimated by VMkernel based on recently touched memory pages.
 - `vsphere.mem.activewrite_kb` (*gauge*)<br>    Estimate for the amount of memory actively being written to by the virtual machine.
 - `vsphere.mem.compressed_kb` (*gauge*)<br>    Amount of memory reserved by userworlds.
 - `vsphere.mem.compression_rate_kbs` (*gauge*)<br>    Rate of memory compression for the virtual machine.
 - `vsphere.mem.consumed_kb` (*gauge*)<br>    Amount of host physical memory consumed by a virtual machine, host, or cluster.
 - `vsphere.mem.decompression_rate_kbs` (*gauge*)<br>    Rate of memory decompression for the virtual machine.
 - `vsphere.mem.entitlement_kb` (*gauge*)<br>    Amount of host physical memory the virtual machine is entitled to, as determined by the ESX scheduler.
 - `vsphere.mem.granted_kb` (*gauge*)<br>    Amount of host physical memory or physical memory that is mapped for a virtual machine or a host.
 - `vsphere.mem.heap_kb` (*gauge*)<br>    VMkernel virtual address space dedicated to VMkernel main heap and related data.
 - `vsphere.mem.heapfree_kb` (*gauge*)<br>    Free address space in the VMkernel main heap.Varies based on number of physical devices and configuration options.
 - `vsphere.mem.latency_percent` (*gauge*)<br>    Percentage of time the virtual machine is waiting to access swapped or compressed memory.
 - `vsphere.mem.ll_swap_in_kb` (*gauge*)<br>    Amount of memory swapped-in from host cache.
 - `vsphere.mem.ll_swap_in_rate_kbs` (*gauge*)<br>    Rate at which memory is being swapped from host cache into active memory.
 - `vsphere.mem.ll_swap_out_kb` (*gauge*)<br>    Amount of memory swapped-out to host cache.
 - `vsphere.mem.ll_swap_out_rate_kbs` (*gauge*)<br>    Rate at which memory is being swapped from active memory to host cache.
 - `vsphere.mem.ll_swap_used_kb` (*gauge*)<br>    Space used for caching swapped pages in the host cache.
 - `vsphere.mem.lowfreethreshold_kb` (*gauge*)<br>    Threshold of free host physical memory below which ESX/ESXi will begin reclaiming memory from virtual machines through ballooning and swapping.
 - `vsphere.mem.overhead_kb` (*gauge*)<br>    Host physical memory (KB) consumed by the virtualization infrastructure for running the virtual machine.
 - `vsphere.mem.overhead_max_kb` (*gauge*)<br>    Host physical memory (KB) reserved for use as the virtualization overhead for the virtual machine.
 - `vsphere.mem.overhead_touched_kb` (*gauge*)<br>    Actively touched overhead host physical memory (KB) reserved for use as the virtualization overhead for the virtual machine.
 - `vsphere.mem.reserved_capacity_mb` (*gauge*)<br>    Total amount of memory reservation used by powered-on virtual machines and vSphere services on the host.
 - `vsphere.mem.shared_kb` (*gauge*)<br>    Amount of guest physical memory that is shared with other virtual machines, relative to a single virtual machine or to all powered-on virtual machines on a host.
 - `vsphere.mem.sharedcommon_kb` (*gauge*)<br>    Amount of machine memory that is shared by all powered-on virtual machines and vSphere services on the host.Subtract this metric from the shared metric to gauge how much machine memory is saved due to sharing -- shared - sharedcommon = machine memory (host memory) savings (KB).
 - `vsphere.mem.state` (*gauge*)<br>    One of four threshold levels representing the percentage of free memory on the host. The counter value determines swapping and ballooning behavior for memory reclamation.
 - `vsphere.mem.swapin_kb` (*gauge*)<br>    Amount swapped-in to memory from disk.
 - `vsphere.mem.swapin_rate_kbs` (*gauge*)<br>    Rate at which memory is swapped from disk into active memory during the interval.
 - `vsphere.mem.swapout_kb` (*gauge*)<br>    Amount of memory swapped-out to disk.
 - `vsphere.mem.swapout_rate_kbs` (*gauge*)<br>    Rate at which memory is being swapped from active memory to disk during the current interval.
 - `vsphere.mem.swapped_kb` (*gauge*)<br>    Current amount of guest physical memory swapped out to the virtual machine swap file by the VMkernel.
 - `vsphere.mem.swaptarget_kb` (*gauge*)<br>    Target size for the virtual machine swap file.
 - `vsphere.mem.swapused_kb` (*gauge*)<br>    Amount of memory that is used by swap.
 - `vsphere.mem.sys_usage_kb` (*gauge*)<br>    Amount of host physical memory used by VMkernel for core functionality, such as device drivers and other internal uses.
 - `vsphere.mem.total_capacity_mb` (*gauge*)<br>    Total amount of memory reservation used by and available for powered-on virtual machines and vSphere services on the host.
 - `vsphere.mem.unreserved_kb` (*gauge*)<br>    Amount of memory that is unreserved.
 - `vsphere.mem.usage_percent` (*gauge*)<br>    Percentage of host physical memory that has been consumed.
 - `vsphere.mem.vmfs_pbc_cap_miss_ratio_percent` (*gauge*)<br>    Trailing average of the ratio of capacity misses to compulsory misses for the VMFS PB Cache.
 - `vsphere.mem.vmfs_pbc_overhead_kb` (*gauge*)<br>    Amount of VMFS heap used by the VMFS PB Cache.
 - `vsphere.mem.vmfs_pbc_size_max_mb` (*gauge*)<br>    Maximum size the VMFS Pointer Block Cache can grow to.
 - `vsphere.mem.vmfs_pbc_size_mb` (*gauge*)<br>    Space used for holding VMFS Pointer Blocks in memory.
 - `vsphere.mem.vmfs_pbc_working_set_max_tb` (*gauge*)<br>    Maximum amount of file blocks whose addresses are cached in the VMFS PB Cache.
 - `vsphere.mem.vmfs_pbc_working_set_tb` (*gauge*)<br>    Amount of file blocks whose addresses are cached in the VMFS PB Cache.
 - `vsphere.mem.vmmemctl_kb` (*gauge*)<br>    Amount of memory allocated by the virtual machine memory control driver.
 - `vsphere.mem.vmmemctltarget_kb` (*gauge*)<br>    Target value set by VMkernal for the virtual machine's memory balloon size.
 - `vsphere.mem.zero_kb` (*gauge*)<br>    Memory that contains 0s only.
 - `vsphere.mem.zip_saved_kb` (*gauge*)<br>    Memory (KB) saved due to memory zipping.
 - `vsphere.mem.zipped_kb` (*gauge*)<br>    Memory (KB) zipped.

#### Group net
All of the following metrics are part of the `net` metric group. All of
the non-default metrics below can be turned on by adding `net` to the
monitor config option `extraGroups`:
 - `vsphere.net.broadcast_rx` (*counter*)<br>    Number of broadcast packets received during the sampling interval.
 - `vsphere.net.broadcast_tx` (*counter*)<br>    Number of broadcast packets transmitted during the sampling interval.
 - `vsphere.net.bytes_rx_kbs` (*gauge*)<br>    Average amount of data received per second.
 - `vsphere.net.bytes_tx_kbs` (*gauge*)<br>    Average amount of data transmitted per second.
 - `vsphere.net.dropped_rx` (*counter*)<br>    Number of received packets dropped during the collection interval.
 - `vsphere.net.dropped_tx` (*counter*)<br>    Number of transmitted packets dropped during the collection interval.
 - `vsphere.net.errors_rx` (*counter*)<br>    Number of packets with errors received during the sampling interval.
 - `vsphere.net.errors_tx` (*counter*)<br>    Number of packets with errors transmitted during the sampling interval.
 - `vsphere.net.multicast_rx` (*counter*)<br>    Number of multicast packets received during the sampling interval.
 - `vsphere.net.multicast_tx` (*counter*)<br>    Number of multicast packets transmitted during the sampling interval.
 - `vsphere.net.packets_rx` (*counter*)<br>    Number of packets received during the interval.
 - `vsphere.net.packets_tx` (*counter*)<br>    Number of packets transmitted during the interval.
 - `vsphere.net.received_kbs` (*gauge*)<br>    Average rate at which data was received during the interval.
 - `vsphere.net.transmitted_kbs` (*gauge*)<br>    Average rate at which data was transmitted during the interval. This represents the bandwidth of the network.
 - `vsphere.net.unknown_protos` (*counter*)<br>    Number of frames with unknown protocol received during the sampling interval
 - `vsphere.net.usage_kbs` (*gauge*)<br>    Network utilization (combined transmit- and receive-rates) during the interval.

#### Group power
All of the following metrics are part of the `power` metric group. All of
the non-default metrics below can be turned on by adding `power` to the
monitor config option `extraGroups`:
 - `vsphere.power.energy_joules` (*counter*)<br>    Total energy used since last stats reset.
 - `vsphere.power.power_cap_watts` (*gauge*)<br>    Maximum allowed power usage.
 - `vsphere.power.power_watts` (*gauge*)<br>    Current power usage.

#### Group rescpu
All of the following metrics are part of the `rescpu` metric group. All of
the non-default metrics below can be turned on by adding `rescpu` to the
monitor config option `extraGroups`:
 - `vsphere.rescpu.actav1` (*gauge*)<br>    CPU active average over 1 minute.
 - `vsphere.rescpu.actav15_percent` (*gauge*)<br>    CPU active average over 15 minutes.
 - `vsphere.rescpu.actav5_percent` (*gauge*)<br>    CPU active average over 5 minutes.
 - `vsphere.rescpu.actpk15_percent` (*gauge*)<br>    CPU active peak over 15 minutes.
 - `vsphere.rescpu.actpk1_percent` (*gauge*)<br>    CPU active peak over 1 minute.
 - `vsphere.rescpu.actpk5_percent` (*gauge*)<br>    CPU active peak over 5 minutes.
 - `vsphere.rescpu.max_limited15_percent` (*gauge*)<br>    Amount of CPU resources over the limit that were refused, average over 15 minutes.
 - `vsphere.rescpu.max_limited1_percent` (*gauge*)<br>    Amount of CPU resources over the limit that were refused, average over 1 minute.
 - `vsphere.rescpu.max_limited5_percent` (*gauge*)<br>    Amount of CPU resources over the limit that were refused, average over 5 minutes.
 - `vsphere.rescpu.runav15_percent` (*gauge*)<br>    CPU running average over 15 minutes.
 - `vsphere.rescpu.runav1_percent` (*gauge*)<br>    CPU running average over 1 minute.
 - `vsphere.rescpu.runav5_percent` (*gauge*)<br>    CPU running average over 5 minutes.
 - `vsphere.rescpu.runpk15_percent` (*gauge*)<br>    CPU running peak over 15 minutes.
 - `vsphere.rescpu.runpk1_percent` (*gauge*)<br>    CPU running peak over 1 minute.
 - `vsphere.rescpu.runpk5_percent` (*gauge*)<br>    CPU running peak over 5 minutes.
 - `vsphere.rescpu.sample_count` (*gauge*)<br>    Group CPU sample count.
 - `vsphere.rescpu.sample_period_ms` (*gauge*)<br>    Group CPU sample period.

#### Group storage_adapter
All of the following metrics are part of the `storage_adapter` metric group. All of
the non-default metrics below can be turned on by adding `storage_adapter` to the
monitor config option `extraGroups`:
 - `vsphere.storage_adapter.commands_averaged` (*gauge*)<br>    Average number of commands issued per second by the storage adapter during the collection interval.
 - `vsphere.storage_adapter.max_total_latency_ms` (*gauge*)<br>    Highest latency value across all storage adapters used by the host.
 - `vsphere.storage_adapter.number_read_averaged` (*gauge*)<br>    Average number of read commands issued per second by the storage adapter during the collection interval.
 - `vsphere.storage_adapter.number_write_averaged` (*gauge*)<br>    Average number of write commands issued per second by the storage adapter during the collection interval.
 - `vsphere.storage_adapter.read_kbs` (*gauge*)<br>    Rate of reading data by the storage adapter.
 - `vsphere.storage_adapter.total_read_latency_ms` (*gauge*)<br>    Average amount of time for a read operation by the storage adapter. Total latency = kernel latency + device latency.
 - `vsphere.storage_adapter.total_write_latency_ms` (*gauge*)<br>    Average amount of time for a write operation by the storage adapter. Total latency = kernel latency + device latency.
 - `vsphere.storage_adapter.write_kbs` (*gauge*)<br>    Rate of writing data by the storage adapter.

#### Group storage_path
All of the following metrics are part of the `storage_path` metric group. All of
the non-default metrics below can be turned on by adding `storage_path` to the
monitor config option `extraGroups`:
 - `vsphere.storage_path.commands_averaged` (*gauge*)<br>    Average number of commands issued per second on the storage path during the collection interval.
 - `vsphere.storage_path.max_total_latency_ms` (*gauge*)<br>    Highest latency value across all storage paths used by the host.
 - `vsphere.storage_path.number_read_averaged` (*gauge*)<br>    Average number of read commands issued per second on the storage path during the collection interval.
 - `vsphere.storage_path.number_write_averaged` (*gauge*)<br>    Average number of write commands issued per second on the storage path during the collection interval.
 - `vsphere.storage_path.read_kbs` (*gauge*)<br>    Rate of reading data on the storage path.
 - `vsphere.storage_path.total_read_latency_ms` (*gauge*)<br>    The average time a read issued on the storage path takes.
 - `vsphere.storage_path.total_write_latency_ms` (*gauge*)<br>    Average amount of time for a write issued on the storage path. Total latency = kernel latency + device latency.
 - `vsphere.storage_path.write_kbs` (*gauge*)<br>    Rate of writing data on the storage path.

#### Group sys
All of the following metrics are part of the `sys` metric group. All of
the non-default metrics below can be turned on by adding `sys` to the
monitor config option `extraGroups`:
 - `vsphere.sys.heartbeat` (*counter*)<br>    Number of heartbeats issued per virtual machine during the interval.
 - `vsphere.sys.os_uptime_seconds` (*gauge*)<br>    Total time elapsed, in seconds, since last operating system boot-up.
 - `vsphere.sys.resource_cpu_act1_percent` (*gauge*)<br>    CPU active average over 1 minute of the system resource group.
 - `vsphere.sys.resource_cpu_act5` (*gauge*)<br>    CPU active average over 5 minutes of the system resource group.
 - `vsphere.sys.resource_cpu_alloc_min_mhz` (*gauge*)<br>    CPU allocation reservation (in MHz) of the system resource group.
 - `vsphere.sys.resource_cpu_alloc_shares` (*gauge*)<br>    CPU allocation shares of the system resource group.
 - `vsphere.sys.resource_cpu_max_limited1_percent` (*gauge*)<br>    CPU maximum limited over 1 minute of the system resource group.
 - `vsphere.sys.resource_cpu_max_limited5_percent` (*gauge*)<br>    CPU maximum limited over 5 minutes of the system resource group.
 - `vsphere.sys.resource_cpu_run1_percent` (*gauge*)<br>    CPU running average over 1 minute of the system resource group.
 - `vsphere.sys.resource_cpu_run5_percent` (*gauge*)<br>    CPU running average over 5 minutes of the system resource group.
 - `vsphere.sys.resource_cpu_usage_mhz` (*gauge*)<br>    Amount of CPU used by the Service Console and other applications during the interval by the Service Console and other applications.
 - `vsphere.sys.resource_fd_usage` (*gauge*)<br>    Number of file descriptors used by the system resource group.
 - `vsphere.sys.resource_mem_alloc_max_kb` (*gauge*)<br>    Memory allocation limit (in KB) of the system resource group.
 - `vsphere.sys.resource_mem_alloc_min_kb` (*gauge*)<br>    Memory allocation reservation (in KB) of the system resource group.
 - `vsphere.sys.resource_mem_alloc_shares` (*gauge*)<br>    Memory allocation shares of the system resource group.
 - `vsphere.sys.resource_mem_consumed_kb` (*gauge*)<br>    Memory consumed by the system resource group.
 - `vsphere.sys.resource_mem_cow_kb` (*gauge*)<br>    Memory shared by the system resource group.
 - `vsphere.sys.resource_mem_mapped_kb` (*gauge*)<br>    Memory mapped by the system resource group.
 - `vsphere.sys.resource_mem_overhead_kb` (*gauge*)<br>    Overhead memory consumed by the system resource group.
 - `vsphere.sys.resource_mem_shared_kb` (*gauge*)<br>    Memory saved due to sharing by the system resource group.
 - `vsphere.sys.resource_mem_swapped_kb` (*gauge*)<br>    Memory swapped out by the system resource group.
 - `vsphere.sys.resource_mem_touched_kb` (*gauge*)<br>    Memory touched by the system resource group.
 - `vsphere.sys.resource_mem_zero_kb` (*gauge*)<br>    Zero filled memory used by the system resource group.
 - `vsphere.sys.uptime_seconds` (*gauge*)<br>    Total time elapsed, in seconds, since last system startup.

#### Group virtual_disk
All of the following metrics are part of the `virtual_disk` metric group. All of
the non-default metrics below can be turned on by adding `virtual_disk` to the
monitor config option `extraGroups`:
 - `vsphere.virtual_disk.large_seeks` (*gauge*)<br>    Number of seeks during the interval that were greater than 8192 LBNs apart.
 - `vsphere.virtual_disk.medium_seeks` (*gauge*)<br>    Number of seeks during the interval that were between 64 and 8192 LBNs apart.
 - `vsphere.virtual_disk.number_read_averaged` (*gauge*)<br>    Average number of read commands issued per second to the virtual disk during the collection interval.
 - `vsphere.virtual_disk.number_write_averaged` (*gauge*)<br>    Average number of write commands issued per second to the virtual disk during the collection interval.
 - `vsphere.virtual_disk.read_iosize` (*gauge*)<br>    Average read request size in bytes.
 - `vsphere.virtual_disk.read_kbs` (*gauge*)<br>    Rate of reading data from the virtual disk.
 - `vsphere.virtual_disk.read_latency_us` (*gauge*)<br>    Read latency in microseconds.
 - `vsphere.virtual_disk.read_load_metric` (*gauge*)<br>    Storage DRS virtual disk metric for the read workload model.
 - `vsphere.virtual_disk.read_oio` (*gauge*)<br>    Average number of outstanding read requests to the virtual disk during the collection interval.
 - `vsphere.virtual_disk.small_seeks` (*gauge*)<br>    Number of seeks during the interval that were less than 64 LBNs apart.
 - `vsphere.virtual_disk.total_read_latency_ms` (*gauge*)<br>    Average amount of time for a read operation from the virtual disk. Total latency = kernel latency + device latency.
 - `vsphere.virtual_disk.total_write_latency_ms` (*gauge*)<br>    The average time a write to the virtual disk takes.
 - `vsphere.virtual_disk.write_iosize` (*gauge*)<br>    Average write request size in bytes.
 - `vsphere.virtual_disk.write_kbs` (*gauge*)<br>    Rate of writing data to the virtual disk.
 - `vsphere.virtual_disk.write_latency_us` (*gauge*)<br>    Write latency in microseconds.
 - `vsphere.virtual_disk.write_load_metric` (*gauge*)<br>    Storage DRS virtual disk metric for the write workload model.
 - `vsphere.virtual_disk.write_oio` (*gauge*)<br>    Average number of outstanding write requests to the virtual disk during the collection interval.

### Non-default metrics (version 4.7.0+)

**The following information applies to the agent version 4.7.0+ that has
`enableBuiltInFiltering: true` set on the top level of the agent config.**

To emit metrics that are not _default_, you can add those metrics in the
generic monitor-level `extraMetrics` config option.  Metrics that are derived
from specific configuration options that do not appear in the above list of
metrics do not need to be added to `extraMetrics`.

To see a list of metrics that will be emitted you can run `agent-status
monitors` after configuring this monitor in a running agent instance.

### Legacy non-default metrics (version < 4.7.0)

**The following information only applies to agent version older than 4.7.0. If
you have a newer agent and have set `enableBuiltInFiltering: true` at the top
level of your agent config, see the section above. See upgrade instructions in
[Old-style whitelist filtering](../legacy-filtering.md#old-style-whitelist-filtering).**

If you have a reference to the `whitelist.json` in your agent's top-level
`metricsToExclude` config option, and you want to emit metrics that are not in
that whitelist, then you need to add an item to the top-level
`metricsToInclude` config option to override that whitelist (see [Inclusion
filtering](../legacy-filtering.md#inclusion-filtering).  Or you can just
copy the whitelist.json, modify it, and reference that in `metricsToExclude`.


