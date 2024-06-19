## Install Clickhouse on Ubuntu

### 1. Update system

```
sudo apt update
sudo apt upgrade
```

### 2. Add Clickhouse repo

```
sudo apt install -y apt-transport-https ca-certificates dirmngr
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv E0C56BD4
echo "deb https://repo.clickhouse.com/deb/stable/ main/" | sudo tee /etc/apt/sources.list.d/clickhouse.list
sudo apt update
```

### 3. Install Clickhouse

```
sudo apt install -y clickhouse-server clickhouse-client
```

### 4. Run Clickhouse 

```
sudo clickhouse start
```

### 5. Connection to Clickhouse

```clickhouse-client```