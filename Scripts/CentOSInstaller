# CentOS install and setup script

errorUser(){
	
	echo -e "\e[31mEnter a username\e[0m"
}

# If no argument supplied, throw error.
[[ $# -eq 0 ]] && errorUser

# OS Updates
yum -y update

# Create user
adduser $1

# Set default text editor to Nano
cat <<EOF >>/etc/profile.d/nano.sh
export VISUAL="nano"
export EDITOR="nano"
EOF

# Install git
yum -y install git

# Install Python
yum -y install Python

# Enable EPEL Repo: http://www.tecmint.com/how-to-enable-epel-repository-for-rhel-centos-6-5/
wget http://download.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
rpm -ivh epel-release-6-8.noarch.rpm