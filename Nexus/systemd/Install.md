sudo apt install bash-completion
sudo useradd -m -d  /home/nexus nexus -s /bin/bash
 su nexus
 sudo usermod -aG sudo nexus
sudo apt install openjdk-8-jre-headless
java -version
su root
cd /opt
wget https://download.sonatype.com/nexus/3/nexus-3.41.1-01-unix.tar.gz
tar -zxvf nexus-3.41.1-01-unix.tar.gz
sudo mv /opt/sonatype-work nexus-3.41.1-01/
sudo chown -R nexus:nexus /opt/sonatype-work/
sudo chown -R nexus:nexus /opt/nexus-3.41.1-01
-----------------------------------------------------------------------------
>>>>>>>>>>To run nexus as service at boot time, open /opt/nexus/bin/nexus.rc file, uncomment it and add nexus user as shown below
sudo nano /opt/nexus-3.41.1-01/bin/nexus.rc
run_as_user="nexus"
------------------------------------------------------------------------------
>>>>>>>> To Increase the nexus JVM heap size, open the /opt/nexus/bin/nexus.vmoptions file, you can modify the size as shown below
>>>>>>>> In the below settings, the directory is changed from ../sonatype-work to ./sonatype-work


vi /opt/nexus-3.41.1-01/bin/nexus.vmoptions



-Xms1024m
-Xmx1024m
-XX:MaxDirectMemorySize=1024m

-XX:LogFile=/opt/nexus-3.41.1-01/sonatype-work/nexus3/log/jvm.log
-XX:-OmitStackTraceInFastThrow
-Djava.net.preferIPv4Stack=true
-Dkaraf.home=.
-Dkaraf.base=.
-Dkaraf.etc=etc/karaf
-Djava.util.logging.config.file=/etc/karaf/java.util.logging.properties
-Dkaraf.data=/opt/nexus-3.41.1-01/sonatype-work/nexus3
-Dkaraf.log=/opt/nexus-3.41.1-01/sonatype-work/nexus3/log
-Djava.io.tmpdir=/opt/nexus-3.41.1-01/sonatype-work/nexus3/tmp
-------------------------------------------------------------------------
#4: Run Nexus as a service using Systemd
>>>>To run nexus as service using Systemd
sudo nano /etc/systemd/system/nexus.service
>>>>paste the below lines into it.

[Unit]
Description=nexus service
After=network.target

[Service]
Type=forking
LimitNOFILE=65536
ExecStart=/opt/nexus-3.41.1-01/bin/nexus start
ExecStop=/opt/nexus-3.41.1-01/bin/nexus stop
User=nexus
Restart=on-abort

[Install]
WantedBy=multi-user.target
----------------------------------------------------------------------------
>>>>To start nexus service using systemctl
sudo systemctl start nexus

>>>>To enable nexus service at system startup
sudo systemctl enable nexus

>>>>To check nexus service status
sudo systemctl status nexus

>>>>To stop Nexus service
sudo systemctl stop nexus

>>>>if the nexus service is not started, you can the nexus logs using below command
tail -f /opt/nexus-3.41.1-01/sonatype-work/nexus3/log/nexus.log
>>>>We have covered How to Install Nexus Repository on Ubuntu 20.04 LTS.
---------------------------------------------------------------------------
127.0.0.1:8081
-----------------------------------------------------------------
>>>To find default password run the below command
cat /opt/nexus-3.41.1-01/sonatype-work/nexus3/admin.password
----------------------------------------------------------------
