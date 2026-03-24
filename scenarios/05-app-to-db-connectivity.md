# Scenario 05 - App to DB Connectivity

## Objective
Simulate an application failing to connect to a database due to firewall rules.

---

## Step 1 - On DB server (VM1), start listener

```bash
nc -l -p 5432
```

---

## Step 2 - Verify listener

```bash
ss -tulnp | grep 5432
```

Expected output:

<img width="772" height="51" alt="image" src="https://github.com/user-attachments/assets/db320f8c-0310-4f55-b82d-abf3410e5e19" />


---

## Step 3 - From app server (VM2), test connection

```bash
nc -vz -w 3 <DB_IP> 5432
```

Expected success:

<img width="527" height="48" alt="image" src="https://github.com/user-attachments/assets/e3d5ca74-8ea2-4eb5-bcbe-23a213b5c754" />


---

## Step 4 - Block port on DB server

```bash
sudo ufw deny 5432/tcp
```

---

## Step 5 - Test again from VM2

```bash
nc -vz -w 3 <DB_IP> 5432
```

Expected failure:

<img width="653" height="49" alt="image" src="https://github.com/user-attachments/assets/356ba7c6-25a7-402e-9f0b-148490b07736" />


---

## Step 6 - Fix firewall

```bash
sudo ufw allow 5432/tcp
```

---

## Step 7 - Verify fix

```bash
nc -vz -w 3 <DB_IP> 5432
```

Expected success again:

<img width="540" height="51" alt="image" src="https://github.com/user-attachments/assets/a50646f0-3004-4887-8802-675a6b27a6b4" />


---

## Key Takeaway

When connectivity fails, isolate the problem by checking:

- service state  
- listening ports  
- network reachability  
- firewall rules  
