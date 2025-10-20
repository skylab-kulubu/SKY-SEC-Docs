---
sidebar_position: 3
---

# n8n

<div align="right">
  <a href="#tr">🇹🇷 Türkçe</a> | <a href="#en">English</a>
</div>

## <span id="tr">🇹🇷 Türkçe</span>

### Gereksinimler
- 250 MB RAM
- `n8n.<alan-adınız>.<uzantınız>` için SSL ve DNS ayarları

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
3. **Klasöre girin:**
   ```sh
   cd n8n
   ```
4. **Docker ağı oluşturun:**
   ```sh
   docker network create your_network_name
   ```

   ```text
   Bu ağın nginx için kullanılan ağ ile aynı olması gerekmektedir.
   ```

5. **Ortam değişkenlerini ayarlayın:**
   ```sh
   nano .env ile DOMAIN_NAME, GENERIC_TIMEZONE ve SSL_EMAIL bilgilerini güncelleyiniz.
   ```

6. **docker-compose.yml dosyasını güncelleyin:**
   ```sh
   nano docker-compose.yml
   ```

   ```text
   - User id bilgisini güncelleyin
   user: "1000:1000" -->  user: "uid:uid" ???????
   
   - Group id bilgisini güncelleyin 
   group_add:
      - gid
   
   - Log yollarını güncelleyin:
   Kullanmayacağınız tool'ların yolunu silebilirsiniz.
   volumes:
      - n8n_data:/home/node/.n8n
      - ./local-files:/files
      - /home/backend/ossec/alerts.log:/var/ossec/logs/alerts.log:ro
	  - /var/log/snort/alert.csv:/var/snort/logs/alert.csv:ro
      - /home/backend/sky_guard_logs:/data/snort_logs

   - Network bilgisini güncelleyin:
   networks:
     your_network_name:
       external: true
   ```

7. **n8n çalıştırma:**
   ```sh
   docker compose up --build -d
   ```

8. **Test:**
   ```sh
   n8n.<alan-adınız>.<uzantınız> adresine gittiğinizde n8n ekranı ile karşılaşmanız gerekmektedir.
   ```

### Snort Bildirim Sistemi Kurma

1. **:**
   ```sh
   
   ```

### Ossec Bildirim Sistemi Kurma

1. **:**
   ```sh
   
   ```

## <span id="en">English</span>

### Requirements
- 250 MB RAM
- SSL and DNS configuration for `n8n.<your-domain-name>.<tld>`

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
   
3. **Enter the folder:**
   ```sh
   cd n8n
   ```

4. **Create a Docker network:**
   ```sh
   docker network create your_network_name
   ```

   ```text
   This network must be the same as the one used for Nginx.
   ```

5. **Set environment variables:**
   ```sh
   nano .env ile DOMAIN_NAME, GENERIC_TIMEZONE ve SSL_EMAIL bilgilerini güncelleyiniz.
   ```

6. **Update the docker-compose.yml file:**
   ```sh
   nano docker-compose.yml
   ```

   ```text
   - Update log paths:
   You can remove paths for tools you won't use.
   volumes:
     - n8n_data:/home/node/.n8n
     - ./local-files:/files
     - /home/backend/ossec/alerts.log:/var/ossec/logs/alerts.log:ro
  
   - Update network information:
   networks:
    your_network_name:
      external: true
   ```

7. **Run n8n:**
   ```sh
   docker compose up --build -d
   ```

8. **Test:**
   ```sh
   You should see the n8n interface when you visit n8n.<your_domain_name>.<tld>
   ```
