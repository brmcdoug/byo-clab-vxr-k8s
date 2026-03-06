# BYO-CLAB-VXR-K8s-Lab

A short guide to building your own Containerlab + VXR + K8s lab (or reproducing Cisco Live Lab LTRSPG-2212) in your own lab or in the cloud

## Contents
* Lab Hosts [LINK](#lab-hosts)
* Topology Host[LINK](#topology-host)


## Lab Hosts

* Topology Host: Ubuntu (22.04 or 24.04) VM or server: we recommend 32 vCPU, 96GB RAM, 200GB disk
* Jalapeno Host: Ubuntu VM or server with Kubernetes (Kind or Kubeadm)

**First Step** - update [hosts](./topology-host-vms/ansible/hosts) ip addresses and playbook user/pw info to suit your env

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
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
```

4. Run Ansible *`vms-playbook`*
```
cd topology-host-vms/ansible/
ansible-playbook -i hosts vms-playbook.yaml -e "ansible_user=cisco ansible_ssh_pass=cisco123 ansible_sudo_pass=cisco123" -vv
```

The script will operate apt update, update hostnames, timezones, etc., on both the *`topology-host`* and *`jalapeno`* VMs.

On the *`topology-host`* the script will install containerlab and the clab fork of vrnetlab
On the *`jalapeno`* VM the script will install Docker, Kind, and Helm. It will launch a Kind cluster and run the helm chart to install Jalapeno on the cluster.

5. Verify Containerlab on *`topology-host`*
```
clab version
```

6. ssh to the *`jalapeno`* VM and verify Kind cluster and Jalapeno install:
```

```
   

7. Install VXR (contact Cisco account team for image download access): 

   https://www.cisco.com/c/en/us/td/docs/iosxr/cisco8000-emulator/cisco8000-hardware-emulator-installation-guide.html

8.  Download/Acquire XRd image(s) - choose XRd Control Plane option: 

   https://www.cisco.com/c/en/us/support/routers/ios-xrd/series.html#~tab-downloads 






