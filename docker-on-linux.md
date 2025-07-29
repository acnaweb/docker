
# **Instalação do Docker no Linux (Ubuntu/WSL)**

## **1. Objetivo**
Instalar e configurar o Docker Engine em um ambiente Linux (Ubuntu), incluindo suporte ao WSL (Windows Subsystem for Linux), garantindo que o usuário possa executar containers sem privilégios de `root`.

---

## **2. Pré-requisitos**
- Sistema Linux (Ubuntu) ou WSL 2 instalado.
- Permissão de `sudo` para execução dos comandos.
- Conexão com a internet para baixar pacotes.

---

## **3. Passo a Passo**

### **3.1 Atualizar os repositórios do sistema**
```bash
sudo apt-get update
```

### **3.2 Instalar pacotes necessários**
```bash
sudo apt-get install ca-certificates curl
```

### **3.3 Adicionar a chave GPG oficial do Docker**
```bash
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

### **3.4 Adicionar o repositório oficial do Docker**
```bash
echo   "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu   $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" |   sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
```

### **3.5 Instalar Docker Engine e Plugins**
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### **3.6 Testar instalação**
```bash
sudo docker run hello-world
```

---

## **4. Configuração Pós-instalação**

### **4.1 Adicionar usuário ao grupo docker**
```bash
sudo groupadd docker   # Cria o grupo docker (se não existir)
sudo usermod -aG docker $USER
newgrp docker
```

### **4.2 Testar sem sudo**
```bash
docker run hello-world
```

---

## **5. Extras e Dicas**
- **Verificar versão:**
  ```bash
  docker --version
  docker compose version
  ```
- **Habilitar Docker no boot (Linux):**
  ```bash
  sudo systemctl enable docker
  sudo systemctl start docker
  ```
- **No WSL:** 
  - Certifique-se de usar **WSL 2**:
    ```powershell
    wsl --set-default-version 2
    ```
  - Instale o **Docker Desktop** no Windows para integração ou siga este tutorial apenas no WSL.

---

## **6. Solução de Problemas**
- **Erro: Cannot connect to the Docker daemon**  
  Execute:
  ```bash
  sudo service docker start
  ```
- **Erro de permissão:**  
  Certifique-se que reiniciou a sessão após adicionar ao grupo `docker`.

---

✅ **Instalação concluída!**
