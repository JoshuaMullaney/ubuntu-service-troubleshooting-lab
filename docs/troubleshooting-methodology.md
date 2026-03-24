# Troubleshooting Methodology

The main habit I wanted to build in this lab was to troubleshoot in layers instead of jumping straight to a fix.

## My general approach

### 1. Confirm the symptom
First I verify that the problem is real and reproducible.

Examples:
- service cannot be reached
- hostname does not resolve
- remote host cannot connect to a port

### 2. Identify what still works
I try to narrow the scope as quickly as possible.

Examples:
- IP connectivity works, but DNS fails
- localhost works, but host IP fails
- service is listening, but remote access fails

### 3. Check the layer most likely involved
Some examples from this lab:

- service state: `systemctl`, `journalctl`
- sockets and ports: `ss -tulnp`
- routing and addressing: `ip addr`, `ip route`
- DNS: `resolvectl`
- reachability: `ping`, `curl`, `nc`
- host firewall: `ufw status`

### 4. Apply one fix at a time
I try not to make multiple changes at once. That makes it easier to verify what actually resolved the issue.

### 5. Validate from the right place
One of the most useful lessons in this lab was that local tests are not always enough. A service may work on localhost and still fail for remote clients. In those cases, testing from a second VM gives a clearer answer.
