# LugaNodesTask4
Soham Pal (20BCB0003) - Task 4 - Firewalld Configuration

## Task 4: Firewall Setup and Configuration

### Features:

Install and set up firewalld using nftables on a linux virtual machine.
Use trusted-zone, internal-zone, and public-zone.

### Resources:

Manpage to firewalld

### Deliverables:

Documentation: Must include thorough documentation of each step. (Github Link)
Video Demonstration: Demonstrate the working of firewalld, its configuration process and an explanation of each step. (Video Link)

## Solution:

Firewall Setup and Configuration using Firewalld with nftables on Kali Linux
This process will walk you through the process of installing and configuring Firewalld with nftables on a Kali Linux virtual machine. Firewalld is a firewall management tool that provides a dynamic way to manage firewall rules. Nftables is the packet filtering framework used by Firewalld.

## Step 1: Install Firewalld

Open a terminal in your Kali Linux virtual machine.
Update the package list to ensure you have the latest version of packages:

```
sudo apt update
```

### Install Firewalld using the package manager:

``` sudo apt install firewalld ```

## Step 2: Start and Enable Firewalld

### Start the Firewalld service:

``` sudo systemctl start firewalld```

### Enable Firewalld to start on boot:

``` sudo systemctl enable firewalld ```

## Step 3: Understanding Firewalld Zones

Firewalld uses zones to group interfaces and services with specific trust levels. The default zones are public, trusted, home, internal, and work. In this, we will use trusted for trusted interfaces, internal for internal (private) network interfaces, and public for public-facing network interfaces.

## Step 4: Configure Firewalld Zones

### List available zones to check if the default zones are present:

``` sudo firewall-cmd --get-zones ```

### If the default zones are not available, create them:

```sudo firewall-cmd --permanent --new-zone=trusted```
```sudo firewall-cmd --permanent --new-zone=internal```
```sudo firewall-cmd --permanent --new-zone=public```

### Assign interfaces to each zone. 

```sudo firewall-cmd --permanent --zone=trusted --add-interface=eth1```
```sudo firewall-cmd --permanent --zone=internal --add-interface=eth2```
```sudo firewall-cmd --permanent --zone=public --add-interface=eth0```

### Set the trust level for each zone. For example, set the trusted zone to the highest trust level:


```sudo firewall-cmd --permanent --zone=trusted --set-target=ACCEPT```
```sudo firewall-cmd --permanent --zone=internal --set-target=DROP```
```sudo firewall-cmd --permanent --zone=public --set-target=DROP```

### In this configuration, the trusted zone allows all traffic, the internal zone only allows traffic from the trusted zone, and the public zone only allows traffic related to established connections (outgoing traffic).

### Reload Firewalld to apply the changes:

```sudo firewall-cmd --reload```

## Step 5: Configure Services

### Check available services:

```sudo firewall-cmd --get-services```

### Add services to the trusted and internal zones as needed. For example, to allow SSH access only from the trusted zone:

```sudo firewall-cmd --permanent --zone=trusted --add-service=ssh```

### Reload Firewalld to apply the service changes:

```sudo firewall-cmd --reload```

## Step 6: Verify Configuration

### Check the active zones and their interfaces:

```sudo firewall-cmd --get-active-zones```

### Verify the rules in each zone:

```sudo firewall-cmd --list-all-zones```

Test the firewall rules to ensure they are working as intended.

We have successfully installed and configured Firewalld with nftables on your Kali Linux virtual machine. Ensure you review the configuration and rules to meet your specific security requirements. 
