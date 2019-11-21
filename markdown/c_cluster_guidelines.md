# Clustering guidelines

There are various ways to set up clustering and load balancing. Refer to the third-party user documentation for the methods you want to implement. However, the following are points to keep in mind when setting up <madcap:variable name="axway_variables.Component Short Name"></madcap:variable> in an active-active cluster.

*   Make sure <madcap:variable name="axway_variables.Component Short Name"></madcap:variable> servers (all nodes) have full access to the shared database.
*   12/16/2015. Jagan: This needs to be removed since sharing shared secret is encrypted with version 1.4 and should not be shared and same according to PSG guidelines. Use the same shared secret on all nodes.
*   Configure  <madcap:variable name="axway_variables.Component Short Name"></madcap:variable> servers to use a shared file system. Depending on how the shared file system is set up, you might have to edit the `setenv.sh` script in the installation directory to point to the correct location. The shared file system normally shares the <span class="code">wflow</span> directory and the  `appstudio-keystore` and `appstudio-truststore` files found in each node's installation directory.
*   Make sure all <madcap:variable name="axway_variables.Component Short Name"></madcap:variable> servers have read-write access to the shared file system. Edit `setenv.sh` and configure `Dsecure.config.file` variable to the absolute path of the shared secret key as follows:
*   `-Dsecure.config.file=<user-home dir>/.appStudio/.appstudio/`
*   For example: `-Dsecure.config.file=/home/axway/.appStudio/.appstudio/;` where `axway` is the user installed <madcap:variable name="axway_variables.Component Short Name"></madcap:variable>.
*   Do not use URLs in the format `https://<node IP_address>/appstudio/<other content>`. Such URLs cannot be relied upon to redirect to the load balancer.
*   Edit the `server.xml` file at `<install directory>\apache-tomcat-<version>\conf` to point to the load balancer or proxy or firewall so traffic is routed correctly.
*   Edit the `server.xml` file to have identical values on all cluster nodes for the following properties:

    *   `keystoreFile` is the absolute path of the keystore
    *   `keystorePass` is the keystore password
*   Edit the `repair.sh` and `recover.sh` scripts in `<install directory>/cli-tools/` to replace the string:

 -DappStudioData=$AppStudioDataDir

 With:

-DappStudioData=<user-home dir>/.appStudio

*   Where `<user-home dir>` is the path of the user's home directory in Linux.<madcap:relationshipsproxy></madcap:relationshipsproxy>