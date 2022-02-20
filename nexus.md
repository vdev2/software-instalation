>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>nexus on ubuntu >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

https://kifarunix.com/install-nexus-repository-manager-on-ubuntu/

sudo su -
apt update
apt install openjdk-8-jdk
java -version
useradd -M -d /opt/nexus -s /bin/bash -r nexus
echo "nexus   ALL=(ALL)       NOPASSWD: ALL" > /etc/sudoers.d/nexus
mkdir /opt/nexus
cd /opt/nexus
wget https://sonatype-download.global.ssl.fastly.net/repository/downloads-prod-group/3/nexus-3.29.2-02-unix.tar.gz

tar -xvzf nexus-3.29.2-02-unix.tar.gz -C /opt/nexus --strip-components=1

chown -R nexus: /opt/nexus
vi /opt/nexus/bin/nexus.vmoption

-Xms1024m
-Xmx1024m
-XX:MaxDirectMemorySize=1024m


sed -i 's/#run_as_user=""/run_as_user="nexus"/' /opt/nexus/bin/nexus.rc


Therefore, edit the /opt/nexus/bin/nexus.vmoptions and adjust the path of the Nexus directory (in the below settings, the directory is changed from ../sonatype-work to ./sonatype-work).

vim /opt/nexus/bin/nexus.vmoptions

sudo -u nexus /opt/nexus/bin/nexus start
tail -f /opt/nexus/sonatype-work/nexus3/log/nexus.log
netstat -altnp | grep :8081

cat > /etc/systemd/system/nexus.service << 'EOL'
[Unit]
Description=nexus service
After=network.target

[Service]
Type=forking
LimitNOFILE=65536
ExecStart=/opt/nexus/bin/nexus start
ExecStop=/opt/nexus/bin/nexus stop
User=nexus
Restart=on-abort

[Install]
WantedBy=multi-user.target
EOL

/opt/nexus/bin/nexus stop

systemctl daemon-reload
systemctl enable --now nexus.service

systemctl status nexus


tail -f /opt/nexus/sonatype-work/nexus3/log/nexus.log



If UFW is running, you need to open port 8081 to allow external access.

ufw allow 8081/tcp

You can now access Nexus repository from browser using the address http://server-IP-or-resolvable-hostname:8081.

>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>nexus on ubuntu >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
