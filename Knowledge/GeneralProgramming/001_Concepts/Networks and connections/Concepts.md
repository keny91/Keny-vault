#networks #connections 

## 🔍 4. **Terms Recap**

| Term           | What it Means                                                                |
| -------------- | ---------------------------------------------------------------------------- |
| **IP address** | Unique number for a device on your network (`192.168.0.34`)                  |
| **Subnet**     | A block of IPs, in this case `192.168.0.0/24` means `.0` to `.255`           |
| **Netmask**    | Defines how big your subnet is (`255.255.255.0` = 256 addresses)             |
| **Gateway**    | The router — used to talk to the internet or outside subnets (`192.168.0.1`) |
| **Interface**  | The network card (`eth0`, `wlan0`, `wlp2s0`)                                 |
| **DNS**        | Resolves names like `keny-linux.ts.net` to IPs                               |
| **DHCP**       | Auto-assigns IPs. You’ve disabled this in favor of static IPs for stability  |
| **Static IP**  | Manually assigned, does not change on reboot                                 |
| **Tailscale**  | Creates a VPN between your devices using a separate (private) IP block       |


Example:

Here's a diagram to visualize your current home setup:

          [ Internet ]
               |
         [ Your Router ]
         (192.168.0.1/24)
               |
     -------------------------
     |            |           |
 [Laptop]   [RPi Orchestrator] [RPi Worker]
  (0.25)        (0.34)             (TBD)
   wlp2s0       eth0              eth0
     |            |                 |
     +-----> Local SSH, Ansible Control
     +-----> Optional DNS or Tailscale access

- Subnet: 192.168.0.0/24
- Netmask: 255.255.255.0
- Gateway: 192.168.0.1 (router)

