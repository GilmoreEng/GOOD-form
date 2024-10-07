1. [Cyberinfrastructure and Advanced Research Computing](index.html)
2. [Cyberinfrastructure and Advanced Research Computing Home](Cyberinfrastructure-and-Advanced-Research-Computing-Home_26640754.html)
3. [HPC Cluster documentation](HPC-Cluster-documentation_26640757.html)

# Cyberinfrastructure and Advanced Research Computing : \_Common problems









Created by  Mike Robbert, last modified on Jan 26, 2024


### Node management

All of these r\* commands must be run as root on the management node of the cluster.

- Reboot any node managed by xCAT (compute, gpu, storage, DTN)
  - **rpower $NODENAME boot**
  - The "boot" argument in the above command can be replaced with on, off, reset
- View hardware logs of a node (SEL - System Event Log) - Used to troubleshoot hardware issues like memory failure or power issues
  - **reventlog $NODENAME**
- Turn on the identification light of a node to find its physical location in the rack
  - **rbeacon $NODENAME on**
  - Run again with the off argument to turn it off. If you remove power from the node this isn't needed.
- Get inventory data from a node - Serial numbers, Firmware versions
  - **rinv $NODENAME**
- Get current sensor data from a node - internal voltages, temperatures, fan speeds
  - **rvitals $NODENAME**
  - Optional arguments may be added to filter output - rvitals noderange {temp\|voltage\|wattage\|fanspeed\|power\|leds\|all}
- Start a console session on a node
  - **rcons $NODENAME**
- Reinstall the OS of a compute node
  - **rinstall $NODENAME**

#### Diagnosing repeated node reboots (specifically Wendian nodes)

If a node shows up as down in Slurm you first check it with **scontrol show node $NODENAME**

If the Reason looks like the following then you'll want to diagnose why the node rebooted: Reason=Node unexpectedly rebooted \[slurm@2024-01-23T16:27:21\]

You can check if the kernel crashed by logging into the node and seeing if there are any files in the /var/crash/ directory. This directory is usually empty, but if the kernel crashes it should leave some diagnostic data. The files will be time-stampped to confirm that they are from the reboot you're diagnosing or possibly left from a prior crash. Diagnosing a kernel crash is beyond the scope of this article.

The other thing to check in this instance is the BMC's system event log(SEL) which can be done from the cluster management node with **reventlog $NODENAME**

Here are some common messages that you'll see in the log:

- c012: 01/23/2024 16:24:11 System Event, Boot (Sensor 0x00)
- c012: 01/23/2024 16:25:21 OS Boot, Boot completed - boot device not specified (Sensor 0x22)
  - The above 2 messages are normally seen together any time a node reboots for any reason.
- c012: 06/20/2018 15:39:34 Processor, Processor Presence Detected (CPU0\_Status)
  - The above message is usually seen twice together, once for each CPU socket and typically indicates that the hardware did a full reset. I believe that this is usually a power problem and if it happens repeatedly work needs to be done related to the power input to the node.
- c064: 07/18/2023 08:03:49 Voltage, Lower Non-critical - going low (VR\_P0\_VIN reading 10.75 Volts with threshold 10.75 Volts)
  - This is indicative of a power problem. It could be with a specific component. In the above case the component is VR\_P0\_VIN (Voltage Regulator on Processor 0).
- c004: 07/09/2023 14:00:30 Temperature, Upper Non-critical - going high (CPU0\_TEMP reading 98 C (208 F) with threshold 102 C (216 F)) - Recovered

Voltage of node components can be checked in 2 ways:

1. Realtime/instantaneous as root on the cluster management node: rvitals $NODENAME voltage
2. Historical data logged to Grafana: Dashboards → Node stats. Datasource: Wendian-prom Job: compute Host: $NODENAME. Scroll down to the Hardware Misc section and look for the Voltage panel. This panel should show all components that should be in the 12V range. Note that it is normal to see some voltage drop when there is a load on the node. Below 10.75V is where we start to see SEL warnings.

Steps to troubleshoot a single node power problem on Wendian:

1. See if you can reproduce the issue by running a CPU intensive code on the node. i.e. HPL  Repeat this step after each other step.
2. Jiggle the node - grab the handle on the node and without depressing the release lever move it around. Check component voltages before and after doing that to see if there is a significant jump.
3. Pull the node and check all power connections inside of the chassis. Check the screws where the busbar clips connect to the PDB and check all the PDB connections.
4. Replace the busbar clip if we have any available.
5. Replace the PDB board.

### GPFS issues (Mio cluster only) - Read more about GPFS here: [GPFS Intro](GPFS-Intro_63340621.html)

- Stale file handle on GPFS file system

  - This is caused by the file system in question becoming unmounted, usually due to a node being expelled from the cluster.

  - Possible troubleshooting

    - Check the GPFS logs on management and/or affected nodes - /var/adm/ras/mmfs.log.latest
    - Search for all nodes in the cluster that may have this problem by trying to list files on the file system and see which ones return the error:
      - xdsh compute,gpu,ppc,login "ls /gpfs/lb" \| xcoll
      - Any nodes where the file system isn't mounted will show as an exception with either blank output or some kind of error.
    - Look for hung nodes. Typically shown in a Down state in Slurm and attempts to SSH to node hang. These nodes should be rebooted with " **rpower $NODENAME boot**"
  - FIX: This is usually fixed by running the following command, choosing the correct file system name "lb". Note that when this happens it usually happens to many nodes at once. The following command is safe to run even on unaffected nodes so I usually wrap it in a command to run on all nodes.
    - This command will work from the affected node: **mmmount all**

    - This command will fix it across the cluster: **xdsh compute,gpu,ppc,login "mmmount all"**

### **Slurm issues - Read more about Slurm here: [Slurm intro](Slurm-intro_63340618.html)**

- Slurm node state drained
  - Slurm may put a node into a drained state for many reasons if the node is up and responding, but Slurm feels there may be some problem with running jobs on the node.
  - Diagnosis- Check the reason that it is drained
    - **scontrol show node $NODENAME**
  - Fix - determined by the reason
    - If the Reason code starts with NHC then the drain was triggered by the Node Health Check and can usually by tracked to a hardware or OS level problem based on the description that follows. Hopefully all the checks are fairly obvious, but if not the configuration for NHC is stored at /etc/nhc/nhc.conf. The canonical version of this file is stored on the cluster management server and pushed to all nodes via xCAT.
    - If the Reason code is something to do with epilog scripts then this is a known intermittent problem that I haven't been able to track down. I usually just tell Slurm to ignore it by telling it to undrain the node with the following command:
      - **scontrol update node $NODENAME State=undrain**
    - If this starts happening consistently you can check accounting records or the slurmd log on the node to find the JobID that had unkillable processes and check with the user. It is likely an application that is misbehaving.
    -  If the Reason code is not one of the above, look it up in the slurm documentation
- Slurm node state down
  - As above check the reason with: **scontrol show node $NODENAME**
  - If there is a \* after the state it indicates that the Slurm control daemon can't reach the slurmd on the node. Either the node is down or off the network or the slurmd service isn't running on that node.
  - If the Reason is "Node unexpectedly rebooted" you should investigate why the node rebooted. Use **reventlog $NODENAME** to see if there is anything the BMC SEL.
  - If the node is reachable and you want to clear the state use: **scontrol update Nodename=$NODENAME State=resume**

```

```

Document generated by Confluence on May 14, 2024 06:51

[Atlassian](https://www.atlassian.com/)
