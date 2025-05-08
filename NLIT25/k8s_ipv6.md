# Kubernetes in IPv6 only Networks - Are we there yet? 

- Provide connectivity to applications --> to end users, and between microservices
- Need DNS64/NAT64, ip6tables, IPv6 address planning for cluster nodes
- IPv6 capable load balancer or BGP enabled router
- Uses Cilium as the CNI to move away from iptables
- Separate backplane and IPv6 net (for external connections)
