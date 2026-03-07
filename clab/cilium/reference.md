## Cilium reference and debug commands

### "show commands"
```
kubectl get IsovalentSRv6LocatorPool -A
kubectl get IsovalentVRF -A
kubectl get IsovalentBGPClusterConfig -A
kubectl get IsovalentBGPPeerConfig -A
kubectl get IsovalentBGPVRFConfig -A
kubectl get IsovalentBGPAdvertisement -A
kubectl get IsovalentBGPNodeConfigOverride -A
kubectl get IsovalentSRv6EgressPolicy -A 
kubectl get IsovalentSRv6EgressPolicy -o yaml
kubectl get IsovalentSRv6EgressPolicy -o jsonpath="{.items[*].spec}" | jq
kubectl get IsovalentSRv6EgressPolicy -o jsonpath="{.items[*].spec}" | jq
kubectl get IsovalentSRv6EgressPolicy -o jsonpath="Name: {.items.metadata.name} | Spec: {.items.spec}"

   echo && kubectl get sidmanager london-vm-02 -o jsonpath="Host: {.metadata.name} | VRF: {.status.sidAllocations[*].sids[*].metadata} | SID: {.status.sidAllocations[*].sids[*].sid.addr} | Behavior: {.status.sidAllocations[*].sids[*].behavior}" && echo
kubectl get IsovalentSRv6SIDManager -A
!
kubectl -n cilium logs ds/cilium | grep -i bgp
kubectl -n cilium exec -it cilium-kll2t -- cilium bgp routes available ipv4 mpls_vpn
kubectl exec -n cilium cilium-q72tf -- cilium-dbg bpf srv6 vrf
kubectl exec -n cilium cilium-q72tf -- cilium-dbg bpf srv6 sid
kubectl exec -n cilium cilium-q72tf -- cilium-dbg bpf srv6 policy
kubectl -n <cilium namespace> <cilium pod running on the target node> logs | grep -E "subsys=.*bgp-control-plane"
kubectl -n cilium logs ds/cilium -f | grep SRv6
kubectl exec -n cilium ds/cilium -- cilium-dbg endpoint list
kubectl exec -n cilium ds/cilium -- cilium-dbg monitor --related-to 476
kubectl get pods -n customer-1 --show-labels
```

### Debug, eBPF maps, etc.
```
kubectl -n kube-system exec ds/cilium -- cilium-dbg bpf srv6 sid list

kubectl -n kube-system exec ds/cilium -- cilium-dbg bpf policy get 1662
kubectl -n kube-system exec cilium-rc6cd -- cilium-dbg endpoint list
kubectl -n kube-system exec cilium-rc6cd -- cilium-dbg bpf policy get 1662
kubectl -n kube-system exec cilium-rc6cd -- cilium-dbg map list
kubectl -n kube-system exec cilium-rc6cd -- cilium-dbg map get cilium_srv6_policy_v4
kubectl -n kube-system exec cilium-rc6cd -- cilium-dbg map get cilium_srv6_vrf_v4
kubectl -n kube-system exec cilium-rc6cd -- cilium-dbg map get cilium_srv6_sid
kubectl -n kube-system exec cilium-rc6cd -- cilium-dbg map get cilium_policy_01662

kubectl -n kube-system exec cilium-rc6cd -- cilium-dbg monitor --type trace -v
kubectl -n kube-system exec cilium-rc6cd -- cilium-dbg metrics list | grep srv6
```