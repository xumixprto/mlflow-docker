# MLflow Server with Nginx Proxy

This repository contains the necessary files to set up and run an MLflow server using Docker Compose. The setup uses Nginx as a reverse proxy to redirect traffic from port 80 to the MLflow server running on port 5000.

---

## Prerequisites

1. **A Newly Created Virtual Machine (VM)**:
   - Ensure the VM is accessible and has administrative privileges.
   - Update the system packages before proceeding.

2. **Docker and Docker Compose**:
   - These are required to run the MLflow server and Nginx services.

3. **Nginx** (Optional):
   - If Nginx is not included in the Docker setup, it can be installed manually.

---

## Setup Instructions

### 1. Install Required Software

#### Update the System
```bash
sudo apt update && sudo apt upgrade -y
```

#### Install Docker
```bash
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
sudo add-apt-repository "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
sudo apt install -y docker-ce
```

#### Install Docker Compose
```bash
sudo curl -L "https://github.com/docker/compose/releases/download/$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep tag_name | cut -d '"' -f 4)/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

#### Verify Installation
```bash
docker --version
docker-compose --version
```

#### (Optional) Install Nginx
If Nginx needs to be installed separately:
```bash
sudo apt install -y nginx
```

---

### 2. Clone the Repository

SSH into your VM and clone this repository:
```bash
git clone <repository-url>
cd <repository-name>
```

---

### 3. Run Docker Compose

Start the MLflow server and Nginx services:
```bash
docker-compose up -d
```

This command will:
1. Launch the MLflow server on port 5000.
2. Set up the Nginx reverse proxy to redirect traffic from port 80 to port 5000.

---

### 4. Access the MLflow Server

- Open your browser and navigate to:
  - **http://<your-vm-ip>** (or **http://<your-domain>** if using a domain name).

You should see the MLflow interface.

---

## Managing the Services

- **Stop the services**:
  ```bash
  docker-compose down
  ```
- **View logs**:
  ```bash
  docker-compose logs -f
  ```
- **Restart services**:
  ```bash
  docker-compose restart
  ```

---

## Troubleshooting

1. **Port Conflicts**:
   - Ensure no other services are using ports 80 or 5000 on your VM.

2. **Nginx Errors**:
   - Check the Nginx logs:
     ```bash
     docker logs <nginx-container-name>
     ```

3. **MLflow Errors**:
   - Check the MLflow server logs:
     ```bash
     docker logs <mlflow-container-name>
     ```

---

## Customization

- To persist MLflow artifacts or metadata, modify the `docker-compose.yaml` to include volume mounts for the MLflow service.
- Update the `nginx.conf` file for advanced configurations such as load balancing or caching.

---

## References

- [MLflow Documentation](https://www.mlflow.org/docs/latest/index.html)
- [Nginx Documentation](https://nginx.org/en/docs/)
- [Docker Compose Documentation](https://docs.docker.com/compose/)