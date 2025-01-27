# Secure-Server

### Update the Server
```
apt update && apt upgrade -y
```

### Install Reqired PKGs using APT
```
apt install nano curl ufw fail2ban python3-systemd -y
```

### Setup Firewall
```
ufw default deny incoming && ufw default allow outgoing && ufw allow ssh && ufw enable && ufw status
```

### Create the Jail.local File
```
nano /etc/fail2ban/jail.local
```

### Content for Jail.local File
```
[DEFAULT]
bantime = 30m
findtime = 20m
maxretry = 1
bantime.increment = true
allowipv6 = true
banaction = ufw

[sshd]
enabled = true
backend = systemd

[other-jail]
enabled = false
```

### Restart Fail2ban
```
systemctl restart fail2ban && systemctl status fail2ban
```

### (Optional) Install Docker
```
curl -fsSL https://get.docker.com -o get-docker.sh && chmod +x get-docker.sh && ./get-docker.sh
```

### (Optional) Install casaos, this will install all the stuff
```
curl -fsSL https://get.casaos.io | bash
```

### Limit Docker Log Size by Creating daemon.json
```
nano /etc/docker/daemon.json
```

### Stuff to write in daemon.json
```
{
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "10m",
    "max-file": "2"
  }
}
```

### Restart Docker
```
systemctl restart docker
```
