>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>jenkins on ubuntu >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

sudo su -
sudo apt-get update
sudo apt-get install opendjdk-8-jdk -y
java --version
find / -name java-11*
----need to down load the jenkins packages
-- to install jenkins

wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'

sudo apt-get update
apt install jenkins
systemctl start jenkins
systemctl status jenkins

apt-get install maven  -y

mvn -v

--chek the publicip:8080 
--set admin paswd




>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>jenkins on ubuntu >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
