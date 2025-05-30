# UFW Firewall Configuration on Kali Linux

## Objective

This guide details how to configure a firewall on Kali Linux using UFW (Uncomplicated Firewall). It includes installation, rule management, traffic filtering, and verification steps.

---

## Step 1: Install UFW

Update your package list and install UFW:

```bash
sudo apt update
sudo apt install ufw
```

If GPG key errors occur during update, resolve them by importing the missing key using official Kali instructions.

---

## Step 2: Allow SSH (Port 22)

To avoid being locked out if you're connected via SSH:

```bash
sudo ufw allow 22
```

---

## Step 3: Enable UFW

Enable the firewall:

```bash
sudo ufw enable
```

Check the firewall status:

```bash
sudo ufw status verbose
```

---

## Step 4: List Current Firewall Rules

View the current rules with numbers for future reference:

```bash
sudo ufw status numbered
```

---

## Step 5: Block Inbound Traffic on Port 23 (Telnet)

To block Telnet port 23:

```bash
sudo ufw deny 23
```

Verify the rule:

```bash
sudo ufw status numbered
```

---

## Step 6: Test the Rule

Install Telnet if not available:

```bash
sudo apt install telnet
```

Test the port block:

```bash
telnet localhost 23
```

Expected output:

```
telnet: Unable to connect to remote host: Connection refused
```

This indicates that port 23 is successfully blocked by the firewall.

---

## Step 7: Re-allow SSH (Port 22)

To ensure continued SSH access:

```bash
sudo ufw allow 22
```

---

## Step 8: Remove the Block Rule on Port 23

List rules with their numbers:

```bash
sudo ufw status numbered
```

Remove the block rule using its number (replace 1 with the actual number):

```bash
sudo ufw delete 1
```

Confirm removal:

```bash
sudo ufw status
```

---

## How Firewall Filters Traffic

UFW simplifies the configuration of iptables and filters traffic based on:

* **Port Filtering**: Allows or denies traffic to specific ports (e.g., 22 for SSH, 23 for Telnet)
* **Direction Control**: Separates rules for incoming and outgoing traffic
* **Protocol Filtering**: Supports both TCP and UDP

**Default UFW Policies:**

* Deny all incoming traffic
* Allow all outgoing traffic

These features allow secure control over network access and reduce attack surfaces.

---

## Summary of Commands Used

```bash
sudo apt update
sudo apt install ufw
sudo ufw allow 22
sudo ufw enable
sudo ufw status verbose
sudo ufw status numbered
sudo ufw deny 23
sudo apt install telnet
telnet localhost 23
sudo ufw allow 22
sudo ufw delete 1
sudo ufw status
```

---

## Conclusion

This task demonstrated:

* Installing and enabling UFW
* Allowing and verifying SSH access
* Blocking and testing access to Telnet
* Managing firewall rules with clarity
* Understanding how Linux firewalls handle network traffic


