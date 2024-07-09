## How to Set Up SSH Keys on Ubuntu

### 1. Create user 

```
sudo adduser user
sudo usermod -aG sudo user
```

### 2. Disable root login

```
sudo nano /etc/ssh/sshd_config
change PermitRootLogin yes to PermitRootLogin no
sudo systemctl restart ssh
```

### 3. Create SSH key

```
ssh-keygen -t rsa -b 4096
```

### 4. Copy local key to server

```
ssh-copy-id user@111.222.333
```

### 5. Disable password login

```
sudo nano /etc/ssh/sshd_config
```

Set

```
PubkeyAuthentication yes
PasswordAuthentication no
```

Restart SSH

```
sudo systemctl restart ssh
```