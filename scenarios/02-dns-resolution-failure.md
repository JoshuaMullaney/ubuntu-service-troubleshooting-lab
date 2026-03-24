# Scenario 02 - DNS Resolution Failure

## Objective
Simulate a system where IP connectivity works but DNS fails.

---

## Step 1 - Verify baseline

```bash
ip addr
ip route
resolvectl status
ping -c 3 8.8.8.8
ping -c 3 google.com
```

<img width="830" height="812" alt="image" src="https://github.com/user-attachments/assets/9028304b-1b34-461d-9bcf-33b3b330d3e5" />

---

## Step 2 - Break DNS

```bash
sudo resolvectl dns enp0s3 1.2.3.4
```

---

## Step 3 - Confirm DNS change

```bash
resolvectl status
```

<img width="651" height="193" alt="image" src="https://github.com/user-attachments/assets/f2558a67-82a4-4870-85b4-ab9c9f8580ef" />

---

## Step 4 - Test connectivity

```bash
ping -c 3 8.8.8.8
ping -c 3 google.com
curl -I https://google.com
```

<img width="523" height="232" alt="image" src="https://github.com/user-attachments/assets/9c8e9003-6cda-4523-b4f7-b2c152ac608a" />

---

## Expected Result

- ping 8.8.8.8 works
- ping google.com fails
- curl shows "Could not resolve host"

---

## Step 5 - Fix DNS

```bash
sudo resolvectl dns enp0s3 192.168.1.1
```

---

## Step 6 - Verify fix

```bash
ping -c 3 google.com
curl -I https://google.com
```
<img width="1256" height="415" alt="image" src="https://github.com/user-attachments/assets/6be6ae07-95f7-4824-98f0-545232d08e7f" />

---

## Key Takeaway

If IP connectivity works but hostname fails, DNS is the issue.
