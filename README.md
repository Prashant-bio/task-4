# task-4
firewall

Ubuntu Firewall (UFW)
1. Update package index & install UFW:
   ```bash
   sudo apt update
   sudo apt install ufw -y
   ```
2. Check status:
   ```bash
   sudo ufw status verbose
   ```
3. Allow SSH first (important for remote systems):
   ```bash
   sudo ufw allow 22/tcp
   ```
4. Block Telnet (port 23):
   ```bash
   sudo ufw deny 23/tcp
   ```
5. Test locally with netcat:
   ```bash
   nc -l -p 2323      # listener terminal
   nc -vz localhost 2323   # tester terminal
   ```
6. Scan with nmap:
   ```bash
   nmap -p 23,2323 -Pn localhost
   ```
7. Remove the deny rule:
   ```bash
   sudo ufw status numbered
   sudo ufw delete <rule-number>
   ```

---

## 🔹 Kali Linux Firewall (UFW or iptables)

### Enable and configure UFW (recommended)
1. Install and enable:
   ```bash
   sudo apt update
   sudo apt install ufw -y
   sudo ufw allow 22/tcp
   sudo ufw enable
   ```
2. Block Telnet:
   ```bash
   sudo ufw deny 23/tcp
   ```
3. Test with nmap:
   ```bash
   nmap -p 23 -Pn localhost
   ```
4. Remove the deny rule:
   ```bash
   sudo ufw delete deny 23/tcp
   ```

### Alternative: iptables
1. Block port 23:
   ```bash
   sudo iptables -I INPUT -p tcp --dport 23 -j DROP
   ```
2. List rules:
   ```bash
   sudo iptables -L INPUT -n --line-numbers
   ```
3. Remove rule:
   ```bash
   sudo iptables -D INPUT <line-number>
   ```

---

## 🔹 Summary: How Firewalls Filter Traffic
- Firewalls inspect **network packets** based on **rules** (protocol, port, direction).  
- **Inbound rules** control traffic entering the system.  
- **Outbound rules** control traffic leaving the system.  
- If a packet matches a “block/deny” rule → it’s dropped or rejected.  
- If it matches an “allow” rule → it’s permitted.  
- Default policies apply if no rules match.  
- Example: Blocking Telnet (23) protects against an old, insecure protocol.

---
