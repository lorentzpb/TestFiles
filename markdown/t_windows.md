# Clustering on Windows

??11/5/2013. Vivian advises that we not provide this level of detail as there are various ways to cluster and load balance. This topic is deprecated.

source

https://sites.google.com/site/acmonboarding/the-projects/onboarding-toolkit/knowledge-base/steps-to-setup-active-active-cluster-with-session-synchronization-running-on-windows

Use this procedure to set up active-active clustering for <madcap:variable name="axway_variables.Component Short Name"></madcap:variable> on Windows with session synchronization.
<madcap:snippetblock src="../Resources/Snippets/clustering/cluster_assumption.flsnp"></madcap:snippetblock>

## Set up cluster

1.  Install MySQL 5.6.12 or later on the shared database server.
2.  Create a database for <madcap:variable name="axway_variables.Component Short Name"></madcap:variable>. Use the following commands to grant access to the application servers (the cluster nodes):
3.  <span class="code">Open MySQL Command Line Client</span><![CDATA[ ]]>
4.  <span class="code">create database <database name>;</span> (for example, <span class="code">axwaydb</span>)
5.  <span class="code">show databases;</span><![CDATA[ ]]>
6.  The show command displays the list of databases. Make sure the database you created is listed. Then run the following command to grant database access to the application server:
7.  <span class="code">grant ALL on *.* to 'root'@'<IP address of the application server>' identified by '<database password>';</span><![CDATA[ ]]>
8.  You need to grant access to all application servers (all nodes in the cluster).
9.  Install all components of <madcap:variable name="axway_variables.Component Short Name"></madcap:variable> on application server 1. Make sure to point to the database created in the earlier step.
10.  Install <madcap:variable name="axway_variables.Component Short Name"></madcap:variable> on application server 2 and any additional servers. Uncheck the Wflow and DB components when installing on server 2 and any additional servers.
11.  Do the following to create the shared <span class="code">wflow</span> directory on the shared file system server.

    1.  Create a directory on the shared file system server. For example, you can name it <span class="code">onboarding-toolkit</span>.
    2.  Copy the <span class="code">wflow</span> directory on application server 1 to the <span class="code">onboarding-toolkit</span> directory.
    3.  Share the directory to give access to the application servers.
12.  Configure each application server to use the shared <span class="code">wflow</span> directory.

    1.  Delete the local <span class="code">wflow</span> directory
    2.  Map network drive to point to the shared <span class="code">wflow</span> directory.
    3.  Edit the <span class="code">joget-start.bat</span> file to use the shared wflow directory.
    4.  <span style="color: #ff0000;">??Please specify the properties to edit and what values to change or add in the  file.</span>

## Configure load balancer

Perform the following steps for each application server.

1.  Edit the <span class="code">server.xml</span> file in <span class="code"><install directory>\apache-tomcat-6.0.37\conf</span>.
2.  <span style="color: #ff0000;">??Please specify the properties to edit and what values to change or add in the  file.</span>
3.  Edit the <span class="code">web.xml</span> file at <span class="code"><install directory>\apache-tomcat-6.0.37\webapps\jw\WEB-INF</span>.
4.  At the end of the file, just before <span class="code"></web-app></span>, insert the following line:
5.  <span class="code"><distributable /></span><![CDATA[ ]]>