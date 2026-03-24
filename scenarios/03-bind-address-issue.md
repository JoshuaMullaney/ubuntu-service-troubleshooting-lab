# Scenario 03 - Bind Address Issue

## Objective
Show how a service can be running but not reachable externally.

---

## Step 1 - Start service bound to localhost

```bash
python3 -m http.server 8080 --bind 127.0.0.1
```
<img width="576" height="51" alt="image" src="https://github.com/user-attachments/assets/9da42a17-0955-48a6-8117-f8d64bddc0a3" />

---

## Step 2 - Verify listening port

```bash
ss -tulnp | grep 8080
```

Expected output (example):

```text
127.0.0.1:8080
```
<img width="805" height="90" alt="image" src="https://github.com/user-attachments/assets/905a47d3-1f06-420f-95f2-61da8b355e5b" />

---

## Step 3 - Test access

```bash
curl http://localhost:8080
curl 192.168.1.159:8080
```

---

## Expected Result

- localhost → works  
- host IP → fails  

Example failure:

<img width="770" height="594" alt="image" src="https://github.com/user-attachments/assets/3e445bb4-7732-438d-bdda-748c29df6e10" />


---

## Step 4 - Fix bind address

Stop server (Ctrl+C), then run:

```bash
python3 -m http.server 8080 --bind 0.0.0.0
```

---

## Step 5 - Verify fix

```bash
ss -tulnp | grep 8080
curl http://$(hostname -I | awk '{print $1}'):8080
```

Expected output:

<img width="814" height="607" alt="image" src="https://github.com/user-attachments/assets/3a87338b-d3d5-491a-bfe2-df3b21712383" />


---

## Key Takeaway

A service bound to 127.0.0.1 is not reachable externally.
