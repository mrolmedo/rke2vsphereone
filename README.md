# 

This project contains a rke2 cluster template helm chart for the Vsphere environment, which can be applied with values.yaml as configurations to create clusters.
This template creates a new cluster, one single Machine Pool with three roles: worker, control-plane, and etcd. The CNI is cilium. Modify the cluster.yaml chart to select a different one.

## Values example
```
cloudprovider: vsphere
cloudCredentialSecretName:
kubernetesVersion: kubernetes_version+rke2
# Specify nodepool options. Can add multiple node groups, specify etcd, controlplane and worker roles.
nodepools:
- etcd: true
  controlplane: true
  worker: true
  quantity: 1
  # Pause node pool
  paused: false
  # specify displayName
  displayName: "Master Pool 1"
  name: "nodepool-1-name"
  cloneFrom: "/datacentername/vm/templates-folder-path/ubuntu-22.04-cloudimg" ## # If you choose creation type clone a name of what you want to clone is required
  cpuCount: '2'
  creationType: "vm"            #Creation type when creating a new virtual machine. Supported values: vm, template, library, legacy'
  vcenter: "vcentername"        # vSphere IP/hostname for vCenter
  datacenter: "datacenter"      # vSphere datastore for virtual machine
  datastore: "datastorepath"    # vSphere datastore for virtual machine
  datastoreCluster: ""          # vSphere datastore cluster for virtual machine
  diskSize: '20480'             # vSphere size of disk for docker VM (in MB)
  folder: "folderpath"          # vSphere folder for the docker VM. This folder must already exist in the datacenter
  # hostsystem: ""
  memorySize: '2048'            # vSphere size of memory for docker VM (in MB)
  network:                      # vSphere network where the virtual machine will be attached
    - /datacentername/network/VM Network
    - /datacentername//network/VM Network_01
  pool: "path-to-resources"     # vSphere resource pool for docker VM
  sshPort: '22'                 # If using a non-B2D image you can specify the ssh port
  sshUserGroup: staff           # If using a non-B2D image the uploaded keys will need chown'ed, defaults to staff e.g. docker:staf
  vcenterPort: '443'            # vSphere Port for vCenter
```
## Links
- https://raw.githubusercontent.com/rancher/cluster-template-examples/main/README.md
