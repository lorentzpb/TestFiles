# Clustering on Linux

??11/5/2013. Vivian advises that we not provide this level of detail as there are various ways to cluster and load balance. This topic is deprecated.

source:

https://sites.google.com/site/acmonboarding/the-projects/onboarding-toolkit/knowledge-base/steps-to-setup-active-active-cluster-with-session-synchronization-running-on-linux

Use this procedure to set up active-active clustering for <madcap:variable name="axway_variables.Component Short Name"></madcap:variable> on Linux without session synchronization.
<madcap:snippetblock src="../Resources/Snippets/clustering/cluster_assumption.flsnp"></madcap:snippetblock>

## Set up cluster

1.  Install MySQL 5.6.12 or later on the shared database server.
2.  Create a database for <madcap:variable name="axway_variables.Component Short Name"></madcap:variable>. Use the following commands to grant access to the application servers (the cluster nodes):
3.  <span class="code">Open MySQL Command Line Client</span><![CDATA[ ]]>
4.  <span class="code">create database <database name>;</span> (for example, <span class="code">axwaydb</span>) 
5.  <span class="code">show databases;</span><![CDATA[ ]]>
6.  The show command displays the list of databases. Make sure the database you created is listed. Then run the following command to grant database access to the application server:
7.  <span class="code">grant ALL on *.* to 'root'@'<IP address of the application server'> identified by '<database password>';</span><![CDATA[ ]]>
8.  You need to grant access to all application servers (all nodes in the cluster).
9.  Install <madcap:variable name="axway_variables.Component Short Name"></madcap:variable> on each application server.  Make sure to point to the database you created in an earlier step.
10.  Run the following commands to create the shared <span class="code">wflow</span> directory on the shared file system server.   

11.  1.  Go to the <span class="code">/opt</span> directory on the file system server:
    2.  <span class="code">cd /opt</span><![CDATA[ ]]>
    3.  Create the directory. For example:
    4.  <span class="code">mkdir toolkit</span><![CDATA[ ]]>
    5.  Change the directory:
    6.  <span class="code">cd /toolkit</span><![CDATA[ ]]>
    7.  Create a shared <span class="code">wflow</span> directory on the file system server by copying the <span class="code">wflow</span> directory from the application server. For example:
    8.  <span class="code">scp -r root@(application server ip) :/opt/<install directory>/wflow</span><![CDATA[ ]]>
    9.  Start the file system server if it is not running:
    10.  <span class="code">start nfs server</span><![CDATA[ ]]>
12.  Run the following commands to configure each application server to use the shared <span class="code">wflow</span> directory.

    1.  Go to the directory where <madcap:variable name="axway_variables.Component Short Name"></madcap:variable> is installed:
    2.  <span class="code">cd /opt/< path to installation directory></span><![CDATA[ ]]>
    3.  Remove the local <span class="code">wflow</span> directory:
    4.  <span class="code">rm -rf wflow</span><![CDATA[ ]]>
    5.  Change the directory:
    6.  <span class="code">cd /mnt</span><![CDATA[ ]]>
    7.  Create a directory under <span class="code">/mnt.</span> For example:
    8.  <span class="code">mkdir toolkit</span><![CDATA[ ]]>
    9.  Mount the external shared <span class="code">wflow</span> directory on each application server. For example:
    10.  <span class="code">mount -t nfs <IP address of the file system server>:/opt/<installation directory>j toolkit</span><![CDATA[ ]]>
    11.  Change the directory:
    12.  <span class="code">cd /opt/<install directory></span><![CDATA[ ]]>
    13.  Create a soft link to connect the shared <span class="code">wflow</span> directory:
    14.  <span class="code">ln -s /mnt/toolkit/wflow wflow</span><![CDATA[ ]]>
13.  Run the following commands on each application server to set up the Apache Tomcat cluster.

    1.  Go to the Tomcat directory on the application server. For example:
    2.  <span class="code">cd /opt/<install directory>/apache-tomcat-6.0.37/</span><![CDATA[ ]]>
    3.  Change the directory:
    4.  <span class="code">cd conf/</span><![CDATA[ ]]>
    5.  Edit the <span class="code">server.xml</span> file in the <span class="code">conf</span> directory. You need to edit the file on all application servers.
    6.  <span style="color: #ff0000;">??Please specify the properties to edit and what values to change or add in the  file.</span>

## Configure load balancer

You can rename the load balancer files if you want: <span class="code"> lb.conf</span> and <span class="code">lb-ssl.conf</span>. 

1.  Install the Apache web server  ([http://httpd.apache.org/](http://httpd.apache.org/))
2.  Purchase a server certificate or generate a self-sign certificate.
3.  Copy the server.<span class="code">cer</span> and server<span class="code">.key</span> files to the web server at:
4.  <span class="code"> /etc/apache2/vhost.d/</span><![CDATA[ ]]>
5.  Go to the directory where the web server is installed:
6.  <span class="code">cd /etc/apache2/vhost.d/</span><![CDATA[ ]]>
7.  Edit the <span class="code">lb.conf</span> file.
8.  <span style="color: #ff0000;">??Please specify the properties to edit and what values to change or add in the  file.</span>
9.  Edit the <span class="code">lb-ssl.conf</span> file.
10.  <span style="color: #ff0000;">??Please specify the properties to edit and what values to change or add in the  file.</span>
11.  Change the directory:
12.  <span class="code">cd/etc/apache2/</span><![CDATA[ ]]>
13.  Edit the <span class="code">listen.conf</span> file.
14.  <span style="color: #ff0000;">??Please specify the properties to edit and what values to change or add in the  file.</span>
15.  Change the directory:
16.  <span class="code">cd /etc/rc.d</span><![CDATA[ ]]>
17.  Start the load balancing service:
18.  <span class="code">run “./apache2 start”</span><![CDATA[ ]]>

If there is error starting the load balancer, check the <span class="code">error_log</span> at <span class="code">/var/log/apache2</span>.

To stop the load balancing service, go to <span class="code">” /etc/rc.d ”</span> and execute <span class="code">run “./apache2 stop”</span>.