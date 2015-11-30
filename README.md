# Technologies Used
* [Ansible](http://www.ansible.com/)
* [Docker](https://www.docker.com/)
* [Vagrant](https://www.vagrantup.com/)
* [Jenkins](https://jenkins-ci.org/)
* [Nginx](https://www.nginx.com/resources/wiki/)


# Languages Used
* Bash
* Python

# Projects

**Docker Deployer**

Create scripts using Ansible and Bash to set up two Docker containers inside of a Vagrant VM. One container will contain a Jenkins installation. The second will run a nginx proxy to access Jenkins on the appropriate port. The Jenkins CLI port must be accessible from outside of the Docker containers. Afterwards, I will install a job that compiles a multi-tier application (Curl is a good candidate) using Jenkins, programatically, with a scripting library. Backup restore will not count. Then it must execute the newly compiled command.

1. Deploy Vagrant VM
2. Create two Docker Containers within Vagrant VM
3. Install Jenkins on VM#1
4. Install Nginx Proxy on VM#2
5. Configure Jenkins port information for Jenkins.
6. Validate Nginx proxy functionality. 
7. Validate Jenkins CLI port accessbility from external to Docker containers.
8. Create job to build multi-tier app; e.g. Curl

**[Linux Sysadmin Stuff?](https://www.reddit.com/r/linuxadmin/comments/2s924h/how_did_you_get_your_start/cnnw1ma)**


1. Set up a KVM hypervisor.  
2. Inside of that KVM hypervisor, install a Spacewalk server. Use CentOS 6 as the distro for all work below. (For bonus points, set up errata importation on the CentOS channels, so you can properly see security update advisory information.)      
3. Create a VM to provide named and dhcpd service to your entire environment. Set up the dhcp daemon to use the Spacewalk server as the pxeboot machine (thus allowing you to use Cobbler to do unattended OS installs).  Make sure that every forward zone you create has a reverse zone associated with it. Use something like "internal.virtnet" (but *not* ".local") as your internal DNS zone.  
4. Use that Spacewalk server to automatically (without touching it) install a new pair of OS instances, with which you will then create a Master/Master pair of LDAP servers.  Make sure they register with the Spacewalk server. Do *not* allow anonymous bind, do *not* use unencrypted LDAP.  
5. Reconfigure all 3 servers to use LDAP authentication.    
6. Create two new VMs, again unattendedly, which will then be Postgresql VMs. Use pgpool-II to set up master/master replication between them.  Export the database from your Spacewalk server and import it into the new pgsql cluster.  Reconfigure your Spacewalk instance to run off of that server.    
7. Set up a Puppet Master.  Plug it into the Spacewalk server for identifying the inventory it will need to work with.  (Cheat and use ansible for deployment purposes, again plugging into the Spacewalk server.)    
8. Deploy another VM. Install iscsitgt and nfs-kernel-server on it. Export a LUN and an NFS share.  
9. Deploy another VM. Install bakula on it, using the postgresql cluster to store its database.  Register each machine on it, storing to flatfile. Store the bakula VM's image on the iscsi LUN, and every other machine on the NFS share.  
10. Deploy two more VMs. These will have httpd (Apache2) on them. Leave essentially default for now.  
11. Deploy two *more* VMs. These will have tomcat on them. Use JBoss Cache to replicate the session caches between them. Use the httpd servers as the frontends for this.  The application you will run is [JBoss Wiki](http://jbosswiki.jboss.org/).  
12. You guessed right, deploy another VM. This will do iptables-based NAT/round-robin loadbalancing between the two httpd servers.   
13. Deploy another VM.  On this VM, install postfix. Set it up to use a gmail account to allow you to have it send emails, and receive messages only from your internal network.  
14. Deploy another VM.  On this VM, set up a Nagios server. Have it use snmp to monitor the communication state of every relevant service involved above. This means doing a "is the right port open" check, *and* a "I got the right kind of response" check *and* "We still have filesystem space free" check.  
15. Deploy another VM.  On this VM, set up a syslog daemon to listen to every other server's input. Reconfigure each other server to send their logging output to various files *on the syslog server*.  (For extra credit, set up logstash or kibana or greylog to parse those logs.)  
16. Document every last step you did in getting to this point in your brand new Wiki.  
17. Now go back and create Puppet Manifests to ensure that every last one of these machines is authenticating to the LDAP servers, registered to the Spacewalk server, and backed up by the bakula server.  
18. Now go back, reference your documents, and set up a Puppet Razor profile that hooks into each of these things to allow you to recreate, from scratch, each individual server.  
19. Destroy every secondary machine you've created and use the above profile to recreate them, joining them to the clusters as needed.  
20. Bonus exercise: create three more VMs. A CentOS 5, 6, and 7 machine.  On *each* of these machines, set them up to allow you to create custom RPMs and import them into the Spacewalk server instance. Ensure your Puppet configurations work for all three and produce like-for-like behaviors.