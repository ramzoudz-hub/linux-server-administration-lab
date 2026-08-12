
Today I worked on several troubleshooting problems in my Linux server lab.

I tried not to just run random commands. I tried to think about what could be wrong and check the possible causes one by one.

---

# 1. The Website Was Not Working

The first problem I faced was that the website was not working while I was already inside the server.

The first thing I was thinking about was whether the process was still running, so I tried:

```bash
ps aux
````

I could also use `grep` with it if I wanted to find a specific process.

Then I checked the service with:

```bash
systemctl status <service-name>
```

If I was working on an older Linux system, I could also use:

```bash
service <service-name> status
```

I found that the service was dead.

If I didn't find the problem from the service status, I would check its logs with:

```bash
journalctl -u <service-name>
```

This helps me see the previous activity of the service and understand why it failed or stopped.

After fixing the service, I tested the application from inside the server using:

```bash
curl http://localhost
```

This helped me verify that the website was actually responding.

## My Troubleshooting Approach

```text
Check the process
       ↓
Check the service
       ↓
Check the logs
       ↓
Find the cause
       ↓
Fix the problem
       ↓
Test with curl
       ↓
Verify that it works
```

---

# 2. The Server Could Not Access the Internet

Another problem I faced was that the server itself was running, but it couldn't access the internet.

I didn't immediately assume that the problem was DNS.

First, I checked whether the server had an IP address:

```bash
ip addr
```

Then I checked the routing table:

```bash
ip route
```

I looked for the default gateway.

After finding the default gateway, I tested whether I could reach it:

```bash
ping <default-gateway-ip>
```

If I could reach the gateway, I knew that the local network connection was probably working.

Then I tested internet connectivity directly using an IP address:

```bash
ping 8.8.8.8
```

I did this before testing a domain name because I wanted to separate an internet connectivity problem from a DNS problem.

If `8.8.8.8` worked but something like:

```bash
ping google.com
```

didn't work, then DNS became a likely problem.

So I checked:

```bash
cat /etc/resolv.conf
```

and used:

```bash
dig google.com
```

or:

```bash
nslookup google.com
```

After checking the network and DNS configuration, I also checked the firewall:

```bash
sudo ufw status
```

I found that UFW was active, so I checked its rules:

```bash
sudo ufw status numbered
```

I found that one of the firewall rules was causing the problem.

I fixed the rule and tested the connection again.

## My Troubleshooting Approach

```text
Check IP address
       ↓
Check default route
       ↓
Ping the gateway
       ↓
Ping an external IP
       ↓
Check DNS
       ↓
Check firewall
       ↓
Find the blocking rule
       ↓
Fix it
       ↓
Test again
```

This taught me an important thing:

> Don't assume that every internet problem is a DNS problem.

I need to check the network step by step and use the results to narrow down the possible causes.

---

# 3. Setting Up SSH Public Key Authentication

I also worked on SSH access.

First, I installed and activated the SSH server and checked the service with:

```bash
sudo systemctl status ssh
```

Then I generated an SSH key pair using:

```bash
ssh-keygen -t ed25519
```

I used Ed25519 because it is a modern SSH key type.

Other key types also exist, such as RSA.

The command generated a private key and a public key.

The private key stays on my client machine, while the public key can be placed on the server.

I then copied my public key to the user I wanted to connect to:

```bash
ssh-copy-id support@<server-ip>
```

The public key was added to the user's:

```text
~/.ssh/authorized_keys
```

After that, I tested the connection:

```bash
ssh support@<server-ip>
```

This allowed me to authenticate using my SSH key instead of entering the account password every time.

## SSH Structure

```text
Client
 ├── Private key
 └── Public key
          │
          │
          ▼
       Server
          │
          └── ~/.ssh/authorized_keys
```

One important thing I learned is that SSH problems are not always caused by the password or the key itself.

They can also be caused by:

* Wrong username
* Wrong key
* Wrong permissions
* SSH configuration
* Wrong port
* Firewall rules
* SSH service problems
* Authentication errors in the logs

---

# 4. Service Troubleshooting

During the lab, I also practiced troubleshooting Linux services.

If I notice that an application or service is not working, I first check whether its process exists:

```bash
ps aux
```

Then I check the service:

```bash
systemctl status <service-name>
```

If the service is stopped or failed, I investigate the logs:

```bash
journalctl -u <service-name>
```

The logs can help me understand what happened before the service stopped.

Depending on the problem, the cause could be:

* Configuration error
* Permission problem
* Port conflict
* Missing dependency
* Missing file
* Application crash
* Incorrect service configuration

Instead of immediately restarting the service, I try to understand why it stopped.

---

# 5. My Troubleshooting Method

The biggest thing I learned from these labs was not a specific command.

It was how to approach a problem.

Instead of immediately changing things, I try to ask:

1. What exactly is failing?
2. What could cause it?
3. How can I test each possibility?
4. What does the result tell me?
5. Can I fix the actual root cause?
6. How can I verify that the problem is solved?

My basic troubleshooting process is:

```text
Problem
   ↓
Gather information
   ↓
Check possible causes
   ↓
Test
   ↓
Find the root cause
   ↓
Fix
   ↓
Verify
```

---

# 6. Commands I Practiced

## Processes

```bash
ps aux
```

## Services

```bash
systemctl status <service-name>
systemctl start <service-name>
systemctl stop <service-name>
systemctl restart <service-name>
```

For older systems:

```bash
service <service-name> status
```

## Logs

```bash
journalctl -u <service-name>
```

## Networking

```bash
ip addr
ip route
ping <gateway-ip>
ping 8.8.8.8
```

## DNS

```bash
cat /etc/resolv.conf
dig google.com
nslookup google.com
```

## Firewall

```bash
sudo ufw status
sudo ufw status numbered
```

## SSH

```bash
sudo systemctl status ssh
ssh-keygen -t ed25519
ssh-copy-id support@<server-ip>
ssh support@<server-ip>
```

---

# What I Learned

These labs helped me understand Linux administration more practically instead of just memorizing commands.

I learned that troubleshooting is about understanding the system and using evidence to narrow down the possible causes.

The main idea I want to keep improving is:

**Don't guess. Investigate, test, fix, and verify.**
