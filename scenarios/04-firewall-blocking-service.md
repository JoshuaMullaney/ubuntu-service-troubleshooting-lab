# Scenario 04 - Firewall Blocking Service

## Objective
Show how firewall rules can block access even when a service is healthy.

---

## Step 1 - Start web service

```bash
python3 -m http.server 8080 --bind 0.0.0.0
```

---

## Step 2 - Enable firewall

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow ssh
sudo ufw enable
```

<img width="644" height="209" alt="image" src="https://github.com/user-attachments/assets/10f16073-b9d6-430c-8601-15fb4727471d" />

---

## Step 3 - Verify firewall

```bash
sudo ufw status verbose
```

Expected output (example):

<img width="546" height="191" alt="image" src="https://github.com/user-attachments/assets/42034e8d-5415-431a-b3d2-bc0fa98b7755" />


---

## Step 4 - Test locally

```bash
curl http://localhost:8080
```
<img width="589" height="574" alt="image" src="https://github.com/user-attachments/assets/ace57272-b171-40d6-bdd7-a81035f1dfec" />

---

## Step 5 - Test from second VM

```bash
curl http://<SERVER_IP>:8080
```

---

## Expected Result

- local → works  
- remote → fails  

<img width="826" height="60" alt="image" src="https://github.com/user-attachments/assets/f5180d19-d31c-49f3-b881-fe3232410588" />

---

## Step 6 - Fix firewall

```bash
sudo ufw allow 8080/tcp
```

---

## Step 7 - Verify fix

```bash
sudo ufw status
```
<img width="493" height="171" alt="image" src="https://github.com/user-attachments/assets/94e5412c-64ef-4239-991f-1d3923d7c1b5" />

Then test again from second VM:

```bash
curl http://<SERVER_IP>:8080
```
<img width="611" height="579" alt="image" src="https://github.com/user-attachments/assets/c8c2de31-ec84-4d9b-8383-dcb151b0a827" />

---

## Key Takeaway

Local success does not guarantee external access. Always test from another host.
