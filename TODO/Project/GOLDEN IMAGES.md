#golden-images

# 🟩 **1. Flash Armbian 24.8.1**

I can give you the download link _once you tell me Bookworm vs Jammy_.

After flashing → boot → log in as the default user (`root` or `orangepi`, depends on image).

# 🟩 **2. Create your new permanent user**

This will be the user Ansible and k3s use (`keny` or whatever you choose).

```
sudo adduser keny && echo 'keny:Ojete123' | sudo chpasswd && sudo usermod -aG sudo keny

sudo hostnamectl set-hostname "oranxxx-goldenImage"

sudo passwd -l root

# Edit the SSH config file

sudo sed -i 's/^#PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config

sudo sed -i 's/^PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config

#LOG OFF -> LOG IN 'keny'

sudo loginctl kill-user orangepi
sudo loginctl terminate-user orangepi
ps -u orangepi
# nothing?
sudo usermod --expiredate 1 orangepi
sudo passwd -l orangepi


```


# 🟩 **3. Install your SSH public key** (SKIPPED, bootstrap does)

This ensures the golden image boots with automatic SSH access.

```
sudo mkdir -p /home/keny/.ssh
sudo chown -R keny:keny /home/keny/.ssh

sudo chmod 700 /home/keny/.ssh echo "YOUR_PUBLIC_KEY_HERE" | sudo tee /home/keny/.ssh/authorized_keys
sudo chmod 600 /home/keny/.ssh/authorized_keys
```

sudo deluser --remove-home orangepi


If user is `root` only:

- DO NOT delete root
    
- Just **lock it** (recommended):
    

`sudo passwd -l root`


# 🟩 **5. Freeze kernel to avoid breaking upgrades**

This prevents Armbian from updating into the broken vendor kernel (critical!):

```
sudo apt-mark hold linux-image-* linux-dtb-* linux-headers-*
```


# 🟩 **6. Install minimal dependencies (safe, universal)**

These packages are never harmful and help your bootstrap:

```
sudo apt update
sudo apt install -y curl wget git htop vim net-tools jq ca-certificates software-properties-common
```

Optional for your orchestrator:

```
sudo apt install -y python3 python3-venv python3-pip
```


# 🟩 **7. Enable Cgroups required for k3s**

Armbian 6.1 kernel already supports them, but ensure GRUB has the flags.

Confirm:

```
grep cgroup /proc/filesystems
```

You should see:

- `cgroup`
- `cgroup2`

If not (rare), add:

```
sudo sed -i 's/$/ cgroup_enable=cpuset cgroup_enable=memory cgroup_memory=1/' /boot/armbianEnv.txt
```

Then reboot.

# 🟩 **8. Make sure the image is “stateless”**

**Very important for a golden image:**

Clean host identifiers so clones don’t conflict:

```
sudo rm -f /etc/machine-id sudo systemd-machine-id-setup
```

Remove SSH host keys so each clone generates new ones:

```
sudo rm -f /etc/ssh/ssh_host_*
```

On first boot after cloning, SSH keys regenerate automatically.


# 🟩 **9. Final clean-up**

Before shutting down to image:

```
sudo apt autoremove --purge -y
sudo apt autoclean
sudo apt clean
```

Remove your shell history:

```
history -c sudo rm -f /root/.bash_history
sudo rm -f /home/keny/.bash_history
```



------



## EXTRA ARMBIAN IMAGE ISSUE

A particular image had a first boot script that would colapse if we cleaned up:

Resolved by:

```
sudo rm -f /etc/machine-id
sudo touch /etc/machine-id
ls -l /var/lib/dbus/machine-id
sudo ln -s /etc/machine-id /var/lib/dbus/machine-id

```


```
sudo tee /etc/systemd/system/regen-ssh-keys.service >/dev/null << 'EOF'
[Unit]
Description=Regenerate SSH host keys if missing
Before=ssh.service

[Service]
Type=oneshot
ExecStart=/usr/bin/ssh-keygen -A

[Install]
WantedBy=multi-user.target
EOF


sudo systemctl enable regen-ssh-keys.service


#OPTIONAL
sudo rm -f /var/log/*.gz /var/log/*-???????? /var/log/*.[0-9]
sudo journalctl --rotate
sudo journalctl --vacuum-time=1s
history -c

sudo rm -f /var/lib/dhcp/*.leases
sudo poweroff


```















___________

# Flash the golden image

# 🟦 **STEP 1 — Identify the Device**

On your Ubuntu workstation:

`lsblk`

Look for something like:

```
sdc 14.9G ├─sdc1 └─sdc2
```

# 🟦 **STEP 2 — Clone the Entire Disk Into an Image**

Use `dd`:

```
sudo dd if=/dev/sdc of=orangepi5pro-golden.img bs=4M status=progress
sync
```


# 🟦 **STEP 3 — Minimize and Compress**


	#### WARNING. Does not preserve original file


```
sudo chown keny:keny orangepi5pro-golden.img


sudo resize2fs -P orangepi5pro-golden.img

#resize2fs 1.47.0 (5-Feb-2023)
#Estimated minimum size of the filesystem: MIN_BLOCKS

sudo resize2fs orangepi5pro-golden.img MIN_BLOCKS

sudo truncate -s $((MIN_BLOCKS * 4096)) orangepi5pro-golden.img

```


OR

```
sudo pishrink orangepi5pro-golden.img
```


# 🟦 **STEP 4 — Compress for storage**

Use `dd`:

```
xz -z orangepi5pro-golden.img
sudo eject /dev/sda
```


## CAREFULL!!!

sudo parted /dev/loop0
(parted) print
(parted) resizepart 1 100%
(parted) quit

sudo e2fsck -f /dev/loop0p1
sudo resize2fs /dev/loop0p1