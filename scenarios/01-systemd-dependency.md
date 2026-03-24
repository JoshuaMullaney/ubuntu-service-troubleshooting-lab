# Scenario 01 - systemd Dependency Behavior

## Objective
Create two services where one depends on the other and observe how systemd handles stopping the dependency.

---

## Step 1 - Create directories

sudo mkdir -p /opt/testApp /opt/testDB

---

## Step 2 - Create DB script

<img width="570" height="113" alt="image" src="https://github.com/user-attachments/assets/ab8c5f52-4f6f-48f8-b368-7e2274187919" />



---

## Step 3 - Create App script via nano command:

<img width="564" height="136" alt="image" src="https://github.com/user-attachments/assets/f3f288f5-3651-4caf-9a2d-52a3b6b1994f" />


---

## Step 4 - Create DB service via nano command

<img width="489" height="244" alt="image" src="https://github.com/user-attachments/assets/d5e317eb-aeb1-4a60-a0ac-c61e869ed6a1" />


---

## Step 5 - Create App service (depends on DB) via nano command

<img width="488" height="253" alt="image" src="https://github.com/user-attachments/assets/b1a7c2a5-6c07-4845-b64a-69108f312e76" />


---

## Step 6 - Reload and start services

<img width="644" height="57" alt="image" src="https://github.com/user-attachments/assets/b0f65c4a-ed8f-460c-bce0-0556494e4434" />


---

## Step 7 - Verify both are running

<img width="685" height="430" alt="image" src="https://github.com/user-attachments/assets/cf96ca77-7d2f-4d34-bd3c-90edf67724ac" />


---

## Step 8 - Stop DB (simulate failure)

<img width="557" height="17" alt="image" src="https://github.com/user-attachments/assets/3eb0f06c-5313-4f55-8e9d-42174f87035e" />

---

## Step 9 - Observe result

systemctl status testApp
journalctl -u testApp -n 20

<img width="1004" height="388" alt="image" src="https://github.com/user-attachments/assets/9432521d-4d3f-4559-b89e-c1a48f313322" />

---

## Expected Result

- testApp stops automatically
- logs show SIGTERM (systemd stopped it)

---

## Key Takeaway

systemd enforces dependencies, but only after reloading and restarting services.

<img width="689" height="231" alt="image" src="https://github.com/user-attachments/assets/6f54e7f3-fa76-4afb-8faa-b8b0491fd8f0" />
