<!DOCTYPE html>
<html>

<body>

  <h1>Syslog Messages to Azure Sentinel with HA and Keepalived (HighAvailability-LoadBalancing)</h1>

  <h2>Overview</h2>

  <p>I have implemented a robust solution using <strong>HAProxy</strong> and <strong>Keepalived</strong> to ensure high availability for my syslog-ng servers. This setup enables seamless log transmission from my on-premises environment to Azure. <strong>HAProxy</strong> takes care of load balancing, while <strong>Keepalived</strong> ensures failover mechanisms, providing a resilient and reliable syslog infrastructure.</p>

  <p>You have 2 scenarios for this deployment, I've draw for you to make it easier 🙂</p> 
  
 ![image](https://github.com/t0neex/Syslog-messages-to-Azure-Sentinel-w-HA-and-Keepalived-Disaster-Cluster-LoadBalancing-/assets/100233276/cc807632-7025-4cf6-b34f-2aa820f05aa3)

  <h2>Installation</h2>

  <h3>1. HAProxy Installation</h3>

  <p>Follow the instructions for your distribution <a href="https://haproxy.debian.net">here</a>.</p>

  <h3>2. Keepalived Installation</h3>

  <p>Follow the instructions for your distribution <a href="https://keepalived.readthedocs.io/en/latest/installing_keepalived.html#installing-from-the-repositories">here</a>.</p>

  <h2>High-Level Configuration Steps</h2>

  <h3>HAProxy Configuration</h3>

  <p>Modify the global settings by changing the value of "log" to <strong>tcp</strong> and set "option" as <strong>tcplog</strong>. Replace the IP addresses of syslog_server1 and syslog_server2 with your syslog servers' IP addresses. Repeat these steps on your second HAProxy server, ensuring consistency between the two servers.</p>

  <img src="https://github.com/t0neex/Syslog-messages-to-Azure-Sentinel-w-HA-and-Keepalived-Disaster-Cluster-LoadBalancing-/assets/100233276/b53c2fdf-6c81-4d28-8110-5d83a6a5b822" alt="HAProxy Configuration">

  <h3>Keepalived Configuration</h3>

  <p>Specify your Ethernet interface (e.g., enp0s3) and set one Keepalived server as <strong>MASTER</strong> and others as <strong>BACKUP</strong>. In case of a system problem, the BACKUP server(s) will take over the MASTER role. Ensure the consistency of the virtual IP and replace real server IP addresses accordingly.</p>

  <img src="https://github.com/t0neex/Syslog-messages-to-Azure-Sentinel-w-HA-and-Keepalived-Disaster-Cluster-LoadBalancing-/assets/100233276/518d13d2-21d3-48f1-84bd-8487789a300a" alt="Keepalived Configuration">

  <h3>Syslog-ng Configuration</h3>

  <p>Define the log file name and enter your HAProxy/Keepalived servers' IP addresses in the syslog-ng configuration file.</p>

  <img src="https://github.com/t0neex/Syslog-messages-to-Azure-Sentinel-w-HA-and-Keepalived-Disaster-Cluster-LoadBalancing-/assets/100233276/b343b469-13b0-40b3-bfd0-eda34935a520" alt="Syslog-ng Configuration">

<br><br><br>
🥳<p>That's all! Just send your syslog messages to the Virtual IP of the Keepalived servers, and you will see the messages in the log file on the syslog servers. After you create your custom table at Azure Log Analytics you'll see the messages in a few minutes!</p>🥳

  <p>Feel free to reach out if you have any questions or need further clarification!</p>

</body>

</html>
