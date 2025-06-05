# ID-7-Monitor-Sys-Resources-Using-Netdata

# ✅ Task 7 - Monitor System Resources Using Netdata

## 🧠 Objective

In this task, I have installed and configured **Netdata** on my **Ubuntu droplet** using **Docker** to monitor real-time system and application performance metrics like CPU, memory, disk usage, and running containers.

---

## 🛠 Tools Used

* Ubuntu 22.04 DigitalOcean Droplet
* Docker
* Netdata (Docker container)

---

## 🔧 Steps I Have Performed

### 1. Updated the System

I began by updating and upgrading my system packages to ensure everything is current.

```bash
sudo apt update && sudo apt upgrade -y
```

---

### 2. Installed Docker

I installed Docker by adding its official repository and dependencies.

```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io -y

sudo systemctl start docker
sudo systemctl enable docker

docker --version
```

---

### 3. Ran the Netdata Container

I ran the Netdata container using the full command below, which ensures it can access system-level data like `/proc`, `/sys`, and `/etc/passwd`.

```bash
sudo docker run -d --name=netdata -p 19999:19999 \
  --cap-add SYS_PTRACE \
  --security-opt apparmor=unconfined \
  -v netdataconfig:/etc/netdata \
  -v netdatalib:/var/lib/netdata \
  -v netdatacache:/var/cache/netdata \
  -v /etc/passwd:/host/etc/passwd:ro \
  -v /etc/group:/host/etc/group:ro \
  -v /proc:/host/proc:ro \
  -v /sys:/host/sys:ro \
  -v /etc/os-release:/host/etc/os-release:ro \
  netdata/netdata
```

---

### 4. Accessed the Netdata Dashboard

After running the container, I accessed the Netdata dashboard by visiting:

```
http://<my-droplet-ip>:19999
```

To find my public IP, I ran:

```bash
curl ifconfig.me
```

---

### 5. Captured Screenshot

Once I confirmed the dashboard was working and displaying live system metrics, I took a screenshot of the dashboard to include in this repository.

---

## 📁 Files in this Repository

* `README.md` – Task explanation and steps
* `Screenshot_-------.png` – Screenshot of the Netdata dashboard
* `ScreenRecording_____.mp4` - Screenrecording of the Netdata dashboard

---

## 🔺 Conclusion

By completing this task, I have learned how to:

* Install Docker
* Run a containerized monitoring tool
* Visualize system metrics in real-time
* Understand key metrics like CPU usage, memory consumption, and disk I/O

This setup provides a lightweight, powerful monitoring solution for any Linux-based server.
