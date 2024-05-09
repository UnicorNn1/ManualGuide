# <h1 align="center">Avail Light Node Setup</h1>
![image](https://github.com/Unicorn1807/ManualGuide/assets/82544940/dd8c3ae7-6eb8-4a89-801e-a1ee5f4606e8)


## Links:
 * [Avail Official Website](https://www.availproject.org/)
 * [Avail Official Twitter](https://twitter.com/AvailProject)
 * [Avail Official Discord](https://discord.gg/kkHAXZCNZa)
 * [Avail Light Node Documentation](https://docs.availproject.org/operate/node/light-client/)
 * [Avail Light Node Form](https://docs.google.com/forms/d/e/1FAIpQLSeL6aXqz6vBbYEgD1cZKaQ4vwbN2o3Rxys-wKTuKySVR-oS8g/viewform)

### System Requirements
| System | Minimum Requirements | 
| ------------ | ------------ |
| ✔️CPU |	2+ vCPU|
| ✔️RAM	| 4+ GB |
| ✔️Storage	| 40+ GB SSD |
| ✔️UBUNTU | 22 |
## Update
```
sudo apt update && sudo apt upgrade -y
sudo apt-get install make clang pkg-config libssl-dev build-essential
```
```
screen -S alight
```
### Install Avail Light Client
```
cd
wget https://github.com/availproject/avail-light/releases/download/v1.7.8/avail-light-linux-amd64.tar.gz
tar -xvzf avail-light-linux-amd64.tar.gz
mv avail-light-linux-amd64 avail-light
rm -rf avail-light-linux-amd64.tar.gz
```



#### Let's create the service file
```
sudo tee /etc/systemd/system/availd.service > /dev/null <<EOF
[Unit]
Description=Avail Light Client
After=network.target
StartLimitIntervalSec=0
[Service]
User=root
ExecStart=/root/avail-light --network goldberg
Restart=always
RestartSec=120
[Install]
WantedBy=multi-user.target
EOF
```

#### Let's start
```
sudo systemctl daemon-reload
systemctl enable availd
sudo systemctl restart availd
```

## Logs
```
journalctl -u availd -fo cat
```

#### Final block display
```
curl "http://localhost:7000/v1/latest_block"
```
