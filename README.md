
Introduction
------------

Fail2Ban is a security tool that protects servers from brute-force attacks by automatically banning suspicious IPs. This guide walks through the installation, configuration, and testing of Fail2Ban.

Step 1: Connecting to the Server
--------------------------------

Connect to the remote server using SSH:

`   ssh root@45.79.38.118   `

Step 2: Installing Fail2Ban
---------------------------

Update the package list and install Fail2Ban:

`   sudo apt-get update  sudo apt-get install fail2ban   `

Step 3: Enabling the Fail2Ban Service
-------------------------------------

Enable Fail2Ban so that it starts automatically on boot:

`   sudo systemctl enable fail2ban.service   `

Step 4: Navigating to Fail2Ban Configuration Files
--------------------------------------------------

Fail2Ban stores configuration files in /etc/fail2ban/. To view and navigate:

`   ls -sl /etc/fail2ban/  cd /etc/fail2ban/   `

Step 5: Editing the Jail Configuration File
-------------------------------------------

Fail2Ban operates using 'jails' that define banning rules. Instead of modifying jail.conf, create a custom configuration file in jail.d/:

`   cd jail.d  ls  sudo vi defaults-debian.conf   `

Enable the SSH jail and define monitoring rules:

*   enabled = true
    
*   port = ssh
    
*   filter = sshd
    

Step 6: Restarting Fail2Ban to Apply Changes
--------------------------------------------

After modifying configurations, restart the Fail2Ban service:

`   sudo systemctl restart fail2ban   `

Step 7: Checking Fail2Ban Status
--------------------------------

Verify that Fail2Ban is running and protecting the server:

`   sudo fail2ban-client status  sudo fail2ban-client status sshd   `

Step 8: Testing Fail2Ban (Simulating an Attack)
-----------------------------------------------

Make incorrect SSH login attempts from another terminal:

`ssh testuser@server-ip`

`ssh anotheruser@server-ip`

`ssh randomuser@server-ip`

Fail2Ban should detect multiple failed attempts and ban the IP.

Step 9: Checking the Ban Status
-------------------------------

Confirm that the IP has been banned:

`   sudo fail2ban-client status sshd  sudo tail -n 50 /var/log/fail2ban.log   `

Step 10: Unbanning an IP
------------------------

To manually unban an IP:

`   sudo fail2ban-client set sshd unbanip <server-ip>  `

Conclusion
----------

Fail2Ban effectively protects servers by banning IPs with repeated authentication failures. This guide demonstrated how to install, configure, and test Fail2Ban for SSH security.

