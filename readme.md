sudo apt-get update
sudo apt-get upgrade -y
sudo apt-get install build-essential nano git -y
cd /opt/
sudo -s
## Gõ mật khẩu của user máy ubuntu vào (Nó sẽ không hiện ra gì đâu cứ gõ bình thường thôi)
git clone https:##github.com/kebe7jun/linux-kms-server
useradd -s /usr/sbin/nologin -r -M vlmcsd
cd /opt/linux-kms-server/vlmcsd/
make
nano /lib/systemd/system/vlmcsd.service
## Copy nội dung sau Paste vào
[Unit]
Description=vlmcsd KMS emulator service
After=network-online.target
Wants=network-online.target 
 
[Service]
Type=forking
User=vlmcsd
ExecStart=/opt/linux-kms-server/vlmcsd/vlmcsd -l /var/log/vlmcsd/vlmcsd.log 
 
[Install]
WantedBy=multi-user.target

mkdir /var/log/vlmcsd
chown vlmcsd:vlmcsd /var/log/vlmcsd
systemctl enable vlmcsd
systemctl start vlmcsd
systemctl status vlmcsd
ufw disable
ifconfig 
## Tìm dòng inet4 để lấy IP LAN của máy Ubuntu (Hoặc có thể set IP tĩnh trước - tuỳ)