# BYO-CLAB-VXR-K8s-Lab

A short guide to building your own Containerlab + VXR + K8s lab (or reproducing Cisco Live Lab LTRSPG-2212) in your own environment or in the cloud


## Lab Hosts

* Topology Host: Ubuntu (22.04 or 24.04) VM or server: we recommend 32 vCPU, 96GB RAM, 200GB disk
* Jalapeno Host: Ubuntu (22.04 or 24.04) VM or server: we recommend 4 vCPU, 16GB RAM, 80GB disk

**First Step** - update [hosts](./topology-host-vms/ansible/hosts) ip addresses and playbook user/pw info to suit your env

## Topology Host

1. Apt update/upgrade
```
sudo apt update && sudo apt upgrade
```

2. Install python3-pip and sshpass
```
sudo apt install python3-pip sudo sshpass
```

3. Install Ansible
```
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
```

4. Clone this repo
```
git clone https://github.com/brmcdoug/byo-clab-vxr-k8s.git
```

5. Run Ansible *`vms-playbook`*
```
cd topology-host-vms/ansible/
ansible-playbook -i hosts vms-playbook.yaml -e "ansible_user=cisco ansible_ssh_pass=cisco123 ansible_sudo_pass=cisco123" -vv
```

The script will operate apt update, update hostnames, timezones, etc., on both the *`topology-host`* and *`jalapeno`* VMs.

On the *`topology-host`* the script will install containerlab and the clab fork of vrnetlab

On the *`jalapeno`* VM the script will install Docker, Kind, and Helm. It will launch a Kind cluster and run the helm chart to install Jalapeno on the cluster.

6. Verify Containerlab on *`topology-host`*
```
clab version
```

7. ssh to the *`jalapeno`* VM and verify Kind cluster and Jalapeno install:
```
kubectl get nodes
kubectl get pods -A
```

Expected output should include several pods in the *`jalapeno`* namespace
   
8. Install VXR (contact Cisco account team for image download access): 

   https://www.cisco.com/c/en/us/td/docs/iosxr/cisco8000-emulator/cisco8000-hardware-emulator-installation-guide.html

9. untar the VXR package
```
tar -xvf 8000-emulator-eft16.0.tar
```

And the sonic package if you have it
```
tar -xvf 8000-sonic-eft16.0.tar 
```

10. cd into the 8000-eft scripts directory and run the Ubuntu install script
```
cd 8000-eft16.0/scripts/

sudo ./ubuntuServerManualSetup.sh 
```


11. Download/Acquire XRd image(s) - choose XRd Control Plane option: 

   https://www.cisco.com/c/en/us/support/routers/ios-xrd/series.html#~tab-downloads 






