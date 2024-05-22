## Commands To Setup:

```shell
##################----INSTALL TOMCAT----##################

cd /opt
sudo wget https://archive.apache.org/dist/tomcat/tomcat-9/v9.0.65/bin/apache-tomcat-9.0.65.tar.gz
sudo tar -xvf apache-tomcat-9.0.65.tar.gz

# Configure tomcat-users.xml
sudo tee -a /opt/apache-tomcat-9.0.65/conf/tomcat-users.xml > /dev/null <<EOF
<user username="admin" password="admin1234" roles="admin-gui, manager-gui"/>
EOF

# Create symbolic links for startTomcat and stopTomcat commands
sudo ln -s /opt/apache-tomcat-9.0.65/bin/startup.sh /usr/bin/startTomcat
sudo ln -s /opt/apache-tomcat-9.0.65/bin/shutdown.sh /usr/bin/stopTomcat

# Configure manager and host-manager context.xml
sudo sed -i 's|<Valve className="org.apache.catalina.valves.RemoteAddrValve"|<!-- <Valve className="org.apache.catalina.valves.RemoteAddrValve"|g' /opt/apache-tomcat-9.0.65/webapps/manager/META-INF/context.xml
sudo sed -i 's|<Valve className="org.apache.catalina.valves.RemoteAddrValve"|<!-- <Valve className="org.apache.catalina.valves.RemoteAddrValve"|g' /opt/apache-tomcat-9.0.65/webapps/host-manager/META-INF/context.xml


sudo chmod -R 757 apache-tomcat-9.0.65

# Stop and start Tomcat
sudo stopTomcat
sudo startTomcat

```
#### After copying the Artifact in webapps folder we can see the deployed application
```
sudo cp target/*.war /opt/apache-tomcat-9.0.65/webapps
```
