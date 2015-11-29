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