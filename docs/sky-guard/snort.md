---
sidebar_position: 2
---

# Snort 2.9.20

<div align="right">
  <a href="#tr">🇹🇷 Türkçe</a> | <a href="#en">English</a>
</div>

## <span id="tr">🇹🇷 Türkçe</span>

### Gereksinimler
- 32 MB RAM
- root access

### Kurulum

1. **Projeyi klonla:**
   ```sh
   git clone https://github.com/skylab-kulubu/SKYGuard.git
   ```
2. **User oluştur:**
   ```sh
   sudo useradd -m -s /bin/bash sky_guard && echo "sky_guard:<sifreniz>" | sudo chpasswd
   ```
   ```sh
   "id sky_guard" sonucundaki uid ve gid bilgilerini not edin
   ```
3. **İzinleri güncelle:**
   ```sh
   chmod +x snort/snort_setup.sh
   ```
4. **Ağ arayüzü ve HomeNet IP adresini öğren:**
   ```bash
   root@ubuntu:~# ip a
   2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    ...
    inet 192.168.1.0/24 metric 100 scope global dynamic eth0
    ...
   ```

   ```sh
   - ip a sonucundan dinlemek istediğiniz ağ arayüzünü seçiniz, eth0 örnek olarak verilmiştir
   - HOME_NET_IP="192.168.1.0/24"
   - NETWORK_INTERFACE="eth0"
   ```
5. **Snort kurulum:**
   ```sh
   - "nano snort/snort_setup.sh" ile variables kısmından WORK_DIR, LOG_DIR, HOME_NET_IP ve NETWORK_INTERFACE bilgilerini güncelle
   - ./snort/snort_setup.sh
   ```
6. **Snort çalıştırma:**
   ```sh
   - sudo systemctl daemon-reload
   - sudo systemctl enable snort
   - sudo systemctl start snort
   - sudo systemctl status snort --no-pager
   ```
   ```bash
   snort.service - Snort IDS Daemon
     Loaded: loaded (/etc/systemd/system/snort.service; enabled; preset: enabled)
     Active: active (running)
   ```
7. **Test ve Log görüntüleme:**
   ```sh
   - Canlı olarak log izlemek için "tail -F /var/log/snort/alert.fast"
   - Başka bir linux makinede snort_rule_test.sh dosyasını oluşturunuz
   - chmod +x snort_rule_test.sh
   - "./snort_rule_test.sh <TARGET_IP> [HTTP_PORT]"
   - "ICMP Detection Rule", "SSH Connection Attempt" ve "Command Execution Attempt" içerkli kayıtları görmeniz gerekiyor
   ```

## <span id="en">English</span>

### Requirements
- 32 MB RAM

### Installation

1. **Clone the project:**
   ```sh
   git clone https://github.com/skylab-kulubu/SKYGuard.git
   ```
2. **Create a user:**
   ```sh
   sudo useradd -m -s /bin/bash sky_guard && echo "sky_guard:<your_password>" | sudo chpasswd
   ```
   ```sh
   Then run: "id sky_guard" and note down the uid and gid values
   ```
3. **Update permissions:**
   ```sh
   chmod +x snort/snort_setup.sh
   ```
4. **Find network interface and HomeNet IP address:**
   ```bash
   root@ubuntu:~# ip a
   2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    ...
    inet 192.168.1.0/24 metric 100 scope global dynamic eth0
    ...
   ```

   ```sh
   - From the ip a output, select the network interface you want to monitor (eth0 is used as an example)
   - HOME_NET_IP="192.168.1.0/24"
   - NETWORK_INTERFACE="eth0"
   ```
5. **Install Snort:**
   ```sh
   - Open the setup file with "nano snort/snort_setup.sh" and update WORKDIR, HOME_NET_IP, and NETWORK_INTERFACE variables
   - ./snort/snort_setup.sh
   ```
6. **Run Snort:**
   ```sh
   - sudo systemctl daemon-reload
   - sudo systemctl enable snort
   - sudo systemctl start snort
   - sudo systemctl status snort --no-pager
   ```
   ```bash
   snort.service - Snort IDS Daemon
     Loaded: loaded (/etc/systemd/system/snort.service; enabled; preset: enabled)
     Active: active (running)
   ```
7. **Testing and viewing logs:**
   ```sh
   - Close your ssh session
   - ping -c 1 <server-ip> (use -n on Windows)
   - curl http://<server-ip>/etc/passwd
   - Reconnect with ssh
   - cat /var/log/snort/alert.csv
   - You should see entries containing "ICMP Detection Rule", "SSH Connection Attempt" and "Command Execution Attempt"
   ```
