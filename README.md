# BYO-CLAB-VXR-K8s-Lab

A short guide to building your own Containerlab + VXR + K8s lab (or reproducing Cisco Live Lab LTRSPG-2212) in your own lab or in the cloud

## Contents
* Lab Hosts [LINK](#lab-hosts)
* Topology Host[LINK](#topology-host)


## Lab Hosts

* Topology Host: Ubuntu (22.04 or 24.04) VM or server: we recommend 32 vCPU, 96GB RAM, 200GB disk
* Jalapeno Host: Ubuntu VM or server with Kubernetes (Kind or Kubeadm)

## Topology Host

1. Apt update/upgrade
```
sudo apt update && sudo apt upgrade
```

2. Install python3-pip
```
sudo apt install python3-pip
```

3. Install Ansible
```
python3 -m pip install --user ansible
```

4. Run Ansible *`vms-playbook`*
```
cd 

```

5. Install Containerlab: 

   https://containerlab.dev/install/
   
6. Install the containerlab fork of *`vrnetlab`*:

   ```
   git clone https://github.com/srl-labs/vrnetlab
   ```

7. Install VXR (contact Cisco account team for image download access): 

   https://www.cisco.com/c/en/us/td/docs/iosxr/cisco8000-emulator/cisco8000-hardware-emulator-installation-guide.html

8. Download/Acquire XRd image(s) - choose XRd Control Plane option: 

   https://www.cisco.com/c/en/us/support/routers/ios-xrd/series.html#~tab-downloads 






