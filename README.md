# IB Gateway Docker for Theseus

This repository provides a **Dockerized setup** for running **Interactive Brokers Gateway** with **IBC (IB Controller)**, customized for **Theseus**.

## 🚀 Setup Instructions

### **1️⃣ Choose the Build Context**
In `docker-compose.yml`, the **context** specifies which directory is being built:

```yaml
context: ./latest  # or ./stable
```
By default, this setup is configured to use `./latest`.

---

### **2️⃣ Download Required Files**
You must manually download the required **IB Controller (IBC)** and **IB Gateway** files and place them in the appropriate directory (`./latest/` or `./stable/`).

🔹 **Download IBC** from:  
➡ [IBC Releases](https://github.com/IbcAlpha/IBC/releases)  
Place the downloaded `.zip` file in `./latest/` or `./stable/`.

🔹 **Download IB Gateway** from:  
➡ [IB Gateway Latest Version](https://www.interactivebrokers.com/en/trading/ibgateway-latest.php)  
Place the `.sh` installer in `./latest/` or `./stable/`.

---

### **3️⃣ Ensure Correct Version Variables**
In the `Dockerfile`, these environment variables must match the versions of **IBC** and **IB Gateway** that you downloaded:

```dockerfile
ENV IB_GATEWAY_VERSION=10.34.1c
ENV IB_GATEWAY_RELEASE_CHANNEL=latest
ENV IBC_VERSION=3.21.1 
```

Ensure that both occurrences of `IBC_VERSION` are updated correctly.

**Create** `.env`, and configure IB login details:

```env
TWS_USERID='' # required
TWS_PASSWORD='' # required
TWS_SETTINGS_PATH=
TWS_ACCEPT_INCOMING=
TRADING_MODE=paper # required
READ_ONLY_API=no
VNC_SERVER_PASSWORD=
TWOFA_TIMEOUT_ACTION=restart
TWOFA_DEVICE=
BYPASS_WARNING=
AUTO_RESTART_TIME=11:59 PM
AUTO_LOGOFF_TIME=
TWS_COLD_RESTART=
SAVE_TWS_SETTINGS=
RELOGIN_AFTER_TWOFA_TIMEOUT=yes
EXISTING_SESSION_DETECTED_ACTION=primary
ALLOW_BLIND_TRADING=no
TIME_ZONE=Europe/Zurich
CUSTOM_CONFIG=
SSH_TUNNEL=
SSH_OPTIONS=
SSH_ALIVE_INTERVAL=
SSH_ALIVE_COUNT=
SSH_PASSPHRASE=
SSH_REMOTE_PORT=
SSH_USER_TUNNEL=
SSH_RESTART=
SSH_VNC_PORT=
```

---

### **4️⃣ Build and Run the Container**

#### **🔨 Build the Image**
```sh
DOCKER_DEFAULT_PLATFORM=linux/amd64 docker-compose up --build
```

#### **▶️ Run the Container**
```sh
DOCKER_DEFAULT_PLATFORM=linux/amd64 docker-compose up
```

If you see an error saying the image cannot be found, check available images:
```sh
docker images
```

You can then manually run the correct image:
```sh
docker run <IMAGE_ID>
```

---

### **✅ Summary**
1. **Set the correct build context** (`latest/` or `stable/` in `docker-compose.yml`).
2. **Download and place** the required files in the correct directory.
3. **Update the Dockerfile** to match your downloaded versions of **IB Gateway** and **IBC**.
4. **Build and run** the container using the commands above.

Now you're ready to run IB Gateway inside Docker! 🚀

