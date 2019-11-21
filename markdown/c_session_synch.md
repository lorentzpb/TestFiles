# Sticky sessions

??11/18/2014. This topic rewritten because of D-81030 [Documentation] We support only sticky sessions (non-synchronized) in AAS clusters.

<madcap:variable name="axway_variables.Component Short Name"></madcap:variable> supports active-active clustering without session synchronization. Nodes do not share sessions. You must use <madcap:glossaryterm glossterm="clusters.Term1">sticky sessions</madcap:glossaryterm> to have the load balancer send you to the same node you logged on to originally. If that node fails, the load balancer sends you to the other node, where you have to log on again.

# Session synchronization

<madcap:variable name="axway_variables.Component Short Name"></madcap:variable> supports active-active clustering with or without session synchronization.

Session synchronization is when all nodes in a cluster share the JSESSIONID and synchronize session data. When you log on to one node, you also are logged on to the other node. In addition, your session is load balanced. As long as the session remains valid, any node in the cluster can serve subsequent requests on that session.

If you implement <madcap:glossaryterm glossterm="clusters.Term1">sticky sessions</madcap:glossaryterm>, the load balancer sends your session to the node you originally logged on to, unless it is off line. Normally, however, sticky sessions are not used with session synchronization. With session synchronization, if you log out of one node, you also are logged out of the other node.

 If you do not use session synchronization, nodes do not share sessions. You must use sticky sessions to have the load balancer send you to the same node. Otherwise, you would have to log on to each node. If that node fails, the load balancer would send you to the other node, where you would have to log on again.
<madcap:relationshipsproxy></madcap:relationshipsproxy>