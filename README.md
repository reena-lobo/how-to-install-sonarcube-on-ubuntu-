** How to Install SonarQube on Ubuntu 20.04 LTS.**
**SonarQube is an opensource web based tool to manage code quality and code analysis. 
It is most widely used in continuous code inspection which performs reviews of code to detect bugs, code smells and vulnerability issues of programming languages such as PHP, C#, JavaScript, C/C++ and Java .
Also tracks statistics and creates charts that enable developers to quickly identify problems in their code.**

**Prerequisites**
Ubuntu 20.04 LTS with minimum 2GB RAM and 1 CPU.
PostgreSQL Version 9.3 or higher
SSH access with sudo privileges
Firewall Port: 9000

**Increase the vm.max_map_count kernal ,file discriptor and ulimit for current session at runtime.**
 sudo sysctl -w vm.max_map_count=262144
 sudo sysctl -w fs.file-max=65536
ulimit -n 65536
ulimit -u 4096

***To Increase the vm.max_map_count kernal ,file discriptor and ulimit permanently . Open the below config file and Insert the below value as shown below****

sudo nano /etc/security/limits.conf
sonarqube   -   nofile   65536
sonarqube   -   nproc    4096
****update and upgrade System Packages****
sudo apt-get update
 sudo apt-get upgrade

Install wget and unzip package
sudo apt-get install wget unzip -y

Step 1: Install OpenJDK
Install OpenJDK and JRE 11 using following command,
 sudo apt-get install openjdk-11-jdk -y
 sudo apt-get install openjdk-11-jre -y

 Check JAVA Version:
 java -version
Output:
openjdk version "11.0.20" 2023-07-18
OpenJDK Runtime Environment (build 11.0.20+8-post-Ubuntu-1ubuntu120.04)
OpenJDK 64-Bit Server VM (build 11.0.20+8-post-Ubuntu-1ubuntu120.04, mixed mode, sharing)

Step 2: Install and Setup PostgreSQL 10 Database For SonarQube(postgres sql is the database which sonarcube uses)
Add and download the PostgreSQL Repo using following link
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" >> /etc/apt/sources.list.d/pgdg.list'
 wget -q https://www.postgresql.org/media/keys/ACCC4CF8.asc -O - | sudo apt-key add -
Install the PostgreSQL database Server by using following command,
sudo apt-get -y install postgresql postgresql-contrib
Start PostgreSQL Database server
sudo systemctl start postgresql
Enable it to start automatically at boot time.
 sudo systemctl enable postgresql
Change the password for the default PostgreSQL user.
 sudo passwd postgres
Switch to the postgres user.
su - postgres
Create a new user by typing:
createuser sonar
Switch to the PostgreSQL shell.
psql
