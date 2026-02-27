# SSH Tips

##  Problem

SSH is a powerful tool but most developers use only its most basic feature — remote login. You're typing passwords every time, or struggling with tunneling.

##  Solution

Master SSH config, key-based authentication, and tunneling to make remote work fast and secure.

##  Example

### SSH Key Authentication
```bash
# Generate an SSH key pair (Ed25519 — modern and secure)
ssh-keygen -t ed25519 -C "your.email@example.com"
# → Creates ~/.ssh/id_ed25519 (private) and ~/.ssh/id_ed25519.pub (public)

# Copy public key to server (enable passwordless login)
ssh-copy-id user@server.com
# or manually:
cat ~/.ssh/id_ed25519.pub | ssh user@server.com "cat >> ~/.ssh/authorized_keys"

# Now login without password:
ssh user@server.com
```

### SSH Config File (~/.ssh/config)
```
# Instead of: ssh -i ~/.ssh/id_ed25519 -p 2222 user@192.168.1.100 -L 8080:localhost:3000
# Configure once, use everywhere:

Host myserver
    HostName 192.168.1.100
    User     ubuntu
    Port     2222
    IdentityFile ~/.ssh/id_ed25519

Host production
    HostName prod.example.com
    User     deploy
    IdentityFile ~/.ssh/prod_key
    ServerAliveInterval 60    # keep alive

Host bastion
    HostName bastion.example.com
    User     ec2-user
    IdentityFile ~/.ssh/aws_key.pem

# Jump through bastion to reach private server:
Host private-server
    HostName 10.0.1.50
    User     ubuntu
    ProxyJump bastion
```

```bash
# Now simply:
ssh myserver
ssh production
ssh private-server  # automatically jumps through bastion!
```

### Port Forwarding / Tunneling
```bash
# LOCAL tunnel: forward local port → remote
# Access remote DB (port 5432) as if it's localhost:5433
ssh -L 5433:localhost:5432 user@server.com
# → psql -h localhost -p 5433

# REMOTE tunnel: expose local service on remote server
ssh -R 8080:localhost:3000 user@server.com
# → People on server can access your local :3000 via :8080

# Dynamic SOCKS proxy (use server as proxy)
ssh -D 1080 user@server.com
# → Configure browser to use SOCKS5 localhost:1080

# Run command without interactive shell
ssh user@server.com "df -h && free -m"
```

##  Explanation

### Security Best Practices
- Use Ed25519 keys (stronger, shorter than RSA)
- Set `PasswordAuthentication no` in `/etc/ssh/sshd_config`
- Use `fail2ban` to block brute force
- Keep SSH port non-standard for reduced bot traffic

##  Related Tips

- [Process Management](process-management.md)
- [Customizing Prompt](customizing-prompt.md)

---

[← Back to Terminal Tips](README.md)
