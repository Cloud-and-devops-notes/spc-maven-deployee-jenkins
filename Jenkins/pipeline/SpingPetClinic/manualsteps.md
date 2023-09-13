sudo apt update &&sudo apt install openjdk-17-jdk -y
wget https://dlcdn.apache.org/maven/maven-3/3.9.4/binaries/apache-maven-3.9.4-bin.tar.gz
sudo mkdir /usr/share/maven
tar -xvzf apache-maven-3.9.4-bin.tar.gz -C /usr/share/maven
sudo tar -xvzf apache-maven-3.9.4-bin.tar.gz -C /usr/share/maven
sudo vi ~/.bashrc   --->export PATH="$PATH:/usr/share/maven/apache-maven-3.9.4/bin"
source ~/.bashrc
mvn --version
git clone https://github.com/spring-projects/spring-petclinic.git
cd spring-petclinic && mvn package
EXPOSE 8080
java -jar /spring-petclinic/target/spring-petclinic-3.1.0-SNAPSHOT.jar


sh 'sudo apt update &&sudo apt install openjdk-17-jdk -y'
sh 'wget https://dlcdn.apache.org/maven/maven-3/3.9.4/binaries/apache-maven-3.9.4-bin.tar.gz'
sh 'sudo mkdir /usr/share/maven'
sh 'tar -xvzf apache-maven-3.9.4-bin.tar.gz -C /usr/share/maven'
sh 'sudo tar -xvzf apache-maven-3.9.4-bin.tar.gz -C /usr/share/maven'
sh 'export PATH=$PATH:/usr/share/maven/apache-maven-3.9.4/bin  >> sudo vi ~/.bashrc'
sh 'source ~/.bashrc'
sh 'mvn --version'
sh 'git clone https://github.com/spring-projects/spring-petclinic.git'
sh 'cd spring-petclinic && mvn package'
sh 'EXPOSE 8080'
sh 'java -jar /spring-petclinic/target/spring-petclinic-3.1.0-SNAPSHOT.jar'