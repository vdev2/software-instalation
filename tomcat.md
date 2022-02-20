--tomcat on ubuntu

sudo su -
apt-get update
apt-get install openjdk-8-jdk -y
apt-get update
mkdri cd/opt/tomcat/
cd /opt/tomcat/

--down load the tomcat from https://tomcat.apache.org/
--cpoy the  link of tarz file of that what version
wget https://dlcdn.apache.org/tomcat/tomcat-8/v8.5.75/bin/apache-tomcat-8.5.75.tar.gz
tax -xvzf <apache-tomcat-8.5.75.tar.gz>
mv <> tomcat
cd /tomcat/

chown R ubuntu:ubuntu tomcat

create link files for tomcat startup.sh and shutdown.sh
ln -s /opt/tomcat/bin/startup.sh /usr/bin/tomcatup
ln -s /opt/tomcat/bin/shutdown.sh /usr/bin/tomcatdown
tomcatup

--access from public ip  but wheh u click on weebapp manager or hostmanager error 403 to avoid 
find / -name context.xml

-- below files comment the value <!--   -->

/opt/tomcat/webapps/host-manager/META-INF/context.xml
/opt/tomcat/webapps/manager/META-INF/context.xml

find / -name tomcat-users.xml

--Update users information in the tomcat-users.xml file goto tomcat home directory and Add below users to conf/tomcat-users.xml file
 
<role rolename="manager-gui"/>
<role rolename="manager-script"/>
<role rolename="manager-jmx"/>
<role rolename="manager-status"/>
<user username="admin" password="admin" roles="manager-gui, manager-script, manager-jmx, manager-status"/>
<user username="deployer" password="deployer" roles="manager-script"/>
<user username="tomcat" password="s3cret" roles="manager-gui"/>

