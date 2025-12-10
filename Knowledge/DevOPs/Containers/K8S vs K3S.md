#kubernetes #k8s #k3s

# ✅ **Differences Between k3s and k8s—and Why You’d Use k3s**

Think of **Kubernetes (k8s)** as the _full-size, enterprise edition_…

…and **k3s** as the _lightweight, optimized edition for edge devices, home labs, IoT, laptops, and small servers_.

### ✔️ **k3s is a CNCF-certified Kubernetes distribution**

Meaning: it _is_ Kubernetes — passes conformance tests, APIs work the same, manifests are identical.

---

# 🆚 **k3s vs k8s Comparison**

| Feature                   | k8s (upstream)                                                                    | k3s                                                                |
| ------------------------- | --------------------------------------------------------------------------------- | ------------------------------------------------------------------ |
| **Binary size**           | ~1 GB+ total components                                                           | Single ~50–60 MB binary                                            |
| **Dependencies**          | etcd, kubelet, kubeadm, kube-controller, kube-proxy, container runtime, CNI, CSI… | **Everything bundled**, including container runtime, CNI, ingress  |
| **Default datastore**     | etcd required (heavy)                                                             | SQLite (default), can use etcd or MySQL if you want HA             |
| **Node resources needed** | High (4–8 GB RAM recommended)                                                     | Low (512 MB – 1 GB RAM nodes run fine)                             |
| **Use cases**             | Cloud, data centers                                                               | Edge, home labs, small servers, IoT                                |
| **Complexity**            | Higher                                                                            | Much simpler                                                       |
| **Server count for HA**   | Needs 3+ control-plane nodes                                                      | Can do HA with only 2 servers                                      |
| **Security**              | Good, but you configure                                                           | Hardened by default (SELinux, AppArmor, TLS auto-generation, etc.) |
| **Networking**            | 3rd-party CNI required                                                            | Flannel included by default                                        |
| **Package manager**       | Helm                                                                              | Helm (same)                                                        |